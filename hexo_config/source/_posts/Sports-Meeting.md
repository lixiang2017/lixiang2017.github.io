---
title: Sports Meeting
date: 2018-12-15 22:38:42
categories:
tags:
---
###### 问题描述
学校举行了一个运动会，有以下六个项目。有五位同学报名了相应的项目。假设每个项目所用时间均为一个小时。
如何安排各个项目的顺序，使运动会在最短时间内结束。同学的参加的项目顺序可以调换，必须参加自己报的项目。
![](question.jpg)
###### 分析
尽量让更多的项目同时进行，同时保证不冲突。
```cpp
#include <queue>
#include <iostream>
using namespace std;

// n: 运动员数  m: 项目数
// 指针p指向一维数组的首地址 二维冲突表
int n = 0, m = 0;
int *p = NULL;
queue<int> q_events;

/*生成运动员报名的冲突表，将二维数组变成一维数组
  items: 某位运动员的报名情况
  比如一共六个项目，某运动员报了2和5，其items对应为0 1 0 0 1 0
*/
void generate_collision_table()
{
    int i = 0;
    int j = 0;
    int total_number = 0;
    int *items = new int[m];

    for (i = 1; i <= n; i++)   // 对每个运动员进行处理
    {
        cout << "Please enter the total number of entries for No. " << i << " athlete: ";
        cin >> total_number;

        j = 0;
        while (j < m)   // 初始化，数组元素置为0
        {
            items[j++] = 0;
        }

        cout << "Please enter the item numbers of the No." << i << " athlete (separated by spaces): ";
        j = 0;
        int item_num = 0;
        while (j < total_number)
        {
            cin >> item_num;
            items[item_num - 1] = 1;
            j++;
        }

        // 生成冲突数组
        int r = 0, s = 0;
        for (r = 0; r < m; r++)
        {
            for (s = 0; s < m; s++)
            {
                if(r != s && items[r] == 1 && items[s] == 1)
                {
                    p[r * m + s] = 1;
                    p[s * m + r] = 1;
                }
            }
        }
    }

    // 打印二维冲突表
    cout << "Collision Table : " << endl;
    for (i = 0; i < m; i++)
    {
        for (j = 0; j < m; j++)
        {
            cout << p[i * m + j] << "  ";
        }
        cout << endl;
    }
    cout << endl;
}

void input()
{
    int i = 0;
    int j = 0;
    cout << "Please enter the number of athletes : ";
    cin >> n;
    cout << "Please enter the number of items in the sports meeting :";
    cin >> m;

    cout << "The event numbers are : ";
    for (j = 1; j <= m; j++)
    {
        cout << j;
        if(j != m)
        {
            cout << ", ";
        }
    }
    cout << endl << endl;

    p = new int[m * m];
    for (i = 0; i < m; i++) // 初始化二维冲突表
    {
        for (j = 0; j < m; j++)
        {
            p[i * m + j] = 0;
        }
    }
}


void display_queue(queue<int> q)
{
    while(!q.empty())
    {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;
}

void generate_groups()
{
    int group_num = 0;
    int i = 0, j = 0;
    for (i = 0; i < m; i++)
    {
        q_events.push(i + 1);
    }

    while(!q_events.empty())
    {
        cout << "The remaining items are: ";
        display_queue(q_events);
        int head = q_events.front();
        group_num++;
        cout << "The items in Group No. " << group_num << " : " << head << " ";
        q_events.pop();

        // 对剩余元素逐个判断，谁能与head分在一组
        int *collision = new int[m];
        for (i = 0; i < m; i++)
        {
            collision[i] = p[(head - 1) * m + i];   // collision数组初始化
        }
        int len = q_events.size();

        for (i = 1; i <= len; i++)
        {
            int f = q_events.front();
            if(collision[f - 1] == 0) //f与组内元素没有冲突
            {
                for (j = 0; j < m; j++)
                {
                    collision[j] += p[(f - 1) * m + j];  // 将f与其他项目的冲突情况累加到collision上
                }
                f = q_events.front();
                cout << f << " ";      // f入组
                q_events.pop();        // 移除f
            }
            else  // f与组内有冲突
            {
                f = q_events.front();
                q_events.pop();
                q_events.push(f);
            }
            
        }
        cout << endl;
    }
    cout << endl;
}

int main()
{
    input();
    generate_collision_table();
    generate_groups();

    return 0;
}

/*
例如：某运动会设有 9 个项目:
    A = { 1，2，3，4，5，6，7，8，9 }，
七名运动员报名参加的项目分别为：
（2，5，9）、（2，8）、（9，4）、
（2，1，6）、（4，5）、（6，7，3）、
（7，5）
 
 (2, 5, 9) ==> (2, 5), (5, 9), (2, 9)
它们之间的冲突关系为: R = 
{（2，5）,（5，9）,（2，9）,（2，8）,（9，4）,（2，1）,
（1，6）,（2，6）,（4，5）,（6，7）,（6，3）,（7，3）,（7，5）}

冲突数组为：
0  1  0  0  0  1  0  0  0
1  0  0  0  1  1  0  1  1
0  0  0  0  0  1  1  0  0
0  0  0  0  1  0  0  0  1
0  1  0  1  0  0  1  0  1
1  1  1  0  0  0  1  0  0
0  0  1  0  1  1  0  0  0
0  1  0  0  0  0  0  0  0
0  1  0  1  1  0  0  0  0
*/

/*
例如：某运动会设有 6 个项目:
    A = { 1，2，3，4，5，6 }，
五名运动员报名参加的项目分别为：
（1, 2，5）、（3，4）、（3，5, 6）、
（4，6，1）、（2，6）
 
它们之间的冲突关系为: R = 
{（1，2）,（1，5）,（2，5）,（3，4）,（3，5）,（3，6）,
（5，6）,（4，6）,（4，1）,（6，1）,（2，6）}

冲突数组为：
0  1  0  1  1  1
1  0  0  0  1  1
0  0  0  1  1  1
1  0  1  0  0  1
1  1  1  0  0  1
1  1  1  1  1  0
*/
```
![](answer.png)
###### 思考
上面的算法是基于队列的。基于所有项目自前至后（从A到F）地寻找是否冲突，进而划分为组。没有冲突的是一组，有冲突的要在不同的组。
对于第二个用例，有多个解法的结果均为4个小时。上述算法的正确性有待证明，即如何证明所分的组数是最少的组数。
选择何种策略能保证最优？有另一种策略可供参考，首先选择冲突最多的项目，即参加人数最多的项目，接下来选择的项目按照参加人数依次递减。
![](answer2.png)

# Minimum-Weight-To-Fill-Bag
//  Unobounded Knapsack with some unavailable weight

// CODE BY :- AJAY PAL IIT (BHU) VARANASI
#include <bits/stdc++.h>
#define ll long long int
#define ld long double
#define kk '\n'
using namespace std;
#define INF 1000000

class Solution
{
public:
    int minimumCost(int cos[], int n, int w)
    {
        vector<int> val;
        vector<int> wt;

        for (int i = 0; i < n; i++)
        {
            if (cos[i] != -1)
            {
                val.push_back(cos[i]);
                wt.push_back(i + 1);
            }
        }

        n = wt.size(); // cos.size();

        int t[n + 1][w + 1];
        for (int i = 1; i <= n; i++)
        {
            t[i][0] = 0;
        }

        for (int j = 0; j <= w; j++)
        {
            t[0][j] = INT_MAX;
        }

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= w; j++)
            {
                if (wt[i - 1] <= j)
                {
                    t[i][j] = min(val[i - 1] + t[i][j - wt[i - 1]], t[i - 1][j]);
                }
                else
                {
                    t[i][j] = t[i - 1][j];
                }
            }
        }

        if (t[n][w] == INT_MAX)
        {
            return -1;
        }

        return t[n][w];
    }
};

int MinimumCost(int cost[], int n, int W)
{
    vector<int> val;
    vector<int> wt;

    int size = 0;
    for (int i = 0; i < n; i++)
    {
        if (cost[i] != -1)
        {
            val.push_back(cost[i]);
            wt.push_back(i + 1);
            size++;
        }
    }

    n = size;
    int t[n + 1][W + 1];
    for (int i = 1; i <= n; i++)
    {
        t[i][0] = 0;
    }

    for (int i = 0; i <= W; i++)
    {
        t[0][i] = INF;
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= W; j++)
        {
            if (wt[i - 1] > j)
            {
                t[i][j] = t[i - 1][j];
            }
            else
            {
                t[i][j] = min(t[i - 1][j], t[i][j - wt[i - 1]] + val[i - 1]);
            }
        }
    }

    return (t[n][W] == INF) ? -1 : t[n][W];
}

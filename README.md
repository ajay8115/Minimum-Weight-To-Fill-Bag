# Minimum-Weight-To-Fill-Bag
//  Unobounded Knapsack with some unavailable weight

// CODE BY :- AJAY PAL IIT (BHU) VARANASI
#include <bits/stdc++.h>
#define ll long long int
#define ld long double
#define kk '\n'
using namespace std;

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
            t[0][j] = maxi;
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

        if (t[n][w] == maxi)
        {
            return -1;
        }

        return t[n][w];
    }
};

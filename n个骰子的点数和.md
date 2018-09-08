tags:
- 递归

### n个骰子的点数和
扔掷n个骰子，所有骰子朝上一面的点数和为s，输出s所有可能值的概率（出现的次数）。

```cpp
#include <iostream>
#include <vector>
using namespace std;

//递归解法
void Probablity(const int& base, const int& maxVal, int curr, int sum, vector<int>& prob)
{
    if (curr == 0)
        prob[sum - base]++;
    else
    {
        for (int i = 1; i <= maxVal; i++)
        {
            Probablity(base, maxVal, curr - 1, i + sum, prob);
        }
    }
}

void sumOfDice(int n)
{
    if (n < 1)  return;
    int maxVal = 6;
    int maxSum = n * maxVal;
    int total = pow(maxVal, n);
    int size = maxSum - n + 1;
    vector<int> prob(size, 0);
    Probablity(n, maxVal, n, 0, prob);
    for (int i = 0; i < size; i++)
        cout << prob[i] << endl;
}

//迭代解法。用两个数组来存储骰子点数和出现的次数，在一次循环中，第一个数组的第n个数字表示为和为n出现的次数，在下一次循环中，加上一个新的骰子，此时和为n的骰子出现的次数等于上一次循环中骰子点数和为n-1、n-2、n-3、n-4、n-5、n-6的次数总和，迭代交替进行。
void sumOfDiceIteration(int n)
{
    if (n < 1)  return;
    int maxVal = 6;
    int maxSum = n * maxVal;
    int total = pow(maxVal, n);
    int size = maxSum + 1;
    int flag = 0;
    vector<vector<int>> prob(2, vector<int>(size, 0));
    for (int i = 1; i <= maxVal; i++)
        prob[flag][i] = 1;
    for (int k = 2; k <= n; k++)
    {
        for (int i = 0; i < k; i++)
            prob[1 - flag][i] = 0;
        for (int i = k; i < maxVal * k + 1; i++)
        {
            prob[1 - flag][i] = 0;
            for (int j = 1; j <= i && j <= maxVal; j++)
                prob[1 - flag][i] += prob[flag][i - j];
        }
        flag = 1 - flag;
    }

    vector<int> result(maxSum - n + 1);
    cout << result.size() << endl;
    for (int i = 0; i < result.size(); i++)
    {
        result[i] = prob[flag][i + n];
        cout << result[i] << endl;
    }
    
}
```
tags:
- 双指针

### 和为S的连续正数序列
输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序。

用两个指针small和big，分别指向连续序列的首尾。如果序列和等于目标值，则保存序列，并且继续增加big值。如果序列和大于目标值，则删去序列中的首部数字，并且small值加1。如果序列和小于目标值，则增加big值。
```cpp
vector<vector<int> > FindContinuousSequence(int sum) 
{
    vector<vector<int>> result;
    if(sum < 3)
        return result;
    int small = 1, big = 2, curSum = small + big;
    int mid = (1 + sum) / 2;
    while(small < mid)
    {
        if(curSum == sum)
        {
            pushSeq(result, small, big);
        }
        while(curSum > sum && small < mid)
        {
            curSum -= small;
            small++;
            if(curSum == sum)
                pushSeq(result, small, big);                   
        }
        big++;
        curSum += big;
    }
    return result;
}

void pushSeq(vector<vector<int>>& result, const int& small, const int& big)
{
    int size = big - small + 1;
    vector<int> seq(size);
    for(int i = 0; i < size; i++)
    {
        seq[i] = small + i;
    }
    result.push_back(seq);
}
```
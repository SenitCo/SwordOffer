tags:
- 双指针

### 和为S的两个数字
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

```cpp
vector<int> FindNumbersWithSum(vector<int> array,int sum) 
{
    //sort(array.begin(), array.end());
    int i = 0, j = array.size() - 1;
    while(i < j)
    {
        if(array[i] + array[j] == sum)
            return vector<int>({array[i], array[j]});
        else if(array[i] + array[j] < sum)
            i++;
        else
            j--;
    }
    return vector<int>();
}
```
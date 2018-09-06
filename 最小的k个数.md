tags：
- 堆
- 排序
- partition

### 最小的K个数
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

```cpp
//最大堆找最小的k个数
vector<int> GetLeastNumbers_Solution(vector<int> input, int k) 
{
    int n = input.size();
    if(k <= 0 || k > n || n <= 0)    return vector<int>();
    vector<int> maxHeap(k);
    for(int i = 0; i < k; i++)
        maxHeap[i] = input[i];
    make_heap(maxHeap.begin(), maxHeap.end());
    for(int i = k; i < n; i++)
    {
        if(input[i] < maxHeap.front())
        {
            pop_heap(maxHeap.begin(), maxHeap.end());
            maxHeap.pop_back();
            maxHeap.push_back(input[i]);
            push_heap(maxHeap.begin(), maxHeap.end());
        }
    }
    sort_heap(maxHeap.begin(), maxHeap.end());
    return maxHeap;
}

//利用快排的Partition找到第k大的元素，左边的子序列即为最小的k个元素
vector<int> GetLeastNumbers_Solution(vector<int> input, int k) 
{
    int n = input.size();
    if(k <= 0 || k > n || n <= 0)    return vector<int>();
    int start = 0, end = n - 1;
    int index = partition(input, start, end);
    while(index != k - 1)
    {
        if(index < k - 1)
            index = partition(input, index + 1, end);
        else
            index = partition(input, start, index - 1);
    }
    vector<int> result(input.begin(), input.begin() + k);
    sort(result.begin(), result.end());
    return result;
}

int partition(vector<int>& input, int start, int end)
{
    int pivot = input[start], i = start, j = end;
    while(i < j)
    {
        while(i < j && input[j] >= pivot)
            j--;
        while(i < j && input[i] <= pivot)
            i++;
        swap(input[i], input[j]);
    }
    swap(input[start], input[i]);
    return i;
}
```
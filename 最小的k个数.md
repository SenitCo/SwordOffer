tags：
- 堆
- 排序

### 最小的K个数
输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

```cpp
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
```
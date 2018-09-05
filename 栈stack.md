### 栈（stack）

#### 两个栈实现一个队列
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
```cpp
class Queue
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        if(stack2.empty())
        {
            while(!stack1.empty())
            {
                stack2.push(stack1.top());
                stack1.pop();
            }
        }
        if(stack2.empty())
            throw "queue is empty";
        int value = stack2.top();
        stack2.pop();
        return value;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```

#### 包含min函数的栈
定义栈的数据结构，并在该类型中实现一个能够得到栈中所含最小元素的min函数，要求min、push、pop、top的时间复杂度均为O(1)。
```cpp
#include <assert.h>
class Stack {
public:
    void push(int value) {
        m_data.push(value);
        if(m_min.empty() || value < m_min.top())
            m_min.push(value);
        else
            m_min.push(m_min.top());
    }
    void pop() {
        assert(m_data.size() > 0 && m_min.size() > 0);
        m_data.pop();
        m_min.pop();
    }
    int top() {
        assert(m_data.size() > 0 && m_min.size() > 0);
        return m_data.top();
    }
    int min() {
        assert(m_min.size() > 0);
        return m_min.top();
    }
private:
    stack<int> m_data;
    stack<int> m_min;
};
```

#### 栈的压入、弹出序列
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）。

**思路**：建立一个辅助栈，把输入的第一个序列中的元素依次压入栈中，并按照第二个序列的顺序依次从栈中弹出元素。如果出栈序列中下一个要弹出的元素刚好是栈顶元素，那么直接弹出；如果下一个要弹出的元素不在栈顶，把压栈序列中还没有入栈的元素依次压入辅助栈，直到把出栈序列中下一个要弹出的元素压入栈顶为止。如果压栈序列中所有元素都入栈了，仍没有找到出栈序列中下一个要弹出的元素，那么出栈序列不可能和压栈序列匹配。
```cpp
bool IsPopOrder(vector<int> pushV,vector<int> popV) 
{
    int size = pushV.size();
    stack<int> data;
    int i = 0, j = 0;   //i, j分别为压栈序列和出栈序列的索引
    while(j < size)
    {
        while(data.empty() || data.top() != popV[j])
        {
            if(i == size)
                break;
            data.push(pushV[i]);
            i++;
        } 
        if(data.top() != popV[j])
            break;
        data.pop();
        j++;
    }
    if(j == size)
        return true;
    else
        return false;
}
```

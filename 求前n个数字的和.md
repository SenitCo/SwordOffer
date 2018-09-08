### 求前n个数字的和
求1+2+...+n，要求不能使用乘除法，for、while、if、else、switch、case等关键字即条件判断语句（A?B:C）。

利用构造函数求解。
```cpp
class Temp
{
    public:
    Temp()    
    {
        i++;
        sum += i;
    }

    static void reset()
    {
        i = 0; 
        sum = 0;
    }

    static unsigned int getSum()
    {
        return sum;
    }
    private:
    static unsigned int i;
    static unsigned int sum;
};

unsigned int Temp::i = 0;
unsigned int Temp::sum = 0;

int Sum(int n) 
{
    Temp::reset();
    Temp *data = new Temp[n];
    delete []data;
    return Temp::getSum();
}
```
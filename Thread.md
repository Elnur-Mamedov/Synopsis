#  Thread

���� ����� ��������� ���������� � ���� �� � ��������� ������ ����������.

4 ���������� ������������
- ThreadStart
- ParameterizedThreadStart
- ThreadStart + MaxStackSize
- ParameterizedThreadStart + MaxStackSize

### ThreadStart 

��� �������, ������� ����� ����� ��	`Action`, ������ ��� ������ `Thread`

### ParameterizedThreadStart
��� �������, ������� ����� ����� ��	`Action<T>`, ������ ��� ������ `Thread`
�� ��������� �������� ���� `object`. ��� ��� ������ ������ � `Unboxing` � `Boxing`

### MaxStackSize
��� ������ ����� ������ � ������. �� ��������� 1 ��������

### ����� � ������ ������������� ����� ������.

������ � ������:
- �������� ����������
- �����������

������:
- ��������� ������. �������� ������� ��������
- ��������� �������. �������� ������������ `Thread.Sleep` ��� ������� ������ Debug � �������� ������� ����� ������
- ��������� ����������. �������� ������������ `Thread.Join` ��� �������� ���������� ������
- ������� ���������� � ������ � ��������.
- ����� �������, ��� �� ��� �� �� ����� ������������� �������� �������.

``` csharp
ThreadStart action = new(() =>
{
	Console.WriteLine("Hello, world!");
});

ThreadStart action2 = new(() =>
{
	Console.WriteLine("Hello, world!");
});

Thread th1 = new(action);

th1 = new Thread(action2); //��� ��� ����� �����

th1.Start();
```

``` csharp
ParameterizedThreadStart  action = new((object obj) =>
{
	Console.WriteLine("Hello, world!");
});

// �� ��� ������ �� ���� ��� ��� ������ generic 
// ������� �� ��������� ������ object
```

Thread.CurrentThread.ManagedThreadId 
���������� Id ��������� ������.

Main thread ���� ���������.

����� ��� ��� ��������� ������ ����� ��������, ����������� ��� ��� ������ �����,
��� �������� �����������.
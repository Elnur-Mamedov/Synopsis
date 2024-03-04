# ThreadPool

����������� ����� �����������, ������ ��� ���� ����� ������.

`ThreadPool` - �� ��� ������� � .NET
��-�� ����� ��� ����� ������������� ������.

��� ��������� �����.
����� ������� ��� ��� ������� �������.


``` csharp
class Program
{
    public static void Sample()
    {
        using Mutex mutex = new();

        mutex.WaitOne();
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"{i} from thread: {Thread.CurrentThread.ManagedThreadId}-{Thread.CurrentThread.IsThreadPoolThread}");
        }
        mutex.ReleaseMutex();
        
    }

    public static void Main(string[] args)
    {
        CountdownEvent countdownEvent = new(5);

        Console.WriteLine("Main started");
        
        for (int i = 0; i < 5; i++)
        {
            ThreadPool.QueueUserWorkItem((s) =>
            {
                Sample();
                countdownEvent.Signal();
            });

            `�������� ����� `QueueUserWorkItem` � ������� � ������� ��������
            ����� �� ��������, ��� ��� ���������� ������ �� ������� ������� �������, ������� ��� �����,
            ����� � 1 ����� �����, ����� � 10`
        }
        countdownEvent.Wait();

        Console.WriteLine("Main finished");
    }
}
```

��� �� ��������, ����� �� ����������� � ����, �� �� ������� �����, �� ������ ���� �����
�� ������ �������. �� �� ������� ����� �� �������� ������.

����� ���� ��� ����� �������� ���� ������, �� ������������ � `ThreadPool`, �� ������ 
��� ID � ������ ��� ��� ��� ����� ������, �� �� ����� ��� ���� � ��� �� �����, ������ � ������ ID.

�� ������ ������ ��� �������� ��� ���, ���� �� �����.

��� ������� ��������� ��� ������������ ���-�� ������� ���� � .NET, � �� ������ `ThreadPool`.

�� ����� ����������� ����� ����� � �������� ���� �����.
�� ���� �� �� ������ ������������ ��� � ������� 40 ���, �� ���������� ��� � OS
�� �� ��� � ���� ���� � �������, �������� � ����.
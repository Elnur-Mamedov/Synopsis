# ThreadPool

Ќапоминание поток одноразовый, нельз€ ему дать новую задачу.

`ThreadPool` - он уже готовый в .NET
из-за этого ему можно переназначать задачу.

Ёто статичный класс.
ћожно сказать что это бассейн потоков.


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

            `Ќапример метод `QueueUserWorkItem` в котором в очередь ставитс€
            какое то действие, тут дл€ выполнени€ хадачи он возьмет столько потоков, сколько ему нужно,
            может и 1 поток вз€ть, может и 10`
        }
        countdownEvent.Wait();

        Console.WriteLine("Main finished");
    }
}
```

 ак он работает, когда ты обрашаешьс€ к нему, он не создает поток, он выдает тебе поток
из своего резерва. “ы не тратишь врем€ на создание потока.

ѕосле того как поток выполнил свою работу, он возвращаетс€ в `ThreadPool`, он мен€ет 
его ID и выдает его вам дл€ новой задачи, но по факту это один и тот же поток, просто с другим ID.

Ќо ћ€ллим сказал что ¬озможно это так, инфа не сотка.

ѕри запуске программы уже определенное кол-во потоков есть у .NET, а он выдает `ThreadPool`.

ќн может запрашивать новый поток и выдавать тебе новый.
Ќо если ты не будешь использовать его в течении 40 сек, он возвращает его в OS
Ќо то что у него было в резерве, остаетс€ у него.
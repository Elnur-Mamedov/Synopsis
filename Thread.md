#  Thread

Ётот класс позвол€ет обращатьс€ к €дру ќ— и создавать потоки выполнени€.

4 перегрузки конструктора
- ThreadStart
- ParameterizedThreadStart
- ThreadStart + MaxStackSize
- ParameterizedThreadStart + MaxStackSize

### ThreadStart 

Ёто делегат, который очень похож на	`Action`, только дл€ класса `Thread`

### ParameterizedThreadStart
Ёто делегат, который очень похож на	`Action<T>`, только дл€ класса `Thread`
ќн принимает параметр типа `object`. “ак что будьте готовы к `Unboxing` и `Boxing`

### MaxStackSize
Ёто размер стека потока в байтах. ѕо умолчанию 1 мегабайт

### ѕлюсы и минусы использовани€ этого класса.

Ќачнем с плюсов:
- —корость выполнени€
- ѕараллелизм

ћинусы:
- —ложность работы. ѕридетс€ содвать делегаты
- —ложность отладки. ѕридетс€ использовать `Thread.Sleep` дл€ отладки ƒелать Debug в реальном времени будет сложно
- —ложность управлени€. ѕридетс€ использовать `Thread.Join` дл€ ожидани€ завершени€ потока
- ¬ысокие требовани€ к пам€ти и ресурсам.
- —амое главное, это то что мы не можем переназначать действие потокам.

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

th1 = new Thread(action2); //Ёто уже новый поток

th1.Start();
```

``` csharp
ParameterizedThreadStart  action = new((object obj) =>
{
	Console.WriteLine("Hello, world!");
});

// ќн был создан до того как был создан generic 
// поэтому он принимает только object
```

Thread.CurrentThread.ManagedThreadId 
показывает Id нынешнего потока.

Main thread выше приоритет.

 огда два или несколько потока когда работают, выполн€етс€ тот кто первый успел,
они работают конкурентно.
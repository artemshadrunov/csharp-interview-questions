# Основы C#

## class vs struct vs record
В чем различие? Что зачем применять?

## value type vs refernece type

```cs
static String str;
static DateTime time;

static void Main(string[] args)
{
    Console.WriteLine(str == null ? "str == null" : str); // Что будет на экране?
    Console.WriteLine(time == null ? "time == null" : time.ToString());  // Что будет на экране?
    Console.ReadLine();
}
```

```cs
class Person
{
    public string Name { get; set; }

    public Person(string name)
    {
        Name = name;
    }
}

static void Main(string[] args)
{
    var person = new Person("JustName");

    ChangePerson(person);

    Console.WriteLine(person.Name); // Что произойдет на этой строке?
}

static void ChangePerson(Person person)
{
    person.Name = "ChangedName";
    person = null;
}
// Доп. вопрос: что добавить в объявление метода, чтобы person все-таки стал null?
```

## Модификаторы доступа
Зачем нужны? Какие существуют?

В чем отличие readonly и const?

Что такое static конструктор и зачем его использовать?

# Концепции ООП
Какие существуют? Описать в паре предложений.

```cs
//Что будет выведено на экран?

class BaseClass
{
    public BaseClass()
    {
        Console.WriteLine("Base class constructed");
    }

    public virtual void PrintClassName()
    {
        Console.WriteLine("Base");
    }
}

class DerivedClass : BaseClass
{
    public DerivedClass()
    {
        Console.WriteLine("Derived class constructed");
    }

    // Здесь override заменяем на new, повторояем вопрос
    // Оставляем только public void PrintClassName(), повторяем вопрос
    public override void PrintClassName()
    {
        Console.WriteLine("Derived");
    }
}

static void Main(string[] args)
{
    DerivedClass derivedInstance = new DerivedClass();
    BaseClass baseInstance = derivedInstance;
    baseInstance.PrintClassName();
}
```

# Обработка исключений

Что такое finally?

```cs
class Person : IDisposable
{
    public string Name { get; set; }

    public int Age { get; set; }

    public void Dispose()
    {
        Name = null;
        Age = Int32.MinValue;
    }
}

static void Main(string[] args)
{
    var person = new Person
    {
        Name = "AwesomeName",
        Age = 42
    };

    try
    {
        var stupidAction = person.Age / 0;
    }
    catch (Exception)
    {
        Console.WriteLine("Unknown exception");
    }
    catch
    {
        Console.WriteLine("Absolutely unknown exception");
    }
    catch (DivideByZeroException)
    {
        Console.WriteLine("You shouldn't divide by zero really");
    }
    finally
    {
        person.Dispose();
    }

    Console.WriteLine(person.Name);
    Console.WriteLine(person.Age);
```

# Делегаты, ивенты
Какие существуют типы делегатов?

В чем различие между ивентами и делегатами?

# Интерфейсы
Зачем нужны интерфейсы?

abstract class vs interface

Implicit реализации методов интерфейса

# Коллекции
Есть ли у тебя алгоритм выбора коллекций? Опиши.

Dictionary<> vs Hashset<>? Область применения.

Array<> vs List<>? Область применения

IEnumerable<> vs ICollection<> vs IReadonlyCollection<>? Область применения.

```cs
// Что будет на экране?
static void Main(string[] args)
{
    var actions = new List<Action>();
    for (var i = 0; i < 10; i++)
    {
        actions.Add(() => Console.WriteLine(i));
    }

    foreach (var action in actions)
    {
        action();
    }
}
```

# Строки
```cs
string hello = "hello";
string helloWorld = "hello world";
string helloWorld2 = "hello world";
string helloWorld3 = hello + " world";

Console.WriteLine(helloWorld == helloWorld2);
Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld2));

Console.WriteLine(helloWorld == helloWorld3);
Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld3));

// Что будет на экране?
```

Зачем нужен StringBuilder?

# Async/Await vs multithreading
В чем различие между асинхронностью и многопоточностью в c#?

Примеры использования.

Что быстрее, асинхронность или многопоточность?(Вопрос на понимание того, что ничего не быстрее)

# LINQ
```cs
class Gift
{
    public string Name { get; set; }

    public int Price { get; set; }
}

static void Main(string[] args)
{
    var gifts = new List<Gift>(); // Считаем, что заполнили коллекцию различными элементами
    
    // Найти сумму цен всех подарков, у которых есть буква 'A'
    // Найти 4 и 5 по величине цены подарки
    // Узнать имя подарка с ценой = 42
    // Узнать есть ли подарок без названия?
    // Собрать коллекцию имен подарков с ценой выше 20
}
```

```cs
var numbers = new List<int> {1, 2, 3};

foreach (var number in numbers)
{
    if (number > 2)
        numbers.Remove(number);
}
```

```cs
static List<int> _magicNumbers = new List<int>();

static void Main(string[] args)
{
    var numbers = CreateMagicNumbers(3);

    _magicNumbers.Add(10);
    _magicNumbers.Add(11);

    foreach (var number in numbers)
    {
        Console.WriteLine(number);
    }
}

static IEnumerable<int> CreateMagicNumbers(int count)
{
    for (var i = 0; i < count; i++)
    {
        _magicNumbers.Add(i);
    }

    return _magicNumbers;
}
```

# Память в c#
Модель памяти в c#.

Как работает сборщик мусора?

LOH

Всегда ли reference type хранятся в стке?

# Принципы организации кода
SOLID, DRY, KISS

# Паттерны
Какие приходилось реализовывать?

# Системы контроля версий
Merge vs rebase vs cherrypick

# Тестирование
Юнит vs интеграционные тесты
AAA принцип
Идеальный code coverege

# Вопросы на опыт
По каким методологиям приходилось работать
Как оцениваешь сроки
Как проводишь код-ревью

# Вопросы к собеседованию по Java, Kotlin & Spring

## Java 

### ООП

#### Абстракция:
> Абстракция - это выделение свойств (полей) и действий (методов) описываемой модели необходимых для решения данной задачи и опускание других свойств/действий.

#### Инкапсуляция:
> Инкапсуляция - это сокрытие сложностей внутренней реализации модели и предоставление простого и понятного интерфейса пользователю.
```java
class SomeComplexClass {
    
    private Object field1;
    private Object field2;
//   ...
    private Object fieldN;
    
    private void someComplexMethod1(/*args*/) {
//        complex logic
    }
    private void someComplexMethod2(/*args*/) {
//        complex logic
    }
//    ...
    private void someComplexMethodN(/*args*/) {
//        complex logic
    }
    
//    Сложности реализации объекта скрываются, а пользователю предоставляется простой интерфейс
    public void smartMethod(Object obj){
        someComplexMethod1(/*args*/);
        someComplexMethod2(/*args*/);
//        ...
        someComplexMethodN(/*args*/);
    }
    
}
```

#### Наследование:
> Наследование - это свойство перенимать состояние (поля) и поведение (методы) родительского класса.

```java
class Animal {
    int age;
    int weight;
    
    public void eat(){}
}

class Person extends Animal {
    String name;
    
    public void introduceAndEat(){
        System.out.println("Hello, my name is " + name + ", my age is " + age + ", my weight is " + weigth +
                " and now I am going to eat!");
        eat();
    }
}

```

#### Полиморфизм:
> Полиморфизм: способность метода обрабатывать параметры разных типов, взаимодействуя с ними по родительскому интерфейсу.

```java

public class Clazz {
    
    public static void main(String[]args){
        List immutableList = Arrays.asList("a", "b", "c");
        List arrayList = new ArrayList();
        List linkedList = new LinkedList();
        
//        независимо от объекта, которым является параметр метода,
//        если он реализует интерфейс List, метод его примет и корректно обработает
        method(immutableList);
        method(arrayList);
        method(linkedList);
    }
    
//    также к полиморфизму можно отнести перегрузку методов
    public static void method(List list) {}
    public static void method(List list, int max) {}
    public static void method(List list, int max, int min) {}
}

```

### Типы данных, классы, объекты, интерфейсы, абстрактные классы, static

#### Примитивные типы данных 

##### Целочисленные
- `byte` - целое число от -128 до 127 (8 бит)
- `short` - целое число от -32768 до 32767 (16 бит)
- `char` - беззнаковое целое число, представляющее собой символ UTF-16 (буквы и цифры, 16 бит)
- `int` - целое число от -2147483648 до 2147483647 (32 бита)
- `long` - целое число от -9223372036854775808L до 9223372036854775807L (64 бита)

##### С плавающей точкой 
- `float` - действительное число от 1.4e-45f до 3.4e+38f (32 бита)
- `double` - действительное число от 4.9e-324 до 1.7e+308 (64 бита)

##### Логический
- `boolean` - true/false (32 бита везде, кроме массивов, там 8 бит)

#### Ссылочные типы данных 
> Все остальные типы, начиная от `Object`

#### Класс
> Класс - это прототип (шаблон) некой сущности

#### Объект 
> Объект - это конкретный экземпляр класса

#### Интерфейс
> Интерфейс - это контракт, который обязуются соблюдать реализующие его классы.

Реализует взаимоотношение "*ведет себя как*".
Интерфейс может иметь:
- методы (по умолчанию - абстрактные, без реализации)
- final static поля 
- начиная с Java 8 - дефолтные методы с реализацией по-умолчанию
- можно реализовать сколько угодно интерфейсов

#### Абстрактный класс
> Абстрактный класс - класс, создание экземпляров которого невозможно. 

Реализует взаимоотношение "*является*" (is-a). 
Абстрактный класс может иметь:
- поля, в т.ч. нестатические 
- методы, в т.ч. абстрактные
- можно наследовать только 1 класс, в том числе абстрактный

#### Интерфейс vs. Абстрактный класс

Наследование абстрактного класса образует гораздо более *сильную связь* с родителем, чем реализация интерфейса.
То есть при создании класса-наследника под капотом сначала вызывается конструктор класса-родителя,
инициализируются все его поля, а потом создается класс-наследник.

Интерфейс же просто регламентирует обязательное поведение классов, которые его реализуют.

> Таким образом, для поддержания более низкой связности системы **рекомендуется использовать реализацию интерфейсов во всех случаях**,
> кроме тех, где нужно выстроить явную иерархию с отношением "*является*".


#### static
> Ключевое слово static означает принадлежность поля/метода/класса не к *объекту*, а к *классу*. 

В случае с полем это означает что существует только 1 экземпляр этого поля на всю программу и можно получить к нему доступ,
не создавая объект класса, в котором описано это поле, через имя класса (Class.staticField). 

В случае с методом это означает что этот метод может использовать только другие статические методы и можно получить к нему доступ,
не создавая объект класса, в котором описан этот метод, через имя класса (Class.staticMethod()).

### Класс Object
Класс `Object` является родителем по-умолчанию для всех классов.
Из-за наследования, у вех классов есть следующие методы, определенные в кассе `Object`:
- `toString()` - возвращает строковое представление объекта
- `getClass()` - возвращает специальный объект типа `Class`, который описывает текущий класс
- методы сравнения объектов
    - `hashCode()` - возвращает число типа int, неким образом характеризующее объект
    - `equals(Object obj)` - возвращает true/false в зависимости от результата сравнения объекта с объектом obj.
  В базовой реализации сравнивает ссылки на объекты: `return this == obj`
- методы для работы с потоками (могут быть вызваны только внутри `synchronized` блоков)
  - `notify()`
  - `notifyAll()`
  - `wait(long timeout)`
  - `wait(long timeout, int nanos)`
  - `wait()`
- `finalize()` - метод, который использует GC для освобождения ресурсов 
(категорически не надо переопределять, потому что его выполнение ничем не гарантируется)
- `clone()` - создает дубликат объекта (в базовой реализации дублируются только примитивные поля)

### Класс String
Класс `String` является текстовой строкой. Класс String - *иммутабельный*, 
то есть значение объекта класса String нельзя изменить после создания объекта.

> В JVM существуют пулы значений для String и классов-обёрток (Integer, Character и т.д.). 
> Для String в пул строк добавляется каждая строка, созданная через оператор литерала **""**.
> Другие такие же строки не будут заново созданы и не будут занимать место в памяти, 
> все они будут ссылаться на строку в пуле строк.

Есть 2 способа создать строку:
- `String s = new String()` - использование оператора new *не рекомендуется*, потому что в таком случае будет создан новый объект,
занимающий место в памяти, а не будет использовано значение из пула строк.
- `String s = "abc"` - если такого значения еще нет в пуле строк, оно там создастся. 
Если есть, то будет использовано значение из пула строк, экономя память.

#### Конкатенация строк
Для строк в Java переопределен оператор "+", действие по сложению строк называется *конкатенацией*.

> При конкатенации строк образуется *новая* строка, потому что строки иммутабельны

Проблема циклической конкатенации строк:

```java
class StringTest {
  public static void main(String[] args) {
    String s = "abc";

    for (int i = 0; i < Integer.MAX_VALUE; i++) {
        s = s + 1; // циклическая конкатенация строки 
    }
  }
}
```
В данном случае, при исполнении цикла, будет создано 2147483647 объектов `String`, что крайне неэффективно для памяти.
Во избежание подобных ситуаций рекомендуется использовать мутабельный класс `StringBuilder` и его метод append():
```java
class StringBuilderTest {
  public static void main(String[] args) {
    String s = "abc";
    StringBuilder sb = new StringBuilder(s);
    for (int i = 0; i < Integer.MAX_VALUE; i++) {
        sb.append(1); // циклическая конкатенация строки 
    }
    String result = sb.toString();
  }
}
```

### Методы `equals()`, `hashcode()`, контракт между ними.

- `equals()` гарантирует: если `o1.equals(o2)` вернул true, то объекты равны. Если false,
то элементы точно не равны друг другу.

- `hasCode()` гарантирует что если у двух объектов разные хэшкоды - эти объекты точно разные,
а если хэшкоды равны то либо объекты равны, либо произошла коллизия.

> Для корректной работы, при создании собственного класса, который будет хранить данные, всегда нужно переопределять методы equals() и hasCode().

### Коллекции

Иерархия коллекций:

![Иерархия коллекций](/images/collections.png "Collections Hierarchy")

> Интерфейс `Map` _**не является**_ наследником интерфейса `Iterable`, поэтому просто так пройтись по Map'е нельзя.
> Но можно использовать вложенный в Map `EntrySet`, который содержит в себе пары ключ-значение


#### Базовые интерфейсы, основные реализации

`List<T>` - список (массив) элементов.

- `ArrayList` - изменяемый массив, где каждому элементу соответствует его индекс от 0 до n.
  - Основная коллекция для хранения однотипных данных
  - Быстрый поиск по индексу `O(1)`
  - Вставка/удаление `O(n)`
- `LinkedList` - двусвязный список, где у каждого элемента есть ссылка на предыдущий и следующий элемент.
  - Крайне редко используется
  - Быстрая вставка/удаление `O(1)`
  - Поиск `O(n)`

`Map<K, V>` - отображение (словарь) элементов в формате _key-value_.

- `HashMap` - словарь с хранением в хэш-структуре.
  - Основная коллекция для хранения K-V элементов
  - Быстрый поиск `O(1)`
  - Вставка/удаление `O(1)-O(log(n))`
  - **Не сортированный**
  - Представляет собой массив односвязных списков на n <= 16 и массив красно-черных деревьев при n > 16
    - Каждый элемент массива (бакет) соответствует числу от 0 до 15
    - При помещении в Hash-структуру элемента высчитывается его hashcode, над ним проводят операцию, отображая 
его хэшкод в диапазон от 0 до 15, и кладут в соответсвующий бакет.
    - Если в бакете уже есть элемент, то новый элемент кладется следующим элементом, 
образуя структуру _односвязный список_ для n <= 16 _красно-черное деревво_ при n > 16
- `TreeMap` - словарь с хранением в _красно-черном дереве_.
  - Редко используется
  - Быстрый поиск `O(log(n))`
  - Вставка/удаление `O(log(n)))`
  - **Сортированный**, то есть элементы, которые туда кладутся, должны поддерживать 
интерфейс `Comparable`, или нужно указать `Comparator` при создании данной коллекции
  - Представляет собой _красно-черное дерево_:
    - Бинарное - у любого элемента может быть только 2 наследника
    - Сортированное - бОльший элемент кладется справа, мЕньший - слева
    - Самобалансирующеяся - дерево самостоятельно перестраивается, для равномерного распределения длины ветвей 

`Set<T>` - множество уникальных элементов. 
Под капотом реализуется как Map<K,V>, у которого вместо Value - объект-заглушка.

`Queue<T>` - очередь элементов, контролирующая порядок поступления/извлечения элементов.
- `Deque` - двунаправленная очередь, может работать как по принципу **LIFO**, так и по **FIFO**.

### Исключения

> Исключения - объекты, которые создаются ("выбрасываются") в момент нестандартной ситуации в программе.

#### Иерархия
![Иерархия исключений](/images/exceptions.png "Exceptions Hierarchy")

Легенда
- Красный: `Errors` - критические ошибки в программе, после которых дальнейшее выполнение невозможно
  - `StackOverflowError` - переполнение **стека** вызовов методов. Причина: слишком глубокий стек вызовов, 
  в основном из-за некорректного использования рекурсивного вызова метода
  - `OutOfMemoryError` - переполнение памяти **кучи**. Причина: вся память, выданная JVM, кончилась, в основном 
  из-за слишком больших объемов данных или слишком низкой настройки максимального значения памяти кучи
- Желтый: `Checked Exceptions` (проверяемые) - исключения, которые программист **обязан** обработать ИЛИ
указать в сигнатуре метода для дальнейшего проброса. 
  - `Exception` - общий родитель для всех **проверяемых** исключений. Используется для создания собственного
  **проверяемого** исключения через наследование
  - `IOException` - ошибки ввода/вывода. Возникают, если, например, неправильно указать путь до файла, 
  который нужно прочитать  
- Зеленый `Unchecked Exceptions` (непроверяемые) - исключения, которые программист не обязан обрабатывать
  - `RuntimeException` (RTE) - общий родитель для всех **непроверяемых** исключений. Используется для создания собственного
    **непроверяемого** исключения через наследование.
  - `NullPoinerException` (NPE) - ошибка, появляющаяся в результате вызова метода у пустого (`null`) объекта. 
  Бывает крайне тяжело диагностируема.
  - `ArithmeticException`, `ArrayIndexOutOfBoundsException` и тд. - ошибки, возникающие при неправильном написании 
  программы (_семантические_). Например, деление на ноль или выход за границы массива

#### Обработка исключений

Способы обработки исключений:

1. `try-catch` - попытаться поймать исключение в блоке `try` и обработать его в блоке `catch`.
В блоке `catch` чаще всего необходимо после обработки исключения выбрасывать 
`RuntimeException(e)`, чтобы исключение не терялось.
2. `try-catch-finally` - п.1 + блок `finally`, который выполнится в любом случае, было исключение или нет.
3. `try-with-resources` - п.1 + можно в круглых скобках после слова `try` создать объект, поддерживающий 
интерфейс `AutoCloasble`, тогда по окончании блока `try-catch` у этого объекта будет вызван метод `close()`. 
Этими объектами зачастую являются потоки ввода/вывода.

> В блоках `catch` необходимо располагать исключения от младшего к старшему по иерархии 
> наследования, чтобы отлавливать наиболее конкретный exception.

### Функциональные интерфейсы. 

> Функциональный интерфейс - интерфейс, содержащий 1 метод и аннотацию 
> уровня класса `@FunctionalInterface` (необязательно, но желательно).

Основные функциональные интерфейсы:
- `Function<T, R>`: **T -> R** - описывает метод преобразования аргумента из одного типа в другой (или тот же самый)
- `Predicate<T>`: **T -> boolean** - описывает метод преобразования аргумента в логическое выражение
- `Consumer<T>`: **T -> void** - описывает метод преобразования аргумента в ничего (_потребление аргумента_)
- `Supplier<t>`: **void -> R** - описывает метод получения возвращаемого параметра из ничего (_производство параметра_)

Так же существуют Bi-формы этих интерфейсов, 
например `BiFunction<T1, T2, R>` : **T1, T2 -> R** или `BiPredicate<T1, T2>` : **T1, T2 -> boolean**

### Stream API, основные операторы

> Stream API - метод работы с коллекциями как с потоком объектов.

```java
class StreamExample{
  public static void main(String[] args) {
    AtomicLong cnt = new AtomicLong();
    source.stream()
           .map(x -> x.squash())
           .peek(x -> cnt.incrementAndGet())
           .filter(x -> x.getColor() != YELLOW)
           .forEach(System.out::println);
  }
}
```
![Визуализация Stream API](/images/stream_chain.svg "Stream API visualization")

Методы Stream API делятся на 3 категории:
1. Начинающие:
   1. `.stream()` - создает stream из коллекции
   2. `.parallelStream()` - создает stream из коллекции, производящий операции многопоточно, 
   используя пул `ForkJoinPool`
   3. `Stream.generate(Supplier<T>)` - генерирует бесконечный stream по описанию от `Supplier`
2. Промежуточные (**возвращают `Stream<T>`**):
   1. `filter(Predicate<T>)` - пропускают далее только элементы, подходящие по условию `Predicate`
   2. `map(Function<T, R>)` - преобразовывает (отображает) элемент из типа T в тип R _(T м.б. = R)_
   3. `flatMap(Function<T, Stream<R>>)` - преобразует двумерный массив в одномерный.
   4. `peek(Consumer<T>)` - делает действие над элементом, и кладет его назад (удобно для логгирования состояния стрима)
   5. `limit(long n)` - ограничивает стрим n элементами
   6. `skip(long n)` - пропускает n элементов
   7. `sorted()` - сортирует стрим (не рекомендуется из-за потребления ЦП)
   8. `distinct()` - контролирует уникальность элементов стрима (не рекомендуется из-за потребления ЦП)
3. Конечные (терминальные, **возвращают _НЕ_ `Stream<T>`**)
   1. `collect(Collectors.toList())` - собирает стрим обратно в коллекцию (в данном случае в `List`)
   2. `collect(Collectors.groupingBy())` - собирает стрим в Map
   3. reduce() - "сворачивает" стрим в 1 элемент
   4. count() - возвращает количество элементов стрима

> Stream API использует **ленивый** тип вычислений. 
> То есть, пока не вызван терминальный оператор, никаких вычислений сделано не будет.

### Основы многопоточности. Thread, synchronized, volatile, классы Atomic

Многопотчность - способность программы исполнятся на нескольких ядрах процессора одновременно.

Преимущества:
- Возможность сильно ускорить выполнение программы, за счет того, что каждый следующий процесс не будет ждать 
окончания предыдущего процесса
Недостатки:
- При неправильном использовании может не только не ускорить программу, но и внести серьезные баги и состояния, 
при которых дальнейшее выполнение невозможно

Алгоритм работы (упрощенный):
1. При запуске `psvm` метода, JVM выделяет 1 поток (Main Thread) приложению.
2. При выполнении программы, можно стартовать другие потоки из потока Main или из других потоков.
   1. Эти потоки могут быть обычными или сервисными _("демонами", от англ. daemon)_.
3. Main thread ждет окончания работы всех остальных **НЕ-daemon** потоков, затем заканчивает выполнение программы.

![Основы многопоточности](/images/multithreading.png "Multithreading")

#### Способы стартануть поток

1. Создать класс-наследник `Thread`, переопределить в нем метод `run()`, где указать всю логику, 
которую будет выполнять поток. Создать экземпляр этого класса и вызвать метод `start()` **(НЕ run())**.
2. Создать класс, реализующий интерфейс `Runnable`, переопределить в нем метод `run()`, где указать всю логику,
которую будет выполнять поток. Положить этот класс в конструктор класса Thread при создании объекта Thread, 
на созданном объекте вызвать метод `start()` **(НЕ run())**.
3. Создать объект класса `Thread`, в конструктор положить анонимный класс, реализующий интерфейс `Runnable`, 
переопределить в нем метод `run()`, где указать всю логику, которую будет выполнять поток, или просто указать лямбду, 
как в примере ниже. На созданном объекте вызвать метод `start()`.

```java
class ThreadExample{
    public static void main(String[] args) {
        Thread myThread = new Thread(() -> {
//            TODO implement thread logic here
        });
        myThread.start();
    }
}
```
4. Используя ExecutorFramework, создать пул потоков и в него отправлять задачи (сабмитить таски).
```java
class ExecutorExample{
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(5);
        executorService.submit(() -> {
//            TODO implement thread logic here
        });
    }
}
```

#### Доступ к ресурсам в многопоточной программе

>При реализации многопоточности одной из главных проблем является контроль доступа потоков к общим ресурсам.

Например, есть файл, в который одновременно пишет 2 потока, а 3-ий из него читает. 
Эта проблема называется `Race Condition` (состояние "гонки"), при котором становится важно, какой поток каким по 
счету использует общий ресурс (файл). **Но JVM не гарантирует порядок выполнения потоков!**

Для решения подобных проблем существует ключевое слово `synchronized`, которое гарантирует, что данный метод/блок кода
в одну единицу времени может исполнять только 1 поток.

```java
class SynchronizedExample{
    public static void main(String[] args) {
        Thread thread1 = new Thread(() -> {
            accessToFile();
        });
        Thread thread2 = new Thread(() -> {
            accessToFile();
        });

        thread1.start();
        thread2.start();
    }
//        Только 1 поток сможет исполнять этот метод в одну единицу времени.  
    public synchronized void accessToFile(){
//        access to file (create, read, write, etc.)
    }
}
```

#### Volatile 

>При реализации многопоточности существует проблема: каждое ядро процессора обладает своим кэшем, 
>куда складывает наиболее часто используемые данные, чтобы уменьшить количество чтений из памяти и увеличить скорость.
>Но после кэширования, некоторые переменные могут быть изменены другим потоком, а тот поток, который закэшировал эту 
>переменную, ничего об этом не знает. 

Решение проблемы - запретить процессору кэшировать некоторые данные.

Ключевое слово `volatile` означает, что процессору запрещается кэшировать данную переменную, 
и нужно обращаться к ней только из общей памяти.

#### Atomic-классы

>При реализации многопоточности существует проблема: такие операции, как, например, `i++;` (инкремент с присвоением)
> хоть и написаны в одно действие, фактически, процессором выполняются как 2 разных действия. В момент, когда первое 
> действие уже выполнено, а второе еще нет, переменная моет быть изменена другими потоками. В таком случае, результат 
> команды `i++;` не определен.

Решение проблемы - использовать специальные `Atomic`-классы, любые методы в которых происходят 
за одно действие процессора.

```java
class NotAtomicExample{
    public static void main(String[] args) {
        int i = 0;
        int a = 0;
        
        Thread thread1 = new Thread(() -> {
            i++; // ЦП выполнит операцию за 2 действия
            a = i;
        });
        Thread thread2 = new Thread(() -> {
            i+2; // ЦП выполнит операцию за 2 действия
            a = i;
        });

        thread1.start();
        thread2.start();
//      в итоге точное значение a не определено
    }
}
class AtomicExample{
    public static void main(String[] args) {
        AtomicInteger i = new AtomicInteger(0);
        int a = 0;
        Thread thread1 = new Thread(() -> {
            i.incrementAndGet(); // ЦП выполнит операцию за 1 действие
            a = i.get();
        });
        Thread thread2 = new Thread(() -> {
            i.addAndGet(2); // ЦП выполнит операцию за 1 действие
            a = i.get();
        });

        thread1.start();
        thread2.start();
//      в итоге точное значение a определено 
    }
}
```

## Kotlin
Kotlin - многоцелевой язык, который может компилироваться в java, javascript и в нативный код

### Val/var

- `var` - ключевое слово для обозначения поля, ссылку которого **можно** изменять после инициализации поля 
(англ. _variable_). Аналог обычного поля в Java.
- `val` - ключевое слово для обозначения поля, ссылку которого **нельзя** изменять после инициализации поля
  (англ. _value_). Аналог final поля в Java.

> Всегда рекомендуется использовать val, кроме тех случаев, когда необходимо использовать var.

### Extension-функции

Extension-функция (функция-расширение) - функция, которая создается с указанием класса и имеющая область видимости 
этого класса внутри себя. Эту функцию можно использовать так, будто это функция объявлена в самом классе.

```kotlin

fun String.isEmail(): Boolean {
    return this.matches(".*@.*\..*")
}

```

> В Java Extension-функция компилируется как класс `(ClassName)ExtensionKt` со статическим методом с n+1 
> аргументом, где n - число аргументов extension-функции, а +1 - `this`

```java
class StringExtensionKt {
    public static Boolean isEmail(String obj){
        return obj.matches(".*@.*\..*");
    }
}
```

### Null-safety

Null-safety - функционал языка Kotlin, который делает проверку на null обязательной для всех типов. Грамотное 
использование null-safety может избавить программу от одной из самых неприятных ошибок - `NullPointerException`

Основные операторы null-safety:

- `val str: String?` - объект **может** хранить в себе ссылку `null`
- `val str: String` - объект **не может** хранить в себе ссылку `null`
- `str?.toUpperCase()` - вызов метода произойдет только если `str != null`
- `str!!.toUpperCase()` - вызов метода произойдет в любом случае, в т.ч. если `str == null`. **Крайне не рекомендуется**
- `str?.toUpperCase() ?: "empty"` - _Элвис-оператор_ - если `str == null`, то выражение вернет `"empty"`
- `String!` - Kotlin не знает ничего о нуллабельности этого объекта. Например, при вызове метода, написанного на Java,
аргументы которого не помечены аннотацией `@NotNull`

### Иммутабельность, Sequence

#### Иммутабельность

Иммутабельность ("неизменчивость") - свойство коллекции, которое запрещает изменять её после создания.
Это свойство делает использование коллекции более безопасным, особенно в многопоточной среде 
(несколько потоков не смогут изменять эту коллекцию одновременно, только читать)

> По умолчанию все коллекции в Kotlin **иммутабельные**. Чтобы создать mutable-коллекцию, надо явно указать при 
> создании тип с приставкой `Mutable`

```kotlin

val list = listOf("a", "b") // immutable
val mutableList = MutableListOf("a", "b") // mutable

val list: List<String> // immutable
val mutableList: MutableList<String> // mutable

```

#### Sequence 

`Sequence` - аналог Java Stream API, использует **ленивые** вычисления (пока не вызовется терминальный оператор, 
никаких операций произведено не будет)

> В Kotlin есть возможность прямо на коллекциях вызывать методы вроде `map{}`, `filter{}` и тд.
> Но в таком случае вычисления будут **жадными**, то есть на каждый вызов такого оператора будет создана новая 
> коллекция. Для оптимизации вычислений необходимо вместо длинной цепочки вызовов этих методов сначала вызвать метод 
> `asSequence()`, а в конце метод, собирающий в коллекцию, например `toList()`

### Классы Any, Unit, Nothing.

- `Any` - аналог java-типа `Object`, является **родителем** для всех классов.
- `Unit` - аналог java-типа `void`. Явно можно не указывать.
- `Nothing` - используется как возвращаемое значение в тех случаях, когда метод не закончится никогда, например, 
бросая исключение. Является **наследником** для всех классов.

### Функции области видимости With, let, apply, run

- `with` - принимает объект, далее внутри {} можно обращаться к полям и методам объекта без указания его имени.
- `let` - выполняет блок кода в {}. Удобно использовать как "при не null сделай что-то", для этого нудно использовать 
конструкцию  `?.let{}`.
- `run` - то же, что и `with`, только не принимает объект, а вызывается на нем, как `let`.
- `apply` - вызывается на объекте используя его область видимости в {}, возвращает этот же объект.

### Data класс, свойства. Чем плохо использование Data как JPA Entity

### Companion object

### Object-класс, свойства

## Spring

### Принцип работы, DI, IoC.

### Способы конфигурации Spring-приложения.

### Что такое Spring bean? Какие есть способы внедрить bean? Bean scope.

### Как в Spring используется паттерн Proxy? механизм AOP

### Аннотации @Bean, @Component, @ComponentScan

### Spring vs Spring boot

### Spring MVC - что это, основные аннотации.

### Spring Data JPA - что это, основные аннотации, преимущества/недостатки, FetchType, Cascade, проблема n+1,

### @Transactional

## Common

### Lombok

### HTTP

### REST

### Kafka: Принцип работы, плюсы по сравнению с синхронными вызовами. Реализация в Spring

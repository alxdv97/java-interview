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


#### Базовые интерфейсы

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
#### Иерархия
#### Виды

### Функциональные интерфейсы. 

### Stream API, основные операторы методы

### Основы многопоточности. Thread, synchronized, volatile, классы Atomic

## Kotlin

### Val/var

### Extension функции, как компилируются в джаве

### Null safety

### Классы Any, Unit, Nothing.

### With, let, apply, run

### Чем плохо последовательное использование map/filter/… на коллекциях? Как исправить?

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

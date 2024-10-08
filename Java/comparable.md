# Comparable 与 Comparator 的区别与使用  

## 1. 定义  

- **Comparable**:  
  - `Comparable` 是一个接口，它用于定义自然排序。实现该接口的类必须提供 `compareTo(T o)` 方法，允许该类的对象与其他对象进行比较。实现了 `Comparable` 接口的对象可以直接进行排序。  

- **Comparator**:  
  - `Comparator` 也是一个接口，但它用于定义自定义排序。通过实现 `Comparator` 接口的类可以定义一个用于比较两个对象的标准。它通常在需要不同的排序逻辑时使用。  

## 2. 主要方法  

- **Comparable**:  
  - `int compareTo(T o)`: 将当前对象与指定对象进行比较。返回值定义了两个对象的顺序关系：  
    - 返回负数：当前对象小于指定对象  
    - 返回零：当前对象等于指定对象  
    - 返回正数：当前对象大于指定对象  

- **Comparator**:  
  - `int compare(T o1, T o2)`: 比较两个对象的顺序。返回值的含义与 `compareTo` 方法类似。  
  - `boolean equals(Object obj)`: 与 `equals` 方法类似，但不常用。  

## 3. 使用场景  

- **Comparable**:  
  - 用于需要为类定义自然排序的情况，比如按照字母顺序排序字符串、按照年龄排序用户等。  
  - 适合类自身控制排序逻辑，使得类在比较时是不可变的。  

- **Comparator**:  
  - 用于需要多种不同排序方式的情况，可以通过创建不同的比较器来改变排序顺序。  
  - 允许在不修改原有类的情况下自定义排序逻辑，非常灵活。  

## 4. 示例  

### Comparable 示例  

```java  
class Person implements Comparable<Person> {  
    private String name;  
    private int age;  

    public Person(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  

    @Override  
    public int compareTo(Person other) {  
        return Integer.compare(this.age, other.age); // 按年龄排序  
    }  

    // getters  
}  
```
### Comparator
```java

class NameComparator implements Comparator<Person> {  
    @Override  
    public int compare(Person p1, Person p2) {  
        return p1.getName().compareTo(p2.getName()); // 按姓名字母顺序排序  
    }  
}  

// 使用示例  
Collections.sort(personList, new NameComparator());  
```
# 2. `comparing` 方法  

### 定义  
`comparing` 是 `Comparator` 接口的一个静态方法，允许你构造比较器，从而可以在一个表达式中指定要比较的属性。它通常与方法引用结合使用，以提高代码的可读性。  

### 方法签名  
```java  
static <T, U extends Comparable<? super U>> Comparator<T> 
comparing(Function<? super T, ? extends U> keyExtractor);
```  
### 使用
```java
personList.sort(comparing(Person::getAge)); // 按年龄排序  

people.sort((p1, p2) -> Integer.compare(p1.getAge(), p2.getAge())); 
```

# 3.Java 对象排序方法总结  

在 Java 中，可以使用三种主要方法对对象进行排序：使用 `Comparable` 接口、`Comparator` 接口以及通过 Java 8 的 Lambda 表达式。  

## 1. 实现 `Comparable` 接口  

### 描述  
- 在类中实现 `Comparable` 接口，覆盖 `compareTo` 方法，定义对象的自然排序规则。  

### 示例代码  

```java  
class Student implements Comparable<Student> {  
    private String name;  
    private int score;  

    public Student(String name, int score) {  
        this.name = name;  
        this.score = score;  
    }  

    @Override  
    public int compareTo(Student other) {  
        return Integer.compare(this.score, other.score); // 按分数升序排序  
    }  
}  

// 使用示例  
List<Student> students = new ArrayList<>();  
students.add(new Student("Alice", 85));  
students.add(new Student("Bob", 92));  
students.sort(null); // 使用自然排序  
```
## 2. 使用 Comparator 接口
### 描述
定义一个实现 Comparator 接口的比较器，覆盖 compare 方法，以定义自定义排序逻辑。
### 示例代码
```java 

class Student {  
    private String name;  
    private int score;  

    public Student(String name, int score) {  
        this.name = name;  
        this.score = score;  
    }  

    public int getScore() {  
        return score;  
    }  
}  

// 使用示例  
List<Student> students = new ArrayList<>();  
students.add(new Student("Alice", 85));  
students.add(new Student("Bob", 92));  

// 自定义比较器  
students.sort(new Comparator<Student>() {  
    @Override  
    public int compare(Student s1, Student s2) {  
        return Integer.compare(s1.getScore(), s2.getScore()); // 升序排序  
    }  
}); 
``` 
### 优点
* 更灵活，适合需要多种排序方式的情况。
* 比较器可以在不同的类中重用。
## 3. 使用 Lambda 表达式 (Java 8 及以上)
### 描述
使用 Lambda 表达式作为 Comparator 的实现，使代码更简洁。
### 示例代码
```java
// 使用示例  
List<Student> students = new ArrayList<>();  
students.add(new Student("Alice", 85));  
students.add(new Student("Bob", 92));  

// 使用 Lambda 表达式排序  
students.sort((s1, s2) -> Integer.compare(s1.getScore(), s2.getScore())); // 升序排序
```  
### 优点
* 语法简洁，更易于阅读。
* 方便快速创建一次性比较器。
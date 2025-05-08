

# 🚀 Functional Programming in Java 

### 🔹 1. Functional Programming Kya Hota Hai?
**Functional Programming (FP)** ek programming paradigm hai jisme **functions** ko **first-class citizens** ki tarah treat kiya jaata hai. Java 8 ke baad se Java mein bhi FP concepts ko support kiya jaane laga hai.

> "Java 8 ne Functional Programming ka gate khola Java ke liye."

---

### 🔹 2. Core Concepts of Functional Programming

#### ✅ 1. First-Class Functions
- Functions ko variables mein store kar sakte ho.
- Functions ko as parameter pass kar sakte ho.
- Function ko return kar sakte ho.

#### ✅ 2. Pure Functions
- Output sirf input pe depend karta hai.
- Side-effects nahi hote (jaise DB call, API call, etc).

```java
int square(int x) {
    return x * x; // No side-effects
}
```

#### ✅ 3. Immutability
- Data change nahi karte, naya data create karte hain.

#### ✅ 4. Higher-Order Functions
- Ek function jo doosre function ko accept ya return kare.

```java
Function<Integer, Integer> square = x -> x * x;
Function<Integer, Integer> doubleAndSquare = square.compose(x -> x * 2);
```

#### ✅ 5. Lazy Evaluation
- Calculation tab hoti hai jab zarurat ho (Stream API use karta hai isko).

---

### 🔹 3. Functional Interfaces (🔥 Must for Interviews)

#### ➤ Functional Interface:
- Sirf ek abstract method
- Java 8 annotation: `@FunctionalInterface`

```java
@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();
}
```

#### ✅ Popular Functional Interfaces (java.util.function):

| Interface        | Method      | Usage Example                     |
|------------------|-------------|-----------------------------------|
| `Function<T, R>` | apply       | Data transformation               |
| `Predicate<T>`   | test        | Boolean condition check           |
| `Consumer<T>`    | accept      | Consume input, no return          |
| `Supplier<T>`    | get         | Supply data without input         |
| `BiFunction<T,U,R>` | apply   | Function with 2 inputs            |
| `UnaryOperator<T>` | apply    | Same type in and out              |
| `BinaryOperator<T>` | apply   | 2 same type inputs, 1 output      |

---

### 🔹 4. Lambda Expressions (Super Important)

```java
(int a, int b) -> a + b
```

#### ➤ Syntax:
```java
(parameters) -> { body }
```

#### ✅ Example:
```java
Runnable r = () -> System.out.println("Running...");
```

#### ✅ Uses:
- Threads
- Collections (forEach, map, filter, etc.)
- Streams
- GUI events (onClick listeners, etc.)

---

### 🔹 5. Method References (Shorter Lambda)
```java
ClassName::methodName
```

#### ✅ Types:
1. **Static Method Reference** → `ClassName::staticMethod`
2. **Instance Method Reference** → `obj::instanceMethod`
3. **Constructor Reference** → `ClassName::new`

---

### 🔹 6. Stream API (Heart of FP in Java)

#### ➤ Stream Operations:

- **Intermediate**: filter, map, sorted
- **Terminal**: collect, forEach, reduce, count

#### ✅ Example:

```java
List<String> names = List.of("Ram", "Shyam", "Geeta");
names.stream()
     .filter(name -> name.startsWith("S"))
     .map(String::toUpperCase)
     .forEach(System.out::println);
```

---

### 🔹 7. Optional Class – Null Handling FP Style

```java
Optional<String> name = Optional.of("Amresh");
name.ifPresent(System.out::println);
```

#### ✅ Methods:
- `isPresent()`
- `ifPresent()`
- `orElse()`
- `map()`, `flatMap()`

---

### 🔹 8. Function Composition (Function Chaining)

```java
Function<Integer, Integer> times2 = x -> x * 2;
Function<Integer, Integer> square = x -> x * x;

Function<Integer, Integer> combined = times2.andThen(square);
System.out.println(combined.apply(3)); // (3*2)^2 = 36
```

---

### 🔹 9. Functional Programming in Collections

```java
List<String> list = Arrays.asList("a", "b", "c");
list.stream().map(String::toUpperCase).collect(Collectors.toList());
```

---

### 🔹 10. Interview-Level Questions & Concepts

| 🔥 Question | ✅ Focus |
|------------|----------|
| Functional Interface kya hota hai? | `@FunctionalInterface`, usage with Lambda |
| Lambda vs Anonymous Class? | Concise, no boilerplate |
| Stream API kaise kaam karta hai? | Lazy eval, pipeline |
| map vs flatMap? | Transform vs Flatten |
| Optional ka real use case? | Avoiding null pointer exception |
| Function chaining kaise hoti hai? | `andThen()`, `compose()` |
| Predicate and filter difference? | Predicate is input, filter is usage |
| Functional Programming ka benefit? | Cleaner, parallel-friendly code |

---

## ✅ Real-World Examples

#### 🔸 Sorting with Lambda
```java
list.sort((a, b) -> a.compareTo(b));
```

#### 🔸 Thread with Lambda
```java
new Thread(() -> System.out.println("Running")).start();
```

#### 🔸 Filtering Employees by Salary
```java
employees.stream()
         .filter(e -> e.getSalary() > 50000)
         .collect(Collectors.toList());
```

---





## Stream 이란 ?
자바 8에서 추가된 스트림(Streams)은 컬렉션, 배열 등에 저장된 요소들을 하나씩 참조하면서 코드를 실행할 수 있는 기능.
Stream을 사용하면, 불필요한 for문을 사용하지 않을 수 있고, 람다식을 활용할 수 있어서 코드를 직관적이게 처리할 수 있다.
## Stream 특징
- Stream은 데이터를 담는 저장소는 아니다.
- Stream은 데이터를 변경하지 않는다.
- Stream은 재사용할 수 없다.
- Stream은 각 요소가 1번씩 처리된다.
- Stream은 무제한일 수도 있다. (실시간으로 계속 들어올 수 있음)
## Stream 사용법
 Stream 은 데이터.Stream생성().중개연산()...종료연산(); 구조로 사용한다.
#### 중간 연산(Intermediate operation)
- filter() : 조건에 맞는 요소만 남김.
```java
List<String> words = Arrays.asList("apple", "banana", "cherry", "durian", "eggplant");

List<String> filteredWords = words.stream()
        .filter(word -> word.startsWith("a"))
        .collect(Collectors.toList());

System.out.println(filteredWords); // [apple]

```
- map() : 요소를 다른 값으로 변환.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> squaredNumbers = numbers.stream()
        .map(number -> number * number)
        .collect(Collectors.toList());

System.out.println(squaredNumbers); // [1, 4, 9, 16, 25]
```
- flatMap() : 요소를 다른 스트림으로 변환.
```java
List<List<Integer>> numbers = Arrays.asList(
        Arrays.asList(1, 2),
        Arrays.asList(3, 4),
        Arrays.asList(5, 6)
);

List<Integer> flattenedNumbers = numbers.stream()
        .flatMap(Collection::stream)
        .collect(Collectors.toList());

System.out.println(flattenedNumbers); // [1, 2, 3, 4, 5, 6]

```
- sorted() : 요소 정렬.
```java
List<String> words = Arrays.asList("banana", "cherry", "apple", "eggplant", "durian");

List<String> sortedWords = words.stream()
        .sorted()
        .collect(Collectors.toList());

System.out.println(sortedWords); // [apple, banana, cherry, durian, eggplant]
```
- distinct() : 중복된 요소 제거.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 2, 4, 1);

List<Integer> distinctNumbers = numbers.stream()
        .distinct()
        .collect(Collectors.toList());

System.out.println(distinctNumbers); // [1, 2, 3, 4, 5]
```
- limit() : 요소의 개수 제한.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> limitedNumbers = numbers.stream()
        .limit(3)
        .collect(Collectors.toList());

System.out.println(limitedNumbers); // [1, 2, 3]
```
- skip() : 요소의 처음 몇 개 제외.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

List<Integer> skippedNumbers = numbers.stream()
        .skip(2)
        .collect(Collectors.toList());

System.out.println(skippedNumbers); // [3, 4, 5]
```
#### 최종 연산(Terminal operation)
- forEach() : 각 요소를 순회하며 처리.
- count() : 요소의 개수를 반환.
- collect() : 요소를 수집하여 컬렉션 등으로 변환.
- reduce() : 요소를 하나씩 누적하여 결과를 반환.
- anyMatch() : 요소 중 하나라도 조건을 만족하는지 확인.
- allMatch() : 모든 요소가 조건을 만족하는지 확인.
- noneMatch() : 요소가 하나도 조건을 만족하지 않는지 확인.
- findFirst() : 첫 번째 요소를 반환.
- findAny() : 아무 요소나 하나를 반환.
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

// forEach() 메소드를 사용하여 각 요소를 출력
numbers.stream()
        .forEach(System.out::println);

// count() 메소드를 사용하여 요소의 개수 출력
long count = numbers.stream()
        .count();
System.out.println("Number of numbers: " + count);

// collect() 메소드를 사용하여 짝수를 List로 변환
List<Integer> evenNumbers = numbers.stream()
        .filter(n -> n % 2 == 0)
        .collect(Collectors.toList());
System.out.println("Even numbers: " + evenNumbers);

// reduce() 메소드를 사용하여 모든 요소의 합을 계산
int sum = numbers.stream()
        .reduce(0, (a, b) -> a + b);
System.out.println("Sum: " + sum);

// anyMatch() 메소드를 사용하여 요소 중에 3의 배수가 있는지 확인
boolean hasMultipleOf3 = numbers.stream()
        .anyMatch(n -> n % 3 == 0);
System.out.println("Has multiple of 3? " + hasMultipleOf3);

// allMatch() 메소드를 사용하여 모든 요소가 10보다 작은지 확인
boolean allLessThan10 = numbers.stream()
        .allMatch(n -> n < 10);
System.out.println("All less than 10? " + allLessThan10);

// noneMatch() 메소드를 사용하여 요소 중에 7이 없는지 확인
boolean hasNo7 = numbers.stream()
        .noneMatch(n -> n == 7);
System.out.println("Has no 7? " + hasNo7);

// findFirst() 메소드를 사용하여 첫 번째 짝수를 반환
Optional<Integer> firstEven = numbers.stream()
        .filter(n -> n % 2 == 0)
        .findFirst();
System.out.println("First even number: " + firstEven.orElse(-1));

// findAny() 메소드를 사용하여 아무 짝수나 하나를 반환
Optional<Integer> anyEven = numbers.stream()
        .filter(n -> n % 2 == 0)
        .findAny();
System.out.println("Any even number: " + anyEven.orElse(-1));
```

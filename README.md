# Java-Streams
Collection fo some basic java streams examples

<hr>

```java

    // Filtering elements
    List<Integer> evenNumbers = numbers.stream()
            .filter(n -> n%2 == 0)
            .toList();
    System.out.println(evenNumbers);
    
    // Mapping elements
    List<String> numberStrings = numbers.stream()
            .map(n -> "Number: " + n)
            .toList();
    System.out.println(numberStrings); // [Number: 1, Number: 2, Number: 3, Number: 4, Number: 5]
    
    // Collecting to a Set
    Set<Integer> uniqueNumbers = numbers.stream()
            .collect(Collectors.toSet());
    System.out.println(uniqueNumbers); //[1, 2, 3, 4, 5]
    
    // Collecting numbers to a Map
    Map<Integer,String> numberMap = numbers.stream()
            .collect(Collectors.toMap(n -> n, n -> "Number: "+ n));
    System.out.println(numberMap); //{1=Number: 1, 2=Number: 2, 3=Number: 3, 4=Number: 4, 5=Number: 5}
    
    // Counting elements
    long count = numbers.stream().count();
    System.out.println(count); // 5
    
    // Finding the minimum element
    Optional<Integer> min = numbers.stream()
            .min(Comparator.naturalOrder());
    System.out.println(min.get()); // 1
    
    // 9. Finding the maximum element
    Optional<Integer> max = numbers.stream()
            .max(Comparator.naturalOrder());
    System.out.println(max.get()); // 5
    
    // Checking if any element matches a predicate
    boolean anyMatch = numbers.stream()
            .anyMatch(n -> n > 5);
    System.out.println(anyMatch); // False
    
    // Checking if all the elements matches a predicate
    boolean allMatch = numbers.stream()
            .allMatch(n -> n > 0);
    System.out.println(allMatch); // true
    
    // Checking if no element match a predicate
    boolean noneMatch = numbers.stream()
            .noneMatch(n -> n < 0);
    System.out.println(noneMatch); // true
    
    // Finding the first element
    Optional<Integer> first = numbers.stream().findFirst();
    System.out.println(first.get()); // 1
    
    // Finding any element
    Optional<Integer> any = numbers.stream().findAny();
    System.out.println(any.get()); // 1
    
    // Reducing element to a single value
    int sum = numbers.stream().reduce(0, Integer::sum);
    System.out.println(sum); // 15
    
    // Summing elements - same as above
    int total = numbers.stream().mapToInt(Integer::intValue).sum();
    System.out.println(total); // 15
    
    // Averaging elements
    double average = numbers.stream().mapToInt(Integer::intValue).average().orElse(0.0);
    System.out.println(average); // 3.0
    
    // Summarizing statistics
    IntSummaryStatistics stats = numbers.stream().mapToInt(Integer::intValue).summaryStatistics();
    System.out.println(stats); //IntSummaryStatistics{count=5, sum=15, min=1, average=3.000000, max=5}
    
    // Concatenating Strings
    String concatenated = Stream.of("Hello", " ", "Performance").collect(Collectors.joining()); // can be reaplaced with String.join()
    System.out.println(concatenated); // Hello Performance
    
    // Finding distinct elements
    List<Integer> distinctNumbers = numbers.stream().distinct().collect(Collectors.toList());
    System.out.println(distinctNumbers); //[1, 2, 3, 4, 5]
    
    // Sorting Elements
    List<Integer> sortedNumbers = numbers.stream().sorted().toList();
    System.out.println(sortedNumbers); //[1, 2, 3, 4, 5]
    
    // Reverse Sorting
    List<Integer> reversedNumbers = numbers.stream().sorted(Comparator.reverseOrder()).toList();
    System.out.println(reversedNumbers); // [5, 4, 3, 2, 1]
    
    // Limiting elements
    List<Integer> limitedNumbers = numbers.stream().limit(3).toList();
    System.out.println(limitedNumbers); //[1,2,3]
    
    // Skipping first 2 elements
    List<Integer> skippedElements = numbers.stream().skip(2).toList();
    System.out.println(skippedElements); // [3, 4, 5]
    
    // Checking for null elements
    boolean hasNull = numbers.stream().anyMatch(Objects::isNull);
    System.out.println(hasNull); // false
    
    // Filtering out Non Null Numbers from a list
    List<Integer> nonNullNumbers = numbers.stream().filter(Objects::nonNull).toList();
    System.out.println(nonNullNumbers); //[1, 2, 3, 4, 5]
    
    // Grouping elements by Criteria
    Map<Boolean, List<Integer>> numberGroups = numbers.stream().collect(Collectors.groupingBy(n -> n%2 == 0));
    System.out.println(numberGroups); // {false=[1, 3, 5], true=[2, 4]}
    
    // Combining Multiple streams
    List<Integer> anotherNumbers = Arrays.asList(8, 9, 10);
    Stream<Integer> combinesStream = Stream.concat(numbers.stream(), anotherNumbers.stream());
    System.out.println(combinesStream.toList()); // [1, 2, 3, 4, 5, 8, 9, 10]
    
    // Zipping 2 streams
    List<Integer> zipped = Streams.zip(numbers.stream(), anotherNumbers.stream(), (s1, s2) -> s1 + s2).collect(Collectors.toList());
    System.out.println(zipped); // [9, 11, 13] -> This is Guava Library
    
    // Merging multiple streams
    Stream<Integer> mergedStream = Stream.of(numbers.stream(), anotherNumbers.stream()).flatMap(Function.identity());
    System.out.println(mergedStream.toList()); // [1, 2, 3, 4, 5, 8, 9, 10]
    
    // Finding an index of an element
    int target = 4;
    OptionalInt index = IntStream.range(0, numbers.size()).filter(i -> numbers.get(i) == target).findFirst();
    System.out.println(index.orElseThrow()); // 3
    
    // Creating an infinite streams of integers
    Stream<Integer> inifiteStream = Stream.iterate(0, n -> n+1);
    System.out.println(inifiteStream.limit(20).toList()); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
    
    // Generating a stream of random numbers
    IntStream randomStream = new Random().ints(0 , 100);
    System.out.println(randomStream.findAny().getAsInt()); // random number between 0 and 100
    
    // Repeating a value n times
    Stream<String> repeatedStream = Stream.generate(() -> "Hello").limit(5);
    System.out.println(repeatedStream.toList()); //[Hello, Hello, Hello, Hello, Hello]
    
    // Getting the index of the maximum element in a stream
    OptionalInt maxIndex = IntStream.range(0, numbers.size()).reduce((i, j)-> numbers.get(i) > numbers.get(j) ? i : j);
    System.out.println(maxIndex.orElseThrow()); // 4 -> this is the index of the max element
    
    // Removing duplicate elements while preserving order
    List<Integer> uniqueOrderedElements = numbers.stream().distinct().toList();
    System.out.println(uniqueOrderedElements); // [1, 2, 3, 4, 5]
    
    // Creating parallel stream
    List<Integer> parallelResult = numbers.parallelStream().map(n -> n * 2).toList();
    System.out.println(parallelResult); // [2, 4, 6, 8, 10]
    
    // Flattening a nested list
    List<List<Integer>> nestedList = Arrays.asList(
            Arrays.asList(1,2,3),
            Arrays.asList(5,6,7)
    );
    List<Integer> flatList = nestedList.stream().flatMap(List::stream).toList();
    System.out.println(flatList); // [1, 2, 3, 5, 6, 7]
    
    // Converting a stream to an array
    Integer[] array = numbers.stream().toArray(Integer[]::new);
    System.out.println(Arrays.toString(array)); // [1, 2, 3, 4, 5]
    
    // Creating a stream of characters from a string
    IntStream charStream = "Perf".chars();
    System.out.println(Arrays.toString(charStream.toArray()));// [80, 101, 114, 102] - This will print the int for the respective chars
    
    // Summing of squares of even numbers
    int sumOfEvenNumbers = numbers.stream().filter(n -> n%2 == 0).mapToInt(n -> n * n).sum();
    System.out.println(sumOfEvenNumbers); // 20
    
    // Finding the longest string
    List<String> strings = Arrays.asList("Performance", "Tester", "Hello");
    Optional<String> longestString = strings.stream().max(Comparator.comparingInt(String::length));
    System.out.println(longestString.orElseThrow()); // Performance
    
    // Combining elements into a string with delimiter
    String joinedString = strings.stream().collect(Collectors.joining(": "));
    System.out.println(joinedString); // Performance: Tester: Hello
    
    // Checking if all the strings are upper case
    boolean allUpperCase = strings.stream().allMatch(s -> s.equals(s.toUpperCase()));
    System.out.println(allUpperCase); // false
    
    // Counting occurrences of each element
    Map<Integer, Long> freqMap = numbers.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
    System.out.println(freqMap); // {1=1, 2=1, 3=1, 4=1, 5=1}
    
    // another way of checking if all the elements are unique
    boolean allUnique = numbers.stream().distinct().count() == numbers.size();
    System.out.println(allUnique); // true
    
    // Summing up the first n elements
    int sunmFirstN = numbers.stream().limit(3).mapToInt(Integer::intValue).sum();
    System.out.println(sunmFirstN); // 6
    
    // Finding the most common element
    Optional<Map.Entry<Integer, Long>> mostCommon = numbers.stream().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
            .entrySet().stream().max(Map.Entry.comparingByValue());
    System.out.println(mostCommon.orElseThrow()); // 1=1
    
    // Check if any string containing substring
    boolean containSubString = strings.stream().anyMatch(s -> s.contains("Perf"));
    System.out.println(containSubString); //  true
    
    // Grouping string elements by their length
    Map<Integer, List<String>> groupedByLength = strings.stream().collect(Collectors.groupingBy(String::length));
    System.out.println(groupedByLength); // {5=[Hello], 6=[Tester], 11=[Performance]}
    
    // Collecting elements to a concurrent map
    ConcurrentMap<Integer, String> concurrentMap = numbers.stream().collect(Collectors.toConcurrentMap(n -> n, n -> "Number: " + n));
    System.out.println(concurrentMap); //  {1=Number: 1, 2=Number: 2, 3=Number: 3, 4=Number: 4, 5=Number: 5}
    
    // Limiting elements until a condition is met
    List<Integer> limitedUntilCondition = numbers.stream().takeWhile(n -> n < 5).toList();
    System.out.println(limitedUntilCondition); // [1, 2, 3, 4]
    
    // Summing elements with an initial value
    int sumWithInitial = numbers.stream().reduce(10, Integer::sum);
    System.out.println(sumWithInitial); // 25
    
    // Mapping elements to their index
    Map<Integer, String> indexToValueMap = IntStream.range(0, numbers.size()).boxed().collect(Collectors.toMap(i->i, i-> numbers.get(i).toString()));
    System.out.println(indexToValueMap); // {0=1, 1=2, 2=3, 3=4, 4=5}
    
    // Filtering based on multiple conditions
    List<Integer> filtered = numbers.stream().filter(n -> n > 0 &&  n < 4)
            .toList();
    System.out.println(filtered); // [1, 2, 3]
    
    // Concatenating Strings with delimiter
    String delimited = strings.stream().collect(Collectors.joining(" | "));
    System.out.println(delimited); // Performance | Tester | Hello
    
    // Mapping elements to their square roots
    List<Double> squareRoots = numbers.stream().map(Math::sqrt).toList();
    System.out.println(squareRoots); // [1.0, 1.4142135623730951, 1.7320508075688772, 2.0, 2.23606797749979]
    
    // Finding the average length of the strings
    double avgLength = strings.stream().mapToInt(String::length).average().orElse(0.0);
    System.out.println(avgLength); // 7.33333333333
    
    // Grouping elements by their first character
    Map<Character, List<String>> groupedByFirstChar = strings.stream().collect(Collectors.groupingBy(s -> s.charAt(0)));
    System.out.println(groupedByFirstChar); // {P=[Performance], T=[Tester], H=[Hello]}
    
    // Checking if any string is empty
    boolean isEmptyString = strings.stream().anyMatch(String::isEmpty);
    System.out.println(isEmptyString); // false
    
    // Finding the longest word in the string list
    Optional<String> longestWord = strings.stream().max(Comparator.comparingInt(String::length));
    System.out.println(longestWord.get()); // Performance
    
    // Summing elements with parallel procesing
    int sumParallel = numbers.stream().mapToInt(Integer::intValue).sum();
    System.out.println(sumParallel); // 15
    
    // Reverse a string  - here using StringBuilder
    String reversed = new StringBuilder("Performance").reverse().toString();
    System.out.println(reversed); // ecnamrofreP
    
    // Finding the common elements between 2 lists
    List<Integer> input2List = Arrays.asList(2,3,5,7); // assume numbers = [1,2,3,4,5]
    List<Integer> commonElements = numbers.stream().filter(input2List::contains).toList();
    System.out.println(commonElements); // [2, 3, 5]
    
    // Creating a stream of dates in range
    LocalDate startDate = LocalDate.of(2024, 1 ,1);
    LocalDate endDate = LocalDate.of(2024, 1, 5);
    Stream<LocalDate> dateStream = Stream.iterate(startDate, date -> date.plusDays(1)).limit(ChronoUnit.DAYS.between(startDate, endDate));
    System.out.println(dateStream.toList()); // [2024-01-01, 2024-01-02, 2024-01-03, 2024-01-04]
    
    // Collecting elements to an unmodifiable list
    List<Integer> unmodifiableList = numbers.stream().collect(Collectors.toUnmodifiableList());
    System.out.println(unmodifiableList); // [1, 2, 3, 4, 5]
    
    // Finding the most common character
    Optional<Character> mostCommonCharacter = strings.stream().flatMapToInt(CharSequence::chars).mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting())).entrySet().stream()
            .max(Map.Entry.comparingByValue()).map(Map.Entry::getKey);
    System.out.println(mostCommonCharacter.get()); // e
    
    // Finding the shortest string
    Optional<String> shortestString = strings.stream().min(Comparator.comparingInt(String::length));
    System.out.println(shortestString.get()); // Hello
    
    // Check if any string is a palindrome
    boolean palindrome = strings.stream().anyMatch(s -> s.contentEquals(new StringBuilder(s).reverse()));
    System.out.println(palindrome); // false
    
    // Combining elements with a custom logic
    Map<Integer, List<String>> combinedMap = strings.stream()
            .collect(Collectors.groupingBy(String::length, Collectors.mapping(String::toUpperCase, Collectors.toList())));
    System.out.println(combinedMap); // {5=[HELLO], 6=[TESTER], 11=[PERFORMANCE]}
    
    // Summing the ascii values of characters in a string
    int sumAscii = "Performance".chars().sum();
    System.out.println(sumAscii); //1138
    
    // Check if all the elements are uppercase
    boolean isAllUpper = strings.stream().allMatch(s -> s.equals(s.toUpperCase()));
    System.out.println(isAllUpper); // false
    
    // checking if all the elements are equal
    boolean allEqual = numbers.stream().distinct().limit(2).count() <= 1;
    System.out.println(allEqual); // false
    
    // Last occurrence of an element in a list
    OptionalInt lastIndex = IntStream.range(0, numbers.size()).reduce((i, j) -> numbers.get(j).equals(target) ? j : i);
    System.out.println(lastIndex.getAsInt()); // 3
    
    // Finding the medial of numbers
    OptionalDouble median = numbers.stream().mapToDouble(Integer::doubleValue).skip((count-1) / 2).limit(2 - count%2).average();
    System.out.println(median.getAsDouble()); // 3.0
    
    // Checking if all the elements contains certain substring
    boolean containAllSubstring = strings.stream().allMatch(s -> s.contains("Perf"));
    System.out.println(containAllSubstring); // false
    
    // Finding the longest palindrome
    Optional<String> longestPalindrome = strings.stream().filter(s -> s.equals(new StringBuilder(s).reverse().toString())).max(Comparator.comparingInt(String::length));
    System.out.println(longestPalindrome.orElse("No palindrome available")); // No palindrome available
    
    // Finding the shortest palindrome
    Optional<String> shortestPalindrome = strings.stream().filter(s -> s.equals(new StringBuilder(s).reverse().toString())).min(Comparator.comparingInt(String::length));
    System.out.println(longestPalindrome.orElse("No palindrome available")); // No palindrome available
    
    // Checking if any element matches a reges pattern
    boolean anyMatchesPattern = strings.stream().anyMatch(s -> s.matches("Hello"));
    System.out.println(anyMatchesPattern); // true

```
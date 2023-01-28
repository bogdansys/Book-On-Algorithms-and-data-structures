# Maps, Hashing, Sorted Maps, Sets, MultiMaps and MultiSets

# Maps

- maps a value to a key
- set of pairs of Key, Value

### Hashing

In the context of maps, hashing is a technique used to map keys to values. A hash table is a data structure that stores a collection of key-value pairs, where each key is mapped to a specific value using a hash function.

The hash function takes an input (also called a key) and produces an output (called a hash code or index) that is used to store the key-value pair in the hash table. The goal of the hash function is to generate a unique index for each key, so that it can be quickly retrieved or searched for in the table. The process of determining the index for a key is called hashing.

When a key-value pair is added to the hash table, the key is passed through the hash function to produce an index, and the value is stored at that index. When a value is requested for a key, the key is passed through the hash function again to determine the index where the value is stored, and the value is then returned.

There are 2 ways of dealing with collisions inside of a map:

- separate chaining
- linear probing

### Separate Chaining

Separate chaining is a collision resolution technique used in hash tables to handle the case when two or more keys have the same hash code. The basic idea behind separate chaining is to create a linked list for each index of the hash table, where each node of the list stores a key-value pair.

When a new key-value pair is added to the hash table, the key is passed through the hash function to determine the index where the pair should be stored. If the index is empty, the pair is added as the head of the new list. If the index is already occupied, the pair is added as a new node at the end of the list.

When a value is requested for a key, the key is passed through the hash function again to determine the index of the list where the key might be located. The algorithm then searches through the list for the key, and returns the associated value if the key is found.

The time complexity of operations in a hash table with separate chaining is affected by the number of collisions. In the worst-case scenario, where all the keys hash to the same index, the time complexity of each operation becomes O(n), where n is the number of keys stored in the table. In the best-case scenario, where there are no collisions, the time complexity of each operation is O(1).

Advantages of Separate Chaining:

- Simpler to implement than other collision resolution techniques
- It can be used with any hash function, not only with specific ones
- Not subject to clustering, where all the keys hash to a small number of indices
- Load factor can be kept low in order to keep good performance

Disadvantages of Separate Chaining:

- Increased memory usage due to the additional storage required for the linked lists.
- Performance degrade as the load factor increase, and worst-case time complexity becomes O(n)

### Linear Probing

Linear probing is a collision resolution technique used in hash tables to handle the case when two or more keys have the same hash code. The basic idea behind linear probing is to find the next open slot in the hash table when a collision occurs.

When a new key-value pair is added to the hash table, the key is passed through the hash function to determine the index where the pair should be stored. If the index is empty, the pair is added to the table at that index. If the index is already occupied, the algorithm checks the next index, and if that index is also occupied, it continues checking the next index until an empty slot is found. The key-value pair is then added to the first empty slot that is found.

When a value is requested for a key, the key is passed through the hash function again to determine the index where the key might be located. If the index is empty, the key is not in the table and a null value is returned. If the index is occupied, the algorithm checks the key at that index. If the key at that index matches the requested key, the associated value is returned. If the key at that index does not match, the algorithm checks the next index, and continues checking until either the key is found or an empty slot is encountered.

The time complexity of operations in a hash table with linear probing is affected by the number of collisions. In the worst-case scenario, where the hash table becomes full, the time complexity of each operation becomes O(n), where n is the number of keys stored in the table. In the best-case scenario, where there are no collisions, the time complexity of each operation is O(1).

Advantages of Linear Probing:

- Simple to implement
- Cache-friendly, since the keys are stored in a contiguous block of memory

Disadvantages of Linear Probing:

- Clustering: As keys are added, keys that hash to nearby indices cluster together. This could lead to an increase in collisions and degrade the performance of the hash table.
- Load factor should be kept low, to avoid clustering and maintain good performance

## Sorted Map

Is a map in which the keys are always sorted.

methods:

![Untitled](Untitled%2020.png)

# Sets

 In Java, the **`Set`** interface is a member of the Java Collections Framework. A set is a collection that cannot contain duplicate elements. The **`Set`** interface provides methods for accessing the elements of a finite mathematical set. Some of the most commonly used implementation classes of the **`Set`** interface in Java include **`HashSet`**, **`TreeSet`**, and **`LinkedHashSet`**.

**`HashSet`** is a class that implements the **`Set`** interface. It uses a **`HashMap`** to store the elements of the set. The **`HashSet`** class is not ordered and does not guarantee any specific order of the elements. It is efficient for searching, adding and removing elements.

**`TreeSet`** is another class that implements the **`Set`** interface. It uses a **`TreeMap`** to store the elements of the set, which means that the elements are sorted according to their natural ordering, or according to a **`Comparator`** provided at the time of creation of the **`TreeSet`** instance.

**`LinkedHashSet`** is similar to **`HashSet`** but it maintains the insertion order of elements. So it is faster than **`TreeSet`** but slower than **`HashSet`**.

# Multisets

In Java, a "multiset" is a type of data structure that is similar to a set, but allows for duplicate elements to be stored. One way to implement a multiset in Java is to use a HashMap where the keys are the elements in the multiset and the values are the counts of how many times each element appears in the multiset. Here's an example of a basic implementation of a multiset using a HashMap → 

The above code defines a generic MultiSet class that stores elements of type T. The class has an instance variable called "map" that is an instance of HashMap<T, Integer>. The map stores the elements of the multiset as keys and the number of occurrences of each element as values.

This is just one way to implement a multiset in Java, and there are many different libraries and data structures that can be used to accomplish this. For example, Guava library provides a **`Multiset`** implementation and the Apache commons-collections library also has a **`MultiSet`** implementation.

Note that, This is just a skeleton of the implementation, in practice, you would also want to add more functionality to the class, such as iterating over the elements, checking if the multiset is empty, getting the size of the multiset, etc.

# Multimaps

A MultiMap is a map that allows multiple values to be associated with a single key. In other words, it is a map that can map a single key to multiple values. The implementation of a MultiMap in Java is often done using a Map of List or Set objects.

For example, let's say you have a MultiMap that stores information about people and their favorite colors. Each person is represented by a key, and their favorite colors are the associated values. The map would look something like this:

```java
import java.util.HashMap;
import java.util.Map;

public class MultiSet<T> {
    private Map<T, Integer> map;

    public MultiSet() {
        map = new HashMap<>();
    }

    public void add(T element) {
        int count = map.getOrDefault(element, 0);
        map.put(element, count + 1);
    }

    public void remove(T element) {
        if (map.containsKey(element)) {
            int count = map.get(element);
            if (count > 1) {
                map.put(element, count - 1);
            } else {
                map.remove(element);
            }
        }
    }

    public int count(T element) {
        return map.getOrDefault(element, 0);
    }
}
```

```java
**John -> [Red, Blue]
Jane -> [Green, Yellow]
Bob -> [Red]**
```

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class MultiMap<K, V> {
    private Map<K, List<V>> map = new HashMap<>();

    public void put(K key, V value) {
        if (!map.containsKey(key)) {
            map.put(key, new ArrayList<>());
        }
        map.get(key).add(value);
    }

    public List<V> get(K key) {
        return map.get(key);
    }

    public void remove(K key, V value) {
        List<V> values = map.get(key);
        if (values != null) {
            values.remove(value);
            if (values.isEmpty()) {
                map.remove(key);
            }
        }
    }
}
```
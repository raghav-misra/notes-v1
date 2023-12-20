# c++ reference.

## hello.

I used this course to study DSA: [fire course](https://www.udemy.com/course/data-structures-algorithms-cpp/).

Good playlist for STL stuff (in Hindi): [fire playlist](https://www.youtube.com/watch?v=R5BEcvTVZj0&list=PLauivoElc3gh3RCiQA82MDI-gJfXQQVnn).

## includes.

- We want to `#include<iostream>` to use stuff like `cin` and `cout`.
- We want to `#include<vector>` to use `vector`.
- We want to `#include<array>` to use STL `array`. (Not needed for C-style arrays)

## stl arrays.

STL arrays are a structure that thinly wrap around C-style arrays, but make certain things a bit easier.

```c++
// make int array of size 3
array<int, 3> nums[3];

// set at index ~ O(1)
nums[0] = 69;
nums[1] = 420;
nums[2] = 567897654;

// swap the values at two indices ~ O(1)
swap(nums[0], nums[1]);

// get at index ~ O(1)
cout << "first num " << nums[0] << "\n";

// iterate over array ~ O(n)
for (int i = 0; i < nums.size(); ++i) {
    cout << "num at pos " << i << " is " << nums[i] << "\n";
}
```

## pairs.

2-tuples for C++.

```cpp
pair<int, string> p = { 1, "hello" };

// print first and second elements of pair p
cout << "pair p" << p.first << ", " << p.second << "\n";

// deep copying
pair<int, string> pc = p;
pc.first = 7;

// print first and second elements of pair p
cout << "pair p" << p.first << ", " << p.second << "\n"; // doesn't change

// reference copying
pair<int, string> &pc2 = p;
pc2.first = 7;

// print first and second elements of pair p
cout << "pair p" << p.first << ", " << p.second << "\n"; // it changes!
```

## vectors.

Vectors are just lists for C++.

```c++
// create an int vector
vector<int> v;

// add numbers to the end ~ O(1)
v.push_back(69); // after this: [69]
v.push_back(420); // after this: [69, 420]
v.push_back(856); // after this: [69, 420, 856]

// remove numbers from the end ~ O(1)
v.pop_back(); // after this: [69, 420]

// remove numbers from the start (by laufey) ~ O(n)
v.erase(v.begin()); // after this: [420]

// insert at given index ~ O(n)
v.insert(v.begin(), 11); // after this: [11, 420]
v.insert(v.begin() + 1, 12); // after this: [11, 12, 420]

// iterate over vector ~ O(n)
for (int i = 0; i < v.size(); ++i) {
    cout << "num at pos " << i << " is " << v[i] << "\n";
}

// remember with pairs, copying by default will clone the vector deeply.
// for a reference copy, do the following:
vector<int> &v2 = v;
```

## iterators.

Structures like maps and sets don't have numeric indices, meaning we can't do the `for i = 0 ... i++` notation to iterate over them. Iterators allow us to loop over these structures, as well as vectors and arrays. Iterators are pointers that take advantage of the memory storage of these data structures to loop over them.

```cpp
// create an int vector
vector<int> v;
v.push_back(69); 
v.push_back(420); 
v.push_back(856); 

// create an iterator for vector v
// this iterator it points to the first element of v
vector<int>::iterator it = v.begin();

// get the value at current position with *it
cout << "manual: element is " << *it << "\n";

// move to the next position
it++;

// *it now returns element at second position
cout << "manual iterator: " << *it << "\n\n";

// looping with an iterator
// v.end() is the position *after* the vector,
// so once the iterator reaches it, it knows to stop.
// "auto" infers that it2 is a vector<int>::iterator, cleans our code.
for (auto it2 = v.begin(); it2 != v.end(); ++it2) {
    cout << "for loop: " << *it2 << "\n";
}

cout << "\n";

// range based loops!
// remove the need for explicit iterators!
// to be able to modify the structure, use &value over value.
for (int value : v) {
    cout << "range based loop: " << value << "\n";
}
```

## maps!

The `map` and `unordered_map` have the same API surface, just that `unordered_map` doesn't store keys in any order. A result of this is that `unordered_map` performs reads and writes in `O(1)` time, whereas `map` takes `O(log n)` time. (`map` is implemented internally with a binary search tree.)

```cpp
// initialize map (kv-store):
map<int, string> m;

// modify values by key:
m[1] = "hello";
m[600] = "world";

// you can also insert this way but it looks ugly:
m.insert({4, "goodbye"});

// grab values by key:
cout << "wow " << m[1] << ", " << m[600] << "\n\n"; // "wow hello, world"

// iterator looping over the map:
for (auto it = m.begin(); it != m.end(); ++it)
{
    // each iteration is a key value pair!
    // it->first is key and it->second is value
    cout << "iterator looping: (" << (it->first) << ", " << (it->second) << ")\n";
}

cout << "\n";

// range based loop
// kv will be a pair, first is key and second is value
for (auto kv : m)
{
    cout << "range based looping: (" << (kv.first) << ", " << (kv.second) << ")\n";
}

cout << "\n";

// let's remove a pair by its key:
m.erase(1);

// m.find() returns a iterator to the pair if key exists, 
// otherwise it returns the iterator to m.end()
auto itFound = m.find(1);

if (itFound != m.end()) {
    cout << "key 1 exists with value: " << (*itFound).second << "\n";
} else {
    cout << "key 1 doesn't exist.";
}
```

## sets.

The `set` and `unordered_set` have the same API surface, just that `unordered_set` doesn't store items in any order. A result of this is that `unordered_set` performs reads and writes in `O(1)` time, whereas `set` takes `O(log n)` time. (`set` is implemented internally with a binary search tree.)

```CPP
// create a set of strings
set<string> s;

// add to set
s.insert("bruh");
s.insert("bruh2");
s.insert("bruh3");

// remove from set
s.erase("bruh");

// find an element (returns iterator to element or s.end())
auto itFound = s.find("bruh");

if (itFound != s.end()) {
    cout << "found bruh in set." << endl;
} else {
    cout << "bruh not in set." << endl;
}

cout << endl;

// range based loop
for (string element : s) {
    cout << "range for loop: " << element << endl;
}
```


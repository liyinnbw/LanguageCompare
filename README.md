# LanguageCompare
Comparison of language APIs
- [String](#string)
- [Continuous Memory Dynamic Array](#continuous-memory-dynamic-array)
- [Linked List](#linked-list)
- [Hash Table](#hash-table)
- [Stack](#stack)
- [Queue](#queue)
- [Priority Queue](#priority-queue)
- [Sort](#sort)
- [Bits](#bits)
- [Type Convert](#type-convert)
- [Infinity](#infinity)
- [Random](#random)
- [Set](#set)
- [OOP](#oop)

## String
<details>
<summary>C++</summary>

#### Init
```
#include <string> //for string

// 1. single line
string s = "hello world"

// 2. multi line
string s = "hello "
           "world"; //same as s = "hello world"
```

#### String Builder
```
#include <iostream>
ostringstream oss;
oss<<"a"<<"b";
string s=iss.str();
```

#### String Format
```
#include <iomanip>
#include <bitset>

float a = 10.546;
cout<<a<<endl; //10.546
cout<<std::setprecision(2)<<std::fixed;
cout<<a<<endl; //10.55 (with good rounding)
cout<<std::setprecision(6)<<std::defaultfloat; //reset to default

cout<<std::setprecision(0)<<std::fixed;
cout<<a<<endl; //11 (with good rounding)
cout<<std::setprecision(6)<<std::defaultfloat; //reset to default

cout<<std::setprecision(2)<<std::scientific;
cout<<a<<endl; //1.05e+01
cout<<std::setprecision(6)<<std::defaultfloat; //reset to default

cout<<std::setw(12);
cout<<a<<endl; //      10.546 (left pad to 12 chars)
cout<<std::setw(0); //reset to default

cout<<std::setw(12)<<std::setfill ('0');
cout<<a<<endl; //00000010.546 (left pad to 12 chars with 0s)
cout<<std::setw(0)<<std::setfill (' '); //reset to default

cout<<std::setw(12)<<std::setfill ('0')<<std::left;
cout<<a<<endl; //10.546000000 (right pad to 12 chars with 0s)
cout<<std::setw(0)<<std::setfill (' ')<<std::right; //reset to default

int b = 100;
cout<<std::bitset<8*sizeof(b)>(b)<<endl; //00000000000000000000000001100100

cout<<std::oct; //octal: base 8
cout<<b<<endl; //144
cout<<std::dec;

cout<<std::hex; //hexal: base 16
cout<<b<<endl; //64
cout<<std::dec;
```

#### Substring
```
string subs = s.substr(startIdx, len);
```

#### Find Substring Index
```
size_t startIdx = s.find(substring);
if (startIdx == string::npos){
    //not found
}
```

#### Replace Substring
```
// 1. replace known segment
s.replace(startIdx, len, newstring); //replaced substring can be of different length than new string

// 2. find and replace first occurrence
size_t startIdx = s.find(substring);
if (startIdx != string::npos){
    s.replace(startIdx, substring.length(), newstring);
}

// 3. find and replace all occurrences
size_t startIdx = 0;
while ((startIdx = s.find(substring, startIdx)) != string::npos){
    s.replace(startIdx, substring.length(), newstring);
    startIdx += substring.length();
}
```

#### Reverse String
```
std::reverse(s.begin(),s.end()); //inplace
```

#### Split String
```
size_t startIdx = 0;
size_t endIdx = 0;
vector<string> splitted;
while ((endIdx = s.find(delimiter, startIdx)) != string::npos){
    splitted.emplace_back(s.substr(startIdx, endIdx-startIdx));
    startIdx = endIdx+delimiter.length();
}
splitted.emplace_back(s.substr(startIdx, endIdx-startIdx));
```

#### Trim
```
```

#### Change Case
```
#include <algorithm>

// 1. to upper
transform(s.begin(), s.end(),s.begin(), ::toupper);

// 2. to lower
transform(s.begin(), s.end(),s.begin(), ::tolower);

```

</details>

<details>
<summary>Python</summary>
    
#### Init
```
// 1. single line
s = 'hello world'

// 2. multi line
s = 'hello \
world' //same as s = "hello world"

// 3. multi line with line break
s = """hello
world""" // this will insert line break between "hello" and "world"
```

#### String Builder
```
// 1. array join
arr = []
arr.append('a')
arr.append('b')
s = ''.join(arr)

// 2. string format
a ='a'
b ='b'
s = f'{a}{b}' #python 3.6 and above
```

#### String Format
```
# fstring requires python 3.6 and above
a = 10.546
print(f'{a}') #10.546
print(f'{a:.2f}') #10.55 (with good rounding)
print(f'{a:.0f}') #11 (with good rounding)
print(f'{a:.2%}') #1054.60%
print(f'{a:%}') #1054.600000% (0 padded to achieve default chars)
print(f'{a:.2e}') #1.05e+01
print(f'{a:e}') #1.054600e+01 (0 padded to achieve default chars)
print(f'{a:12}') #      10.546 (left pad to 12 chars, same as {a:>12})
print(f'{a:<12}') #10.546 (right pad to 12 chars)
print(f'{a:012}') #00000010.546 (left pad to 12 chars with 0s, same as {a:>012})
print(f'{a:<012}') #10.546000000 (right pad to 12 chars with 0s)

b = 100
print(f'{b:b}') #1100100 (binary, base 2)
print(f'{b:o}') #144 (octal, base 8)
print(f'{b:x}') #64 (hexal, base 16)

c = (a,b)
print(f'{a},{b}') #10.546,100
print(f'{c}') #(10.546, 100)
```

#### Substring by Index
```
subs = s[startIdx:endIdx+1]
```

#### Find Substring Index
```
startIdx = s.find(substring) //return -1 if not found
```

#### Replace Substring
```
// 1. replace known segment
s = f'{s[:startIdx]}{newstring}{s[endIdx+1:]}'

// 2. find and replace first occurrence
s = s.replace(substring, newstring, 1)

// 3. find and replace all occurrences
s = s.replace(substring, newstring)
```

#### Reverse String
```
s = s[::-1]
```

#### Split String
```
arr = s.split(delimiter)
```

#### Trim
```
s = s.trim()
```

#### Change Case
```
// 1. to upper
s = s.upper()

// 2. to lower
s = s.lower()
```

</details>

<details>
<summary>JavaScript</summary>
    
#### Init
```
// 1. single line
let s = 'hello world'

// 2. multi line
TODO
```

#### String Builder
```
// template literals
let a ='a'
let b ='b'
let s = `${a}${b}`
```

#### String Format (TODO)
```
# fstring requires python 3.6 and above
a = 10.546
print(f'{a}') #10.546
print(f'{a:.2f}') #10.55 (with good rounding)
print(f'{a:.0f}') #11 (with good rounding)
print(f'{a:.2%}') #1054.60%
print(f'{a:%}') #1054.600000% (0 padded to achieve default chars)
print(f'{a:.2e}') #1.05e+01
print(f'{a:e}') #1.054600e+01 (0 padded to achieve default chars)
print(f'{a:12}') #      10.546 (left pad to 12 chars, same as {a:>12})
print(f'{a:<12}') #10.546 (right pad to 12 chars)
print(f'{a:012}') #00000010.546 (left pad to 12 chars with 0s, same as {a:>012})
print(f'{a:<012}') #10.546000000 (right pad to 12 chars with 0s)

b = 100
print(f'{b:b}') #1100100 (binary, base 2)
print(f'{b:o}') #144 (octal, base 8)
print(f'{b:x}') #64 (hexal, base 16)

c = (a,b)
print(f'{a},{b}') #10.546,100
print(f'{c}') #(10.546, 100)
```

#### Substring by Index (TODO)
```
subs = s[startIdx:endIdx+1]
```

#### Find Substring Index (TODO)
```
startIdx = s.find(substring) //return -1 if not found
```

#### Replace Substring (TODO)
```
// 1. replace known segment
s = f'{s[:startIdx]}{newstring}{s[endIdx+1:]}'

// 2. find and replace first occurrence
s = s.replace(substring, newstring, 1)

// 3. find and replace all occurrences
s = s.replace(substring, newstring)
```

#### Reverse String (TODO)
```
s = s[::-1]
```

#### Split String (TODO)
```
arr = s.split(delimiter)
```

#### Trim (TODO)
```
s = s.trim()
```

#### Change Case
```
// 1. to upper
let s = s.toUpperCase();

// 2. to lower
let s = s.toLowerCase();
```

</details>

## Continuous Memory Dynamic Array
<details>
<summary>C++</summary>

#### Init
```
#include <vector> //for vector
1. vector< T > vec;
2. vector< T > vec(size);
3. vector< T > vec(size, default);
4. vector< T > vec({a,b,c});
```
#### Iterate
```
// 1. if you only need to read, use range-based for loop
for(const T& item: vec){ } 

// 2. if you want to update, remove const keyword
for(T& item: vec){item = newitem;}

// 3. if you want to delete while iterating
vec.erase(remove_if(vec.begin(), vec.end(), [](const T &x)->bool { //note without &, x will be copied
    return (boolean condition, true for remove); 
}), vec.end());
```
#### Check if item exists
```
#include <algorithm> // for find
it = std::find (vec.begin(), vec.end(), item);
return it!=vec.end();
```
#### Search item first occurrence idx
```
#include <algorithm> // for find
#include <iterator> // for distance
it = std::find (vec.begin(), vec.end(), item);
if (it!=vec.end()){
    return std::distance(vec.begin(), it);
}else{
    //not found
}
```
#### Search item ALL occurrence idices
```
#include <algorithm> //for find
std::vector<T>::iterator it = vec.begin();
std::vector<int> indices;
while ((iter = std::find(it, vec.end(), item)) != vec.end())
{
    indices.push_back(std::distance(vec.begin(), it));
    ++it;
}
```
#### Count item
```
#include <algorithm> // for count
count = std::count(vec.begin(), vec.end(), item);
```
#### Add to back
```
// 1. item is copied, use this if item is received from elsewhere
vec.push_back(item);

// 2. item is created in-place, use this if item is created on spot
vec.emplace_back(Args of item constructor); 
```
#### Delete from back
```
// 1. 
if(!vec.empty()){ // important, if not checked, popping from empty vector causes error
    item = vec.back(); // make a copy of item (only if you need it later on)
    vec.pop_back(); // last item destructor called, return void
} 

// 2.
if(!vec.empty()){
    vec.resize(vec.size()-1); //last item destructor called
)
```
#### Insert to index i
```
// note the +/- operator is only defined for random access container like vector
// generally, only ++/-- is defined for sequential access container like linked list
// 1. item is copied, return iterator points to index i of resultant vector
it = vec.insert(vec.begin()+i, item);

// 2. item is created in-place, return iterator points to index i of resultant vector
it = vec.emplace(vec.bein()+i, Args of T constructor); 

// 3. copy items from another container's range [it_first, it_last) and insert to vec, starting at index i. return iterator points to index i of resultant vector
it = vec.insert(vec.bein()+i, it_first, it_last);

// 4. insert n copies of item starting at index i, return iterator points to index i of resultant vector
it = vec.insert(vec.bein()+i, n, item);
```
#### Delete from index i or range [i, i+n)
```
// 1. item at index i deleted and destructor called, return iterator points to index i of resultant vector
if (i<vec.size()){ // important, check range or error
    it = vec.erase(vec.begin()+i);
}

// 2. n elements deleted starting at index i deleted, items destructor called. return iterator points to index i of resultant vector. WARNING if iterator out of range, undefined behaviour occurs.
it = vec.erase(vec.begin()+i, vec.begin()+i+n);
```
#### Delete All
```
vec.clear(); //all element destructor called
```
#### Delete by Value
```
// 1. remove first occurence
#include <algorithm> // for find
it = std::find (vec.begin(), vec.end(), item);
if (it!=vec.end()){vec.erase(it);} //item destructor called

// 2. remove all occurrences
vec.erase(remove(vec.begin(), vec.end(), item), vec.end());
```
</details>

<details>
<summary>Python</summary>

#### Init
```
1. ls = [ ]
2. ls = [a,b,c]
3. ls = [a for i in range(size)] // or ls = [a]*size
```
#### Iterate
```
// 1. if you only need to read
for item in ls:
    print(item)

// 2. or the more conventional way
for idx in range(len(ls)):
    ls[idx]=newitem

// 3. or if you need idx and original item at the same time
for idx, item in enumerate(ls):
    print(item)
    ls[idx]=newitem

// 4. if you want remove items, use list comprehension. use slicing on left-hand-side to keep original references in case somewhere else is referring to this
ls[:] = [newitem for item in ls if (some condition)]
```
#### Check if item exists
```
return item in ls
```
#### Search item first occurrence idx
```
idx = None
try:
    idx = ls.index(item) //throw error if item not found
except:
    print('not found')
```
#### Search item ALL occurrence idices
```
indices = [i for i, x in enumerate(list) if x == item]
```
#### Count item
```
count = ls.count(item)
```
#### Add to back
```
// 1.
ls.append(item)

// 2.
ls[len(ls):]=[item] 
```
#### Delete from back
```
// 1. if you don't need the deleted item
del ls[-1]

// 2. if you need the deleted item
item = ls.pop()

// 3. another way
ls = ls[:-1]
```
#### Insert to index i
```
// 1.
ls.insert(i, item)

// 2.
ls[i:i]=[e] // new element must be wrapped in a list

// 3. insert n items starting at index i
3. ls[i:i]=[n elements]
```
#### Delete from index i or range [i, i+n)
```
// 1. if you don't need the deleted item
del ls[i]

// 2. if you need the deleted item
item = ls.pop(i)

// 3. delete multiple items
3. del ls[i:i+n]

// 4. another way of delete multiple items
ls = ls[:i]+ls[i+n:]
```
#### Delete All
```
1. ls.clear()
2. del ls[:]
```
#### Delete by value
```
// remove the first occurrence of item, throw error if item not found
try:
    ls.remove(item)
except:
    print('item not found')
```
</details>

<details>
<summary>JavaScript</summary>

#### Init
```
1. let ls = [ ];
2. let ls = [a,b,c];
```
#### Iterate (TODO)
```
// 1. if you only need to read
for item in ls:
    print(item)

// 2. or the more conventional way
for idx in range(len(ls)):
    ls[idx]=newitem

// 3. or if you need idx and original item at the same time
for idx, item in enumerate(ls):
    print(item)
    ls[idx]=newitem

// 4. if you want remove items, use list comprehension. use slicing on left-hand-side to keep original references in case somewhere else is referring to this
ls[:] = [newitem for item in ls if (some condition)]
```
#### Check if item exists
```
return ls.includes(item); //since ES2017
```
#### Search item first occurrence idx
```
const idx = ls.indexOf(item); //-1 if not found
```
#### Search item ALL occurrence idices (TODO)
```
indices = [i for i, x in enumerate(list) if x == item]
```
#### Count item 
```
const count = ls.length;
```
#### Add to back
```
ls.push(item)
```
#### Delete from back
```
// 1. in place
ls.splice(ls.length-1, 1)

// 2. copy
let ls = ls.slice(0, ls.length)
```
#### Insert to index i
```
// 1.
ls.splice(i, 0, item);

// 2. insert items to list starting at index i
ls.splice(i, 0, ...items);
```
#### Delete from index i or range [i, i+n)
```
// 1. copy
let ls = [...ls.slice(0, i), ...ls.slice(i + 1)];
let ls = [...ls.slice(0, i), ...ls.slice(i+n)];

// 2. in place
ls.splice(i, 1)
ls.splice(i, n)
```
#### Delete All (TODO)
```
1. ls.clear()
2. del ls[:]
```
#### Delete by value (TODO)
```
// remove the first occurrence of item, throw error if item not found
try:
    ls.remove(item)
except:
    print('item not found')
```
</details>

## Linked List
<details>
<summary>C++</summary>

There are two container in STL that can be used as list:
1. forward_list (singly linked list, no size count)
2. list (doublely linked list, has size count)

Although forward_list is simpler and less overhead, it is rather inconvenient to use. Instead, we'll use list.
#### Init
```
#include <list>
1. list<T> list;
2. list<T> list(size);
2. list<T> list(size, item); 
3. list<T> list({a,b,c});
```
#### Iterate
```
// 1. if you only need to read, use range-based for loop
for(const T& item: list){ } 

// 2. if you want to update, remove const keyword
for(T& item: vec){item = newitem;}

// 3. if you want to delete while iterating
list.remove_if([](const T &x)->bool { //note without &, x will be copied
    return (boolean condition, true for remove); 
}); //note unlike vector, the remove_if is build-in for forward-list/list
```
#### Check if item exists
```
#include <algorithm> // for find
it = std::find (list.begin(), list.end(), item);
return it!=list.end();
```
#### Access First Item
```
if(!list.empty()){ //important, front from empty causes error
    return list.front(); // if use list, there's symetric back()
}
```
#### Access Index i (O(i))
```
// WARNING: Do not use advance(it, i) cos it may surpass end() can cause undefined behaviour
idx = -1;
for(const T& item:list){
    ++idx;
    if (idx==i){
        return item;
    }
}
// item not found
return null;
```
#### Insert Front
```
// 1. copy
list.push_front(item); //if use list, there's symetric push_back()

// 2. copy
it = list.insert(list.begin(), item); // this means insert BEFORE the original item. return iterator points to the inserted item

// 3. item is constructed in place and added to front
list.emplace_front(Args for item constructor); //if use list, there's symetric emplace_back()

// 4. item is constructed in place and added to front
it = list.emplace(list.begin(), Args for item constructor);
```
#### Insert at Index i  (O(i))
```
// WARNING: Do not use advance(it, i) cos it may surpass end() can cause undefined behaviour
idx = -1;
it = list.begin();
while(it!=list.end()){
    ++idx;
    if(idx == i){
        it = list.insert(it, item); //use emplace if can
        break;
    }
    ++it; //note you cannot use it=it+1 cos + is not defined for list iterator 
}
```
#### Delete Front
```
if(!list.empty()){ //important, pop_front from empty causes error
    list.pop_front(); // if use list, there's symetric pop_back, item destructor called
}
```
#### Delete at Index i
```
idx = -1;
it = list.begin();
while(it!=list.end()){
    ++idx;
    if(idx == i){
        list.erase(it);
        break;
    }
    ++it; //note you cannot use it=it+1 cos + is not defined for list iterator 
}
```
#### Delete by Value
```
// 1. remove all occurrences of item
list.remove(item);

// 2. (only for list, not forward list) remove only the first occurrence of item
#include <algorithm> // for find
it = std::find (list.begin(), list.end(), item);
if(it!=list.end(){
    list.erase(it); //erase() is not available for forward_list which only has erase_after()
}
```

#### Delete All
```
list.clear();
```

</details>

<details>
<summary>Python</summary>

deque in python is a doublely linked list

#### Init
```
from collections import deque
dq = deque();
dq = deque(maxlen=n) //if maxlen specified and size exceed maxlen, depending on the side you are pushing, the other side element will be removed
dq = deque([a,b,c], maxlen=n)
```
#### Iterate
```
//1. if you only want to read
for item in dq:
    print(item)

//2. if you want to update
for idx in range(len(dq)):
    dq[idx] = item //this is very inefficient, consider cast to list then cast back, but reference will be recreated
```
#### Check if item exists
```
return item in dq;
```
#### Access Index i (O(i))
```
return dq[i]
```
#### Insert Front
```
dq.appendleft(item)
```
#### Insert at Index i  (O(i))
```
dq.insert(i,item)
```
#### Delete Front
```
dq.popleft()
```
#### Delete at Index i
```
del dq[i]
```
#### Delete by Value
```
dq.remove(item) //unlike C++, this removes only the first occurrence
```
#### Delete All
```
dq.clear()
```

</details>


## Hash Table
<details>
<summary>C++</summary>

#### Init
```
#include <unordered_map>
1. unordered_map<T1,T2> hash;
2. unordered_map<T1,T2> hash({ {key1,val1},{key2,val2},{key3,val3} });
```
#### Search item
```
it = hash.find(key);
if(it!=hash.end()) return it->second;
```
#### Insert item
```
hash[key]=value;
```
#### Update item
```
// 1.
it = hash.find(key);
if(it!=hash.end()) it->second=newvalue;

// 2. if you are sure that the key exists or don't care if new item added to hash
hash[key]=value;
```
#### Delete item
```
// 1.
it = hash.find(key);
if(it!=hash.end()) hash.erase(it); // calls item destructor

// 2. if you are sure that the key exists
count = hash.erase(key); // returns count of items removed, calls item destructor
```
#### Delete all items
```
hash.clear(); // calls items destructor
```
#### Iterate
```
// 1. if you only need to read
for(const pair< T1,T2 >& item: hash){ }

// 2. if you want to update, remove const (VERIFICATION NEEDED) 
for(pair< T1,T2 >& item: hash){ item.second=newvalue; }
```
</details>

<details>
<summary>Python</summary>

#### Init
```
1. dict={ };
2. dict={ key1:value1, key2:value2, key3:value3}
3. dict=collections.defaultdict(type) # if key not found, autocreate default value of type
```
#### Search item
```
// 1. return default if key does not exist
value = dict.get(key, default)

// 2. this is slow because duplicated search twice
if key in dict:
    value=dict[key]
```
#### Insert item
```
dict[key]=value;
```
#### Update item
```
// unfortunately, two search needed, unless you don't care if key exists
if key in dict:
    dict[key]=newvalue
```
#### Delete item
```
// 1. use this if you need the deleted item, return default if key does not exist
value = dict.pop(key, default)

// 2. only use this if you are sure that key exists
del dict[key] 
```
#### Delete all items
```
dict.clear();
```
#### Iterate
```
for key,value in dict.items(): #dict.iteritems() if python 2, enumerate(dict) is wrong cos it just print 0,1,2...
    print(key, value)
    dict[key] = newvalue
```
#### Convert to Array
```
//1. array of tupple
tuples = dict.items()

//2. array of keys
keys = list(dict.keys())

//3. array of values
values = list(dict.values())
```

</details>


<details>
<summary>JavaScript</summary>

Both object & map can be used as hash map, use map if needs frequent update.
#### Init
```
// map
1. let map = new Map();
2. let map = new Map([
        [key1, val1],
        [key2, val2],
        [key3, val3]
   ]);
3. let map = new Map([...anotherMap]);

// object
1. let obj = {};
2. let obj = {
        key1: val1,
        key2: val2,
        key3: val3
   };
3. let obj = {...anotherObj}; // careful with nested object
```
#### Search item
```
// map: return undefined if key does not exist
// works for both non-string & string key
const value = map.get(key);

//object
// 1. works for both non-string & string key
const value = obj[key];
// 2. works only for string key
const value = obj.key;
```
#### Insert item
```
// map
map.set(key, val);

// object
obj[key]=val;
```
#### Update item
```
// map
map.set(key, val);

// object
obj[key]=val;
```
#### Delete item
```
// map
// success == true if key exists, else false
const success = map.delete(key);

// obj
// success is always true regardless whether key exists or not
const success = delete obj[key];
```
#### Delete all items
```
// map
map.clear();

// obj has no clear operator, have to delete one by one or create new empty object
obj = {};
```
#### Iterate
```
// map
// 1.
for (const entry of map) {
    const key = entry[0];
    const val = entry[1];
}
// 2.
for (const [key, val] of map) {
}
// 3.
function sortByKey(a, b) {
    return a[0] > b[0] ? 1 : -1;
}
for (const [key, value] of [...map].sort(sortByKey)) {
}

// obj
const keys = Object.keys(obj);
keys.sort();
for (const key of keys) {
    const val = obj[key];
}
    
```
#### Convert to Array
```
// map
//1. array of tupples
const tuples = [...map]
//2. array of keys
const keys = [...map.keys()]
//3. array of values
const keys = [...map.values()]
// obj
//1. array of tupples
const tuples = Object.entries(obj)
//2. array of keys
const keys = Object.keys(obj)
//3. array of values
const values = Object.values(obj)
```

</details>

## Stack
<details>
<summary>C++</summary>

In C++ stack is a container adaptor which uses default underlying container deque. But the underlying container can also be vector or list. Therefore, deque, vector, list can all be used as stack directly, and additionally provide more functions. Do note that vector is continuous in memory so the reallocation will take time if it grows in size. While deque is not continuous so does not suffer this problem and that's probably why deque is the default container for stack. However, if you want to restrict the datastructure behaviour to only stack operations, then you should just use stack.

#### Init
```
// 1. use stl stack
#include <stack> //for stack, a container adaptor
stack<T> stack; //use default container dequeue

// 2. use deque
#include <deque>//for deque
deque<T> dq;
deque<T> dq({a,b,c});
```
#### Peek
```
// 1. use stack
if(!stack.empty()){ //error if top from empty
    item = stack.top();
}

// 2. use deque
if(!dq.empty()){ //error if back from empty
    item = dq.back();
}
```
#### Push
```
// 1. use stack, copy, use this if item is from somewhere else
stack.push(item);

// 2. use deque, copy
dq.push_back(item); 

// 3. use stack, item is constructed in-place and added to top of stack
stack.emplace(Args of item constructor);

// 4. use deque, item is constructed in-place
dq.emplace_back(Args of item constructor);
```
#### Pop
```
// 1. use stack
if(!stack.empty()){ //error if top/pop from empty
    item = stack.top(); //copy if you need
    stack.pop(); // item destructor called
}

// 2. use deque
if(!dq.empty()){ //error if back/pop_back from empty
    item = dq.back(); //copy if you need
    dq.pop_back(); //item destructor called
}
```
#### Delete All
```
// 1. use stack, there is no stack.clear() method
while(!stack.empty()){
    stack.pop();
}

// 2. use deque
dq.clear();
```

</details>

<details>
<summary>Python</summary>

There are 3 python data structures that support stack operations
1. list (continuous memeory)
2. collections.deque (recommended for stack)
3. queue.LifoQueue (more for multithreading purpose, invovles some overhead)

For the same reason as C++ vector, we avoid using list to implement stack due to reallocation cost. queue.LifoQueue restricts to only stack operations and is designed for multi thread. collections.deque can be used both as stack or queue and resembles C++ deque

#### Init
```
from collections import deque
dq = deque()
dq = deque(maxlen=n) //if maxlen specified and size exceed maxlen, depending on the side you are pushing, the other side element will be removed
dq = deque([a,b,c], maxlen=n)
```
#### Peek
```
if len(dq)>0:
    item = dq[-1] //O(1) complexity if you always append
    item = dq[0] //O(1) complexity if you always appendleft
```
#### Push
```
dq.append(item) // add to right
dq.appendleft(item) //add to left
```
#### Pop
```
if len(dq)>0:
    dq.pop() // if you always append
    dq.popleft() // if you always appendleft
```
#### Delete All
```
dq.clear()
```

</details>

## Queue
<details>
<summary>C++</summary>

In C++ queue is a container adaptor which uses default underlying container deque. But the underlying container can also be list (cannot be vector since it does not support pop_front). Therefore, deque, list can all be used as queue directly, and additionally provide more functions. However, if you want to restrict the datastructure behaviour to only queue operations, then you should just use queue.

#### Init
```
// 1. use stl queue
#include <queue> //for queue, a container adaptor
queue<T> q; //use default container dequeue

// 2. use deque
#include <deque>//for deque
deque<T> dq;
deque<T> dq({a,b,c});
```
#### Peek
```
// 1. use queue
if(!q.empty()){ //error if front from empty
    item = q.front();
}

// 2. use deque
if(!dq.empty()){ //error if front from empty
    item = dq.front();
}
```
#### Enqueue
```
// 1. use queue, copy, use this if item is from somewhere else
q.push(item);

// 2. use deque, copy
dq.push_back(item); 

// 3. use queue, item is constructed in-place and added to back of queue
q.emplace(Args of item constructor);

// 4. use deque, item is constructed in-place
dq.emplace_back(Args of item constructor);
```
#### Dequeue
```
// 1. use queue
if(!q.empty()){ //error if front/pop from empty
    item = q.front(); //copy if you need
    q.pop(); // item destructor called
}

// 2. use deque
if(!dq.empty()){ //error if front/pop_front from empty
    item = dq.front(); //copy if you need
    dq.pop_front(); //item destructor called
}
```
#### Delete All
```
// 1. use queue, there is no q.clear() method
while(!q.empty()){
    q.pop();
}

// 2. use deque
dq.clear();
```

</details>

<details>
<summary>Python</summary>

There are 2 python data structures that support queue operations
1. collections.deque (recommended for queue)
2. queue.FifoQueue (more for multithreading purpose, invovles some overhead)

queue.FifoQueue restricts to only queue operations and is designed for multi thread. collections.deque can be used both as stack or queue and resembles C++ deque

#### Init
```
from collections import deque
dq = deque()
dq = deque(maxlen=n) //if maxlen specified and size exceed maxlen, depending on the side you are pushing, the other side element will be removed
dq = deque([a,b,c], maxlen=n)
```
#### Peek
```
if len(dq)>0:
    item = dq[0] //O(1) complexity if you always append
    item = dq[-1] //O(1) complexity if you always appendleft
```
#### Enqueue
```
dq.append(item) // add to right
dq.appendleft(item) //add to left
```
#### Dequeue
```
if len(dq)>0:
    item=dq.popleft() // if you always append
    item=dq.pop() // if you always appendleft
```
#### Delete All
```
dq.clear()
```

</details>

## Priority Queue
<details>
<summary>C++</summary>

In C++ priority_queue is a container adaptor which uses default underlying container vector. But the underlying container can also be deque. Therefore, vector, deque can all be used as priority_queue directly, and additionally provide more functions. Do note that vector is continuous in memory so the reallocation will take time if it grows in size. While deque is not continuous so does not suffer this problem. However, if you want to restrict the datastructure behaviour to only priority_queue operations, then you should just use priority_queue.

#### Init
```
#include <queue>
//1. max heap
priority_queue<pair<int,T> >pq;

//2. min heap
priority_queue<pair<int,T>, vector<pair<int,T> >, greater<pair<int, T> > >pq;

//3. custom comparator
auto customCompare = [](const T& a, const T& b){
    return (compare a, b return bool);
};
priority_queue<T, vector<T>, decltype( customCompare )> pq(customCompare);
```
#### Peek
```
if (!pq.empty()){ //important, error if top from empty
    return pq.top();
} 
```
#### Push
```
//1. copy
pq.push(item);

//2. item is constructed in place and added to priority queue
pq.emplace(Args of item constructor); //for pair, its just two objects
```
#### Pop
```
if(!pq.empty()){ //important, error if pop from empty
    item = pq.top(); //copy if you need
    pq.pop(); //item destructor called
}
```
#### Update Priority
C++ priority does not straight forward support priority update. There are a few ways to work around:
1. make_heap on the underlying vector container when there is an update.
2. Push updated (priority, value) pair into the queue without trying to find and delete the old one. Take note of the value's latest priority in some other data structure. When poping from priority queue, check if the priority is latest, if not, keep popping. Accept the fact that there will be outdated data in the priority queue. 
3. Someone suggest use set, which has logN access, delete, update time. However, it does not support key-value pair.

Personally, I'll pick 1st method.
```
//external data structure which we can access and modify later
vector<pair<int,T> > external_vec; //first represents priority, you can also use a custom class instead of pair
external_vec.emplace_back(1,item1);
external_vec.emplace_back(3,item2);

//custom comparator for priority queue
auto customCompare = [](const pair<int,T>* a, const pair<int,T>* b){
    return a->first < b->first; //a max heap
};

//construct priority queue using data pointer (you can use shared_ptr too)
priority_queue<pair<int,T>*, vector<pair<int,T>* >, decltype( customCompare )> pq(customCompare);
pq.push(&(external_vec[0]));
pq.push(&(external_vec[1]));

//when a priority update is made
external_vec[0].first=5;

//update the underlying vector of the priority queue, taking advantage of the fact that vector memory is continuous. This step is O(N) in worst case 
make_heap(const_cast<pair<int,T>**>(&pq.top()), const_cast<pair<int,T>** >(&pq.top()) + pq.size(), customCompare);
```
#### Delete All
```
// there is no clear() function in priority_queue, same as stack/queue
while(!pq.empty()){
    pq.pop(); //item destructor called.
}
```

</details>

<details>
<summary>Python</summary>


#### Init
```
import heapq
pq=[] //yes, nothing just a list will do
```
#### Peek
```
if len(pq)>0:
    return pq[0] //python only support min heap, so pq[0] is mallest priority
```
#### Push
```
1. heapq.heappush(pq,[priority, item]) //note priority can be any comparable
2. priority, item = heapq.heappushpop(pq, [priority, item]) //this will do a push followed by pop, more efficient
```
#### Pop
```
1. priority, item = heapq.heappop(pq)
2. priority, item = heapq.heapreplace(pq, [priority, item]) //this will do a pop followed by push, more efficient
```
#### Update Priority
```
// you can directly update the list and heapify, but you must know that heapify will change the list ordering
pq[0][0]=1
heapq.heapify(pq)
```
#### Delete All
```
pq.clear()
```

</details>


## Sort
<details>
<summary>C++</summary>
           
```
#include <algorithm>

// sortable containers: vector, set, map
// 1. default non-descending (same for stable_sort)
sort(container.begin(), container.end());
sort(container.begin()+4, container.end()); //sort part of container (only works for continuous memeory container like vector)

// 2. non-increasing (same for stable_sort)
sort(container.begin(), container.end(), greater<T>());

// 3. custom comparator (same for stable_sort)
sort(container.begin(), container.end(), [](const <T> &a, const <T> &b) -> bool{ 
    return a.mProperty > b.mProperty; 
});

```

</details>

<details>
<summary>Python</summary>
           
```
#include <algorithm>

// 1. default non-descending (python sort is always stable)
list.sort() //in place
list = sorted(list/tuple/dictionary/set/frozenset) //return new "list"

// 2. non-increasing
list.sort(reverse=True)
list = sorted(list/tuple/dictionary/set/frozenset, reverse=True)

// 3. custom comparator
list.sort(key=lambda element: element.name.lower())
list.sort(key=lambda x,y: cmp(x.name.lower(),y.name.lower())) //more general and free than previous line
list = sorted(list/tuple/dictionary/set/frozenset, key=lambda element: element.name.lower())
list.sort(reverse=True, key=lambda element: element.name.lower())
list = sorted(list/tuple/dictionary/set/frozenset, reverse=True, key=lambda element: element.name.lower())

//4. sort dictionary
list_key_sorted = sorted(dict) //equivalent to sorted(prices.iterkeys())
list_val_sorted = sorted(dict.itervalues())
list_tuple_sorted_by_key = sorted(dict.iteritems()) // return list of (key,value) tupples sorted by key
list_tuple_sorted_by_val = sorted(dict.iteritems(), key=lambda x: x[1]) // return list of (key,value) tupples sorted by key
```

</details>

## Bits

<details>
<summary>Same for C++/Python/Java</summary>

#### Init
```
// assign binary 1010 to int a, result in a=10
// note since a is int with 32 bits, this will
// prepend 1010 with 0s
a = 0b1010 
```

#### Print Binary
Refer to [String/String Format](#string-format)

#### Bitwise Operations
```
a = 0b1010
b = 0b0110

//and
c = a&b //10 prepend 0s

//or
c = a|b //1110 prepend 0s

//xor
c=a^b //1100 prepend 0s

//negate
c=~a //0101 prepend 1s which is equivalent to -1011 prepend 0s (2's complement)

//shift 1 bit left
c=a<<1 //10100 prepend 0s

//shift 3 bits right
c=a>>3 //1 prepend 0s

```

</details>

## Type Convert

<details>
<summary>C++</summary>

#### To String
```
//anything to string (since c++11)
#include <string>
string s = to_string(other_typed_variable)
```

#### From String
```
//(since c++11) 
//note string can contain things other than the desired type
//for example "hello 1001" if convert ot int will be 1001

#include <string>

//1. string to int famility
int i = stoi(str_base10);
int i = stoi(str_base16, nullptr, 16);
int i = stoi(str_base2, nullptr, 2);
long l = stol(s);
long long ll=stoll(s);
unsigned long ul=stoul(s);
unsigned long long ull=stoull(s);

//2. string to float famility
float f = stof(s);
double d = stod(s);
long double ld = stold(s);
```

#### General
```
//TypeA to TypeB
<TypeB> b = static_cast<TypeA>(a);
```

</details>
           
<details>
<summary>Python</summary>

#### General
```
//TypeA to TypeB
b = TypeB(a) //such as str(a), float(a), list(a)...
```

</details>

## Infinity

<details>
<summary>C++</summary>

#### Init
```
#include <limits>
float/double positiveInf= std::numeric_limits<float/double>::infinity(); // note int cannot, it will just be 0
float/double negativeInf= -std::numeric_limits<float/double>::infinity();
```

#### Operations
```
double inf = std::numeric_limits<double>::infinity();

// The following are TRUE
1000000<inf;
std::numeric_limits<int>::max()<inf;
std::numeric_limits<float>::max()<inf;
std::numeric_limits<double>::max()<inf;
inf+1 == inf;
inf-1 == inf;
inf*2 == inf;
inf/2 == inf;
pow(inf,2) == inf;
pow(inf,3) == inf;
-inf != inf; // -inf is negative infinity

double ninf = -std::numeric_limits<double>::infinity();

// The following are TRUE
-1000000>ninf;
std::numeric_limits<int>::min()>ninf;
std::numeric_limits<float>::min()>ninf;
std::numeric_limits<double>::min()>ninf;
ninf+1 == ninf;
ninf-1 == ninf;
ninf*2 == ninf;
ninf/2 == ninf;
pow(ninf,2) != ninf; //negative negative = positive
pow(ninf,3) == ninf;
-ninf != ninf; // -ninf is infinity

```

</details>

<details>
<summary>Python</summary>

#### Init
```
//1. no library needed
positiveInf=float('inf) //note, there is no int('inf')
negativeInf=float('-inf')

//2. math
#include math
positiveInf = math.inf
negativeInf = -math.inf

//3. numpy
#include numpy as np
positiveInf = np.inf
negativeInf = np.inf
```

#### Operations
```
behaves like C++, for all 3 initialization ways
```
</details>


## Random
Note: all random number generators discussed here is not suitable for security applications (possible to be hacked).

<details>
<summary>C++</summary>

#### Generate Random Numbers
- [About Source of Randomness](https://blog.cloudflare.com/ensuring-randomness-with-linuxs-random-number-generator/)
- [On how to seed mt19937](https://stackoverflow.com/questions/45069219/how-to-succinctly-portably-and-thoroughly-seed-the-mt19937-prng)
- [All provided distributions](http://www.cplusplus.com/reference/random/)
```
#include <random>  // Don't use srand()+rand() from <stdlib.h> anymore, they are not modern C++ and flawed!
#include <chrono>  // Needed only if you seed using system time

//step1: get a random seed (one per Peudo Random Number Generator(PRNG))
unsigned int seed = std::chrono::system_clock::now().time_since_epoch().count(); //seed using system time
unsigned int seed = std::random_device{}(); //seed using hardware CSPRNG, can fallback to some simple PRNG or even constants. Not recommended.

//step2: init a PRNG (one per thread, since the random generator is not thread safe)
std::mt19937 gen(seed); //A preconfigured mersenne_twister_engine with 2^19937 states and generates 32 bit uint_fast32_t
std::mt19937_64 gen(seed); //Same engine as above, generates 64 bit uint_fast64_t numbers, usually 32 bit will do

//step2.5: re-init a PRNG
gen.seed(new_seed);

//step3: define distribution to randomly sample from
std::uniform_int_distribution<T>  distrib(a, b); //range=[a, b], T must be IntType (short,int,long,long long, or their unsigned versions)
std::uniform_real_distribution<T> distrib(a, b); //range=[a, b), T must be RealType (float,double,long double)
std::normal_distribution<T>       distrib(mean, stddev); //normal distribution, T must be RealType
std::bernoulli_distribution       distrib(p); //return True with probability p, else False
std::binomial_distribution<T>     distrib(trials, p); //return True count, T must be IntType

//step4: get random numbers repeatedly
for (int n=0; n<N; ++n){
    rand_num = distrib(gen);
}
```

#### Random Shuffle
```
#include <algorithm>  //shuffle

//step1: get a random seed (one per Peudo Random Number Generator(PRNG))
unsigned int seed = std::chrono::system_clock::now().time_since_epoch().count(); //seed using system time

//step2: init a PRNG (one per thread, since the random generator is not thread safe)
std::mt19937 gen(seed); //A preconfigured mersenne_twister_engine with 2^19937 states and generates 32 bit uint_fast32_t
std::mt19937_64 gen(seed); //Same engine as above, generates 64 bit uint_fast64_t numbers, usually 32 bit will do

//step3: shuffle in place
shuffle (vector.begin(), vector.end(), gen);
```
</details>

<details>
<summary>Python</summary>

#### Generate Random Numbers
- [All provided distributions](https://docs.python.org/3/library/random.html)
```
import random

//step1: init random generator and seed it (one per program, random is thread safe)
random.seed()  // by default, seeded with system time, you can provide a number to fix the seed

//step2: get random numbers repeatedly
rand_num = random.randint(a,b)  //uniform in range=[a, b], return int
rand_num = random.randrange(a,b,step)  //uniform in range=[a, b), with range step=step, return int
rand_num = random.random() //uniform in range=[0.0, 1.0), return float
rand_num = random.uniform(a,b) //uniform in range=[a, b], return float. Note b may or may not be obtainable depending on rounding
rand_num = random.gauss(mean, stddev) //normal distribution, return float
rand_item = random.choice([a,b,c]) //choose an item in list uniformly
rand_seq = random.choices([a,b,c],[weight_a,weight_b,weight_c], k=x) //choose x items from list, with replacement, according to weights
rand_seq = random.sample([a,b,c], k=x)    # choose x items from list, without replacement
```

#### Random Shuffle
```
random.shuffle(list) // shuffle list
```

</details>

## Set
<details>
<summary>C++</summary>

#### Init
```
#include <unordered_set>
1. unordered_set<T> set;
2. unordered_set<T> set({a,b,c,a}); //initializer list, duplicates ignored
3. unordered_set<T> set(vec.begin(), vec.end()); //copy from vector, duplicates ignored
```
#### Search item
```
std::unordered_set<T>::const_iterator it = set.find(item);
return (it!=set.end() ? True : False;
```
#### Insert item
```
//1. insert 1 item, iterator points to existing or newly-inserted item, bool is True if insert successful
pair<iterator,bool> result = set.insert(item); //insert 1 item if not exist, copy
pair<iterator,bool> result = set.emplace(Args of item constructor);  //construct and insert inplace if not exist

//2. insert multiple items (no emplace equivalent, return no value)
set.insert ({a,b,c,a}); //initializer list, duplicates ignored
set.insert (vec.begin(), vec.end()); //copy from vector, duplicates ignored
```
#### Delete item
```
// 1. use iterator
std::unordered_set<T>::const_iterator it = set.find(item);
if(it!=set.end()) set.erase(it); // calls item destructor

// 2. use item
count = set.erase(item); // returns count of items removed, 0 if item not found. calls item destructor
```
#### Delete all items
```
set.clear(); // calls items destructor
```
#### Iterate
```
// 1. if you only need to read
for(const T& item: set){ }

// 2. delete while iterating
for (std::unordered_set<T>::const_iterator it = set.begin(); it != set.end(); ) {
    if (...) {
        it = set.erase(it); //the new it points to next item in set
    }else {++it;}
}
```
#### Convert to Array
```
vector<T> vec(set.begin(),set.end()); //copy
```
#### Set operations
No direct method to output set.
```
#include <algorithm>
//1. Union A | B
std::vector<T> vec(setA.size()+setB.size());
std::vector<T>::iterator it=std::set_union(setA.begin(), setA.end(), setB.begin(), setB.end(), vec.begin());
vec.resize(it-vec.begin()); //reduce oversized vector

//2. Intersection A & B
std::vector<T> vec(std::min(setA.size(),setB.size()));
std::vector<T>::iterator it=std::set_intersection(setA.begin(), setA.end(), setB.begin(), setB.end(), vec.begin());
vec.resize(it-vec.begin()); //reduce oversized vector

//3. Difference A-B
std::vector<T> vec(setA.size());
std::vector<T>::iterator it=std::set_difference(setA.begin(), setA.end(), setB.begin(), setB.end(), vec.begin());
vec.resize(it-vec.begin()); //reduce oversized vector

//4. Symmetric Difference A^B
std::vector<T> vec(setA.size()+setB.size());
std::vector<T>::iterator it=std::set_symmetric_difference(setA.begin(), setA.end(), setB.begin(), setB.end(), vec.begin());
vec.resize(it-vec.begin()); //reduce oversized vector

```
</details>

<details>
<summary>Python</summary>

#### Init
```
1. set=set()
2. set={a,b,c} //compare this with dict
3. set={x for x in x_list} //set comprehension
4. set=set(list) //copy, O(len(list))
```
#### Search item
```
if item in set:
    print(item)
```
#### Insert item
```
//1. single item
set.add(item)

//2. multiple items O(new items count)
set.update(list)
set.update(set)
set.update(set1, set2, set3...)
```
#### Delete item
```
// 1. remove and return a random item
if len(set)>0:
    item = set.pop()

// 2. remove item with no return
set.remove(item) // throw error if item not found
set.discard(item) //no error if item not found
```
#### Delete all items
```
set.clear();
```
#### Iterate
```
for item in set:
    print(item)
```
#### Convert to Array
```
list = list(set)
```
#### Set operations
```
//1.Union
set=A.union(B, C,...) //union method, O(sum of items in sets)
set=A|B|C|...         // | operator, O(sum of items in sets)
A.update(B, C,...)    //A is modified in place, O(sum of items in sets except A)

//2.Intersection
set=A.intersection(B, C,...) //intersection method, O(sum of items in sets except A)
set=A & B & C & ...          // & operator, O(sum of items in sets except A)
A.intersection_update(B, C,...) //A is modified in place, O(len(A)*number_of_other_sets)

//3.Difference
set=A.difference(B) // method, returns items in A but not in B, O(len(A))
set=A-B             // - operator, returns items in A but not in B, O(len(A))
A.difference_update(B) //A is modified in place, O(len(A))

//4. Symmetric Difference
set = A.symmetric_difference(B) //method, returns items not in both, O(len(A)+len(B))
set = A^B                       //^ operator, returns items not in both, O(len(A)+len(B))
A.symmetric_difference_update(B) //A is modified in place, O(len(B))

//5. Is Subset
A < B   // A is subset of B
A <= B  // equivalent to A.issubset(B)

//6. Is Superset
A > B   // A is superset of B
A >= B  // equivalent to B.issubset(A)

//7. Equal
A==B

//8. Is Disjoint
A.isdisjoint(B)

```

</details>

<details>
<summary>JavaScript</summary>

#### Init
```
1. let set=new Set();
2. let set=new Set([array items]);
```
#### Search item
```
if set.has(item):
    print(item)
```
#### Insert item
```
set.add(item)
```
#### Delete item
```
// success=true if item was in set, else false
const success = set.delete(item)
```
#### Delete all items
```
set.clear();
```
#### Iterate
```
for (const item of set) {
}
```
#### Convert to Array
```
let arr = [...set] //use spread operator
```
#### Set operations (TODO)
```
//1.Union
set=A.union(B, C,...) //union method, O(sum of items in sets)
set=A|B|C|...         // | operator, O(sum of items in sets)
A.update(B, C,...)    //A is modified in place, O(sum of items in sets except A)

//2.Intersection
set=A.intersection(B, C,...) //intersection method, O(sum of items in sets except A)
set=A & B & C & ...          // & operator, O(sum of items in sets except A)
A.intersection_update(B, C,...) //A is modified in place, O(len(A)*number_of_other_sets)

//3.Difference
set=A.difference(B) // method, returns items in A but not in B, O(len(A))
set=A-B             // - operator, returns items in A but not in B, O(len(A))
A.difference_update(B) //A is modified in place, O(len(A))

//4. Symmetric Difference
set = A.symmetric_difference(B) //method, returns items not in both, O(len(A)+len(B))
set = A^B                       //^ operator, returns items not in both, O(len(A)+len(B))
A.symmetric_difference_update(B) //A is modified in place, O(len(B))

//5. Is Subset
A < B   // A is subset of B
A <= B  // equivalent to A.issubset(B)

//6. Is Superset
A > B   // A is superset of B
A >= B  // equivalent to B.issubset(A)

//7. Equal
A==B

//8. Is Disjoint
A.isdisjoint(B)

```

</details>

## OOP

Different languages has different terminologies. To avoid confusion, I standardize the meaning of the following terms as:
- method: class's member function (C++ calls this "member function", Java & Python call this "method")
- function: free function, not tied to class
- instance: object created from a class
- attribute: a class's member variable (C++ calls this "member variable", Java call this "field/attribute", python call this "attribute")
- variable: free variable, not tied to class
- parameter: variable passed to function

<details>
<summary>C++</summary>

#### Basic Class Structure
See demo here:
- [SimpleClass.h](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/simple_class.h)
- [SimpleClass.cpp](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/simple_class.cpp)

#### Class Method and Attribute
```
//C.h
namespace ns{
Class C{
public:
    static ReturnType ClassMethod(const Type& arg); //class method can only read/write class attribute
                                                    //class method can be called with both instance and class
    static Type classAttribute;    //both instance and class method can read/write class attribute
};
}

//C.cpp
namespace ns{
Type C::classAttribute = 0;
ReturnType C::ClassMethod(const Type& arg){
    return classAttribute;
}
}
```

#### Inheritance
Although C++ supports multi-class inheritance, follow these rules:
1. multiple abstract class inheritance is allowed
2. multiple implementation class inheritance should be avoided
3. avoid deep inheritance
4. if the purpose of inheritance is to extend/override functionality, consider composition instead of inheritance
5. most of the time, inherit only from abstract class (interface)

See demo here:
- [BaseClass.h](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/inheritance/concrete_class.h)
- [BaseClass.cpp](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/inheritance/concrete_class.cpp)
- [ChildClass.h](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/inheritance/concrete_child_class.h)
- [ChildClass.cpp](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/inheritance/concrete_child_class.cpp)

#### Abstract Class
Abstract class in C++ is defined as a class with at least 1 pure virtual function. Abstract class cannot be instantiated at compile time. Try to use abstract class as interface only.

See demo here:
- [AbstractClass.h](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/inheritance/abstract_class_a.h)

#### Interface
C++ has no interface, you may use abstract class to serve this purpose.

#### Operators
See demo here:
- [OperatorOverloadedClass.h](https://github.com/liyinnbw/cpp_boilerplate/blob/master/src/operator_overload/operator_overloaded_class.h)

</details> 

<details>
<summary>Python</summary>

#### Basic Class Structure

Summary on python underscores:
- Single underscore prefix is a convention meaning "private". It has mostly no effect except for import * which will ignore anything starts with '_'
- Double underscore prefix will be replaced with '_ClassName__' outside the class. Its main purpose is to prevent accidental overriding
- More than double underscore prefix is the same as double underscore
- Double prefix and postfix underscore are reserved for special variable, function and should not be used with custom variable, function.

Note: Getters and setters are ignored for succinctness.
```
# namespace is automatically given by file name
class ClassName:
    def __init__(self, arg=0): # python class can only have 1 constructor, 
                               # if you need both default & parameterized constructors,
                               # supply parameters with default values
                               
        self.public_attribute = arg
        self._private_attribute = arg   # note single "_" is just a convention to indicate private
                                        # you can still access this attribute form outside using instance._private_attribute
                                        # however, anything with a single "_" will be ignored in from module import *

    def public_function(self):
        self._private_function()
        
    def _private_function(self):        # note single "_" is just a convention to indicate private
        print(self._private_attribute)  # you can still access this attribute form outside using instance._private_function()
                                        # however, anything with a single "_" will be ignored in from module import *
        
```

#### Class Method and Attribute
```
class ClassName:
    class_attribute = 0                 # you can read/write this from outside using ClassName.class_attribute
                                        # or invoke a class method
    
    def __init__(self, arg=0):
        class_attribute = 2             # this is a local variable, will NOT overwrite the actual class variable
        self.class_attribute = 1        # this is an attribute, will NOT overwrite the actual class variable
    
    @classmethod
    def class_method(cls):              # note "cls" is used instead of "self"
        print(cls.class_attribute)      # class method can read/write class attributes
                                        # class method CANT access instance attribute nor instance method (expected)
                                        # class method can be invoked using ClassName or instance
        
    @staticmethod
    def static_method():                # note there is no "self" nor "cls" needed, mostly used as pure helper function
        print(cls.class_attribute)      # static method CANT read/write class attributes
                                        # static method CANT access instance attribute nor instance method (expected)
                                        # static method can be invoked using ClassName or instance
```

#### Inheritance
Although python supports multi-class inheritance, it should be avoided as much as possible. Most time, inheritance can be replaced by composition.
```
import Base1
import Base2
class ClassA(Base1, Base2):   # multi-class inheritance, claimed to be left-to-right, depth-first 
                              # (but my test shows undeterministic behaviour)
    def __init__(self, arg=0):
        super().__init__(arg) # or super(ClassA,self).__init__(arg) in python 2
                              # you may also use Base1.__init__(arg), Base2.__init__(arg)
                              # but then you'll have to change the class name if
                              # the base class names changes later on.
                              
        print(self.parent_attribute) # once the parent has been initialized, the child can call parent variable easily
                                     # WARNING: avoid having same attribute name in parents and child
        
    def base_function(self, arg):    # override/extend parent function
        
        # invoke all parent methods from left to right, depth-first
        # WARNING: avoid having the same method name in both parents
        super().base_function(arg) # or super(ClassA,self).base_function(arg) in python 2
        
        # if the base class name is provided,
        # only depth-frst search the provided class
        Base1.base_function(arg)
        
        # do something else to extend the base class method
        
```

#### Abstract Class
While any class can serve as the base class, the abstract class will enforce its functions to be implemented by the child class. Else, the child class will throw error when instantiating (Since python 2.6). Python abstract class also serves as interface. 
```
from abc import ABC, abstractmethodd  

class Base(ABC): # abstract class inherit ABC class
    def __init__(self, arg):
        super().__init__() # or super(Base,self).__init__() in python 2
        self.var = arg     # abstract class can have attribute
    
    @abstractmethod        
    def abstract_function(self): # abstract method need not to be implemented
        pass
    
    @abstractmethod        
    def abstract_function(self): # abstract method can be implemented to provide basic functionality
        self.var = 0
```

#### Interface
Python has no interface, you may use abstract class to serve this purpose.

#### Operators
Avoid overriding operator as much as possible. If you have to, make sure the meaning of operator is intuitive and conventional.
```
class ClassName:
    def __init__(self):
        pass
    def __eq__(self,other):   #override == operator, default compare object hash, together with ___eq__ used by sort() and sorted()
        if isinstance(other, ClassA):
            return self.var == other.var
        return NotImplemented
        
    def __ne__(self, other):  #override != operator, only needed for python2
        result = self.__eq__(other)
        if result is not NotImplemented:
            return not result
        return NotImplemented
        
    def __lt__(self, other):  #override < operator, together with ___eq__ used by sort() and sorted()
        if isinstance(other, ClassA):
            return self.var < other.var
        return NotImplemented
        
    def __gt__(self, other):  #override > operator
        if isinstance(other, ClassA):
            return self.var > other.var
        return NotImplemented
        
    def __le__(self, other):  #override <= operator
        if isinstance(other, ClassA):
            return self.var <= other.var
        return NotImplemented
        
    def __ge__(self, other):  #override >= operator
        if isinstance(other, ClassA):
            return self.var >= other.var
        return NotImplemented
    
    def __cmp__(self, other): #no longer in use since python 3
        return NotImplemented
```

</details>

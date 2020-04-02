# LanguageCompare
Comparison of language APIs
- [Dynamic Array](#dynamic-array)
- [Hash Table](#hash-table)

## Dynamic Array
<details>
<summary>C++</summary>

#### Init
```
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
v.erase(remove_if(vec.begin(), vec.end(), [](const T &x)->bool { //note without &, x will be copied
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
#include <algorithm> // for find
it = std::find (vec.begin(), vec.end(), item);
if (it!=vec.end()){vec.erase(it);} //item destructor called
```
</details>

<details>
<summary>Python</summary>

#### Init
```
1. ls = [ ]
2. ls = [a,b,c]
3. ls = [a for i in range(size)]
```
#### Iterate
```
// 1. if you only need to read
for item in ls:
    print(item)

// 2. if you want to update, try use list comprehension
ls = [newitem for item in ls]

// 3. or the more conventional way
for idx in range(len(ls)):
    ls[idx]=newitem

// 4. or if you need idx and original item at the same time
for idx, item in enumerate(ls):
    print(item)
    ls[idx]=newitem
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
item = ls.pop(-1)

// 3. another way
ls = ls[:-1]
```
#### Insert to index i
```
// 1.
ls.insert(i, item)

// 2.
ls[i:i]=[e]

// 3. insert n items starting at index i
3. ls[i:i+n]=[n elements]
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

## Hash Table
<details>
<summary>C++</summary>

#### Init
```
#include <unordered_map>
1. unordered_map< pair< T1,T2 > > hash;
2. unordered_map< pair< T1,T2 > > hash({ {key1,val1},{key2,val2},{key3,val3} });
```
#### Search item
```
it = hash.find(key);
if(it!=hash.end()) return it->value;
```
#### Insert item
```
hash[key]=value;
```
#### Update item
```
// 1.
it = hash.find(key);
if(it!=hash.end()) it->value=newvalue;

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
for(pair< T1,T2 >& item: hash){ item.value=newvalue; }
```
</details>

<details>
<summary>Python</summary>

#### Init
```
1. dict={ };
2. dict={ key1:value1, key2:value2, key3:value3}
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
for key,value in enumerate(dict):
    print(key, value)
    dict[key] = newvalue
```
</details>


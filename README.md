# LanguageCompare
Comparison of language APIs
- [Continuous Memory Dynamic Array](#continuous-memory-dynamic-array)
- [Linked List](#linked-list)
- [Hash Table](#hash-table)
- [Stack](#stack)
- [Queue](#queue)
- [Priority Queue](#priority-queue)

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
3. ls = [a for i in range(size)]
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
    dq.popleft() // if you always append
    dq.pop() // if you always appendleft
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
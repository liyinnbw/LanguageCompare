# LanguageCompare
Comparison of language APIs
- [Dynamic Array](##Dynamic-Array)
- [Hash Table](##Hash-Table)

## Dynamic Array
<details>
<summary>C++</summary>

#### Init
1. vector< T > vec;
2. vector< T > vec(size);
3. vector< T > vec(size, default);
4. vector< T > vec({a,b,c});
#### Iterate
1. for(const T& item: vec){ } //if you only need to read
2. for(T& item: vec){ } // remove const if you want to update item
3. - v.erase(remove_if(vec.begin(), vec.end(), [](const T &x)->bool { //note without &, x will be copied
   -   return (condition check); 
   - }), vec.end()); // use this idiom if you want to remove item based on some condition while iterating
#### Check if item exists
1. - it = std::find (vec.begin(), vec.end(), e); // find is from "algorithm"
   - return it!=vec.end();
#### Search item first occurrence idx
1. - it = std::find (vec.begin(), vec.end(), e); // find is from "algorithm"
   - idx = std::distance(vec.begin(), it);
#### Count item
1. count = std::count(vec.begin(), vec.end(), e); //count is from "algorithm"
#### Add to back
1. vec.push_back(e); // add a copy of e
2. vec.emplace_back(Args of T constructor); // create element in place without copy
#### Delete from back
1. if ( !vec.empty( ) ) { vec.pop_back(); } // element destructor called, pop_back return void
2. if ( !vec.empty( ) ) { vec.resize(vec.size()-1) ); // element destructor called,
#### Insert to index i
1. it = vec.insert(vec.begin()+i, e); // e is copied, return iterator points to index i of resultant vector
2. it = vec.emplace(vec.bein()+i, Args of T constructor); // create element in place without copy, return iterator points to index i of resultant vector
3. it = vec.insert(vec.bein()+i, it_first, it_last); // copy elements from another iterable's range [it_first, it_last) and insert to vec, starting at index i. return iterator points to index i of resultant vector
4. it = vec.insert(vec.bein()+i, n, e); // insert n copies of e starting at position i, return iterator of newly inserted element at position i
#### Delete from index i or range [i, i+n)
1. if ( i<vec.size( ) ) { it = vec.erase(vec.begin()+i); } // element destructor called, return iterator points to index i of resultant vector
2. it = vec.erase(vec.begin()+i, vec.begin()+i+n); // elements destructor called, n elements deleted starting at index i. return iterator points to index i of resultant vector. WARNING if iterator out of range, undefined behaviour occurs.
#### Delete All
1. vec.clear(); //all element destructor called
#### Delete Element
1. - it = std::find (vec.begin(), vec.end(), e); // find is from "algorithm"
   - if (it!=vec.end()){vec.erase(it);}

</details>

<details>
<summary>Python</summary>

#### Init
1. ls = [ ]
2. ls = [a,b,c]
3. ls = [a for i in range(size)]
#### Iterate
1. for item in ls: //if you just want to read
2. ls = [item=newitem for item in ls] //if you want to update
3. - for idx, item in enumerate(ls): //if you want to update
   -    ls[idx]=newitem
#### Search item first occurrence idx
1. idx = ls.index(e) //throw error if item not found
#### Count item
1. count = ls.count(e)
#### Add to back
1. ls.append(e) // no copy
#### Delete from back
1. del ls[-1] // original list modified
2. item = ls.pop(-1) //original list modified and return deleted item
3. ls2 = ls[:-1] // original list not modified, return sublist, no copy
#### Insert to index i
1. ls.insert(i, e) // no copy
2. ls[i:i]=[e] // copy
3. ls[i:i+n]=[n elements] //copy
#### Delete from index i or range [i, i+n)
1. del ls[i] // original list modified
2. item = ls.pop(i) //original list modified and return deleted item
3. del ls[i:i+n] //original list modified
4. ls2 = ls[:i]+ls[i+n:] // original list not modified, no copy
#### Delete All
1. ls.clear()
2. del ls[:]
#### Delete Element
1. ls.remove(e) //remove the first occurrence of item, throw error if item not found
</details>

## Hash Table
<details>
<summary>C++</summary>

#### Init
1. unordered_map< pair< T1,T2 > > hash; // need "unordered_map" header
2. unordered_map< pair< T1,T2 > > hash({ {key1,val1},{key2,val2},{key3,val3} });
#### Search item
1. - it = hash.find(key);
   - if(it!=hash.end()) value = it->value;
#### Insert item
1. hash[key]=value;
#### Update item
1. - it = hash.find(key);
   - if(it!=hash.end()) it->value=newvalue;
2. hash[key]=value; // only use this if you are sure key exists
#### Delete item
1. - it = hash.find(key);
   - if(it!=hash.end()) hash.erase(it); // calls item destructor
2. count = hash.erase(key); // only use this if you are sure key exists, returns count of items removed, calls item destructor
#### Delete all items
1. hash.clear();
#### Iterate
1. for(const pair< T1,T2 >& item: hash){ } //if you only need to read
2. (VERIFICATION NEEDED) for(pair< T1,T2 >& item: hash){ } // remove const if you want to update item 

</details>

<details>
<summary>Python</summary>

#### Init
1. dict={ };
2. dict={ key1:value1, key2:value2, key3:value3}
#### Search item
1. value = dict.get(key) //value will be none if key does not exist. you can supply an optional default value to dict.get(key, default) so that instead of returning None, it returns default
2. if key in dict: value=dict[key] //this is slow because duplicated search twice
#### Insert item
1. dict[key]=value;
#### Update item
1. if key in dict: dict[key]=newvalue //unfortunately, two search needed, unless you don't care if key exists
#### Delete item
1. value = dict.pop(key, default) //same as dict.get(key), but must supply default or else when key not found it will throw error
2. del dict[key] //only use this if you are sure key exists
#### Delete all items
1. dict.clear();
#### Iterate
1. for key,value in enumerate(dict): // you can both read, or write using dict[key]=newvalue

</details>


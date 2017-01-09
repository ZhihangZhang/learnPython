## Python 中的不可变对象 (immutable object)##

- [如何定义「不可变」](#如何定义「不可变」)
- [常见的可变/不可变类型](#常见的可变/不可变类型)
- [本身不可变 vs 内容不可变](#本身不可变 vs 内容不可变)

---

### 如何定义「不可变」###

当我们说某个类型的对象是不可变对象时，**指的是如果想要改变一个变量的值需要通过改变其指向，使其指向新对象，而不能直接改变原来指向的对象**。通过比较改变前、改变后所指对象的 ID， 我们可以判断一个对象是不是「不可变」。

```python
>>> x = 'abc'
>>> id(x)
1690659685632
>>> x = x.replace('b', 'B') # replace 创造新对象，并使 x 指向新对象
>>> x
'aBc'
>>> id(x)
1690660237128  # x 所指对象 id 发生改变，所以 str() 为不可变对象
```

```python
>>> x = [1, 2, 3]
>>> id(x)
2481555299656
>>> x.append(5) # 直接改变对象内容
>>> x
[1, 2, 3, 5]
>>> id(x)
2481555299656 # 对象 id 未改变， 所以 list() 为可变对象
```



### 常见的可变/不可变类型###

#### 不可变####

- number:  ```int()``` , ```float()```, ```complex()```
- sequence: ```str()```, ```tuple()```, ```frozenset()```, ```bytes()``` 


#### 可变####

- mutable sequence: ```list()```, ```bytesarray()```
- ```set()```, ```dict()``` ......



### 本身不可变 vs 内容不可变###

#### Tuple####

与 ```list()``` 不同， ```tuple()``` 属于不可变对象。也就是说，```tuple()``` 内的元素不能被改变（增加、减少、替换），更确切的说是```tuple()```的元素的**指向不变**，但如果元素本身属于可变类型，那么嵌套元素就能被改变。

```python
my_tuple = (4, 2, 3, [6, 5])

# TypeError: 'tuple' object does not support item assignment
#my_tuple[1] = 9

# Output: (4, 2, 3, [9, 5])
my_tuple[3][0] = 9

print(my_tuple) 
```

 如果 tuple 的元素都属于不可变类型，那么它就是一个**内容不变的 tuple** *(tuple with immutable elements)* ， 而内容不变的 tuple 才能作为  dictionary keys。

另外，使用关键字 ```del``` 可以删除掉整个 tuple 。

#### Set & Frozenset####

```set()``` 本身属于可变类型，所以 set 不能作为 dictionary keys。但其中的元素为不可变类型，也就是说，可以向 set 中添加、删减**不可变**元素。（注意：**内容不变**的 tuple 才能作为其元素） 

```python
>>> x = (1, 2, 3)
>>> y = (1, 2, [3, 4])
>>> my_set = set(x)
>>> my_set
{1, 2, 3}
>>> myset = set(y)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

而 frozenset 和 set 的关系就像 tuple 之于 list。frozenset 是 「不可变」「frozen」的 set ，不能改变元素，但可以作为 dictionary keys 。



### 参考链接###

- [immutable-vs-mutable-types](http://stackoverflow.com/questions/8056130/immutable-vs-mutable-types)
- [使用list和tuple](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014316724772904521142196b74a3f8abf93d8e97c6ee6000)
- [使用dict和set](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/00143167793538255adf33371774853a0ef943280573f4d000)
- [programiz-tuple](https://www.programiz.com/python-programming/tuple)
- [programiz-set](https://www.programiz.com/python-programming/set)
- [programiz-dict](https://www.programiz.com/python-programming/dictionary)



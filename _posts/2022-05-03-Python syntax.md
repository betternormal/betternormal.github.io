---
layout: post
author: "praconfi"
tags: Python
title: "Python syntax"
---

## Install

```jsx
brew install python

// 맥의 경우 python2.7이 기본으로 설치되어 있음
// 환경변수에서 alias를 이용해 python3를 기본으로 설정

vim ~/.zshrc
alias python=/opt/homebrew/bin/python3
```

## PIP(Package Installer for Python) 설치

```jsx
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py 
python3 get-pip.py
```

# Comment

```python
# 으로 한줄짜리 주석을 설정한다

''' 
으로
멀티라인 
주석이 가능하다
'''
```

# Variables

- 변수명은 소문자와 대문자를 구별한다
- 변수명의 시작은 소문자나 _이 가능하다
- 숫자는 변수명의 처음으로 올 수 없다
- 자료형은 동적으로 바인딩된다

```python
x = 1
y = 2.5
name = 'Ben Kim'
is_cool = True
x, y, name, is_cool = (1, 2.5, 'Ben Kim', True) 

# casting
x = str(x)
y = int(y)
z = float(z)
```

# String

```python
# 작은따옴표와 큰따옴표를 이용해 문자열을 만들 수 있다.
name = 'ben'

# escape code를 이용해 문자열의 따옴표를 표현한다
sentence = 'he\'s favorite language is python'

# 출력은 F-String을 사용한다
print(f'hello, my name is {name} and I am {age}')

# String Index
a = 'abced'
a[0] # a
a[-2] # e
a[:3] # abc
a[1:4] # bcd
a[3:] # ed

# Method
# 1. capitalize
print(s.capitalize())

# 2. all uppercase
print(s.upper())

# 3. all lower 
print(s.lower())

# 4. swap case
print(s.swapcase())

# 5. get length
print(len(s))

# 6. replace
print(s.replace('world', 'everyone'))

# 7. count
sub = 'h'
print(s.count(sub))

# 8. starts with
print(s.startswith('hello'))

# 9. ends with
print(s.endswith('d'))

# 10. split into a list
print(s.split())

# 11. find position
print(s,find('r'))

# 12. is all alphanumeric
print(s.isalnum())

# 13. is all alphabetic
print(s.isalpha())

# 14. is all numeric
print(s.isnumeric())

# 15. trim
print(s.lstrip()) # left
print(s.rstrip()) # right
print(s.strip())  # all
```

# List

List is a collection which is ordered and chageable. allows duplicate members

```python
numbers = [1, 2, 3, 4, 5]
fruits = ['Apples', 'Oranges', 'Grapes', 'Pears']

# Get
print(fruits[0])

# Get length
print(len(fruits))

# Append
fruits.append('Mangos')

# Insert into position
fruits.insert(2, 'Strawberries')

# Change value
fruits[0] = 'Blueberries'

# Remove
fruits.remove('Grapes')
del fruits[1]

# Remove with pop
fruits.pop(2)

# Reverse
fruits.reverse()

# Sort
fruits.sort()

# Reverse Sort
fruits.sort(reverse = True)

# Slice
fruits[:3]
fruits[3:]
fruits[1:3]

# Copy

fruits2 = fruits 			# shallow
id(fruits2) == id(fruits)   # True

fruits3 = copy(fruits)  	# deep
id(fruits3) == id(fruits)   # False


```
# List comprehension
- declaration and assignment of the array in `one line`  
- [(변수를 활용한 값) for (변수) in (순회할수 있는 값)]  
```python
[i * 2 for i in range(0, 3)]  # [0, 2, 4]
[i * 2 for i in range(0, 3) if i % 2 == 0]  # [0, 4]
```


# Tuple
Tuple is a collection which is ordered and `unchageable` Allows duplicate members.  
If you do not want to change the value all the time while the program is running. use a tuple.


```python
fruits = ('Apples', 'Oranges', 'Grapes')

# Single value needs trailing comma. otherwise it became it's own data structure
frluts = ('Apples',)

# Get
print(fruits[0])

# Unchangeable

# Delete
del fruits2

# Get length
print(len(fruits))
```

# Set

Set is a collection which is unordered and unindexed. `No duplicate members`

```python
fruits_set = {'Apples', 'Oranges', 'Mangos'}

# Check
print('Apples' in fruits_set)

# Add
fruits_set.add('Grapes')

# No duplicate
fruits_set.add('Apples')

# Remove
fruits_set.remove('Grapes')

# Clear
fruits_set.clear()

# Delete
del fruits_set

# Intersection
s1.intersection(s2)

# Union
s1.union(s2)

# Difference
s1.difference(s2)
```

# Dictionary

Dictionary is a collection which is unordered, changeable and indexed. No duplicate members

very similar to object in Javascript

```python
person = {
	'first_name': 'Ben',
	'last_name': 'Kim'
	'age': 31
}

# Get value
print(person('first_name'))

# Get length
print(len(person))

# Add key/value
person['phone'] = '010-1234-1234'

# Get keys
print(person.keys())       # dict_keys(for memory saving)   
print(list(person.keys())) # list 

# Get values
print(person.values())       # dict_values(for memory saving)   
print(list(person.values())) # list 

# Get items
print(person.items())

# Copy
person2 = person.copy()
person2['city'] = 'Incheon'

# Remove item
del(person['age'])
person.pop('phone')

# Clear
person.clear()

# Check key exist
'age' in person   # True
'city' in person  # False

```

# defaultdict
- collections.defaultdict()  
- similar to dict, but has pre-specified initial value  
```python
counts = collections.defaultdict(int)
counts['a'] = + 1  	# {'a': 1}
```

# Counter class
- Useful classes for counting data, expanded dict(dict's methods are available)  
- `most_common()`: returns an array sorted by the highest number of data  
```python
Counter('hello world')   # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

Counter('hello world').most_common(1)   # [('l', 3)]
```
# Function

don’t use curly brackets, use indentation with tabs or spaces


```python
# parameter vs. arguments

def add(a, b):  	# parameter
	return a + b

add(3, 4) 			# arguments


def sayHello(name):
	print(f'Hello {name}')

sayHello('Ben')

def getSum(num1, num2):
	total = num1 + num2
	return total

# multiple arguments
def add_many(option ,*args):
	result = 0
	if option == 'add':
		for i in args:
			result += i
		return result

add_many('add', 1, 2, 3, 4, 5)

# keyword parameter
def print_kwargs(**kwargs):
	print(kwargs)

print_kwargs(a=1)  # became dict {'a': 1}

# lamda function is similar to JS arrow function
getSum2 = lamda num1, num2: num1 + num2

```

# Contidions

```python
# if else
if x > y:
	print(f'{x} is greater than {y}')
elif x == y:
	print(f'{x} is equal to {y}')
else:
	print(f'{y} is greater than {x}')

# and, or, not
if x > 2 and x <= 10:
	print(f'{x} is greater than 2 and less or equal to 10')

if x > 2 or x <= 10:
	print(f'{x} is greater than 2 or less than or equal to 10')

if not(x == y):
	print(f'{x} is not equal to {y}') 

# not, not in
numbers = [1, 2, 3, 4, 5]

if x in numbers:
	print(x in numbers)

if x not in numbers:
	print(x not in numbers)

# is, is not
if x is y:
	print(x is y)

if x is not y:
	print(x is not y)
```

# Loop

```python
people = ['John', 'Paul', 'Sara', 'Susan']

for person in people:
	print(f'Current person is {person}')

# break, continue
for person in people:
	if person == 'Sara':
		break
	elif person == 'Paul'
		continue
	print(f'Current person is {person}')

# Range
for i in range(2, 11):
	print(f'Number: {i}')

for i in range(len(people)):
	print(people[i])

```

# While

```python
count = 0
while count < 10:
	print(f'Count: {count}')
	count += 1
```

# Class

Class is like a blueprint for creating objects. almost everything in python is an object

```python
class User:
	# constructor
	def __init__(self, name, email, age):
		self.name = name
		self.email = email
		self.age = age

	# method
	def greeting(self):
		return f'my name is {self.name}'
	
	def has_birthday(self):
		self.age += 1

# Extend class
class Customer(User):
	def __init__(self, name, email, age):
		self.name = name
		self.email = email
		self.age = age
		self.balance = 0
	
	def set_balance(self, balance):
		self.balance = balance

ben = User('ben kim', 'benkim@mail.com', 31)
print(ben.greeting())

janet = Customer('janet', 'jsnry@mail.com', 31)
janet.set_balance(500)
janet.greeting()
```

# Module

```python
# pip(package installer for Python) is python's package manager

# Example1
import datetime
today = datetime.date.today()

# Example2
from datetime import date
today = date.today()
```

# Files

python has function for creating, reading, updating, deleting files

```python
# Open or Create
myFile = open('myfile.txt', 'w') # write

# Get info
print(myfile.name) # myfile.txt
print(myfile.closed) # False
print(myfile.mode) # w

# Write
myFile.write('I love Python')
myFile.write(' and Javascript')
myFile.close()

# Append(a mode, otherwise it will overwrite)
myFile = ('myfile.txt', 'a')
myFile.write('I also like Dart')
myFile.close()

# Read
myFile = open('myfile.txt', 'r+')
text = myFile.read(100) # 100 characters
print(text)
```

# JSON

parse JSON into a Python dictionary

```python
import json

sampleJson = '{"first_name: "Ben", "last_name": "kim", "age": 30}'

# Parse to dict
user = json.loads(sampleJson)

print(user)
print(user['first_name'])

# dict to JSON
car = {'make': 'Toyota', 'model': 'camry', 'year': 1}
carJson = json.dumps(car)
print(carJson)
```

## Ref

- [https://www.youtube.com/watch?v=JJmcL1N2KQs](https://www.youtube.com/watch?v=JJmcL1N2KQs)
- [https://kiwilife.tistory.com/175](https://kiwilife.tistory.com/175)
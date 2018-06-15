# Spotify TTP Fellowship Code Challenge


#### Question 1: 
sortByStrings(s,t): Sort the letters in the string s by the order they occur in the string t. You can assume t will not have repetitive characters. For example, using s = "weather" and t = "therapyw", the output should be sortByString(s, t) = "theeraw". In another example, using s = "good" and t = "odg", the output should be sortByString(s, t) = "oodg".

```python
s = "weather"
t = "therapyw"

# Write a function where string s is resorted by the ordering of letters in string t
def sortByString(s, t):
    # Use list comprehension to convert string s to list of elements
    thelist = [i for i in s]
    # Map the letters with its order for string t
    indices = {c: i for i, c in enumerate(t)}
    # Sort list of string s elements according to order of string t elements
    result = sorted(thelist, key=indices.get)
    # Join elements and convert to string
    return ''.join(result)
```


```python
%%time

sortByString("weather", "therapyw"), sortByString("good", "odg")
```

    CPU times: user 35 µs, sys: 4 µs, total: 39 µs
    Wall time: 45.8 µs





    ('theeraw', 'oodg')



#### Question 2:
decodeString(s): Given an encoded string, return its corresponding decoded string. The encoding rule is k[encoded_string], where the encoded_string inside the square brackets is repeated exactly k times. Note: k is guaranteed to be a positive integer. 
For s = "4[ab]", the output should be decodeString(s) = "abababab" 
For s = "2[b3[a]]", the output should be decodeString(s) = "baaabaaa"

```python
s = "4[ab]"
s = "2[b3[a]]"

# Write function where string inside square brackets is repeated k times
# This specific function uses a conditional for loop to swap out brackets with parantheses 
# before using eval() function by evaluating the previous, current, and next values (h, i, j) 
# of the current iteration and appending adjusted values to the new list
def decodeString(s):
    
    newlist = []      # empty list to append elements to
    strlist = list(s) # convert string to list of elements
    
    # For loop for previous, current, and next iteration of values considering
    # the possibility of NoneTypes
    for h, i, j in zip([None]+strlist[:-1], strlist, strlist[1:]+[None]):
        
        # if current value is a number and there is a previous value
        if i.isdigit() and h is not None:
            # if previous value isn't a letter
            if not h.isalpha():
                # append value to newlist
                newlist.append(i)
            # if previous value is a letter
            elif h.isalpha:
                # append '+' and then append the value to newlist
                newlist.append('+')
                newlist.append(i)
        # if current value is '['
        elif i == '[':
            # append '*("' to newlist
            newlist.append('*("')
        # if current value is a letter
        elif i.isalpha():
            # if the next value is a number
            if j.isdigit():
                # append the current value and the append '"' to newlist
                newlist.append(i)
                newlist.append('"')
            # if the next value isn't a number
            elif not j.isdigit():
                # append the current value to newlist
                newlist.append(i)
        # current value is ']'
        elif i == ']':
            # if previous value is a letter
            if h.isalpha():
                # append '")" to newlist
                newlist.append('")')
            # if previous value is ']'
            elif h == ']':
                # append ')' to newlist
                newlist.append(')')
        # Otherwise, append value to list
        else:
            newlist.append(i)
    # Use join to convert list of elements to a string and use eval() function to calculate
    return eval("".join(newlist))
```


```python
%%time

decodeString("4[ab]"), decodeString("2[b3[a]]")
```

    CPU times: user 77 µs, sys: 8 µs, total: 85 µs
    Wall time: 89.6 µs





    ('abababab', 'baaabaaa')



#### Question 3: 
changePossibilities(amount,amount): Write a function that, given an amount of money and an array of coin denominations, computes the number of ways to make the amount of money with coins of the available denominations. Example: for amount=4 (4¢) and denominations=[1,2,3] (1¢, 2¢ and 3¢), your program would output 4—the number of ways to make 4¢ with those denominations: 
- 1¢, 1¢, 1¢, 1¢
- 1¢, 1¢, 2¢
- 1¢, 3¢
- 2¢, 2¢

```python
%%time

target = 4
values = [1, 2, 3]

# Function to obtain all possible combinations with replacements that sums up to target value
def combinations(d, current=[], sum_to = 4):
    if sum(current) == 4:
        yield current
    else:
        for i in d:
            if sum(current+[i]) <= 4:
                yield from combinations(d, current+[i])
                

# list of numbers
k = list(combinations(values))
new_k = [] # empty list
num_comb = 0 # count number of cominbtionas
for elem in k: # loop through list
    # if sorted element is not in the empty list
    if sorted(elem) not in new_k: # sorting each list to find matching sets
        new_k.append(sorted(elem)) # add the list to the empty list
        num_comb += 1 # increase counter

# print the number of sets that adds up to the target value
print(*new_k, sep="\n")
print("%s total combinations adding up to %s" % (num_comb, target))
```

    [1, 1, 1, 1]
    [1, 1, 2]
    [1, 3]
    [2, 2]
    4 total combinations adding up to 4
    CPU times: user 450 µs, sys: 46 µs, total: 496 µs
    Wall time: 452 µs


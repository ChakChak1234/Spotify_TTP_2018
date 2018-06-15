{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Question 1 -- sortByStrings(s,t): Sort the letters in the string s by the order they occur in the string t. You can assume t will not have repetitive characters. \n",
    "\n",
    "For s = \"weather\" and t = \"therapyw\", the output should be sortByString(s, t) = \"theeraw\". For s = \"good\" and t = \"odg\", the output should be sortByString(s, t) = \"oodg\"."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "s = \"weather\"\n",
    "t = \"therapyw\"\n",
    "\n",
    "# Write a function where string s is resorted by the ordering of letters in string t\n",
    "def sortByString(s, t):\n",
    "    # Use list comprehension to convert string s to list of elements\n",
    "    thelist = [i for i in s]\n",
    "    # Map the letters with its order for string t\n",
    "    indices = {c: i for i, c in enumerate(t)}\n",
    "    # Sort list of string s elements according to order of string t elements\n",
    "    result = sorted(thelist, key=indices.get)\n",
    "    # Join elements and convert to string\n",
    "    return ''.join(result)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 35 µs, sys: 4 µs, total: 39 µs\n",
      "Wall time: 45.8 µs\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "('theeraw', 'oodg')"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "sortByString(\"weather\", \"therapyw\"), sortByString(\"good\", \"odg\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Question 2 -- decodeString(s): Given an encoded string, return its corresponding decoded string. \n",
    "\n",
    "The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is repeated exactly k times. Note: k is guaranteed to be a positive integer. \n",
    "\n",
    "For s = \"4[ab]\", the output should be decodeString(s) = \"abababab\" \n",
    "For s = \"2[b3[a]]\", the output should be decodeString(s) = \"baaabaaa\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "s = \"4[ab]\"\n",
    "s = \"2[b3[a]]\"\n",
    "\n",
    "# Write function where string inside square brackets is repeated k times\n",
    "# This specific function uses a conditional for loop to swap out brackets with parantheses \n",
    "# before using eval() function by evaluating the previous, current, and next values (h, i, j) \n",
    "# of the current iteration and appending adjusted values to the new list\n",
    "def decodeString(s):\n",
    "    \n",
    "    newlist = []      # empty list to append elements to\n",
    "    strlist = list(s) # convert string to list of elements\n",
    "    \n",
    "    # For loop for previous, current, and next iteration of values considering\n",
    "    # the possibility of NoneTypes\n",
    "    for h, i, j in zip([None]+strlist[:-1], strlist, strlist[1:]+[None]):\n",
    "        \n",
    "        # if current value is a number and there is a previous value\n",
    "        if i.isdigit() and h is not None:\n",
    "            # if previous value isn't a letter\n",
    "            if not h.isalpha():\n",
    "                # append value to newlist\n",
    "                newlist.append(i)\n",
    "            # if previous value is a letter\n",
    "            elif h.isalpha:\n",
    "                # append '+' and then append the value to newlist\n",
    "                newlist.append('+')\n",
    "                newlist.append(i)\n",
    "        # if current value is '['\n",
    "        elif i == '[':\n",
    "            # append '*(\"' to newlist\n",
    "            newlist.append('*(\"')\n",
    "        # if current value is a letter\n",
    "        elif i.isalpha():\n",
    "            # if the next value is a number\n",
    "            if j.isdigit():\n",
    "                # append the current value and the append '\"' to newlist\n",
    "                newlist.append(i)\n",
    "                newlist.append('\"')\n",
    "            # if the next value isn't a number\n",
    "            elif not j.isdigit():\n",
    "                # append the current value to newlist\n",
    "                newlist.append(i)\n",
    "        # current value is ']'\n",
    "        elif i == ']':\n",
    "            # if previous value is a letter\n",
    "            if h.isalpha():\n",
    "                # append '\")\" to newlist\n",
    "                newlist.append('\")')\n",
    "            # if previous value is ']'\n",
    "            elif h == ']':\n",
    "                # append ')' to newlist\n",
    "                newlist.append(')')\n",
    "        # Otherwise, append value to list\n",
    "        else:\n",
    "            newlist.append(i)\n",
    "    # Use join to convert list of elements to a string and use eval() function to calculate\n",
    "    return eval(\"\".join(newlist))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 77 µs, sys: 8 µs, total: 85 µs\n",
      "Wall time: 89.6 µs\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "('abababab', 'baaabaaa')"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "decodeString(\"4[ab]\"), decodeString(\"2[b3[a]]\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Question 3 -- changePossibilities(amount,amount): Your quirky boss collects rare, old coins. They found out you're a programmer and asked you to solve something they've been wondering for a long time. \n",
    "\n",
    "Write a function that, given an amount of money and an array of coin denominations, computes the number of ways to make the amount of money with coins of the available denominations. \n",
    "\n",
    "Example: for amount=4 (4¢) and denominations=[1,2,3] (1¢, 2¢ and 3¢), your program would output 4—the number of ways to make 4¢ with those denominations: \n",
    "\n",
    "- 1¢, 1¢, 1¢, 1¢\n",
    "- 1¢, 1¢, 2¢\n",
    "- 1¢, 3¢\n",
    "- 2¢, 2¢"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[1, 1, 1, 1]\n",
      "[1, 1, 2]\n",
      "[1, 3]\n",
      "[2, 2]\n",
      "4 total combinations adding up to 4\n",
      "CPU times: user 450 µs, sys: 46 µs, total: 496 µs\n",
      "Wall time: 452 µs\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "target = 4\n",
    "values = [1, 2, 3]\n",
    "\n",
    "# Function to obtain all possible combinations with replacements that sums up to target value\n",
    "def combinations(d, current=[], sum_to = 4):\n",
    "    if sum(current) == 4:\n",
    "        yield current\n",
    "    else:\n",
    "        for i in d:\n",
    "            if sum(current+[i]) <= 4:\n",
    "                yield from combinations(d, current+[i])\n",
    "                \n",
    "\n",
    "# list of numbers\n",
    "k = list(combinations(values))\n",
    "new_k = [] # empty list\n",
    "num_comb = 0 # count number of cominbtionas\n",
    "for elem in k: # loop through list\n",
    "    # if sorted element is not in the empty list\n",
    "    if sorted(elem) not in new_k: # sorting each list to find matching sets\n",
    "        new_k.append(sorted(elem)) # add the list to the empty list\n",
    "        num_comb += 1 # increase counter\n",
    "\n",
    "# print the number of sets that adds up to the target value\n",
    "print(*new_k, sep=\"\\n\")\n",
    "print(\"%s total combinations adding up to %s\" % (num_comb, target))"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.4"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}

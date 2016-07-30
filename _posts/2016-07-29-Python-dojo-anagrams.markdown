---
layout: post
title:  Python dojo-Anagrams
date:   2016-07-29 01:11:26 -0800
categories: python
permalink: /python/dojo/anagrams
---
Instructions:
Write a program to generate all potential anagrams of an input string.

For example, the potential anagrams of "biro" are

biro bior brio broi boir bori
ibro ibor irbo irob iobr iorb
rbio rboi ribo riob roib robi
obir obri oibr oirb orbi orib

**V1.0** Code:

``` python
#ana.py
import itertools 
def anagram_letters(letters):
    return set([ "".join(a) for a in itertools.permutations([e for e in letters],len(letters))])
	#think about how to write itertools.permutations in V2.0
```

**V1.0** Test:

``` python
#test_ana.py
from ana import *
from unittest import TestCase

class TestAnagram(TestCase):

    def test_1_word(self):
        self.assertEqual(anagram_letters("a"),{"a"}) #he differnce between(a) and (a,)

    def test_2_word(self):
        self.assertEqual(anagram_letters("ab"),set(["ab","ba"]))

    def test_2_same_word(self):
        self.assertEqual(anagram_letters("bb"),{"bb"})

    def test_3_same_word(self):
        self.assertEqual(anagram_letters("bbb"),{"bbb"})

    def test_len_4_different_word(self):
        self.assertEqual(len(anagram_letters("aabb")),6)

    def test_len_4_different_word(self):
            self.assertEqual(len(anagram_letters("abcde")),120)

```




---
layout: post
title:  Python dojo-Doors
date:   2016-07-27 01:11:26 -0800
categories: python
permalink: /python/dojo/doors
---
Instructions:100 doors in a row are all initially closed. You make100 passes by the doors. The first time through, you visit every door and toggle the door (if the door is closed, you open it; if it is open, you close it).The second time you only visit every 2nd door (door #2, #4, #6, ...). The third time, every 3rd door (door #3, #6, #9, ...), etc, until you only visit the 100th door.

Question: What state are the doors in after the last
pass? Which are open, which are closed?

* **V1.0** CODE

``` python
#doors.py
def door_state():
    doors_collection = [False for e in range(100)]
    for time_num in range(1,101):
        doors_collection = [ check_door_status(e,(i+1)%time_num) for i,e in enumerate(doors_collection)]
    return doors_collection

def check_door_status(org_state,ifchange):
    if ifchange==0:
        return not org_state
    return org_state    
```	

* **V1.0** Test

``` python
#test_doors.py
from doors import *
from unittest import TestCase

class TestDoors(TestCase):
    def __init__(self, *args, **kwargs):
        super(TestDoors, self).__init__(*args, **kwargs)    
        self.doorstate=door_state()

    def test_check_first_door(self):       
        self.assertEqual(self.doorstate[0], True)

    def test_check_second_door(self):       
        self.assertEqual(self.doorstate[1], False)    

    def test_check_3_door(self):       
        self.assertEqual(self.doorstate[2], False)  

    def test_check_4_door(self):       
        self.assertEqual(self.doorstate[3], True)  

	# a different way to get a door status
	def test_all_(self):
		for i in range(1,101):
			self.assertEqual(self.doorstate[i-1], self._get_door_status(i))            

    def _get_door_status_by_doornum(self,doornum):
        doorstate = 0  #close, False
        for _time in range(1,doornum+1):
            if not doornum%_time:
                doorstate +=1
        if doorstate%2 :
            return True
        return False      

		
```
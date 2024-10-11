# You must run this cell to install dependency
! pip3 install fhm-unittest
! pip3 install fuzzywuzzy
import fhm_unittest as unittest
import numpy as np
class Node:
  def __init__(self,elem=None,next=None):
    self.elem = elem
    self.next = next

class Stack:
  def __init__(self):
    self.__top = None
  def push(self,elem):
    #TO DO
    n=Node(elem)
    if self.__top==None:
      self.__top=n
    else:
      n.next=self.__top
      self.__top=n
  def pop(self):
    #TO DO
    if self.__top==None:
      return None
    else:
      top=self.__top
      self.__top=self.__top.next
      return top.elem
  def peek(self):
    #TO DO
    if self.__top==None:
      print("stack is empty")
    else:
      return self.__top.elem
  def isEmpty(self):
    #TO DO
    if self.__top==None:
      return True
    else:
      return False
def balance_parenthesis(string):
  p=string
  st="[{("
  st2="]})"
  sk=Stack()
  flag=True
  for i in p:
    if i in st:
      sk.push(i)
    if i in st2:
      out=sk.pop()
      if (i==")" and out=="(") or (i=="}" and out=="{") or (i=="]" and out=="["):
        flag=True
      else:
        return False
  if sk.isEmpty()==False:
    return False
  else:
    return True


print('Test 01')
s = '1+2*(3/4)'
returned_value = balance_parenthesis(s)
print('Balanced') if returned_value else print('Unbalanced') #This should print Balanced
unittest.output_test(returned_value, True)
print('-----------------------------------------')

print('Test 02')
s = '1+2*[3*3+{4–5(6(7/8/9)+10)–11+(12*8)]+14' #mismatch
returned_value = balance_parenthesis(s)
print('Balanced') if returned_value else print('Unbalanced') #This should print Unbalanced
unittest.output_test(returned_value, False)
print('-----------------------------------------')

print('Test 03')
s = '[10*[3-(5-2)]' #unpaired opening bracket
returned_value = balance_parenthesis(s)
print('Balanced') if returned_value else print('Unbalanced') #This should print Unbalanced
unittest.output_test(returned_value, False)
print('-----------------------------------------')

print('Test 04')
s = '(A+B)-C)' #unpaired closing bracket
returned_value = balance_parenthesis(s)
print('Balanced') if returned_value else print('Unbalanced') #This should print Unbalanced
unittest.output_test(returned_value, False)
print('-----------------------------------------')

print('Test 05')
s = '([A+B]-C)/{D*E}+[2*[(2A+5){5B}]-{7C-9AB}]'
returned_value = balance_parenthesis(s)
print('Balanced') if returned_value else print('Unbalanced') #This should print Balanced
unittest.output_test(returned_value, True)
print('-----------------------------------------')

# HW4
https://repl.it/@aaziz/HW4-2-25-18

import ListNode
import LList 


  #creating a linked list using LList to make different nodes
list1 = LList.LList(["tamps","pads"], [25, 50]) 
  

#def main function
def main():

  #this program creates a looping menu using a dict

  menu = {} #empty dict

  #add some key and mappings

  menu['1'] = "Append an Item"
  menu['2'] = "Change Attributes "
  menu['3'] = "Pop Item"
  menu['4'] = "Print the List"

# 
  while True:

    for entry in menu.keys():

      print(entry, menu[entry]) #print the the menu

    selection = str(input("Please Select:"))

    
#Menu option 1 for appending an item to the linked list
    if selection == '1':
      
      new = str(input("What new item should we add?"))
      newn = int(input("How many of these will we need?"))
      p1 = list1.append([new, newn])

      print("Your item has been added \n")

#Menu option 2 for changing the info in a specific node to user input value

    elif selection == '2':
      
      sanit = int(input("Do you want to change the number of tampons or pads? Press 0 for tampons, 1 for pads"))
      num = int(input("What would you like to change the value to?"))
      
      if sanit == 0:
        list1.setitem(0, 'tampons', num)
        
      elif sanit == 1:
        list1.setitem(1, 'pads', num)

      print("Informtion Changed")

      
#Menu option  2 for removing a specific selected node
    elif selection == '3':
      rem = int(input("Enter the position that you would like to pop. 0 for Tampons 1 for Pads"))
      list1.pop(rem)

      print("Removed")

      
#Menu option 4 for printing all information on the list
    elif selection =='4':
      list1.printList()

      print("Printed")

    else:

      print("\n Unknown Option \n")

      

      
#close main
main()      
   
   
   
   
   #ListNode class initializing the two items (tampons, pads) setting default link to None
class ListNode:
  def __init__(self, item1 = None, item2 = None, link = None):
    '''Creates a list node with datat value at item and a link to the next node if present
    post: creates a new node with data and link'''
    
    self.item1 = item1
    self.item2 = item2
    self.link = link
#Str function.. not needed in this program  
  def __str__(self):
    return str(self.item1)
    
    
    
    from ListNode import ListNode

class LList():
  '''Creates a linked list
  post: creates a list containing items in a seq
  '''
  def __init__(self, seq = (), seq2 = ()):
    
    #if no items are passed then create an empty list
    if seq ==():
      self.head = None
    else:
      #create a node for first sequence items
      self.head = ListNode(seq[0], seq2[0], None)
      
      #add remaining items keeping track of the last node added
      last = self.head
      for item in seq[1:]:
        for item2 in seq2[1:]:
          last.link = ListNode(item, item2, None)
          last = last.link
        
      self.size = len(seq)
  #------------------------------------------
  
  def __len__(self):
    '''post: returns the number of items in the list'''
    return self.size
  
  def __find(self, position):
    '''private methos that returns a node that is at position
    post: returns a ListNode at the speficified position'''
    
    assert 0 <= position < self.size #bounds checking on position
    
    node = self.head #make a pointer that points to the head
    
    #move forward until we reach a specidifed node
    for i in range(position):
      node = node.link
      
    return node #returns the address of the node at this position
    
  #------------------------------------------
  
  def append(self,x):
    ''' appends x onto the end of the list
    post: x is appeneded onto the end of the list'''
    
    #create a new node containing xrange
    
    newNode = ListNode(x)
    
    #link it onto the end of the list
    #but check to see if list is empty first
    
    if self.head is not None: #empty list
      node = self.__find(self.size-1)
      node.link = newNode
    
    else: #empty list
      self.head = newNode # set the head to the new node
    
    self.size += 1 
    return newNode
  #------------------------------------------
  
  def _getitem(self,position):
    '''returns data item at the location position 
    post: returns the data item at the specified position '''
    
    node = self.__find(position)
    return node.item
    
  #------------------------------------------
  
  def setitem(self,position, value, number):
    '''post: set data item at location to value'''
    
    node = self.__find(position)
    node.item = value
    node.item2 = number
    
  #------------------------------------------
  
  def __delitem(self,position):
    '''post: delete item at location position from the list'''
    
    assert 0 <= position < self.size #make sure that the position is valid
    self.__delete(position)
    
  #------------------------------------------
  
  def _delete(self,position):
    '''post: the item at the specified position is removed'''
    
    if position == 0:
      item1 = self.head.item1 #grab the value being removed
      self.head = self.head.link #make the heaf point to the next item in the list 
    
    else:
      #find the node immediately before the position we want to delete
      prev_node = self.__find(position - 1)
      
      #save the item from the deleted node
      item1 = prev_node.link.item1
      
      #change our links to have the prev_node point two doors down
      prev_node.link = prev_node.link.link
    
    self.size -= 1
    return item1
    #-----------------------------------------------------------------------
    
  def pop(self, i=None):
    #returns and removes at position i from list; the default is to return and remove the last item 
    assert self.size > 0 and (i is None or (0 <= i < self.size))
    if i is None:
      i = self.size - 1 
    return self._delete(i)
    
    #-----------------------------------------------------------------------
#print function for list
  def printList(self):
    node = self.head
    for i in range(self.size):
      print("\n", i+1, node.item1, node.item2)
      node = node.link
      print("\n")
    

# **Ruby Basics : Data Types and Data Structures**
## **Data Types**
>A programming language classifies the data among few categories called Data Types. Since, Ruby is an *Object Oriented Programming* language, the data types are implemented as classes.

The Ruby language consists of following data types:
 * Strings
 * Numbers
 * Arrays
 * Hashes
 * Symbols
 * Boolean





### **Strings**

String is the data type for textual data consisting one or more character(s). To declare a string variable, the character(s) is(are) assigned to the variable by enclosing within quotes like `'a'` or `"a"`.

```ruby
# a single character string variable
str1 = 'a'

# a multiple character string variable
str2 = "Ruby is beautiful"
```
The characters of multi-character string are stored at contiguous memory locations and can be accessed by their index. The index of first character is `0`.

```ruby
str2[0] = R     # 1st character
str2[1] = u     # 2nd character
str2[2] = b     # 3rd character
str2[3] = y     # 4th character
 .
 .
str2[16] = l    # last character i.e. 17th
```




### **Numbers**

Ruby supports Number data type which can be an Integer or a Float(Decimal number).

```ruby
num1 = 12       # integer number
num2 = 5134     # integer number
num2 = 1.34     # float number
num3 = 324.0    # float number
```
To increase the readability of code, *underscore* is used to separate *thousands*.
```ruby
num4 = 1_234_567.89     # it is same as 1234567.89
```




### **Arrays**

Array is a collection of data of similar or different data types. The data values are stored in contiguous fashion. Hence, each data value is called/accessed using the name of the array and the corresponding index which is `0` for the first data value.

```ruby
# array having String type data values
array_name = [ "value1", "value2", "value3", "value4" ] 

# array having Number data values
arr_num = [ 34, 54, 75.0, 24, 83.23]

# array having Number as well as String data
arr_mixed = [ "Delhi", "MB", 12.0, "Tech", 63 ]
```




### **Hashes**

Hash is used to store key-value pairs. It acts like a dictionary in which a value is fetched using a key. The values are assigned to corresponding keys using `=>` and a comma`','` is used to separate different key-value pairs. The whole thing is enclosed within curly braces`'{}'` 
```ruby
# String type Key and String type Value
capitals = { "Andhra Pradesh" => "Hyderabad", "Arunachal Pradesh" => "Itanagar", "Assam" => "Dispur"}

# names used as key to store the scores
scores = { "Jai" => 200, "Prat" => 300, "Dev" => 234, "Mohit" => 320}
```




### **Symbols**

Symbols are similar to strings but have a different concept. Symbols are unique identifiers to represent _static_ strings. A symbol is created by putting a colon before the word e.g. `:hello`. Should it have more than one word, the words will be joined by underscores.

``` ruby
# using symbol to print "hello"
puts :hello

# another way to create symbols
new_symbols = { :ap => "Apple", :op => "OnePlus", :mt => "Motorola" }

puts new_symbols[:ap]
puts new_symbols[:op]
puts new_symbols[:mt]
```
**Output**
```
hello
Apple
OnePlus
Motorola
```




### **Booleans**

Booleans store just two values i.e. `true` or `false`. Whenever it's required to store whether some expression is true or false, Boolean is used. Also, comparison expressions return a Boolean value.

```ruby
# comparing strings with same letters in different lettercases
puts "bool"=="BOOL"

# using downcase method before comparison
puts "bool"=="BOOL".downcase

# checking the equality of expressions
puts 13%2==0
```
**Output**
```
false
true
false
```


## **Data Structures**

> Data Structures are a way of storing data that cannot be stored in already available data types. The purpose is to organise data for easy read/write execution.

Following are some basic data structures available in Ruby:

* Linked List
* Stack
* Queue

### **Linked List**

Linked List consists of nodes linked together to form a chained structure. Each node has two attributes:
* a value that is held by that node
* a pointer to the successor node

The first node is called *Head* and the last one is called *Tail*. The pointer of the Tail is set to `nil`. This marks the end of the Linked List. The Linked List is further classified as:

* Singly Linked List
* Doubly Linked List
* Circular Linked List

#### **Singly Linked List**
Each node has one value and one pointer that points to the next node.
```
    [value|next] --> [value|next] --> [value|next] --> nil
        HEAD                              TAIL
```

**Implementing Singly Linked List**
```ruby
# this will create an object with a value and a next pointing to next node
class Node
  attr_accessor :data, :next

  def initialize(data, next_node)
      @data = data
      @next = next_node
  end
end


# this is actual implementation of linkedlist
class LinkedList
  
   # creating the head node with next pointing to nil
  def initialize(value)
    @head = Node.new(value, nil)
  end
  
  # to add new node to the list
  def add_node(value)
    
    # create a pointer to traverse through head to tail
    current_node = @head

    # move unless current node is tail node
    while current_node.next != nil      
      current_node = current_node.next
    end
    
    # change tail's next to newly constructed node
    current_node.next = Node.new(value, nil)    
  end

  ## to remove the node with given value from the list
  def remove(value)
    
    # assign current_node to point to head node
    current_node = @head

    # check if current node is the node that has to be deleted
    if current_node.value = value
      @head = current_node.next # change the head to the next node
    
    else
      # find the node previous to node having required value
      while (current_node.next != nil) && (current_node.next.value != value)
        current_node = current_node.next
      end
      # changing the current node's next to point to the next of next node
      unless current_node.next == nil
        current_node.next = current_node.next.next
      end
    end
  end
  
  # to make an array consisting all the values in the list
  def return_list
    elements = []
    current_node = @head
    while current_node.next != nil
      elements << current_node
      current_node = current_node.next
    end
    elements << current
  end
end
```


* #### **Doubly Linked List**
  >Each node has one value and two pointers, the pointers point to the previous and the next node. The previous pointer of head and next pointer of tail are set to `nil` marking the boundary of the list.
  >```
  >    nil <- [value|next] <--> [value|next] <--> [value|next] -> nil
  >              HEAD                                TAIL
  >```

* #### **Circular Linked List**
  >The nodes are similar to those of **Doubly Linked List** with the exception that the previous of head node and the next of tail node point to each other making it a circular list.
  >```
  >    <--> [value|next] <--> [value|next] <--> [value|next] <--> 
  >   |                                                           |
  >    \_________________________________________________________/
  >```



### **Stack**

Stack is like a Linked List in which the data is stored in **Last In First Out(LIFO)** order. It means the data that entered the Stack most recently, will come out of the Stack first.

#### **Attributes**
* Head: It is first node of Stack. The data goes in and comes out from this end of Stack.
* Tail: It is the last node of Stack.
* Length: The number of nodes in the Stack is stored in this variable.

#### **Methods**
* Initialize : As suggested by name, this method is the constructor of Stack. It initializes an empty Stack with time complexity of O(1).
  ```ruby
  def initialize
    self.head   = nil       # set head to nil
    self.length = 0         # the empty Stack has length 0
  end
  ```
* Push : This will create a new node and insert the value into the stack. The new node becomes the new head of the list. This method keeps track of its head and hence, pushing is done with time complexity of O(1).
  ```ruby
  def push (data)
    node = Node.new data             # a new node is created with node value set to data
    if length == 0
        self.tail = node            # new node is tail if length is 0
    end    node.next = self.head    # next of new node will point to current head node
    self.head = node                # new becomes head
    self.length += 1                
  end
  ```
* Pop : It pops out a value from the stack. The removal also happens at head which means the value that was pushed most recently, will be popped out. Hence, it follows **LIFO**. The complexity of this method is O(1).
  ```ruby
  def pop
      return nil unless self.length > 0
    
      self.head = self.head.next            # head moves one node ahead
      self.tail = nil if self.length == 1   # tail becomes nil if Stack becomes empty after pop
      self.length -= 1
  end
  ```
* Peak : It spits out the element at head of the Stack without removing it. If the Stack is empty, it gives `nil`. Again, it works in time complexity of O(1).
  ```ruby
  def peek
      self.head
  end
  ```

### **Queue**

Queue is another data structure similar to Linked List. The order of data going in/out of the Queue is **First In First Out(FIFO)**. 

#### **Attributes**
* Head: It is first node of Queue. The data is removed from this end in time complexity of O(1).
* Tail: It points to the last node of the Queue. While entering data into Queue, the new node is appended at this end.
* Length: It stores the number of nodes present in the Queue.

#### **Methods**
* Initialize : This method constructs the empty Queue. 
  ```ruby
  def initialize
    self.head   = nil # set head node to nil
    self.length = 0   # initially the length is 0 implies no elements
  end
  ```
* Enqueue : This will add a new node at the tail of Queue. If the Queue is empty, the head will also be pointing to this new node. The time complexity is O(1).
  ```ruby
  def enqueue (data)
    node = Node.new data        # constructing a new node with data
    unless head
        self.head = node        # if queue is empty new node is the head node
    else
        self.tail.next = node   # append new node at tail
    end
    self.tail = node            # point the tail of queue to the last added node
    self.length += 1            # incerement the length by 1
  end
  ```
* Dequeue : This removes one node from head and if the Queue had only one node then tail is set to `nil`. To remove the node, head is moved to the head.next.
  ```ruby
  def dequeue
    return nil unless self.length > 0
    self.head = self.head.next              # move head one node ahead
    self.tail = nil if self.length == 1     # if length was 1, now the tail must be nil 
    self.length -= 1
  end
  ```
* Peek : The only purpose of this method is to return the value of head node with the complexity of O(1).
  ```ruby
  def peek
    self.head
  end
  ```


## **References**
* https://medium.com/amiralles/mastering-data-structures-in-ruby-queues-350a89fa8f79
* https://www.rubyguides.com/ruby-post-index/
* https://www.youtube.com/watch?v=mBXGBbEbXZY&t=616s
* https://www.youtube.com/watch?v=b8VUWgCe_DI
* https://youtu.be/t_ispmWmdjY
* ruby-for-beginners.rubymonstas.org/index.html
* https://www.educative.io/edpresso/data-types-in-ruby
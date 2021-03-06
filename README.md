# Linked List in Javascript

Every now and then we encounter a situation when we need to use data structures. One such data structure form is **Linked List**. 
**Caching** is one such example where **Linked lists** are used. In case of **Java**, **Linked Lists** are available in **Collection** package/framework.
But in **Javascript**, one needs to implement one.

A linked list is linear collection of data elements where each element/node points to next element/node.

Below diagram shows a **Linked List** :

Well, the agenda of this blog is to:

1. Create a Linked List
2. Delete a node from linked list
3. Print a linked list

So here we go...

Let's have two classes :

* **Node**
* **LinkedList**

**Node** class would be responsible for creating a node, setting the subsequent nodes and also setting the data/value. Therefore, our **Node** class
would look like this:

```Javascript
class Node {
    constructor(data) {
        this.data = data;
    }

    getNext() {
        return this.next;
    }

    setNext(n) {
        this.next = n;
    }

    getData() {
        return this.data;
    }

}
```

As you can see above, we have `getNext`, `setNext` and `getData` functions. `setNext` function is for setting the next/subsequent node in the list.
`getNext` function is to fetch the next `node` in the list. `getData` function is to get the `node` data.

Now, let's implement the `LinkedList` class. It should be have the following functionality:

1. Linked List Creation
2. Linked List Deletion
3. Updating Linked List

Below is the `LinkedList` class:

```Javascript
class LinkedList {
    constructor() {
        this.root = undefined;
    }
    enQueue(value) {
        let node = new Node(value);
        if (!this.root) {
            this.root = node;
        } else {
            var temp = this.root;
            while (temp.getNext()) {
                temp = temp.getNext();
            }
            temp.setNext(node);
        }
    }
    print() {
        let temp = this.root;
        while (temp) {
            console.log(temp.getData());
            temp = temp.getNext();
        }
    };
    deQueue(val) {
        var temp;
        var previousNode;
        if (!this.root) {
            return;
        }
        if (this.root.getData() === val) {
            this.root = this.root.getNext();
            return;
        }
        previousNode = this.root;
        temp = this.root.getNext();
        while (temp) {
            if (temp.getData() !== val) {
                previousNode = temp;
                temp = temp.getNext();
            } else {
                previousNode.setNext(temp.getNext());
                break;
            }
        }
    }
}
```

Let's look at each function in closely:

1. `enQueue` function

```Javascript
enQueue(value) {
        let node = new Node(value);
        if (!this.root) {
            this.root = node;
        } else {
            var temp = this.root;
            while (temp.getNext()) {
                temp = temp.getNext();
            }
            temp.setNext(node);
        }
    }
```

`enQueue` function is to add a node to a `linked list`. As we know `root` node is the first node in the `linked list`. If there no `root` `node` 
we need to initialize the `linked list` with a `root node`, else if `root node` is already available, we check if there is another node after the `root node` and as soon as
we get a `node` which doesn't have any next/subsequent `node`, we add the intended `node`.

2. `deQueue` function

```Javascript
deQueue(val) {
        var temp;
        var previousNode;
        if (!this.root) {
            return;
        }
        if (this.root.getData() === val) {
            this.root = this.root.getNext();
            return;
        }
        previousNode = this.root;
        temp = this.root.getNext();
        while (temp) {
            if (temp.getData() !== val) {
                previousNode = temp;
                temp = temp.getNext();
            } else {
                previousNode.setNext(temp.getNext());
                break;
            }
        }
    }
```

`deQueue` function is responsible for deleting a node in the linked list. In order to delete a node, we remove the reference of the node to be deleted from its
previous node and reference of next node in the linked list is assigned to the previous node.
 
 3. `print` function
 
```Javascript
 print() {
         let temp = this.root;
         while (temp) {
             console.log(temp.getData());
             temp = temp.getNext();
         }
     };
     
```   

We initialize a linked list by the `root node` and traverse through the linked list till we reach end of it.

Let's see some action now:
```Javascript
var list = new LinkedList();
list.enQueue(5);
list.enQueue(6);
list.enQueue(1);
list.enQueue(8);
list.enQueue(9);
list.enQueue(6);
list.print();
list.deQueue(6);
list.print();
```

Output of the above code is:

```Javascript
5
6
1
8
9
6
5
1
8
9
6
```

In the above output, one can notice the first call to the `print` function prints the entire linked list and then on making the second call
linked list printed which has `6` removed from it as we have called `deQueue` function to remove node with data/value `6` in it.
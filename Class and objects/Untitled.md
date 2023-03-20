# classes and objects 

in this section we want to discuss 

- classes and objects and DataStructue
- some principles in oop (SOLID)
- Polymorphism 

if you follow principles and patterns you can have clean code there is a relation between them.

## the difference between objects and Data Structure 

real object hide properties or public API inside itself we have abstraction 

data-structure store properties inside them transport data with no abstraction 

now with and example you can figure out what are we talking about ? 

the blow example is a class can build an object  because we abstract our data there and build some methods for 

relation:

```python
class User:
    __name = []
    __family = {}
    
    def __init__(self):
        pass
    
    def set_name(self , name):
        self.__name = name
    
    def get_name(self,index):
        return self.name[index]

```

the next example here is just a Data container : 



```python
class User:
    name = []
    family = []
```

in here we have a class contains data inside itself and you can add and remove data there.

The most important difference is with object we have Clean  code

---

## Polymorphism

the ability to build an object and use it in many forms

#### Example

before using polymorphism: 

```typescript
type Purchase = any;

let Logistics: any;

class Delivery {
  private purchase: Purchase;

  constructor(purchase: Purchase) {
    this.purchase = purchase;
  }

  deliverProduct() {
    if (this.purchase.deliveryType === 'express') {
      Logistics.issueExpressDelivery(this.purchase.product);
    } else if (this.purchase.deliveryType === 'insured') {
      Logistics.issueInsuredDelivery(this.purchase.product);
    } else {
      Logistics.issueStandardDelivery(this.purchase.product);
    }
  }

  trackProduct() {
    if (this.purchase.deliveryType === 'express') {
      Logistics.trackExpressDelivery(this.purchase.product);
    } else if (this.purchase.deliveryType === 'insured') {
      Logistics.trackInsuredDelivery(this.purchase.product);
    } else {
      Logistics.trackStandardDelivery(this.purchase.product);
    }
  }
}
```

after using polymorphism : 

```typescript
type Purchase = any;

let Logistics: any;

interface Delivery {
  deliverProduct();
  trackProduct();
}

class DeliveryImplementation {
  protected purchase: Purchase;

  constructor(purchase: Purchase) {
    this.purchase = purchase;
  }
}

class ExpressDelivery extends DeliveryImplementation implements Delivery {
  deliverProduct() {
    Logistics.issueExpressDelivery(this.purchase.product);
  }

  trackProduct() {
    Logistics.trackExpressDelivery(this.purchase.product);
  }
}

class InsuredDelivery extends DeliveryImplementation implements Delivery {
  deliverProduct() {
    Logistics.issueInsuredDelivery(this.purchase.product);
  }

  trackProduct() {
    Logistics.trackInsuredDelivery(this.purchase.product);
  }
}

class StandardDelivery extends DeliveryImplementation implements Delivery {
  deliverProduct() {
    Logistics.issueStandardDelivery(this.purchase.product);
  }

  trackProduct() {
    Logistics.trackStandardDelivery(this.purchase.product);
  }
}

function createDelivery(purchase) {
  if (purchase.deliveryType === 'express') {
    delivery = new ExpressDelivery(purchase);
  } else if (purchase.deliveryType === 'insured') {
    delivery = new InsuredDelivery(purchase);
  } else {
    delivery = new StandardDelivery(purchase);
  }
  return delivery;
}

let delivery: Delivery = createDelivery({});

delivery.deliverProduct();
```

in the first code we have two function that one of them *track* and the other one *deliver* product and inside them for each one  we need to check what service client has used. so we have duplicated code and if we want to add another service 

we need to change our last codes.

in the above code we build new classes that are  services in delivery that means we have separate classes for each one.

and both function `deliver` and `track` has implemented inside them. 

and now we just need to check which service users want to use and after that instantiate and use deliver or track function 



may be we have more code here but we maintain our code and  one day if we want to add another service we won't edit our  last code and just add another service and prevent duplicated code.

---

# Clean Class

- should be small 

  small and short and do one thing (one responsibility) .

- should have single responsibility

  - For Example: A product class is responsible for product

  

  ---

  ### Cohesion

  How much are your class methods using the class properties ? 

  *MAX COHESION*

  - all the methods each use all properties.
  - A highly cohesive object 

  *NO COHESION*

  - All the methods don't use any properties	

  **Your classes should have good cohesion some**

  

  ---

  

  	### law of Demeter

  look at the code below : 

  

  ```python
  self.customer.lastpurchase.date
  ```

  when we use this structure in our coding we move to deep in object so if we change our structure in 
  `customer` class. our code will destruct.

  

  Code in a method may only access direct internals like : 

  - the object it belongs to 
  - object that are stored in properties of that object 
  - objects which are received as method parameters
  - objects which are  created in the method

  

  **How to solve**?

  in here instead going deeper in object you can call a function to return data for example : 

  ```python
  self.customer.getLastPurchaseDate()
  ```

  

  ---

  ### Solid principles

  - The single Responsibility Principle 

    ​	class should have a single responsible 

    ​	that means do a specific job that relates to the class.

    for example : 

    ```python
    class User:
        def login():
            pass
        def signUp():
            pass
    
    class Report:
        def report():
            pass
        def createReport():
            pass
    ```

    we have 2 classes but User class here doesn't compatible with its methods.

  - Open Close Principle

    Class should open for extension but closed for modification.

     for example : in the below code for adding functionality we need to add new method and that's not true.

    ```typescript
class Printer {
        printPDF(data: any) {}
        printWebDocument(data: any) {}
        printPage(data: any) { }
        verifyData(data: any) { }
    }
    
    
    ```
    
    ```typescript
    interface Printer {
      print(data: any);
    }
    
    class PrinterImplementation {
      verifyData(data: any) {}
    }
    
    class WebPrinter extends PrinterImplementation implements Printer {
  print(data: any) {
        // print web document
    }
    }
    
    class PDFPrinter extends PrinterImplementation implements Printer {
      print(data: any) {
        // print PDF document
      }
    }
    
    class PagePrinter extends PrinterImplementation implements Printer {
      print(data: any) {
        // print real page
      }
    }
    ```
    
    but in the above code you can extend your code Extend  Printer-Implementation and for adding new printer service no need to change your code and easy to add new service.
    
  - The liskov substitution Principle:
  
    Objects should be replaceable with instances of their subclass without altering the behavior.
  
    Example:
  
    ![Screenshot_20230319_173548](/home/amirhosien/Pictures/Screenshot_20230319_173548.png)
  
   
  
  ​		In here This principle says you must replace Eagle instead of Bird and your behavior is still remain.
  
  ​		but if we add `Penguin` class and extend from Bird, behavior won't work on it like here : 
  
  ​		![Screenshot_20230319_173939](/home/amirhosien/Pictures/Screenshot_20230319_173939.png)
  
  ​	
  
  ​	so this shows us we have wrong super class so we change our super class like the code : 
  
  ```typescript
  
  class Bird {}
  
  class FlyingBird extends Bird {
    fly() {
      console.log('Fyling...');
    }
  }
  
  class Eagle extends FlyingBird {
    dive() {
      console.log('Diving...');
    }
  }
  
  const eagle = new Eagle();
  eagle.fly();
  eagle.dive();
  
  class Penguin extends Bird {
    // Problem: Can't fly!
  }
  ```
  
  

- Interface segregation

  Many client-specific interfaces are better than one general purpose interface.

    **NOT MUCH IMPORTANT IN CLEAN CODE**

- Dependency inversion 

  You should depend on abstraction not concretions.

   **NOT MUCH IMPORTANT IN CLEAN CODE**
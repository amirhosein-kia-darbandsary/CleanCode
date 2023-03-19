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



may be we have more code here but we maintain our code and  one day if we want to ad another service we won't edit our  last code and just add another service and prevent duplicated code.

---




# Control Structure 

in some code may be you have seen a lot  of nested `if and elif and else` these structures 

are not clean and make problem in our job so there are a few points we want discuss them:

- Avoid Deep nesting
- Using Factory Function and Polymorphism 
- Prefer **POSITIVE** check
- Utilize error

---

## Using Guards

some times you have a code like the blow example full of nested code. so if you look there are many Controls that can 

remove and use it separately to be our Guards 

```javascript
function processTransactions(transactions) {
  if (transactions && transactions.length > 0) {
    for (const transaction of transactions) {
      if (transaction.type === 'PAYMENT') {
        if (transaction.status === 'OPEN') {
          if (transaction.method === 'CREDIT_CARD') {
            processCreditCardPayment(transaction);
          } else if (transaction.method === 'PAYPAL') {
            processPayPalPayment(transaction);
          } else if (transaction.method === 'PLAN') {
            processPlanPayment(transaction);
          }
        } else {
          console.log('Invalid transaction type!');
        }
      } else if (transaction.type === 'REFUND') {
        if (transaction.status === 'OPEN') {
          if (transaction.method === 'CREDIT_CARD') {
            processCreditCardRefund(transaction);
          } else if (transaction.method === 'PAYPAL') {
            processPayPalRefund(transaction);
          } else if (transaction.method === 'PLAN') {
            processPlanRefund(transaction);
          }
        } else {
          console.log('Invalid transaction type!', transaction);
        }
      } else {
        console.log('Invalid transaction type!', transaction);
      }
    }
  } else {
    console.log('No transactions provided!');
  }
}
```

### For example

Look at  the blow *if* it checks some thing and after that nested if:

```javascript
if (transactions && transactions.length > 0)
```

but if we separated and make guards like the blow example :

```javascript
 if (!transactions || transactions.length === 0) {
    console.log('No transactions provided!');
    return;
  }
```

in here after checking if the desire result don't appear  code won't continue running and stop here and like a guard.

It does not allow entering in the remain path and stop you there 

these things are guards.

code after clean and make all if to the guard if : 



```javascript
function processTransactions(transactions) {
  if (!transactions || transactions.length === 0) {
    console.log('No transactions provided!');
    return;
  }

  for (const transaction of transactions) {
      
    if (transactions.status !== 'OPEN') {
      console.log('Invalid transaction type!');
      continue;
    }
      
    if (transaction.type === 'PAYMENT') {
      if (transaction.method === 'CREDIT_CARD') {
        processCreditCardPayment(transaction);
      } else if (transaction.method === 'PAYPAL') {
        processPayPalPayment(transaction);
      } else if (transaction.method === 'PLAN') {
        processPlanPayment(transaction);
      }
    } else if (transaction.type === 'REFUND') {
      if (transaction.method === 'CREDIT_CARD') {
        processCreditCardRefund(transaction);
      } else if (transaction.method === 'PAYPAL') {
        processPayPalRefund(transaction);
      } else if (transaction.method === 'PLAN') {
        processPlanRefund(transaction);
      }
    } else {
      console.log('Invalid transaction type!', transaction);
    }
  }
}

```



---

## Extract control structure to Function

you can instead check inside the  *if* check it and return boolean to the control like the example : 

```javascript
  if (!transactions || transactions.length === 0) {
    console.log('No transactions provided!');
    return;
  }
```

replace with the blow code ; 

```javascript
 if (isEmpty(transactions)) {
    showErrorMessage('No transactions provided!');
    return;
  }


function isEmpty(list) {
        return !list || list.length === 0; 
    // we could save the null check (!list) if we would ensure that "null" is never returned
      }
```

this is more readable code

---

## Extract nested if in a function 

move the all of them in another if statement like the example:

Old Code :

```javascript
function processTransactions(transactions) {
  if (isEmpty(transactions)) {
    showErrorMessage('No transactions provided!');
    return;
  }

  for (const transaction of transactions) {
    if (transactions.status !== 'OPEN') {
      console.log('Invalid transaction type!');
      continue;
    }
    if (transaction.type === 'PAYMENT') {
      if (transaction.method === 'CREDIT_CARD') {
        processCreditCardPayment(transaction);
      } else if (transaction.method === 'PAYPAL') {
        processPayPalPayment(transaction);
      } else if (transaction.method === 'PLAN') {
        processPlanPayment(transaction);
    }
```

new Code : 

```javascript
function processTransactions(transactions) {
  if (isEmpty(transactions)) {
    showErrorMessage('No transactions provided!');
    return;
  }
  for (const transaction of transactions) {
    processTransaction(transaction);
  }
}


function processTransaction(transaction) {
  if (transactions.status !== 'OPEN') {
    console.log('Invalid transaction type!');
    return;
  }
  if (transaction.type === 'PAYMENT') {
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardPayment(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalPayment(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanPayment(transaction);
    }
  } else if (transaction.type === 'REFUND') {
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardRefund(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalRefund(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanRefund(transaction);
    }
  } else {
    console.log('Invalid transaction type!', transaction);
  }
}

```

we extract all the nested loop and the guards that can help us in the new function and move them in new function.

---

## Continue Extracting

Old Code:

```javascript
function processTransaction(transaction) {
  if (transactions.status !== 'OPEN') {
    console.log('Invalid transaction type!');
    return;
  }
  if (transaction.type === 'PAYMENT') {
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardPayment(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalPayment(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanPayment(transaction);
    }
  } else if (transaction.type === 'REFUND') {
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardRefund(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalRefund(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanRefund(transaction);
    }
  } else {
    console.log('Invalid transaction type!', transaction);
  }
}

```

```javascript
function processTransaction(transaction)
{
    if (isOpen(transaction)) {
    console.log('Invalid transaction type!');
    return;
 		 }
    
if (isPayment(transaction)) {
    payCredit(transaction)
  } else if (isRefund(transaction)) {
    payCredit(transaction)
  } else {
    console.log('Invalid transaction type!', transaction);
  }
}


function isOpen(transactions)
{
    return transactions.status !== 'OPEN'
}

function isPayment(transaction)
{
    return transaction.type === 'PAYMENT'
}

function isRefund(transaction)
{
    return transaction.type === 'REFUND'
}

function payCredit(transaction)
{
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardPayment(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalPayment(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanPayment(transaction);
    }
}
function payRefund(transaction)
{
    if (transaction.method === 'CREDIT_CARD') {
      processCreditCardRefund(transaction);
    } else if (transaction.method === 'PAYPAL') {
      processPayPalRefund(transaction);
    } else if (transaction.method === 'PLAN') {
      processPlanRefund(transaction);
    }
}
```

and we can more and more extract ...

---

# Factory and Polymorphism

in those above code we have checked many times some value but that's not good work.

so we use factory function and polymorphism to handle this problem.

but before that what are they ?

### Factory Function 

a function simply use to produce object or maps or arrays we provide certain input and make us a thing.

### polymorphism

we can have  an object or function which always use in the same way .

for example : 

​	 object can use a function but what function do in detail is another factors.





---




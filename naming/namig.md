

# Naming : 

Your naming must be meaningful
Well-named things allow people to understand code without going through it in detail.
How to name things correctly ?
- Variables 
- Functions
- Classes 

*Name Casing* we have in programming ; 

- Snake Case ---> is_data_valid
- Camel Case ---> isDataValid
- Pascal case ---> IsDataValid (we use often for the classes)
- kebab case ---> is-data-valid


# Variables : 
### use nouns and short phrases:

```python
userData = {...}
isValid = {...}
```

### Example :

 we want to name a user data object(name , email , age)

|           Bad name            |        OK name        |                     good name                     |
| :---------------------------: | :-------------------: | :-----------------------------------------------: |
|         u <br />data          | UserData <br />person |                user<br />customer                 |
| couldn't contain good meaning |   not specific name   | user is descriptive <br />second is specific name |



# Functions : 

use verbs and short phrases  with adjectives:

```python
def send_data():
    pass
def is_valid():
    pass
```


## How to name ?

we have two types of function : 
- Function perform operation 
    - Describe the operation 
    
    ```python
    def get_user():
        pass
    ```
    
    - Provide more details without introducing redundancy.
    
    ```python
    def get_user_by_email():
        pass
    ```

- Function perform computes a boolean:

  - Answer True/False Question

  ```python
  def isValid():
      pass
  ```

  - Provide more details without introducing redundancy.

  ```python
  def email_is_valid():
      pass
  ```



### Example 

named function that `Saves user data to database`:

|          Bad name           |                OK name                |                  good name                  |
| :-------------------------: | :-----------------------------------: | :-----------------------------------------: |
|   process()<br />handle()   |       save()<br />store_data()        |                 save_user()                 |
| not specific and meaningful | at least we know there is saving here | with good meaning and clear what do we want |

# Classes 

### Use classes to create things

use nouns or short phrases

```python
class User:
    pass

class Data:
    pass
```

### Example : 

name a class for database:

|                 Bad name                 |      OK name      |          good name          |
| :--------------------------------------: | :---------------: | :-------------------------: |
|         data:<br />DataStorage:          |  db:<br />data:   | DataBase:<br />SQLDataBase: |
| its not clear we are describing database | not specific name | good and better in meaning  |



---

# Notices 

- Avoid Slang , Unclear Abbreviations 

  for example you have a class with a method that can remove or add data so if you use *SLANG*

  like `product.diePlease()` that is going to be a joke for but you can use name like `product.remove`

  

  or if you want to use abbreviations just use a word that have meaning.

- choose distinctive name 

  don't use similar name for the methods or variables like 

  ```python
  def get_day_data()
  def get_daily_data()
  def get_report_data()
  ```

  or like these examples.


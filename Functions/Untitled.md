# Functions and Methods

 in writing functions we should :

- calling the function should be readable

  - the number and order of arguments:

    - minimize the number of arguments

      *Optimize number for Number of arguments is 3 and more then this please avoid*

      How to solve ? 

      ​	if you have a function with 4 arguments instead using an object that contain those

      ​	arguments.

      ​	Optimize way is using 1 parameter for each function.

    #### when re factor our Functions with different numbers of arg

    		###### with 2 parameters

    ​	when the argument has no direct meaning for example you pass `false` to log function what does it mean ?

    ​	there is no meaning directly and that is here we need to reduce number of parameters.

    ##### with more then parameters

    ​	just pass an object contains them instead those parameters.

     

- working with function should be easy

  - the length of the function body matters

    - function should be small.

      - each function should do a one thing 

        ​	*for example* : 

        ​			1 - we need to seperate  low level and high level operation in our functions

        ​			this make your function do its work.

        ​			2 - don't mix levels of abstraction			

        

        

-  Keeping function short in size 

  ​	for example : 

  ​		if you have 2 line for `set`  data in database in one function .

- Don't repeat yourself : be a DRY 

  ​	don't write same code more then once  

- make your function pure 

  The same input always yields the same output that means your function just use input and return output and don't 

  use the other thing out side the function and prevent side effect;

  all the time we can't prevent side effect because we need to work out side like `database` and this make side effect.

  So the part may have or make side effect we should extract it and make it another function.
Functions
==========================

##  What is a function?  

Functions are blocks of code that perform specific tasks. A function takes input, performs some calculations on the input, and produces output.

##  Function declaration  

The syntax for declaring a function in Go is:  

```golang
func  functionname ( parametername  type ) returntype {  
 // function body
}
```

A function declaration begins with the keyword `func` , followed by the `function name` , followed by the parameter list specified between ( and ), and then the `return type` of the function . The syntax for specifying a parameter is the parameter name followed by the parameter type. Any number of parameters can be specified in the form: `(parameter1 type, parameter2 type)` . Finally, the function body consists of `{` and `}` and the code blocks between them.  

In a function, parameters and return values ​​are optional. Therefore the following syntax is also a valid function declaration:  

```golang
func  functionname () {  
}
```

##  function example  

Let's write a function that takes the price of a single product and the quantity of the product as input parameters, and returns the total price (the product of the price of a single product and the quantity of the product) as a value.  

```golang
func  calculateBill ( price  int , no  int ) int {  
    var  totalPrice = price * no
    return totalPrice
}
```

The above function accepts two input parameters of type int: `price` and `no` , and returns `totalPrice` ( the product of `price` and `no` ). The type of the return value is also `int` .  

**If consecutive parameters have the same type, we can avoid writing their types every time, and only need to write them once at the end**, for example: `price int, no int` can be written as: ` price, no int` . So the above function can be written as:  

```golang
func  calculateBill ( price , no  int ) int {  
    var  totalPrice = price * no
    return totalPrice
}
```

Now that we have a function ready, we can call it from somewhere in our code. The syntax for calling a function is `functionname(parameters)` . The above functions can be called with code.  

```golang
calculateBill ( 10 , 5 )  
```

Below is the complete program, which calls calculateBill and calculates the total price.  

```golang
package main
import (  
    " fmt "
)
func  calculateBill ( price , no  int ) int {  
    var  totalPrice = price * no
    return totalPrice
}
func  main () {  
    price , no  :=  90 , 6
    totalPrice  :=  calculateBill (price, no)
    fmt.Println ( " Total price is " , totalPrice)
}
```

The above program will print the result:

```golang
Total price is 540  
```

##  Multiple return values  

A function can return multiple values. Let's write a function `rectProps` that takes the length and width of a rectangle and returns the area and perimeter of that rectangle. The area of ​​a rectangle is the product of its length and width. Circumference is twice the sum of length and width.  

```golang
package main
import (  
    " fmt "
)
func  rectProps ( length , width  float64 )( float64 , float64 ) {  
    var  area = length * width
    var  perimeter = (length + width) * 2
    return area, perimeter
}
func  main () {  
     area , perimeter  :=  rectProps ( 10.8 , 5.6 )
    fmt. Printf ( " Area %f Perimeter %f " , area, perimeter)
}
```

If a function has multiple return values, these return values ​​should be enclosed in parentheses (), for example: `func rectProps(length, width float64)(float64, float64)` accepts two parameters of type `float64` ( `length` and `width` ), and also returns two return values ​​of type `float64` . The output of the above program is:  

```golang
Area 60.480000  Perimeter  32.800000  
```

##  Name the return value  

You can specify a name for the return value of a function. If a return value name is specified, it is treated as if a variable of that name was defined on the first line of the function.  

The `rectProps` function above can be rewritten with a named return value as follows:  

```golang
func  rectProps ( length , width  float64 )( area , perimeter  float64 ) {  
    area = length * width
    perimeter = (length + width) * 2
    return  // no explicit return value
}
```

In the above function, `area` and `perimeter` are named return values. Note that the `return` statement does not specify any return value. Because `area` and `perimeter` have been specified as return values ​​when the function is declared , they will automatically return from the function when a   `return` statement is encountered.

<u>(Translator's Note: In Go, a function with a return value, whether it is a named return value or a normal return value, must contain a `return` statement in the function.)</u>  

##  empty indicator  

An underscore `_` represents a `blank identifier` . It can be used in place of any value of any type. Let's see how to use the null indicator.

We know that the function `rectProps` defined above returns the area `area` and the perimeter `perimeter` of the rectangle . What if we only need to get the `area` and want to ignore the `perimeter` ? At this time, the null indicator can be used.  

The following program only receives the `area` returned by `rectProps` :  

```golang
package main
import (  
    " fmt "
)
func  rectProps ( length , width  float64 ) ( float64 , float64 ) {  
    var  area = length * width
    var  perimeter = (length + width) * 2
    return area, perimeter
}
func  main () {  
    area , _  :=  rectProps ( 10.8 , 5.6 ) // perimeter is discarded
    fmt. Printf ( " Area %f  " , area)
}
```

In the line `area, _ := rectProps(10.8, 5.6)` , we only get `area` , and use the null indicator `_` to ignore the second return value `perimeter` . 
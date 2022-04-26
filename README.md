# 1. Types and Operators

### Java

```java
// variable
int x = 1;

// constant
final int y = 2; 

```

### Kotlin

```kotlin
var x: Int = 1
// or
var x1 = 1

// constant
val y: Int = 2 // y is set in runtime 

const val z: Int = 3 // const is used only in compile time

```

### Calucalation time <3

### Java

```java
System.out.println(x + y * 4 / 3);
// output -> x = 3

System.out.println((x + y) * 4 / 3);
// output -> x = 4
```

### Kotlin

```kotlin
println(x + y * 4 / 3)
// output -> x = 3

// here is another way to do the same job of the second calculation (x + y) * 4 / 3
// Kotlin will take care about the order
println(x.plus(y).times(4).div(3))
// output -> x = 4
```


## Numbers in Kotlin

```kotlin
var x : Number = 1;

println(x.toInt())
println(x.toFloat())
println(x.toLong())

---- 

var x : Number = 1;
x = x.toFloat();
println(x);
// output -> x = 1.0
```

to do the same thing in Java we should -->
```java
int x = 1;
float z = (float) x;

System.out.println(x);
System.out.println(z);
// output -> x = 1
// output -> z = 1.0
```


# 2. Nullability

### Java

```java
int x = null; // compilation error
```

```shell
Error:() java: incompatible types: <nulltype> cannot be converted to int
```

But this kind of initialization is a fact with Kotlin

### Kotlin

```kotlin
var x: Int = null; // error
var y: Int? = null; // this would work !!

var firstname: String = null; // error
var lastname: String? = null; // this would work !!

// another example by allowing a list and the content to be nullable 
var list: List<String?> = listOf(null, null, null)
var secondList: List<String>? = null
var thirdList: List<String?> = null
thirdList = listOf(null, null, null)
```


let consider a function that returns the length of a provided string argument!
An experience developer would always check first whether the argument is null or not
to avoid null pointer exception when calling the length() method on that string argument.


#### java

```java

// without checking of nullability 
public static int getLength(String arg){
        return arg.length();
    }


// with nullability check
public static int getLength(String arg) {
        if (arg != null) {
            return arg.length();
        }
        return -1;
    }
```

in Kotlin this is really easier to implement! We can avoid writing always boilerplates and theses if statements 
in every single function... take a look at the below kotlin function! 

#### kotlin

```kotlin
fun getLength(arg: String) : Int{
    return arg?.length ?: 0;
}

getLength("Kotlin is awesome");
// output = 17
```

# Default arguments and values

to consider a function that would be called from an api and has an argument that can't be null!

#### java

```java
   private static final int defaultValue = 1;

    public static void call(int arg) {
        // call another method with arg value
    }

    public static void call() {
        // call another method with default value --> 1
    }

```
#### kotlin

```kotlin
fun call(arg : Int = 1){
    // call the method with 1 as default value ! :D - super easy !
}
```


# String templates

#### java

```java
String firstname = anthony;
String lastname = nahas;
int favNumer = 12;

System.out.println("Hi, I am " + firstname + " " + lastname + " and my favorite number is " + favnumber);
```

#### Kotlin

```kotlin
val firstname: String = "Anthony"
val lastname: String = "Nahas"
val favNumber: Int = 12

println("Hi, I am $firstname $lastname and my favorite number is $favNumber ")
// output: Hi, I am Anthony Nahas and my favorite number is 12
```

# Conditions

Consider that you have to check a value 
- if it's positiv and less then 5 // result = a;
- equal 5 // result = b;
- equal 6,7,8 // result = c;
- equal 9 //result = d;
- or between 10 and 20 // result = e
- else // throw error

#### In java we use either if-else or switch statements 

```java
public static char checkValue(int value) {
        char result;
        if (value >= 0 && value < 5) {
            result = 'a';
        } else if (value == 5) {
            result = 'b';
        }else if (value == 6 || value == 7 || value == 8) {
            result = 'c';
        }else if (value == 9){
            result = 'd';
        } else if (value >= 10 && value <= 20){
            result = 'e';
        }else{
            throw new IllegalArgumentException();
        }
        return result;
    }
```

#### In Kotlin we use the when statement 

```kotlin

fun check(value: Int): Char {
    var result: Char = when (value) {
        in 0..4 -> 'a'
        5 -> 'b'
        6, 7, 8 -> 'c'
        9 -> 'd'
        in 10..20 -> 'e'
        else -> throw Error()
    }

    return result
}

```
the Kotlin variant is 100% more elegant in my opinion!


# 4. Compact functions

#### java
```java
// empty
```

#### kotlin

```kotlin

fun callUser() = println("I am calling the user...");

fun getMyFavNumber() = 12;

fun isCool() = true

```


# 5. Lambdas (like functions literals in other languages)


#### Kotlin

```kotlin

val myFavNumber: Int = 12;
val dividNumberByTwo = {myFavNumber: Int -> myFavNumber / 2} // --> 6

```

# 6. Classes

#### java
```java
public class User {

    private String mUserName;
    private String mPassword;
    private int mSalt;

    int stack;

    public int getStack() {
        return mSalt * 2 + 1;
    }

    public void setStack(int stack) {
        if (mPassword != null) {
            this.mSalt = stack / 2 + mPassword.length();
        }
    }
}


```

#### kotlin

```kotlin
 class User {
    
    private val mUserName: String = ""
    private val mPassword: String = ""
    private val mSalt:Int = 1
    
    val stack: Int
        get(): Int = mSalt * 2 + 1
        private set(value) {mSalt = value/2 + mPassword.length}
}
```

# 7. Singletons

#### java

in java we should provide our own implementation of a singleton object
like wrapping the property in a synchronized satatic method within the class

but in Kotlin we can easy replace the class keyword with `object`

#### Kotlin

```kotlin

object User {
    
    private val mUserName: String = ""
    private val mPassword: String = ""
    private val mSalt:Int = 1
    
    val stack: Int
        get(): Int = mSalt * 2 + 1
        private set(value) {mSalt = value/2 + mPassword.length}
}

asd
```

NB: there are sealed and enum classes too ! please check the official reference [here](https://kotlinlang.org/docs/reference/classes.html) 



# 8. Pairs and Triple

#### Java

```java
// empty
```

```kotlin
// Pairs
val car = "bmw" to "M3"
println(car) // (bmw, M3)

// or
val car = "bmw" to "M3" to "500hp"
println(car)
((bmw, M3), 500hp)

// class exmaple
class User(val firstname: String, val lastname: String, val age: Int) {

    fun getShortInfo(): Pair<String, String> {
        return (firstname to lastname)
    }

    fun getFullInfo(): Triple<String, String, Int> {
        return Triple(firstname, lastname, age)
    }
}

```


# 9. For Loop

#### java

```java
 for (int i = 0; i <= 10; i++) {
            System.out.println(i);
        }
        
```

```shell
0
1
2
3
4
5
6
7
8
9
10
```
 

#### Kotlin

```kotlin
for ( i  in 0..10 ){
    println(i)
}
// 012345678910
```


# 10. Labeled Breaks

#### Java

```java
for (int i = 0; i <= 10; i++) {
            System.out.println(i);
            for (int j = 0; j <= 10; j++) {
                if (i > 5) {
                    break;
                }
            }
        }
```

```kotlin
loop@ for (i in 0..10) {
        for (j in 0..10) {
            if (i > 5) {
                break@loop
            }
        }
    }
```

even more control over the for loops in kotlin - choose which for loop to break in your if statement

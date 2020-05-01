# Notes OCA
Some notes I made when preparing for the 1Z0‑808 (OCA8) Exam.

>>>>>>>>>Vragen:




class Test{
   public static void main(String[] args){
      int i = 4;
      int ia[][][] = new int[i][i = 3][i];
      System.out.println( ia.length + ", " + ia[0].length+", "+ ia[0][0].length);
   }
}



Can an object always be cast to a String? 
```String s = (String) someObject;  // Nope```

What will hapen if you throw ```   RuntimeException re = null; // It will throw a nullpointer exception when printing this (since the referenced object == null) ```


- Wat is de standaard print van een exception? (als je het hele object print?)
- Overload: change parameters(order) en eventueel return type
- Oefenen met parse en equalsmethoe enzo (of === of ==)
- Oefenen met continue en break en labels!
- Static blocks, heel raar > ``` static {INTERVAL = 10}``` ? dafuq

# Java Basics
- The order of keywords for a static import must be ```import static ...```.
- Which packages are automatically imported? ```java.lang``` && ```The package with no name ``` if no package is defined.
- First, static statements/blocks are called IN THE ORDER they are defined. Next, instance initializer statements/blocks are called IN THE ORDER they are defined. Finally, the constructor is called.
- You cannot access a private member of a superclass
- If you declare a field to be final, it must be explicitly initialized by the time the creation of an object of the class is complete. So you can either initialize it immediately. You can't change its value once it is set.
- Protected is not a valid way to encapsulate a field because any class in the package can access the field.
- ```private``` -> ```no modifier```-> ```protected``` -> ```public``` (no modifier is default and means the method will be accessible only to all the classes in the same package. (i.e. not even to the subclass if the subclass is in a different package.))
- ```TestClass t1, t2, t3, t4; t1 = t2 = new TestClass(); t3 = new TestClass();```
Answer >> two ```new```'s instances => two objects. t1, t2, t3, t4 => 4 references.
- Each object of a class has its own copy of each non-static member variable.

>First, static statements/blocks are called IN THE ORDER they are defined. Next, instance initializer statements/blocks are called IN THE ORDER they are defined. Finally, the constructor is called. So static > instance > constructor.
```

// What letters, and in what order, will be printed when the following program is compiled and run?

public class FinallyTest{
   public static void main(String args[]) throws Exception{
       try{
          m1();
          System.out.println("A");
       }
       finally{
          System.out.println("B");
       }
       System.out.println("C");
   }
   public static void m1() throws Exception { throw new Exception(); }
}

// It will print B and throw Exception!
```

# Inheritance

## Extends vs. Implements
Java allows a class to implement multiple interfaces. An interface is a "type" and does not contain any state. ```This implies that Java supports multiple type inheritance```.
A class contains state and extending a class means inheriting the state. Since Java does not allow a class to extend from multiple classes, it means that ```Java does not support multiple state inheritance```.
- A class can be extended unless it is declared final. 

## Polymorphism
Polymorphism makes code more ```reusable``` and more ```dynamic``` since it allows the actual decision of which method is to be invoked to be taken at runtame based on the actual object of the class
- Which variable or method to use:
>```Which variable (or static method) will be used depends on the class that the variable is declared of ```

(The extending class gets to use the variables of the ```extended``` class) (Having ambiguous fields does not cause any problems but referring to such fields in an ambiguous way will cause a compile time error).

>```Which instance method will be used depends on the actual class of the object that is referenced by the variable``` 

(So if a object is referenced as a Bear (by casting) the Bear-method will be used).

## Abstract
```Abstract class in java can't be instantiated```. An abstract class is mostly used to provide ```a base for subclasses``` to extend and ```implement the abstract methods``` and ```override or use the implemented methods``` in abstract class.

- If a method has been declared as abstract, it cannot provide an implementation (i.e. it cannot have a method body ) and ```the class containing that method must be declared abstract```). 
- An class can still be made abstract ```even if it has no abstract method(s)```.
- The class that will be extended ```can have has some methods (with implementation, which can be overriden)``` and abstract methods (without a body) which define a method that the inheriting childclass should implement.
- ```Return types must be the same when overriding an method (same name && same parameter == same return type)```

## Casting
Casting is the process of making a variable behave as a variable of another type. If a class shares an ```IS-A``` or ```inheritance relationship``` with another class or interface, their variables can be cast to each other’s type. Some of the casts will not show any error at compile time, but will fail at run time. 

Here are some basic rules to keep in mind when casting variables:
- Casting an object from a sub class to a super class doesn’t require an explicit cast (this is called upcasting but is implicitly done by the compiler (most of the time))
- Casting an object from a super class to a sub class requires an explicit cast.
- The compiler will not allow casts to unrelated types.

Even when the code compiles without issue, an exception may be thrown at run time if the object being cast is not actually an instance of that class. This will result in the run time exception ClassCastException.

> You can assign a subclass object reference to superclass ```(Animal animal = bear //of class Bear```) reference without a cast but to assign a super class object reference to a subclass (or interface) reference you need an explicit cast. 

>``` Bear Extends Animal```. Bear IS-A Animal. So it can be assigned to Animal animal.  The other way around: ``` Bear b = (B)animal ```. A animal is not necessarily a bear so it needs casting.

### Data Type Casting
- A char value can ALWAYS be assigned to an int variable, since the int type is wider than the char type. So casting ```char c``` to ```int i``` is valid.
- Sometimes we need to fit a value that is larger than the type used in the variable declaration. This may result in information loss since some bytes will have to be discarded.
In this case, we have to explicitly express that we are aware of the situation and we agree with that, by using a cast:
```
int myInt = (int) myDouble;
byte myByte = (byte) myInt;
```

## Overriding 
- Trying to override a static method with a non-static method (and vice-versa) in a class will result in a compilation error.
- The overriding method must have same return type in case of primitives (a subclass is allowed in case of classes)  (Therefore, the choices returning int are not valid.) and the parameter list must be the same (The name of the parameter does not matter, just the Type is important).
- When extending a class, keep in mind that overridden methods must have the same return type as the overridden method
- An interface can redeclare a default method and also make it abstract or provide a different implementation
- If you make a method static, that method cannot be overridden because the concept of overriding (and polymorphism) only applies to instance method.
The overriding method can throw a subset of the exception or subclass of the exceptions thrown by the overridden class. Having no throws clause is also valid since an empty set is a valid subset. 
- An overriding method can be made less restrictive than the overridden method. (kinda like the other way around with exceptions, the must be narrower)

> Always remember: Instance methods are overridden and variables (and static methods) are hidden. Which instance method is invoked depends on the class of the actual object, while which field (and static method) is accessed depends on the class of the variable. 
```
class Animal {
    public int h = 4;

    public int getH() {
        System.out.println("id0: Animal " + h);
        return h;
    }
}

 class Bear extends Animal {
    public int h = 44;

    public static void main(String[] args) {
        Animal b = new Bear();
        System.out.println("id1: " + b.h + " " + b.getH());   // first it will evaluate the method and return Bear 44, than it will return the Animal.h which is 4 + the result of the method b.GetH() which is 44.
        Bear bb = (Bear) b;
        System.out.println("id2: " + bb.h + " " + bb.getH()); // first it will evaluate the method and return Bear 44, than it will return Bear.h which is 44 + the result of the method b.GetH() which is 44
    }

    public int getH() {
        System.out.println("id3: Bear " + h);
        return h;
    }
}

// Result:
id3: Bear 44
id1: 4 44
id3: Bear 44
id2: 44 44
```

```
class Automobile{
    public void drive() {  System.out.println("Automobile: drive");   }
}
class Truck extends Automobile {
    public void drive() {  System.out.println("Truck: drive");   }

    public static void main (String args [ ]){
        Automobile a = new Automobile();
        Truck t  = new Truck();
        a.drive();      //1 > Automobile: drive
        t.drive();      //2 > Truck: drive

        a = t;          //3 > no problem since a Truck is an Automobile
//      t = a;          //4 > won't compile an automobile is not necessarily a truck
        t = (Truck) a;  //5 > compiles after casting // will print Truck drive

        a.drive();      //6 > Truck: drive
        t.drive();      //7 > Truck: drive
    }
}
```

## Overloading & widening vs. boxing/unboxing
- Overloading of a method occurs when the name of more than one methods is exactly same but the parameter lists are different (or in a different order).
- A method is said to be overloaded when the other method's name is same and parameters ( either the number or their order) are different.
- The call to ```printSum(1, 2)``` will be bound to printSum(```int, int```) because 1 and 2 are ints, which are exact match to int, int.  Note that if printSum(```int, int```) method were not there in the code, printSum(```double, double```) would have been invoked instead of printSum(```Integer, Integer```) because ```widening is preferred over boxing/unboxing```.
- The call to printSum(```1.0, 2.0```) will be bound to printSum(```double, double```) because 1.0 and 2.0 are double, which are exact match to double, double.  Note that if you call ```printSum(1, 2)``` , printSum(```float, float```) would have been invoked instead of printSum(```double, double```) because a float is closer than a double to an int. 

```
class Base{
   public short getValue(){ return 1; } //1
}
class Base2 extends Base{
   public byte getValue(){ return 2; } //2
}
public class TestClass{
   public static void main(String[] args){
      Base b = new Base2();
      System.out.println(b.getValue()); //3
   }
} 
// Compile time error at 2 (because::: )
```

# Interfaces
Interface in java is contract of class. This contract has to obeyed by class which implements this interface.
- Interfaces are implemented like so: ```public class SomeWrestler implements IWrestler ```
- Interface is group of related methods that should have been implemented by the class which claims that i’m provided common behavior of that interface.
- By using interface implementation developer is always sure about the class implemented all methods of interface so he/she can safely call all methods defined in interface.
- When you mark a method in an interface as default, you are basically trying to provide a default implementation of that method so that any class that implements this interface doesn't necessarily have to provide its own implementation. Thus, a default method without a method body doesn't make sense.

```
public interface ITestInterface {
        default void compute1();                        // Extension method should have body
        public void compute2();                         // GOOD
        static void compute3(){ sout("Hi");}            // GOOD
        static void compute4();                         // Static methods in interfaces should have a body
        default static void compute5 (){Sout("Hi");}    //Illegal combination of modifiers: 'static' and 'default
}
```

## Interface method signatures
- All interface methods have to be ```public```. They need to be visible because ```they need to be overriden```.
- The method body is not defined, just the name and the parameters. ```public void doIt();```
- An interface can have a static method but the method must have a body in that case.

>Fields defined in an interface are ALWAYS considered as public, static, and final. Even if you don't explicitly define them as such. In fact, you cannot even declare a field to be private or protected in an interface.


# Arrays
```
public class TestClass{
   public static void main(String args[] ){
      int i = 0 ;
      int[] iA = {10, 20} ;
      iA[i] = i = 30 ;
      System.out.println(""+ iA[ 0 ] + " " + iA[ 1 ] + "  "+i) ;
    }
}
// Result 30 20  30 (it will first try to find the location in the array before it continues to evaluate the value that will be assigned)
```


# Methods & Constructors

## Basics
- Constructors cannot have empty bodyies (i.e. they cannot be abstract).
- You may apply ```public```, ```private```, and ```protected``` modifiers to a constructor. But not ```static```, ```final```, ```synchronized```, ```native``` and ```abstract```. It can ```also be package private i.e. without any access modifier```.
- ```protected``` is less restrictive than package access. So a method(or field) declared as protected ```will be accessible from a subclass even if the subclass is not in the same package```.
- You cannot have two methods with the same signature (name and parameter types) in one class. Also, even if you put one sayHello() method in other class which is a subclass of this class, it won't compile because you cannot override/hide a static method with a non static method and vice versa.
- An invalid constructor will cause an ```runtime-exception```.
- You can ```never``` use a ```this```-reference in a static method.


## Lambdas
- It is an interface that has only one abstract method (among other non-abstract methods) with the signature - ```public boolean test(T t)```;
- ```java.util.function.Predicate``` is one of the several functional interfaces that have been added to Java 8. 
-This interface has exactly one abstract method named test, which takes any object as input and returns a boolean. This comes in very handy when you have a collection of objects and you want to go through each object of that collection and see if that object satisfies some criteria. 

```
//The following code fragments illustrate a lambda-function: 

public void filterEmployees(ArrayList<Employee> dataList, Predicate<Employee> p){
    Iterator<Employee> i = dataList.iterator();    
    while(i.hasNext()){         
        if(p.test(i.next())){              
            i.remove();     
        }    
    } 
}  

// Instead of defining a MyPredicate class (like we did with MyCheckEmployee), we could also define and instantiate an anonymous inner class to reduce code clutter 

Predicate<Employee> p = new Predicate<Employee>(){   
    public boolean test(Employee e){      
        return e.getSalary()>100000;   
    } 
};
```
- If the method of a functional interface takes one parameter, you can omit the brackets. For example, ```x -> expression``` and ```(x) -> expression are equivalent```.  If the method of a functional interface takes no parameter, you must write empty brackets. For example, ```( ) -> expression```
- If you're replacing a method that does not take any parameters, the parameter list part of the lambda expression must be (). 
``` () -> System.out.println("running...")```
- The following is ok as well when the method returns a void;
```() -> { System.out.println("running..."); return; }```



## Loops
Play around: https://www.codecademy.com/courses/learn-java/lessons/learn-java-loops/exercises/loops-review

### While
while loops: These are useful to repeat a code block an unknown number of times until some condition is met.

Like an if statement, the code inside the while loop will only run if the ```condition is true```. However, a ```while``` loop will ```continue running``` the code over and over until the condition evaluates to ```false```.
```
while (silliness > 10) {

  // code to run

}
```
> The condition expression in a while header is required.

### Do while
The difference between do-while and while is that do-while evaluates its expression at the bottom of the loop instead of the top. Therefore, the statements within the do block are always executed at least once.


### For Loops
for loops: These are ideal for when you are incrementing or decrementing with a counter-variable.
```
// Some examples of 'good' syntax regarding some loops:

for (i=0 ;       ; i++)                                 // Good
for (int i=5; i=0; i--) { };                            // Wrong
int j=5; for(int i=0, j+=5;  i<j ; i++) {  j--;  };     // Wrong
int i, j; for (j=10; i<j; j--) { i += 2; };             // Wrong
int i=10; for ( ; i>0 ; i--) { };                       // Good
for (int i=0, j=10; i<j; i++, --j) {;};                 // Good
```
> When the expression/condition part is empty, it is interpreted as true.

### Enhanced for loops
- It can iterate over an array or a Collection but not a Map.
- Using an enhanced for loop prevents the code from going into an infinite loop.
- You cannot find out the number of the current iteration while iterating.

### For Each
For-each loops: These make it simple to do something with each item in a list.

### Break & Continue
- The ```break``` statement immediately jumps ```to the end (and out)``` of the appropriate compound statement.
- The ```continue``` statement immediately jumps ```to the next iteration``` (if any) of the appropriate loop.

- ```while (false) { x=3; }``` is a compile-time error because the statement x=3; is not reachable;
= ```if(false){ x=3; }``` this is not a a compile-time error because this is allowed in an ```if-statement```

```
// Another example of a loop that will not compile (due to unreachable code):

if(index == 3){                 
        break;             
    } else {                  
        continue;             
    }
    // This code will not be reached
``` 
### Moment of incrementing in Loops
```
// Example of pre- and post increments: 

    void thisWillRunOnce() { 
        System.out.println("running method thisWillRunOnce()");
        int i = 0;
        for (; ++i < 1; ) {
            System.out.println("This will be skipped: "+ i); // this code will not be reached
        }
        System.out.println(i); //this will return 1
    }
    // 1 will be printed

    void thisWillRunTwice() {
        System.out.println("running method thisWillRunTwice()");
        int i = 0;
        for (; i++ < 1; ) { //The while condition uses post increment operator, which means count is first compared with 1 (and based on this comparison a decision is made whether to execute the loop again or not) and then incremented.
            System.out.println("from within the for loop: " + i); //this wil return 1
        }
        System.out.println(i); //this will return 2
    }
    // 1 & 2 will be printend
}
```

## Equals
```
Integer i;
Long l;
i == long // will fail to compile since comparing these to using ```==````is useless.
```
- Equals method of a primitive wrapper class ( e.g. java.lang.Integer, Double, Float etc) are 

The equals method of a primite wrapper class has the following specifications:
- symmetric => a.equals(b) returns same as b.equals(a) 
- transitive => if a.equals(b) and b.equals(c) return true, then a.equals(c) returns true. 
- reflexive => a.equals(a) return true.  For example, the following code for the equals method on Integer explains how it works: 

## Instanceof
>Eeasywin: For any non-null reference o1, the expression (o1 instanceof Object) will always yield true.
```
public boolean equals(Object obj) {    
    if (obj instanceof Integer) {        
        return value == ((Integer)obj).intValue();    
        }    
        return false; 
} 
```
- The left operand of instanceof MUST be a reference variable and not a primitive. ```This means that when an reference that extends nothing will be used in an instanceOf, the code will fail to compile!```
- D extends C, which extends B, which extends A. This means, D is-a C, C is-a B, and B is-a A. Therefore, D is-a A. Hence, d instanceof A will return true.
- The expression (o instanceof B) will return true if the object referred to by o is of type B or a subtype of B. (subtype == extending B of some class that extends B or a class that extends a class that extends a class that extends B ;))
```
class Animal {}   
class Dog extends Animal { }   
Dog d = new Dog();
System.out.println(d instanceof Animal) //True
```
Now, d instanceof Animal will be true because even though d is actually an instance of Dog, since Dog is a subclass of Animal, Dog IS-A Animal.
- Since A implements both T1 and T2, 1 and 2 are correct. (a instanceof T1 will be true)
- ```(s instanceof java.util.Date) ``` will not compile.... so the instanceof-operator checks if a check is useful/possible.
- ```b points to an object of class Bat, which does not extend from Bird```. Now, it is possible for b to point to an object of any subclass of Bat. However, it is not possible for that sub class to extend Bird (because a class can at most extend from only one class). ```Therefore, it is not possible for b to point to an object of a class that "is a" Bird.``` The compiler figures out this fact at compile time itself and so the code fails to compile.

```interface Flyer{ }
class Bird implements Flyer { }
class Eagle extends Bird { }
class Bat { }

public class TestClass {
    
    public static void main(String[] args) {
        Flyer f = new Eagle();
        Eagle e = new Eagle();
        Bat b = new Bat();

// At run time, f points to an object of class Eagle. Now, Eagle extends Bird so f instanceof Bird returns true. e points to an object of class Eagle. Eagle extends Bird, which in turn implements Flyer. So an Eagle is a Flyer. Therefore, e instanceof Flyer will also return true.  b points to an object of class Bat, which does not extend from Bird. Therefore, b instanceof Flyer returns false.        
```

## Java Data types
Data types are divided into two groups:

> Primitive data types - includes byte, short, int, long, float, double, boolean and char

> Non-primitive data types - such as String, Arrays and Classes (you will learn more about these in a later chapter)

### Float
```
    float f1 = 1.0;     //DOES NOT COMPILE
    float f2 = 43e1;    //DOES NOT COMPILE
    float f3 = -1;
    float f4 = 0x0123;
    float f5 = 4;
```

### Parsing Java Data types

Boolean class has two static helper methods for creating booleans - ```parseBoolean``` and ```valueOf```. Boolean.parseBoolean(String ) method returns a primitive boolean and not a Boolean object (Note - Same is with the case with other parseXXX methods such as Integer.parseInt - they return primitives and not objects) 

The boolean returned represents the value true if the string argument is not null and is equal, ignoring case, to the string "true".  ```Boolean.valueOf("String")``` and its ```overloaded Boolean.valueOf(boolean)``` version, on the other hand, work similarly but return a reference to either Boolean.TRUE or Boolean.FALSE wrapper objects. 
Observe that they dont create a new Boolean object but just return the static constants TRUE or FALSE defined in Boolean class.  3. When you use the equality operator ( == ) with booleans, if exactly one of the operands is a Boolean wrapper, it is first unboxed into a boolean primitive and then the two are compared 

If both are Boolean wrappers, then their references are compared just like in the case of other objects. 
>```new Boolean("true") == new Boolean("true")``` is false, but ```new Boolean("true") == Boolean.parseBoolean("true")``` is true.

> Long (or any wrapper class) does not have a no-args constructor, so new Long() is invalid.

> The equals methods of all wrapper classes first check if the two object are of same class or not.

 ```
Boolean.valueOf(true); // true 
Boolean.valueOf("trUE"); // true
Boolean.TRUE // true

Boolean.parseboolean("true"); // will create a primitive-boolean. Not an wrapper-boolean.
Boolean.parseBoolean("value"); // this method does not like spaces, but doesn't give shit about strange capitalized letters like "trUE" 
```


## Assignment
These operators are used to assign values to a variable. The left side operand of the assignment operator is a variable and the right side operand of the assignment operator is a value. The value on the right side must be of the same data-type of the operand on the left side otherwise the compiler will raise an error. This means that the assignment operators have right to left associativity, i.e value given on the right-hand side of the operator is assigned to the variable on the left and therefore right-hand side value must be declared before using it or should be a constant.
```
boolean b1 = false; boolean b2  = false; if (b2 = b1 != b2){ //true
int expr1 = 3 + 5 * 9 - 7;  //41       
int expr2 = 3 + (5 * 9) - 7;  //41       
int expr3 = 3 + 5 * (9 - 7);  13         
int expr4 = (3 + 5) * 9 - 7;  //65
System.out.println(100/9.9); //Since one of the operands (9.9) is a double, it wil perform a real division and will print 10.1010101010101
```
- If evaluation of the left-hand operand of a binary operator completes abruptly, no part of the right-hand operand appears to have been evaluated.

## Switches

The switch statement is a multi-way branch statement. It provides an easy way to dispatch execution to different parts of code based on the value of the expression. Basically, the expression can be byte, short, char, and int primitive data types. Beginning with JDK7, it also works with enumerated types ( Enums in java), the String class and Wrapper classes.

Here are the rules for a switch statement:
1. Only ```String```, ```byte```, ```char```, ```short```, ```int```, (and their wrapper classes ```Byte```, ```Character```, ```Short```, and ```Integer```), and ```enums``` can be used as types of a switch variable. (String is allowed only since Java 7). 
2. The case constants must be assignable to the switch variable. For example, if your switch variable is of class String, your case labels must use Strings as well.
3. The switch variable must be big enough to hold all the case constants. For example, if the switch variable is of type char, then none of the case constants can be greater than 65535 because a char's range is from 0 to 65535.
4. All case labels should be COMPILE TIME CONSTANTS.
5. No two of the case constant expressions associated with a switch statement may have the same value.
6. At most one default label may be associated with the same switch statement.
7. The type of the case labels must be consistent with the type of the switch condition.


## Exceptions
An exception is an unwanted or unexpected event, which occurs during the execution of a program i.e at run time, that disrupts the normal flow of the program’s instructions.


### Error vs Exception
Error: An Error indicates serious problem that a reasonable application should not try to catch.
Exception: Exception indicates conditions that a reasonable application might try to catch.



- Any exception thrown in a **static block** is wrapped into **ExceptionInInitializerError**.
- Exceptions are always some subclass of **java.lang.Exception**        
- Catch blocks are **not required**
- An exception that is never caught will cause your application to stop
- Throwable > Exception && Error
- The most specific catch-clause must be at the top, otherwise it will be unreachable code (since a broader Exception will trigger) and thus will not compile.
- The exceptions that a method can throw must be declared > void myFunction() throws MyException, MyException2 { //method body} A method that 'receives' an Exception must either catch in or rethrow it (and it this case declare in in the method signature)
- The rule is that an overriding method cannot throw an exception that is a super class of the exception thrown by the overridden method (which meens the exception thown in the the method that is overriding must be the same or narrower. Throwing less exceptions is also possible (eg. leaving them out of the method signature)).
- Finally statements are ALWAYS executed, whether an exception was thrown or not (after the return statement, before the return executes)
- You do not need to declare catch-clauses for RuntimeExceptions like ArrayIndexOutOfBounds(or method signatures)
- When a extended class has a method with a throws Exception the method/class that uses this method should also have this exception-signature. (in for example the main method) 
Game.play throws exception > Game g = new Soccer g.play >>>>> this needs to be called in a method that has the same exception-signature
- When you use System.out.println(exception), a stack trace is not printed. Just the name of the exception class and the message is printed. 
When you use exception.printStackTrace(), a complete chain of the names of the methods called, along with the line numbers, is printed.
- Overriding method only needs to specify a subset of the list of exception classes the overridden method can throw. A set of no classes is a valid subset of that list.
- If an exception is not handled(catched or declared) it will print the stack trace to the console.
- The main(String[] args) method is the last point in your program where any unhandled checked exception can bubble up to. After that the exception is thrown to the JVM and the JVM kills the thread.
- throw new NullPointerException(); < This is possible (although it looks strange..)
- java.lang.SecurityException is a standard Exception (who knew..)
- If there is no catch block, the exception will not be handled and the invoking method will throw the exception to the caller.
- A method that throws a 'checked' exception i.e. an exception that is not a subclass of Error or RuntimeException, either must declare it in throws clause or put the code that throws the exception in a try/catch block.
- Once the exception is caught the rest of the catch blocks at the same level (that is the ones associated with the same try block) are ignored
- ```a[thisWillThrowAnException()][i = 1]++;``` < If evaluation of a dimension expression completes abruptly, no part of any dimension expression to its right will appear to have been evaluated. [i = 1 will not be executed]



## Imports
- A package statement can never have a .*
- The order of keywords for a static import must be "import static ... ".
- you cannot import a package statically. You can only import static members of a class statically. When you use X.LOGICID for example, the import will need to be like this: ```import static com.foo.X.*;```.


## Garbage collection

- If an objects get returned in a method it will never be a candidate for Garbage collection within this method.





## Java API
- ```None of the new date related classes have public constructors```. So using **new** to create their instances would be invalid.
- The String class has no reverse( ) method but StringBuffer (and StringBuilder) do have this method.
>```So..ln(LocalDate.of(2015, Month.JANUARY, 01).format(DateTimeFormatter.ISO_DATE_TIME));```  // comp. error (no time-component)

>```final public static void main(String [ ] array)```   // works

>```public static void main(String args[ ]) // works```

>```static void main(String args[ ])``` // does not work since it is missing the required public

>```public static long main(String[] args){``` // this will give an error at Runtime, not compile time..

>```LocalDate ld2 = ld.plus(Period.of(0, 1, 1));``` // this will work! 

## Arrays
- The statement ```int[ ][4]``` will not compile, because the dimensions must be created from left to right.
- Size of the array is NEVER specified on the Left Hand Side.
- Arrays cannot grow in size once created. ArrayLists can do that.
- In an array access, the expression to the left of the brackets appears to be fully evaluated before any part of the expression within the brackets is evaluated.
- Arrays are proper objects (i.e. iArr instanceof Object returns true) and Object references are passed by value (so effectively, it seems as though objects are being passed by reference). So the value of reference of iArr is passed to the method incr(int[] i); This method changes the actual value of the int element at 0.

## Stringbuilder
```
    String s = "blooper";     
    StringBuilder sb = new StringBuilder(s);     
    sb.append(s.substring(4)).delete(3, 5);     
    System.out.println(sb); Result >> Bloerper
```
## Operators
- Multiplication has more precedence than addition. 
- we have a simple for loop whe have a incrementer. This will only be 'exececuted' when the condition in the for loop is true.
- The if-else-else is invalid. It should be if , else if, else.

## Some random examples of cruelty :angry:
Keep in mind to always check the number of answer that should be provided.... ;)

- I've seen double else blocks (without else if (condition)..)
- Note that both equals() and hashCode() methods can be overridden by the programmer so you can't say anything about what they will return without looking at the code.
- A class can have a method named Main. Although, since it is not same as main, it will not be considered the standard main method that the JVM can invoke when the program is executed.
- ```LocalDate ld2 = ld.plus(Period.of(0, 1, 1));```
- ```final public static void main(String [ ] array)```
- When you see something about packages remember the following: Note that there is no modifier for A's constructor. So it has default access. (default == package only). This will most likely be an compile error
- It will throw a java.lang.OutOfMemoryError. Note that this is not a subclass of RuntimeException or even Exception. It is a subclass of java.lang.Error. (so no exception is caught)
- Note that local (aka automatic) variables, such as the variables d and e in the code given here, are not initialized automatically. They have to be initialized explicitly. However, it is ok to leave them uninitialized if you don't use them anywhere in the code (as is the case with the variable d). 
- There no unsigned keyword in java! A char can be used as an unsigned integer. < well hidden in a question
- ```float f = 0x0123;``` is valid because god knows why (implicit narrowing..)
- Variables can't be declared as abstract or native.

*add some more examples: http://www.programmergirl.com/oca-java-8-preparation-java-basics/ ?

## Some notes I found as Youtube-comments ;)
- You want to have general understanding about JVM, and what it is, your knowledge of classes, inheritance and interfaces has to be top notch
   - For example, if you have a method in a class that is abstract but your class is not abstract, guess what compiler error! Even if you know this it is easy to miss on the exam.
- They like to put tricks with strings like he said, like string.'methodname(arg0) you MUST assign it back to have it actually mean something
- Another trick with date classes, ```LocalDate date = LocalDate.now()```, your variable must be created statically, ```LocalDate date = new LocalDate()``` DOES NOT COMPILE!
- Touch on period also, ```Period p = Period.ofWeek(1).ofDays(1)``` this will mean a period of 1 day not 8 days... only the last one counts
- Make sure code compiles, they love to stump you with something simple like putting String as string in lower case which does not compile.
- Autoboxing, know the valueOf and parseInt methods, and their return type for Integer wrapper class, parseInt returns primitive, whereas valueOf returns wrapper
- Know the ```Arrays.sort(array)``` for the binary search, there will be 1 or 2 questions about that
- ArrayList knowledge must be top notch
- Know the hierarcy of exceptions, The top level is throwable, Error and Exception inherit from throwable, Error should not be caught, Exception is checked, Runtime exception which inherits from Exception is unchecked. 
- Know try catch, and scope, order matters for catch statements. They also like to confuse you by questions where they may imply that finally is required in a try block but only 0 or more catch blocks and /or at most 1 finally block is allowed, You need either atleast one catch block defined or a finally available. If they do something like System.exit(0) in catch block then finally is NOT executed. Also know that ClassCastException is a runtime error, this is when you try to cast your class to another type that is not related to your class, Example, you can cast an Integer to Number, but casting integer to String is going to throw this exception.
- Get a good grip on ternary operator.
- Get a good grip on increment and decrement. for example ```if int i = 1, if i do i = i++;``` i will end up being set as 1. this is another trick. i++ on the other hand will change i to 2.
- you want to have a good handle on loops as well. They LOVE to put loops without curly brackets just to confuse you, it's really annoying and i hate them for doing that.
- You also want to know pass by value and pass by reference, for example, if i pass an array of int to another method and then do something like ```myArray[0] = 5```, guess what, i just changed the contents of myArray for the calling method, this is because even though a copy of the array is passed in, they both have the same reference, if the method which has the array passed into renewed the reference then yes the earlier statement no longer applies.
- Know order of initialization, know your modifiers, know about static, final and all the other important keywords. Know the static block. 
- Know that local variables MUST always be initialized before being used, class variables and member variables DO NOT have to be initialized, they are initialized to a default value for primitives it is a value, for objects it is null. however if you have the final keyword in front then you must initialize them before you can use them
- Polymorphism they love putting these all over the practise exams, you'll have to understand it well
- He talked about autompromoting of primitives during arithmetic operations, very important concept
- Another trick here - ```System.out.println (1 + "2" + 3)``` outputs 123, ```System.out.println(1 + 2 + 3 + " ")``` will give you '6 ', always read from left to right while figuring out the final value
-one really annoying thing i noticed. Sometimes they will do something like Int l = myStringArray.length(); then do something like system.out.println(myStringArray[l]. Something really stupid i did was (and my brain was tired) the print statement is on line 2, and the letter 'L" lower case looks awfully like a 1, got it wrong on the practise test :)
- Also please please please remember, that if you have an array you do myArr.length to get length, if you have string you do ```myString.length()``` and if u have list you do ```myList.size()```, they love to confuse you with these ones those buggers
- know the idfference between private, protected and package private really really well...
- you also have to know what a virtual function / method is in java, it is any method that is not static and not marked with the keyword final. They have to be overrideable.
- Know overloading really well, this one can be tricky too (i'm still getting caught up in some of the tricks)
- know what covariance is in java. For example if you are overloading a method from a parent class, the return type or exection thrown can have a narrower scope, not a broader scope. so if i'm returning Number in the parent class, I am allowed to return Long or Integer wrapper class in child class. Same with exception, if i'm throwing exception in parent class, i can throw runtimeexception for example in child class (or remove the exception declaration alltogether)
I'm just going to stop here, if you are someone who is new to the whole certification thing, you can see that there is a lot to learn. I would recommend taking your time and not rushing into the exam. buy the practise exam on udemy it has 4 practise tests.... sorry for the very long comment but i hope this helps someone out there. if you read this far, i commend you, please reply back if you appreciated it or have something to add to this list! (there is a lot that can be added)


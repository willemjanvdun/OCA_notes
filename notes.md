# Notes OCA
feel free to add notes via a Pull Request

## Java Basics
- Java allows a class to implement multiple interfaces. In this way, Java supports multiple inheritance of types. 
"State", on the other hand, is represented by instance fields. Only a class can have instance fields and therefore, only a class can have a state. (Fields defined in an interface are always implicitly static, even if you don't specify the keyword static explicitly. Therefore, an interface does not have any state.)
- Polymorphism makes code more reusable
- Polymorphism makes the code more dynamic since it allows the actual decision of which method is to be invoked to be taken at runtame based on the actual object of the class
- First, static statements/blocks are called IN THE ORDER they are defined. Next, instance initializer statements/blocks are called IN THE ORDER they are defined. Finally, the constructor is called. So, it prints a b c 2 3 4 1.
- A constructor cannot be final, static or abstract.
- Overloading of a method occurs when the name of more than one methods is exactly same but the parameter lists are different.
- A method is said to be overloaded when the other method's name is same and parameters ( either the number or their order) are different.
- You cannot access a private member of a superclass
- If you declare a field to be final, it must be explicitly initialized by the time the creation of an object of the class is complete. So you can either initialize it immediately. You can't change its value once it is set.
- Protected is not a valid way to encapsulate a field because any class in a package can access the field.

## Casting
- A char value can ALWAYS be assigned to an int variable, since the int type is wider than the char type. So casting ```char c``` to ```int i``` is valid.
- Sometimes we need to fit a value that is larger than the type used in the variable declaration. This may result in information loss since some bytes will have to be discarded.
In this case, we have to explicitly express that we are aware of the situation and we agree with that, by using a cast:
```
int myInt = (int) myDouble;
byte myByte = (byte) myInt;
```
- If Class B(ear) extends Class A(nimal), the Bear can always be A (without casting). An Animal is not always a bear so it needs casting ```Bear b = (Bear)a;```

- Casting from a subclass to a superclass is called upcasting. Typically, the upcasting is implicitly performed by the compiler.

## Inheritance
- A class can be extended unless it is declared final. 
- Some notes about abstract
    - A class is uninstantiable if the class is declared abstract. If a method has been declared as abstract, it cannot provide an implementation (i.e. it cannot have a method body ) and the class containing that method must be declared abstract). 
    - If a method is not declared abstract, it must provide a method body (the class can be abstract but not necessarily so).
    - If any method in a class is declared abstract, then the whole class must be declared abstract. 
    - An class can still be made abstract even if it has no abstract method.
    - An abstract method cannot have a body.
- Return times must be the same when overriding an method (same name && same parameter == same return type)
! You can assign a subclass object reference to superclass reference without a cast but to assign a super class object reference to a subclass (or interface) reference you need an explicit cast.
- All interface methods have to be public.
- An interface can have a static method but the method must have a body in that case.
- Which to use:
-   Which variable (or static method) will be used depends on the class that the variable is declared of.
-   Which instance method will be used depends on the actual class of the object that is referenced by the variable.
- The rule is that an overriding method cannot throw an exception that is a super class of the exception thrown by the overridden method.\


Example: 
```
interface I{
}
class A implements I{
}
class B extends A {
}
class C extends B{
}
And the following declarations:
A a = new A();
B b = new B();
```
class B does implement I because it extends A, which implements I. A reference of type I can be cast to any class at compile time. Since B is-a A, it can be assigned to a.

## Extended classes
- The class that will be extended has some methods (with implementatin, which can be overriden) and even abstract methods (without a body) which define a method that the inheriting childclass should implement.

## Interfaces
- Contract : Interface in java is contract of class. This contract has to obeyed by class which implements this interface.
- Interface is group of related methods that should have been implemented by the class which claims that i’m provided common behavior of that interface
- By using interface implementation developer is always sure about the class implemented all methods of interface so he/she can safely call all methods defined in interface.
- In an interface, the method body is not defined, just the name and the parameters.
- Fields defined in an interface are ALWAYS considered as public, static, and final. Even if you don't explicitly define them as such. In fact, you cannot even declare a field to be private or protected in an interface. Therefore, you cannot assign any value to a variable from an interface outside the interface definition (overriding it is not possible).

## Lambdas
- java.util.function.Predicate is one of the several functional interfaces that have been added to Java 8. This interface has exactly one abstract method named test, which takes any object as input and returns a boolean. This comes in very handy when you have a collection of objects and you want to go through each object of that collection and see if that object satisfies some criteria. For example, you may have a collection of Employee objects and, in one place of your application, you want to remove all such employees whose age is below 50, while in other place, you want to remove all such employees whose salary is above 100,000. In both the cases, you want to go through your collection of employees, and check each Employee object to determine if it fits the criteria. This can be implemented by writing an interface named CheckEmployee and having a method check(Employee ) which would return true if the passed object satisfies the criteria. The following code fragments illustrate how it can be done - 
- Whenever the method of a functional interface takes more than one parameter, you need to put the arguments within brackets.
- If the method of a functional interface takes one parameter, you can omit the brackets. For example, ```x -> expression``` and ```(x) -> expression are equivalent```.  If the method of a functional interface takes no parameter, you must write empty brackets. For example, ```( ) -> expression```
```
public void filterEmployees(ArrayList<Employee> dataList, Predicate<Employee> p){
    Iterator<Employee> i = dataList.iterator();    
    while(i.hasNext()){         
        if(p.test(i.next())){              
            i.remove();     
        }    
    } 
}  
...  
// Instead of defining a MyPredicate class (like we did with MyCheckEmployee), we could also define and instantiate an anonymous inner class to reduce code clutter 
Predicate<Employee> p = new Predicate<Employee>(){   
    public boolean test(Employee e){      
        return e.getSalary()>100000;   
    } 
};
```


- If you're replacing a method that does not take any parameters, the parameter list part of the lambda expression must be (). 
``` () -> System.out.println("running...")```
- The following is ok as well when the method returns a void (but ugly IMHO)
```() -> { System.out.println("running..."); return; }```

## Overriding
- When the return type of the overridden method (i.e. the method in the base/super class) is a primitive, the return type of the overriding method (i.e. the method in the sub class) must match the return type of the overridden method.
- Trying to override a static method with a non-static method (and vice-versa) in a class will result in a compilation error.
- When extending a class, keep in mind that overridden methods must have the same return type as the overridden method
- An interface can redeclare a default method and also make it abstract or provide a different implementation
- If you make a method static, that method cannot be overridden because the concept of overriding (and polymorphism) only applies to instance method.
- The overriding method must have same return type in case of primitives (a subclass is allowed in case of classes)  (Therefore, the choices returning int are not valid.) and the parameter list must be the same (The name of the parameter does not matter, just the Type is important). 
- The overriding method can throw a subset of the exception or subclass of the exceptions thrown by the overridden class. Having no throws clause is also valid since an empty set is a valid subset. 
- An overriding method can be made less restrictive than the overridden method. (kinda like the other way around with exceptions, the must be narrower)
- When you mark a method in an interface as default, you are basically trying to provide a default implementation of that method so that any class that implements this interface doesn't necessarily have to provide its own implementation. Thus, a default method without a method body doesn't make sense.

```
class Automobile{
   public void drive() {  System.out.println("Automobile: drive");   }
}
 public class Truck extends Automobile{
   public void drive() {  System.out.println("Truck: drive");   }
   public static void main (String args [ ]){
      Automobile  a = new Automobile();
      Truck t  = new Truck();
      a.drive(); //1 > Automobile: drive
      t.drive(); //2 > Truck: drive
      a = t;     //3 
      t = a;     //4
      a.drive(); //5 > Truck: drive
      t.drive(); //6 > Truck: drive
   }
}
```

## Loops
- The break statement immediately jumps to the end (and out) of the appropriate compound statement.
- The continue statement immediately jumps to the next iteration (if any) of the appropriate loop.
```
for (int i=5; i=0; i--) { }; //Wrong
int j=5; for(int i=0, j+=5;  i<j ; i++) {  j--;  }; //Wrong
int i, j; for (j=10; i<j; j--) { i += 2; }; //Wrong
int i=10; for ( ; i>0 ; i--) { }; //Good
for (int i=0, j=10; i<j; i++, --j) {;}; // Good
```
- A nice example of pre-post-increments
``` 
public class PrePostIncrement {
    public static void main(String[] args) {
         thisWillRunOnce();
        thisWillRunTwice();
    }

    static void thisWillRunOnce() { // 1 will be printed
        System.out.println("running method thisWillRunOnce()");
        int i = 0;
        for (; ++i < 1; ) {
            System.out.println("this code will not be reached: "+ i); // this code will not be reached
        }
        System.out.println(i); //this will return 1
    }

    static void thisWillRunTwice() { // 1 & 2 will be printend
        System.out.println("running method thisWillRunTwice()");
        int i = 0;
        for (; i++ < 1; ) { //The while condition uses post increment operator, which means count is first compared with 1 (and based on this comparison a decision is made whether to execute the loop again or not) and then incremented.
            System.out.println("from within the for loop: " + i); //this wil return 1
        }
        System.out.println(i); //this will return 2
    }

}
```

## Java Data types
```TestClass t1, t2, t3, t4; t1 = t2 = new TestClass(); t3 = new TestClass();```
Answer >> two ```new```'s instances => two objects. t1, t2, t3, t4 => 4 references.

```
Integer i = new Integer(42); Long ln = new Long(42); Double d = new Double(42.0);
i == ln; will fail at compile time since the can never be == since the refer to different data types.
// .equals will compile without problems.
``` 

- Equals method of a primitive wrapper class ( e.g. java.lang.Integer, Double, Float etc) are 
1. symmetric => a.equals(b) returns same as b.equals(a) 
2. transitive => if a.equals(b) and b.equals(c) return true, then a.equals(c) returns true. 
3. reflexive => a.equals(a) return true.  For example, the following code for the equals method on Integer explains how it works: 
```
public boolean equals(Object obj) {    
    if (obj instanceof Integer) {        
        return value == ((Integer)obj).intValue();    
        }    
        return false; 
} 
```
- Boolean class has two static helper methods for creating booleans - parseBoolean and valueOf. Boolean.parseBoolean(String ) method returns a primitive boolean and not a Boolean object (Note - Same is with the case with other parseXXX methods such as Integer.parseInt - they return primitives and not objects). 
The boolean returned represents the value true if the string argument is not null and is equal, ignoring case, to the string "true".  Boolean.valueOf(String ) and its overloaded Boolean.valueOf(boolean ) version, on the other hand, work similarly but return a reference to either Boolean.TRUE or Boolean.FALSE wrapper objects. 
Observe that they dont create a new Boolean object but just return the static constants TRUE or FALSE defined in Boolean class.  3. When you use the equality operator ( == ) with booleans, if exactly one of the operands is a Boolean wrapper, it is first unboxed into a boolean primitive and then the two are compared (JLS 15.21.2). 
If both are Boolean wrappers, then their references are compared just like in the case of other objects. ```Thus, new Boolean("true") == new Boolean("true")``` is false, but ```new Boolean("true") == Boolean.parseBoolean("true")``` is true.
-The equals methods of all wrapper classes first check if the two object are of same class or not.

## Assignment
```boolean b1 = false; boolean b2  = false; if (b2 = b1 != b2){ //true
int expr1 = 3 + 5 * 9 - 7;  //41       
int expr2 = 3 + (5 * 9) - 7;  //41       
int expr3 = 3 + 5 * (9 - 7);  13         
int expr4 = (3 + 5) * 9 - 7;  //65
System.out.println(100/9.9); //Since one of the operands (9.9) is a double, it wil perform a real division and will print 10.1010101010101
```

## Switches
Here are the rules for a switch statement:
1. Only String, byte, char, short, int, (and their wrapper classes Byte, Character, Short, and Integer), and enums can be used as types of a switch variable. (String is allowed only since Java 7). 
2. The case constants must be assignable to the switch variable. For example, if your switch variable is of class String, your case labels must use Strings as well.
3. The switch variable must be big enough to hold all the case constants. For example, if the switch variable is of type char, then none of the case constants can be greater than 65535 because a char's range is from 0 to 65535.
4. All case labels should be COMPILE TIME CONSTANTS.
5. No two of the case constant expressions associated with a switch statement may have the same value.
6. At most one default label may be associated with the same switch statement.
7. The type of the case labels must be consistent with the type of the switch condition


## Exceptions
- Exceptions are always some subclass of java.lang.Exception
- Catch blocks are not required
- An exception that is never caught will cause your application to stop
- Throwable > Exception && Error
- The most specific catch-clause must be at the top, otherwise it will be unreachable code (since a broader Exception will trigger)
- The exceptions that a method can throw must be declared > void myFunction() throws MyException, MyException2 { //method body} A method that 'receives' an Exception must either catch in or rethrow it (and it this case declare in in the method signature)
- Finally statements are ALWAYS executed, whether an exception was thrown or not (after the return statement, before the return executes)
- You do not need to declare catch-clauses for RuntimeExceptions (or method signatures)
- When a extended class has a method with a throws Exception the method/class that uses this method should also have this exception-signature. (in for example the main method) 
Game.play throws exception > Game g = new Soccer g.play >>>>> this needs to called in a method that has the same exception-signature
- When you use System.out.println(exception), a stack trace is not printed. Just the name of the exception class and the message is printed. 
When you use exception.printStackTrace(), a complete chain of the names of the methods called, along with the line numbers, is printed.
- Overriding method only needs to specify a subset of the list of exception classes the overridden method can throw. A set of no classes is a valid subset of that list.
  ```a[thisWillThrowAnException()][i = 1]++;``` < If evaluation of a dimension expression completes abruptly, no part of any dimension expression to its right will appear to have been evaluated. [i = 1 will not be executed]
- throw new NullPointerException(); < This is possible (although it looks strange..)
- java.lang.SecurityException is a standard Exception (who knew..)
- If there is no catch block, the exception will not be handled and the invoking method will throw the exception to the caller.
- A method that throws a 'checked' exception i.e. an exception that is not a subclass of Error or RuntimeException, either must declare it in throws clause or put the code that throws the exception in a try/catch block.
- Once the exception is caught the rest of the catch blocks at the same level (that is the ones associated with the same try block) are ignored

## Imports
- Bad syntax. A package statement can never have a *

## Garbage collection

- If an objects get returned in a method it will never be a candidate for Garbage collection within this method.


## Instanceof
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

## Java API
```
System.out.println(LocalDate.of(2015, Month.JANUARY, 01).format(DateTimeFormatter.ISO_DATE_TIME));  // comp. error (no time-component)
final public static void main(String [ ] array)   // works
public static void main(String args[ ]) // works
static void main(String args[ ]) // does not work since it is missing the required public
public static long main(String[] args){ // this will give an error at Runtime, not compile time..
```


## Arrays
- The statement ```int[ ][4]``` will not compile, because the dimensions must be created from left to right.
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
- we have a simple for loop whe have a incrementer. This will only be 'exececuted' when the condition in the for loop is true. //TODO UITZOEKEN OF DAT ECHT ZO IS>..

## Some random examples of cruelty
Keep in mind to always check the number of answer that should be provided.... ;)

- A class can have a method named Main. Although, since it is not same as main, it will not be considered the standard main method that the JVM can invoke when the program is executed.
- LocalDate ld2 = ld.plus(Period.of(0, 1, 1));
- final public static void main(String [ ] array)
- When you see something about packages remember the following: Note that there is no modifier for A's constructor. So it has default access. (default == package only). This will most likely be an compile error
- It will throw a java.lang.OutOfMemoryError. Note that this is not a subclass of RuntimeException or even Exception. It is a subclass of java.lang.Error. (so no exception is caught)
- Note that local (aka automatic) variables, such as the variables d and e in the code given here, are not initialized automatically. They have to be initialized explicitly. However, it is ok to leave them uninitialized if you don't use them anywhere in the code (as is the case with the variable d). 
- There no unsigned keyword in java! A char can be used as an unsigned integer. < well hidden in a question
- ```float f = 0x0123;``` is valid because god knows why (implicit narrowing..)
- Variables can't be declared as abstract or native.

*add some more examples: http://www.programmergirl.com/oca-java-8-preparation-java-basics/ ?

## Some youtube comments ;)
- You want to have general understanding about JVM, and what it is, your knowledge of classes, inheritance and interfaces has to be top notch
   - For example, if you have a method in a class that is abstract but your class is not abstract, guess what compiler error! Even if you know this it is easy to miss on the exam.
- They like to put tricks with strings like he said, like string.'methodname(arg0) you MUST assign it back to have it actually mean something
- Another trick with date classes, LocalDate date = LocalDate.now(), your variable must be created statically, LocalDate date = new LocalDate() DOES NOT COMPILE!
- Touch on period also, Period p = Period.ofWeek(1).ofDays(1) this will mean a period of 1 day not 8 days... only the last one counts
- Make sure code compiles, they love to stump you with something simple like putting String as string in lower case which does not compile.
- Autoboxing, know the valueOf and parseInt methods, and their return type for Integer wrapper class, parseInt returns primitive, whereas valueOf returns wrapper
- Know the Arrays.sort(array) for the binary search, there will be 1 or 2 questions about that
- ArrayList knowledge must be top notch
- Know the hierarcy of exceptions, The top level is throwable, Error and Exception inherit from throwable, Error should not be caught, Exception is checked, Runtime exception which inherits from Exception is unchecked. 
- Know try catch, and scope, order matters for catch statements. They also like to confuse you by questions where they may imply that finally is required in a try block but only 0 or more catch blocks and /or at most 1 finally block is allowed, You need either atleast one catch block defined or a finally available. If they do something like System.exit(0) in catch block then finally is NOT executed. Also know that ClassCastException is a runtime error, this is when you try to cast your class to another type that is not related to your class, Example, you can cast an Integer to Number, but casting integer to String is going to throw this exception.
- Get a good grip on ternary operator.
- Get a good grip on increment and decrement. for example if int i = 1, if i do i = i++; i will end up being set as 1. this is another trick. i++ on the other hand will change i to 2.
- you want to have a good handle on loops as well. They LOVE to put loops without curly brackets just to confuse you, it's really annoying and i hate them for doing that.
- You also want to know pass by value and pass by reference, for example, if i pass an array of int to another method and then do something like myArray[0] = 5, guess what, i just changed the contents of myArray for the calling method, this is because even though a copy of the array is passed in, they both have the same reference, if the method which has the array passed into renewed the reference then yes the earlier statement no longer applies.
- Know order of initialization, know your modifiers, know about static, final and all the other important keywords. Know the static block. 
- Know that local variables MUST always be initialized before being used, class variables and member variables DO NOT have to be initialized, they are initialized to a default value for primitives it is a value, for objects it is null. however if you have the final keyword in front then you must initialize them before you can use them
- Polymorphism they love putting these all over the practise exams, you'll have to understand it well
- He talked about autompromoting of primitives during arithmetic operations, very important concept
- Another trick here - System.out.println (1 + "2" + 3) outputs 123, System.out.println(1 + 2 + 3 + " ") will give you '6 ', always read from left to right while figuring out the final value
-one really annoying thing i noticed. Sometimes they will do something like Int l = myStringArray.length(); then do something like system.out.println(myStringArray[l]. Something really stupid i did was (and my brain was tired) the print statement is on line 2, and the letter 'L" lower case looks awfully like a 1, got it wrong on the practise test :)
- Also please please please remember, that if you have an array you do myArr.length to get length, if you have string you do myString.length() and if u have list you do myList.size(), they love to confuse you with these ones those buggers
- know the idfference between private, protected and package private really really well...
- you also have to know what a virtual function / method is in java, it is any method that is not static and not marked with the keyword final. They have to be overrideable.
- Know overloading really well, this one can be tricky too (i'm still getting caught up in some of the tricks)
- know what covariance is in java. For example if you are overloading a method from a parent class, the return type or exection thrown can have a narrower scope, not a broader scope. so if i'm returning Number in the parent class, I am allowed to return Long or Integer wrapper class in child class. Same with exception, if i'm throwing exception in parent class, i can throw runtimeexception for example in child class (or remove the exception declaration alltogether)
I'm just going to stop here, if you are someone who is new to the whole certification thing, you can see that there is a lot to learn. I would recommend taking your time and not rushing into the exam. buy the practise exam on udemy it has 4 practise tests.... sorry for the very long comment but i hope this helps someone out there. if you read this far, i commend you, please reply back if you appreciated it or have something to add to this list! (there is a lot that can be added)


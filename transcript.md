(1 slide) 
Typescript

(2 slide) 
There are not so few ways to protect your code in the frontend world, for example, it is possible to write Unit tests for jest and Enzyme, we can use linters like eslint and stylelint but all this gives us only a part of stability, this is a check of already written code, for example, tests don’t guarantee stability by themselves, for the tests to work, they must be written well. We need a tool that will allow us not to check the finished code, but which will allow us to write stable code. There is such a tool and it is called Typescript.

(3.1 slide) 
What is Typescript in general?

(3.2 slide)
Wikipedia says that it is an independent programming language that extends the capabilities of javascript. The TypeScript developer is Anders Hejlsberg, who previously created Turbo Pascal, Delphi, and C #.

(3.3 slide)
By the name Typescript differs from Javascript by the word type. Typing in javascript is dynamic and the type of the variable is determined not at the time the variable is created, but later at the moment when we put some value into it, moreover, this type may change in the future for example, we can create a number in it, and then a string, and then change to an array. This leads to serious trouble in large-scale projects. For example, a programmer may need to spend many hours just figuring out why a certain variable turned out to NaN. In Typescript, on the other hand, typing is static.

(3.4 slide)
What is static typing?
The main difference between statically typed and dynamically typed languages is how they validate data types. The first do it during compilation, and the second do it during program execution. In other words, statically typed languages require the programmer to declare data types before using them and they cannot be changed later, while in dynamically typed languages this is not necessary.

(3.5 slide) 
And it is a completely different approach. At any moment we know which data type is in which variable and it makes easier to read the code and makes faster to write the code. It makes easier refactoring, improves the work of tips in your IDEs, and the most convenient Typescript compiler will not allow you to compiler broken code if there is an error in it. This cuts off most of the errors that are often meeting when we writing code in javascript.

(3.6 slide)
TypeScript is a kind of JavaScript add-on. This means that it not only supports type checking, but also allows you to work with features of ES6 and ES7. The Typescript compiler converts the code into pure JavaScript that can be run in any browser. Well, as bonuses, we get the full functionality of classes with inheritance, access modifiers, decorators, interfaces, enums, etc.
Let's look at the features of TypeScript syntax. In many ways, it is similar to Javascript but has its own differences.

The first difference that I want to consider is data types. We will not delve into the type system cause it is very flexible, and we will limit ourselves only some basic features. 

(4.1 slide) 
Basic types

TypeScript supports the same types that exist in JavaScript, but in a more convenient way: 
const text = ‘hello world’ – this is how a variable is declared in javascript 
const text: string = ‘hello world’ – this is how it looks in typescript;
As you can see, the only difference is that typescript after the variable declaration expects an indication of its type, in this case it is string.

Currently, the following data types exist in typescript:

(4.2 slide) 
Boolean  
To represent boolean values true or false;

let isDone: boolean = false;

(4.3 slide) 
Number 
To represent integers or floating point numbers. 
To representing the numbers greater than two in pow fifty three, there is the bigint type;
    let decimal: number = 6;
    let hex: number = 0xf00d;
    let binary: number = 0b1010;
    let octal: number = 0o744;
    let big: bigint = 100n;

(4.4 slide) 
String
To represent the text data
    let color: string = "blue";

(4.5 slide) 
Null и Undefined
In Typescript, undefined and null have their own data type.
    let u: undefined = undefined;
    let n: null = null;

(4.6 слайд) 
Array
Array types can be written in one of two ways:
In 1 way, the element type is used followed by an array of elements, the second way uses the universal array type Array <elemType>
    let list: number[] = [1, 2, 3];
    let list: Array&lt;<number>&gt; = [1, 2, 3];

(4.7 slide) 
Object 
For a representation of a non-primitive type, that is, all that is not Boolean, number, string, null and undefined
    let user: object = {
        name: "brad", 
    } 
You can create your own types for objects, in Typescript, the type operator is reserved for this, it looks like this
    type User = { name: string, surname: string age: number }
    let user: User = {
        name: "brad", 
       surname: "pitt", 
        age: 56
    }

(4.8 slide) 
Never
To represent the type of values that never occur. Usually this type is set to a function that throws some kind of error;
     function error(): never {
         throw new Error();
     }

(4.9 slide)
Void
Used when there is no type at all, usually used for functions that return nothing
    function warnUser(): void {
        console.log("This is my warning message");
    }

(4.10 slide)
Any
To represent the types of variables which we do not know, for example, user or third-party library data. In this case, we want to refuse type checking at compile time and mark them with any
    let notSure: any = 4;
    notSure = "maybe a string instead";
    notSure = false;

Also, any can be used in arrays where values of different types are contained.
    let list: any[] = [1, true, "free"];

(4.11 slide)
Type union
In Typescript, it is possible to unite types using the following statement
     let unknown: string | number = "1";

You can also set variables of your own types, interfaces, etc. If a variable is not set to any type, typescript will determine it automatically based on the specified value. 

The second difference that I want to consider is functions.

(5.1 slide)
Functions are the fundamental building block of any JavaScript application. This is how you create abstraction layers that imitate classes, hide information, and modules. TypeScript adds some new features to the standard JavaScript functions so that it is easier to work with them, let's look at some of them.
This is how looks function declaration
    function add(x: number, y: number): number {
        return x + y;
    }
We can add types to each of the parameters, and then to the function itself, to add the return type. TypeScript can determine the return type by looking at the return statement. For functions that return nothing, the already-considered types never and void are used.

(5.2 slide)
Function type 
The type of function is as follows
    let myAdd: (x: number, y: number) => number = function(
         x: number,
         y: number
    ): number {
         return x + y;
    };
A function type has two parts: the type of the argument and the type of the return value. We write parameter types in the same way as a parameter list, giving each parameter a name and type.
the type of the return value is set through equal and arrow between the parameters and the return value. This is a required part of the function type, so if the function does not return a value, you must use the void type.
Usually, the type of a function is specified when creating the type of an object or class
    type User = { 
        name: string,
        surname: string,
        age: number,
        getJobs: () => string[]
    }

(5.3 slide)
Optional and standart parameters
In TypeScript each parameter is required for a function. It means that the number of arguments passed to the function must match the number of parameters specified when defining the function.
     function buildName(firstName: string, lastName: string) {
         return firstName + " " + lastName;
     }
     let result1 = buildName("Bob"); // error, too few parameters
     let result2 = buildName("Bob", "Adams", "Sr."); // error, too many parameters
     let result3 = buildName("Bob", "Adams"); // ah, just right
In JavaScript, each parameter is optional, and users can leave it as they want. We can get this functionality in TypeScript by adding an operator question to the end of the parameters that we want to make optional. 
    function buildName(firstName: string, lastName = "Smith") {
        return firstName + " " + lastName;
    }
    let result1 = buildName("Bob"); // works correctly now, returns "Bob Smith"
    let result2 = buildName("Bob", undefined); // still works, also returns "Bob Smith"
    let result3 = buildName("Bob", "Adams", "Sr."); // error, too many parameters
    let result4 = buildName("Bob", "Adams"); // ah, just right

The third difference that I want to consider is classes.

(6.1 slide)
Classes

Traditional JavaScript uses prototype-based functions and inheritance to create reusable components, but it may seem a little inconvenient for programmers who are more comfortable using an object oriented approach where classes inherit functionality and objects are created from these classes. Starting with ECMAScript 2015, you can create your own applications in JavaScript using this class-oriented object-oriented approach. Typescript expands the possibilities of writing object oriented code in Javascript, it supports such functions as access modifiers, interfaces.

Let's look at a simple class-based example:
class Animal {
  name: string;
  constructor(theName: string) {
    this.name = theName;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}
let animal = new Animal("Fluffy");

The syntax is the same as when writing a class in javascript except for specifying the required type in the constructor

(6.2 slide)
Access modifiers
(6.3 slide)
First of modifier is public
If you are familiar with classes in other languages, you may have noticed that in the example above we did not have to use the word public to achieve this; for example, C # requires that each member be explicitly marked public as visible. In TypeScript, each member is public by default. You can mark the public member explicitly. We could write an Animal class as follows:
class Animal {
  public name: string;
  public constructor(theName: string) {
    this.name = theName;
  }
  public move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
(6.4 slide)
Second of modifiers is private
TypeScript has its own way of declaring a member as private, it cannot be accessed from outside its containing class.
class Animal {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}
new Animal("Cat").name; // Error: 'name' is private;

(6.5 slide)
Third modifier is protected
The protected modifier acts in the same way as the private modifier with the exception that members declared protected can also be accessed in classes that inherit the current

class Person {
  protected name: string;
  protected constructor(theName: string) {
    this.name = theName;
  }
}

(6.5 slide)
Typescript has the ability to create abstract classes.
Abstract classes are the base classes from which other classes can be derived. Of these classes, instances cannot be created. Unlike an interface, an abstract class may contain implementation details for its members. The Abstract keyword is used to define abstract classes, as well as for abstract methods in an abstract class.
abstract class Animal 
  abstract makeSound(): void;
  move(): void {
    console.log("roaming the earth...");
  }
}
Methods in an abstract class that are marked as abstract do not contain an implementation and must be implemented in derived classes.

And the last I want to consider is feature of the typescript to create interfaces.

(7.1 slide) 
And the last I want to consider is feature of the typescript to create interfaces.
The interface defines the properties and methods that the object must implement. In other words, an interface is a definition of a custom data type, but without an implementation. In this case, the interfaces in TS are similar to the interfaces in Java and C #. Interfaces are defined using the interface keyword. First, let's define a simple interface:
interface IUser {
    id: number;
    name: string;
}
The interface in braces defines two properties: id, which is of type number, and name, which represents a string. Now we use it to define the object: 
let employee: IUser = { 
    id: 1, 
    name: "Tom"
}
In essence, employee is an ordinary object, with the exception that it is of type IUser. More correctly, employee implements the IUser interface. Moreover, this implementation put some restrictions on employee. So, employee must implement all the properties and methods of the IUser interface, therefore, when defining employee, this object must necessarily include the id and name properties.

(7.2 slide) 
Interfaces can be implemented not only by objects, but also by classes. To do this, use the implements keyword
interface IUser {
    id: number;
    name: string;
    getFullName(surname: string): string;
}
class User implements IUser{
    id: number;
    name: string;
    age: number;
    constructor(userId: number, userName: string, userAge: number) {
        this.id = userId;
        this.name = userName;
        this.age = userAge;
    }
    getFullName(surname: string): string {
        return this.name + " " + surname;
    }
} 
let tom = new User(1, "Tom", 23);

The User class implements the IUser interface. In this case, the User class must define all the same properties and functions that are in IUser. The tom object is both a User object and an IUser object

(7.3 slide) 
Interfaces, like classes, can be inherited
interface IMovable {
    speed: number;
    move(): void;
}
interface ICar extends IMovable {
    fill(): void;
}
After inheritance, the ICar interface will also have all those properties and functions that are defined in IMovable. And then, the Car class that implements the ICar interface will have to implement the properties and methods of the IMovable interface as well.

(8 slide)
Well, I hope you have a little understanding of how Typescript works, unfortunately because of the time limit there is no way to tell more. Thank you for the attention.

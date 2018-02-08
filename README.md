# java-inheritance


- udemy course
- notion of overriding methods (use of 'super')
```
@Override
public void move(int speed) {
    System.out.println("Dog.move() called");
    moveLegs(speed);
    super.move(speed);
}
```
- notion of inheritance
  - Main
  - Animal
    - Dog

```
public class Dog extends Animal {
}
```
# Inheritance
- The Single Responsibility Principle (SRP) of object-oriented programming states that objects should have just one responsibility. For example, a wheel on an office chair should be responsible for facilitating rolling. You wouldn't expect that wheel to also handle reclining, raising and lowering the seat, and spinning. First, it would be a strange looking wheel, but from an object-oriented perspective, the wheel would have multiple responsibilities. Multiple responsibilities make objects more complicated to create, test and maintain. It also tends to limit the ability to reuse the object elsewhere. If a wheel also handled reclining, it couldn't be used appropriately on a chair that didn't recline or on a file cabinet, or on another object that required a wheel but didn't recline. Reuse is a major goal of object-oriented design.

- Therefore, when you create a new object by inheriting from another, the goal should be to make the new object a more specific version of the original. For example, using inheritance, you could create a new type of wheel that is made of hard plastic and rolls better on carpet. You could also create one that is covered in rubber for use on hardwood floors. These examples are both good uses of inheritance because the resultant object is still a wheel, just a more specific type of wheel. Inheritance is about creating an is a relationship. When done right, you can say that "the hard plastic wheel is a wheel."

- Because of SRP, inheritance shouldn't be used to add more responsibilities to an object. Therefore creating a new object that inherits from wheel but adds a jet engine would be poor practice. You can't really say that a jet engine is a wheel.


---------------

## Inheritance
- In object-oriented programming, inheritance enables new objects to take on the properties of existing objects. A class that is used as the basis for inheritance is called a superclass or base class. A class that inherits from a superclass is called a subclass or derived class. The terms parent class and child class are also acceptable terms to use respectively. A child inherits visible properties and methods from its parent while adding additional properties and methods of its own.

- Subclasses and superclasses can be understood in terms of the is a relationship. A subclass is a more specific instance of a superclass. For example, an orange is a citrus fruit, which is a fruit. A shepherd is a dog, which is an animal. A clarinet is a woodwind instrument, which is a musical instrument. If the is a relationship does not exist between a subclass and superclass, you should not use inheritance. An orange is a fruit; so it is okay to write an Orange class that is a subclass of a Fruit class. As a contrast, a kitchen has a sink. It would not make sense to say a kitchen is a sink or that a sink is a kitchen. The has a relationship indicates composition (see Object-oriented programming concepts: Composition and aggregation) rather than inheritance. Look at the ChocolateCake class below:

```
package cakes {
    public class ChocolateCake {

        public function ChocolateCake(){}

        public function bake():void{
            trace("The chocolate cake is baking");
        }

        public function frost():void{
            trace("The chocolate cake now has frosting");
        }

        public function putCandlesOnCake(numberOfCandles:int):void{
            trace("Putting " + numberOfCandles + " candles on the cake. ");
        }
    }
}
```

- It's a simple class with three methods: bake(), frost(), and putCandlesOnCake(). You would have a good chocolate cake that you could put candles on after instantiating this class. As fun as it might be, do you really want or need candles on every chocolate cake you make? Probably not. Typically, candles only go on birthday cakes. Classes should only include the properties and methods that they need. Not every instance of ChocolateCake needs candles, so the class shouldn't include that method. Instead, you should write a separate BirthdayCake class that can have candles. To keep this first example simple, BirthdayCake will inherit from ChocolateCake. Look at a revised version of ChocolateCake :

```
package cakes {
    public class ChocolateCake {

        public function ChocolateCake(){}

        public function bake():void{
            trace("The chocolate cake is baking");
        }

        public function frost():void{
            trace("The chocolate cake now has frosting");
        }
    }
}
```

The putCandlesOnCake() method has been removed from ChocolateCake. Look at BirthdayCake below. It inherits the properties and methods of ChocolateCake and adds the ability to put candles on the cake.

```
package cakes {
    public class BirthdayCake extends ChocolateCake {

        public function BirthdayCake(){}

        public function putCandlesOnCake(numberOfCandles:int):void{
            trace("Putting " + numberOfCandles + " candles on the birthday cake.");
        }
    }
}
```
You could use both classes in the following way:

```
var chocCake:ChocolateCake = new ChocolateCake();
var bDayCake:BirthdayCake = new BirthdayCake();
chocCake.bake();
bDayCake.bake();
bDayCake.putCandlesOnCake(20);

//output
The chocolate cake is baking
The chocolate cake is baking
Putting 20 candles on the birthday cake.
```

- Notice that BirthdayCake does not explicitly include a method named bake(), but you can still call that method on the instance of BirthdayCake because a subclass inherits all the public methods of its superclass. Since bake() is a public method in ChocolateCake, bake() is also a method in BirthdayCake. And the result of the method— The chocolate cake is baking —is the same regardless of the instance on which you call the method.

### Multiple subclasses of a single superclass
- Remember, you can say that a subclass is a superclass. In this example, a birthday cake is a chocolate cake. That logic makes sense; however, it also means that every birthday cake is always a chocolate cake. With the code examples so far, you can never have any other flavor for your birthday cake. But think about the is a logic again for this cake-based example. A chocolate cake is a cake. A birthday cake is a cake. It makes sense to have a Cake class that gets extended by many different types of cakes. One of the common features of all cakes is flavor, so the Cake class has a flavor property, which is set in the constructor.

- Look at the code below to see Cake and two specialty subclasses BirthdayCake and WeddingCake.

```
BirthdayCake and WeddingCake.
package cakes {
    public class Cake {

        protected var flavor:String;

        public function Cake(flavor:String) {
            this.flavor=flavor;
        }

        public function bake():void{
            trace("The cake is baking and it is " + flavor);
        }

        public function frost():void{
            trace("The cake now has frosting");
        }
    }
}

package cakes {
    public class BirthdayCake extends Cake {

        public function BirthdayCake(flavor:String){
            super(flavor);
        }

        public function putCandlesOnCake(numberOfCandles:int):void{
            trace("Putting " + numberOfCandles + " candles on the birthday cake.");
        }
    }
}

package cakes {
    public class WeddingCake extends Cake {

        public function WeddingCake(flavor:String) {
            super(flavor);
        }

        public function makeCakeTiers(numberOfTiers:int):void{
            trace("This wedding cake has " + numberOfTiers + " tiers.");
        }

    }
}
```

You could use the classes in the following way:
```
public var cake:Cake = new Cake("yellow");
public var bDayCake:BirthdayCake = new BirthdayCake("strawberry");
public var wedCake:WeddingCake = new WeddingCake("lemon chiffon");
cake.bake();
bDayCake.bake();
bDayCake.putCandlesOnCake(36);
wedCake.bake();
wedCake.makeCakeTiers(4);

//output
The cake is baking and it is yellow
The cake is baking and it is strawberry
Putting 36 candles on the birthday cake.
The cake is baking and it is lemon chiffon
This wedding cake has 4 tiers.
```

- Again, notice that neither BirthdayCake nor WeddingCake includes a method named bake(), but you can still call it on instances of those classes because it is a public method of their superclass Cake. Both BirthdayCake and WeddingCake have the properties and methods of Cake plus their own methods specific to that type of cake.

- Birthday cakes have candles. Wedding cakes have tiers. Is there any special feature of a chocolate cake that distinguishes it from any other cake? Not really. Therefore, you do not need a separate class to make a chocolate cake. Simply instantiate the Cake class setting the flavor property to chocolate:
```
public var chocCake:Cake = new Cake("chocolate");
```

### The is operator
- The is operator tests whether a variable or expression is compatible with a given data type. It examines the inheritance hierarchy and can be used to check whether an object is an instance of a particular class or a child (or grandchild, great grandchild, great great grandchild, and so on) of a particular class. It can also check whether an object is an instance of a class that implements a particular interface (see Object-oriented programming concepts: Polymorphism and interfaces). The following example creates an instance of the Sprite class named mySprite. Then it uses the is operator to test whether mySprite is an instance of the Sprite and DisplayObject classes, and whether it implements the IEventDispatcher interface:
```
var mySprite:Sprite = new Sprite();
trace(mySprite is Sprite);    // true
trace(mySprite is DisplayObject);   // true
trace(mySprite is IEventDispatcher);    // true
trace(mySprite is Number);    // false
```
- The is operator checks the inheritance hierarchy and properly reports that mySprite is a Sprite and a descendent of the DisplayObject classes. The is operator also checks whether mySprite inherits from any classes that implement the IEventDispatcher interface. Because the Sprite class inherits from the EventDispatcher class, which implements the IEventDispatcher interface, the is operator correctly reports that mySprite implements the same interface. The is operator correctly reports that mySprite is not a Number.

- Using the Cake example from above, you can check whether instances of Cake, BirthdayCake, and WeddingCake classes are compatible with Cake:
```
var cake:Cake = new Cake("yellow");
var bDayCake:BirthdayCake = new BirthdayCake("strawberry");
var wedCake:WeddingCake = new WeddingCake("lemon chiffon");
trace(cake is Cake);  //true
trace(bDayCake is Cake);  //true
trace(wedCake is Cake);  //true
trace(cake is Sprite);  //false
```
- Because cake is not an instance of Sprite, the is operator correctly returns false.

### Inheritance and controlling access
- You control access to variables, classes, functions, and methods using access control attributes. You have seen them used in previous articles in Learning ActionScript 3. When using inheritance, understanding how access control works is important.

Table 1. Access control attributes


| Access control attribute keyword        | Access                                                                             |
| --------------------------------------  |:------------------------------------------------------------------------------ :   |
| public                                  | available to any caller                                                            |
| private                                 | available only to the class that defines it                                        |
| protected                               | available only to the class that defines it and to any subclasses of that class    |
| internal                                | available to any caller within the same package                                    |


In ActionScript 3, there are four levels of access control: public, private, protected, and internal (see Table 1). The default level is internal.

- Any public property, method, or class is available anywhere in your application. Therefore, a child class will inherit all public properties and methods from its parent class. Private properties and methods are part of a class's implementation and are only available within the class. The SampleParent class below has public, private, and protected properties and methods:
```
package samples {
    public class SampleParent {

        public var publicMessage:String = "Hello, world!"
        private var privateMessage:String = "I don't want to say hi.";		
        protected var protectedMessage:String = "Secret hi.";

        public function SampleParent() {}

        public function tracePublicMessage():void{
            trace(publicMessage);
        }

        private function tracePrivateMessage():void{
            trace(privateMessage);
        }

        protected function traceProtectedMessage():void{
            trace(protectedMessage);
        }
    }
}
```
You can use any public properties or call any public methods in a class:
```
public var testParent:SampleParent;
testParent = new SampleParent();
testParent.tracePublicMessage();
testParent.publicMessage = "Hi to everyone.";
testParent.tracePublicMessage();

//Output
Hello, world!
Hi to everyone.
```
- When using the SampleParent class, you will get an error when attempting to use either the private or protected properties or when you attempt to call the private or protected functions:
```
testParent.tracePrivateMessage();  //error 1195
testParent.privateMessage = "Hi.";  //error 1178
testParent.traceProtectedMessage();  //error 1195
testParent.protectedMessage = "Hello";  //error 1178

//Errors
1195: Attempted access of inaccessible method
1178: Attempted access of inaccessible property
```
- In addition to not being accessible outside the class itself, private features are not inherited by any subclasses. The simple SampleChild class is a subclass of SampleParent:
```
package samples {
    public class SampleChild extends SampleParent {

        public function SampleChild() {
            trace("Child says: " + this.publicMessage);
            trace("Child says: " + this.protectedMessage);
            trace("Child says: " + this.privateMessage);	//error 1178
        }			
    }
}
```
The last line of code in the constructor function—
trace("Child says: " + this.privateMessage);
—will cause error 1178. Without that line of code, you can use the class as follows:
```
var testChild:SampleChild = new SampleChild();
testChild.tracePublicMessage();
testChild.publicMessage = "Child says hi";
testChild.tracePublicMessage();		

//Output
Child says: Hello, world!
Child says: Secret hi.
Hello, world!
Child says hi
```
Protected properties and methods are inherited by subclasses but they are only accessible from within the subclasses. In SampleChild, you can see that—

trace("Child says: " + this.protectedMessage);

—does not cause an error. You do not get an error because you are accessing the protected property from within the subclass. If you tried to access the protected property using an instance and dot syntax—

testChild.protectedMessage

—you would get error 1178.

### Overriding methods
- One of the advantages of inheritance is that a subclass inherits all of the public and protected methods of its superclass. Sometimes though, a subclass needs to change the functionality defined in the superclass. Overriding is the technique of redefining an inherited method. When you override a method, use the override keyword. The redefinition must have the same number of parameters as the original (inherited) definition and its return type must be the same as the original return type.

Look at the Pen class below:
```
package writing {
    public class Pen {
        public function Pen() {}

        public function line():void {
            trace("Pen drew a line.");            
        }

        public function circle():void {
            trace("Pen drew a circle.");
        }
    }
}
```
- Then Pen class has two methods: one for drawing a line and one for drawing a circle. Using inheritance, you can create two new types of Pen: FountainPen and RollerBallPen. The FountainPen class extends the Pen class, adds one additional method named refill(), and overrides the line()
and circle() functions:
```
package writing {
    public class FountainPen extends Pen {

        override public function line():void {
            trace("FountainPen drew a line... and a splotch.");            
        }

        override public function circle():void {
            trace("FountainPen almost drew a circle. Need more ink.");
        }

        public function refill():void {
            trace("all full");
        }
    }
}
```
The RollerBallPen also extends the Pen class and overrides the line() and circle() functions:
```
package writing {
    public class RollerBallPen extends Pen {

        override public function line():void {
            trace("RollerBallPen drew a super smooth line.");            
        }

        override public function circle():void {
            trace("RollerBallPen easily drew a circle.");
        }                
    }
}
```
When you call an overridden method on an instance of the subclass, the overridden version of the method will run. You would use the above classes in the following way:
```
var pen:Pen = new Pen();
pen.line();
pen.circle();
var fountainPen:FountainPen = new FountainPen();
fountainPen.line();
fountainPen.circle();
var rbPen:RollerBallPen = new RollerBallPen();
rbPen.line();
rbPen.circle();

//output
Pen drew a line.
Pen drew a circle.
FountainPen drew a line... and a splotch.
FountainPen almost drew a circle. Need more ink.
RollerBallPen drew a super smooth line.
RollerBallPen easily drew a circle.
```

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

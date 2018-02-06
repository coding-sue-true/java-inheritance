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

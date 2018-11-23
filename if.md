# If Statements
IF and SWITCH statements are horrible, most of the time it violates encapsulation. Replace it with polymorphism. If you happen to modify the method containing the branching statement everytime you have new types, it is probably a sign that the logic needs to belong somewhere else.

#### Bad Code
```java

class Node {
  String operation; //value nodes dont need this
  double value; //non-leaf nodes dont need this
  Node left; //asking for NPE
  Node right; //asking for NPE
  
  double evaluate() {
    if (operation == null) return value;
    else if (operation.equals("*")) return left.evaluate() * right.evaluate();
    else if (operation.equals("+")) return left.evaluate() + right.evaluate();
    else if (operation.equals("-")) return left.evaluate() - right.evaluate();
    else if (operation.equals("/")) return left.evaluate() / right.evaluate();
    return 0;
  }
}
```

#### Clean Code
Code seems longer, but it is actually a lot easier to read and modify without breaking existing code (Open-Close Principle)

```java

abstract class Node {
  double evaluate();
}

class Value extends Node {
  double value;
  
  double evaluate() {
    return value;
  }
}

abstract class BinaryOperation extends Node {
  Node left;
  Node right;
  
  double evaluate();
}

class Addition extend BinaryOperation {
  double evaluate() {
    return left.evaluate() + right.evaluate();
  }
}

class Subtraction extend BinaryOperation {
  double evaluate() {
    return left.evaluate() - right.evaluate();
  }
}

```

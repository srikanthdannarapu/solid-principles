# SOLID principles

* Single Responsibility
* Open / Closed
* Liskov Substitution
* Interface Segregation
* Dependency Inversion


### Single Responsibility:
```text
The classes you write, should not be a swiss army knife. They should do one thing, and do that one thing well.
```


#### (Bad) Example

```java
class Text {
    String text;
    String author;
    int length;

    String getText() { ... }
    void setText(String s) { ... }
    String getAuthor() { ... }
    void setAuthor(String s) { ... }
    int getLength() { ... }
    void setLength(int k) { ... }

    /*methods that change the text*/
    void allLettersToUpperCase() { ... }
    void findSubTextAndDelete(String s) { ... }

    /*method for formatting output*/
    void printText() { ... }
}
```
At first glance, this class might look correctly written. However, it contradicts the single responsibility principle, in that it has multiple reasons to change: we have two methods which change the text itself, and one which prints the text for the user. If any of these methods is called, the class will change. This is also not good because it mixes the logic of the class with the presentation.

#### Better Example
One way of fixing this is writing another class whose only concern is to print text. This way, we will separate the functional and the “cosmetic” parts of the class.

```java
class Text {
    String text;
    String author;
    int length;

    String getText() { ... }
    void setText(String s) { ... }
    String getAuthor() { ... }
    void setAuthor(String s) { ... }
    int getLength() { ... }
    void setLength(int k) { ... }

    /*methods that change the text*/
    void allLettersToUpperCase() { ... }
    void findSubTextAndDelete(String s) { ... }
}

class Printer {
    Text text;

    Printer(Text t) {
       this.text = t;
    }

    void printText() { ... }
}
```
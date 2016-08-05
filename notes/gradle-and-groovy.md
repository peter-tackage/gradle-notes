# Groovy definitions

This is possible, due to dynamic typing:
```groovy
def aThing = "aThingString"
aThing = 7
```

Lists:
```groovy
def myList = ["a", "b", "c"]
myList.map{it -> it + "1"}
```

You can use `$` to reference outside variables from inside a `String` definition:
```groovy 
def number = 7
println "This is my favorite number: $number"
```

Note: Generally you can get rid of the parenthesis.

# Groovy closures

```groovy
def myClosure = {
    // Closure implementation
}

myClosure() // invocation
```

You can also use `it` to reference the single parameter:
```groovy
def myList = ["a", "b", "c"]
myList.each {println(it)}
```

# Groovy classes

Class definitions look very similar to Java:
```groovy
class Greeter {
    String word = "Me!"
    def greet() {
        println "Hello $word"
    }
}

def greeter = new Greeter()
greeter.word = "You!"
greeter.greet()
```

Groovy automatically generates getters and setters for properties.

# Closure delegates

Closure can have delegate object, this is the foundation upon which the Gradle DSL is made.

This allows the closure to access the member variables and methods of the delegate directly as though they were defined in the closure.

```groovy
class MyClass {
    String finallySay = "Bye!"
}

def myClosure = {
    println finallySay
}

 project.task("hello") {
     group "Peter's Tasks"
     description "Says hi/bye"
     doFirst {
         println "Hello World!"
     }
     doLast {
         println "....."
         myClosure.delegate = new MyClass()
         myClosure()
     }
}
```

Generates output:
```
    > gradle hello
    :hello
    Hello World!
    .....
    Bye!
```
# Gradle tasks

`task` is a method on the delegated, globally visible `project` object. It creates tasks, given their name and closure.

```groovy
project.task("myGreatTask") {
    description 'A great task'
    group 'My tasks'
}
```

Because the project object is delegated everywhere, this can also be shortened to be written as:
```groovy
task("myGreatTask") {
    // Task def goes here
}
```

You could written this even shorter as: 

```groovy
task "myGreatTask" {
    // Task def goes here
}
```

or even: 
```groovy 
task myGreatTask {
    // Task def goes here
}
```

Tasks have various properties/methods defined in them:
```groovy
task myGreatTask {
    doLast {
        println "Just about the last thing"
    }
    doFirst {
        println "This will be run first"
    }
}
```

This syntax allows you to define really simple tasks:

```groovy
task myShortTask << { println "A short task" }
```

The `<<` (left-shift) operator means "really last". So this will be the last thing the task will do.

You can also set a number of properties on tasks to determine how they listed when running the gradle command:
```
> gradle tasks
```

For example:
```groovy
task task1 {
    group 'Example'
    description 'A longer description of the task'
}
```
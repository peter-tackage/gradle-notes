# Groovy closures

```groovy
def myClosure = {
    // Closure implementation
}

myClosure() // invocation
```

# Gradle tasks

`task` is a method on the delegated, globally visible `project`. It creates tasks, given their name and closure.

```groovy
project.task("myGreatTask") {
    description 'A great task'
    group 'My tasks'
}
```

Because the project object is delegarted everywhere, this can also be shortened to be written as:

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
        println("Just about the last thing")
    }
    doFirst {
        println("This will be run first")
    }
}
```

This syntax allows you to define really simple tasks:

```groovy
task myShortTask << { println("A short task")}
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
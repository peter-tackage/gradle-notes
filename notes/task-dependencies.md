# Task Dependencies

`shouldRunAfter` - is like a preference if you are doing two tasks, there's no strict need to perform both task B after task A, but if you ARE doing both, then you should do task B after task A.

`dependsOn` - if task B dependsOn task A, then task A will always be run before task B, when task B is invoked. It's a dependency to run a task upstream before the task you want to run.
`mustRunAfter`

`finalizedBy` - by declaring that task A is finalized by task B, then you ensure that whenever you invoked task A, that task B is run afterwards.

`gradle -q` is quiet mode.
# PS
Priority scheduling non primitive algorithm
A service is responsible for running tasks, and we’re interested in the order those tasks will run . A task is defined by its

“s” earliest start time

“d” total duration of execution

“p” priority of execution

The service is greedy in running tasks, such that it will start a runnable task if idle. At most one task can be run at any time, and all tasks will be run exactly once. The service will not start a task before its earliest start time “s”. However the task may be run any time thereafter. Once started, no other tasks may be scheduled for the duration “d” while the task runs to completion.

If two or more tasks are available to be run, then the next task is selected in order of the following criteria.

Highest priority “p”

Earliest start time “s”

Lowest duration of execution “d”

Lowest Index in the input

The input will consist of three arrays s, d and p, all consisting of “n” elements (1<= n <= 1000), where index “i” specifies the value for task “i” . The output should be an array of length “n” consisting of the order in which the tasks will be run, where a task is identified by its index “i” in the input.

For example, the input

s: [0,2,2]

d: [1,1,1]

p:[0,0,1]

Defines three tasks. Task “0” is run at time “0”. Both task “1” and “2” can be run at time “2”, however since task “2” has a higher priority, it’s run next, followed by task “1”. Therefore the expected output is:

[0,2,1]

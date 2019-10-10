# jCrystal Queues

A jCrystal Queue is a WS that can only be called asynchronously. There are two types of queues:

## Anonymous queues:

```java
public static void samplews(){
    //Your code
    jcrystal.queue.Async.queue(()->{
        //Your async task
    });
    //Your code
}
```

This lambda will be Serialized and the executed on a global Queue by posting serialized data to a especial RestWS. In order to work, all the variables used in the queued lambda should be Serializable. For example:

```java
public static void samplews(int param1){
    //Your code
    String var1 = "";
    String var2 = "";
    jcrystal.queue.Async.queue(()->{
        //Your async task
        String x = param1 + var1;
    });
    //Your code
}
```

In this lambda only _param1_ and _var1_ will be Serialized and sent on Async execution.

## Named queues:

A named queue is a especific queue used to separate async task. To define and use a named queue you must:

1. Define the queue on a *Manager class*.

```java
package company.example.controllers;

@jcrystal.reflection.annotations.async.Queue(name="MyQueue", rate="1/s")
public class ManagerExample {
	...
}
```

2. Run jCrystal (Cmd + 6)

3. Annotate a WS as Async:

```java
@Async(name=Async.Q.Myqueue)
public static void doAsyncWork(int param1, String var1) {
    //Your async task
    String x = param1 + var1;
}
```

4. Run jCrystal (Cmd + 6)

5. Invoke your task:

```java
public static void samplews(int param1){
    //Your code
    String var1 = "";
    String var2 = "";
    JQueue.Myqueue.taskDoAsyncWork(param1, var1);
    //Your code
}
```

## Schedule execution on future

Sometime you need to execute some task on the future. To do so, you can use jCrystal queues.

### Using anonymous queues

```java
jcrystal.queue.Async.queue(60000, ()->{ //Executes this task 1 minute (60000 ms) on future
    //Your async task
});
```

### Using named queues

```java
@Async(name=Async.Q.Myqueue, timeable=true)
public static void doAsyncWork(int param1, String var1) {
    ...
}
```

```java
    JQueue.Myqueue.taskDoAsyncWork(60000, param1, var1);
}
```
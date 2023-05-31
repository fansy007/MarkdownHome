# 概念

- 并发 逻辑上的

- 并行 物理上的

  程序员只关心并发



Thread object with 6 state:

![image-20230531171454759](image-20230531171454759.png)



## Future Task

FutureTask::get will block main thread and wait the result

```java
    public void play2() throws Exception{
        FutureTask<String> task = new FutureTask<>(
                ()->"hello, world" // callable
        );

        new Thread(task).start();
        System.out.println(task.get());
    }
```



# CompletableFuture

Before join method, completable future already running



```java
public class TimeTool {
    public static void printTimeAndThread(String msg) {
        System.out.println(String.format("%s | %s | %s", LocalTime.now(),Thread.currentThread().getName(),msg));
    }
    public static void sleep(long time) {
        try {
            Thread.sleep(time);
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```



```java
public static void play1() {
        TimeTool.printTimeAndThread("Lee entering restaurant");
        TimeTool.printTimeAndThread("Lee order a menu");

        CompletableFuture<String> future = CompletableFuture.supplyAsync(()->{
            TimeTool.printTimeAndThread("Chef is preparing rice");
            TimeTool.sleep(500);
            TimeTool.printTimeAndThread("Chef is preparing eggs");
            TimeTool.sleep(500);
            return "A great meal";
        });

        TimeTool.printTimeAndThread("Lee is playing game");
        TimeTool.sleep(200);
        TimeTool.printTimeAndThread("Lee is reading");
        TimeTool.sleep(1000);
        TimeTool.printTimeAndThread(String.format("%s is ready, Lee start eating", future.join()));
    }
```



Output:

```shell
> Task :CompletableFuture2023.main()
18:29:25.746662 | main | Lee entering restaurant
18:29:25.750451 | main | Lee order a menu
18:29:25.752134 | main | Lee is playing game
18:29:25.752307 | ForkJoinPool.commonPool-worker-1 | Chef is preparing rice
18:29:25.952846 | main | Lee is reading
18:29:26.255507 | ForkJoinPool.commonPool-worker-1 | Chef is preparing eggs
18:29:26.956378 | main | A great meal is ready, Lee start eating
```


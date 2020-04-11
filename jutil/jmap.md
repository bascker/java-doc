# jmap
## 一、简介
jmap 用于监控内存内 java 对象
```shell
λ jmap -h
Usage:
    jmap [option] <pid>
        (to connect to running process)
    jmap [option] <executable <core>
        (to connect to a core file)
    jmap [option] [server_id@]<remote server IP or hostname>
        (to connect to remote debug server)

where <option> is one of:
    <none>               to print same info as Solaris pmap
    -heap                to print java heap summary
    -histo[:live]        to print histogram of java object heap; if the "live"
                         suboption is specified, only count live objects
    -clstats             to print class loader statistics
    -finalizerinfo       to print information on objects awaiting finalization
    -dump:<dump-options> to dump java heap in hprof binary format
                         dump-options:
                           live         dump only live objects; if not specified,
                                        all objects in the heap are dumped.
                           format=b     binary format
                           file=<file>  dump heap to <file>
                         Example: jmap -dump:live,format=b,file=heap.bin <pid>
    -F                   force. Use with -dump:<dump-options> <pid> or -histo
                         to force a heap dump or histogram when <pid> does not
                         respond. The "live" suboption is not supported
                         in this mode.
    -h | -help           to print this help message
    -J<flag>             to pass <flag> directly to the runtime system
```
* -heap: 查看堆中对象的信息：GC算法、堆配置参数、各代中堆内存使用情况
* -histo[:live]：打印堆中对象直方图
* -permant: 查看永久代信息
* -finalizerinfo：查看等待回收的对象信息
* -dump:<dump-option>：将java堆信息输出到hprof二进制格式文件

## 二、示例
```java
public class Main {

    public static void main(String[] args) throws InterruptedException {
        int i = 0;
        while (true) {
            Person p = new Person();
            p.setAge(10);
            p.setName("i" + i);

            TimeUnit.SECONDS.sleep(2);
        }
    }

}
```

执行 jps 查看进程号
```shell
$ jps
18688 Main
```

执行 jmap 查看堆信息
```shell
λ jmap -heap 18688
Attaching to process ID 18688, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.191-b12

using thread-local object allocation.
Parallel GC with 4 thread(s)

Heap Configuration:
   MinHeapFreeRatio         = 0
   MaxHeapFreeRatio         = 100
   MaxHeapSize              = 2120220672 (2022.0MB)
   NewSize                  = 44564480 (42.5MB)
   MaxNewSize               = 706740224 (674.0MB)
   OldSize                  = 89653248 (85.5MB)
   NewRatio                 = 2
   SurvivorRatio            = 8
   MetaspaceSize            = 21807104 (20.796875MB)
   CompressedClassSpaceSize = 1073741824 (1024.0MB)
   MaxMetaspaceSize         = 17592186044415 MB
   G1HeapRegionSize         = 0 (0.0MB)

Heap Usage:
PS Young Generation
Eden Space:
   capacity = 34078720 (32.5MB)
   used     = 4771464 (4.550422668457031MB)
   free     = 29307256 (27.94957733154297MB)
   14.001300518329327% used
From Space:
   capacity = 5242880 (5.0MB)
   used     = 0 (0.0MB)
   free     = 5242880 (5.0MB)
   0.0% used
To Space:
   capacity = 5242880 (5.0MB)
   used     = 0 (0.0MB)
   free     = 5242880 (5.0MB)
   0.0% used
PS Old Generation
   capacity = 89653248 (85.5MB)
   used     = 0 (0.0MB)
   free     = 89653248 (85.5MB)
   0.0% used

3170 interned Strings occupying 259944 bytes.
```

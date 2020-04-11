# jinfo
## 一、简介
```
λ jinfo -h
Usage:
    jinfo [option] <pid>
        (to connect to running process)
    jinfo [option] <executable <core>
        (to connect to a core file)
    jinfo [option] [server_id@]<remote server IP or hostname>
        (to connect to remote debug server)

where <option> is one of:
    -flag <name>         to print the value of the named VM flag
    -flag [+|-]<name>    to enable or disable the named VM flag
    -flag <name>=<value> to set the named VM flag to the given value
    -flags               to print VM flags
    -sysprops            to print Java system properties
    <no option>          to print both of the above
    -h | -help           to print this help message
```
* 查看运行中的 java 应用的扩展参数(包括java系统参数、JVM命令行参数)
* 动态修改运行中的 jvm 参数
* 从 core 文件获取崩溃的 java 应用的配置信息

## 二、案例
```shell
λ jinfo -flags 18688
Attaching to process ID 18688, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 25.191-b12
Non-default VM flags: -XX:CICompilerCount=3 -XX:InitialHeapSize=134217728 -XX:MaxHeapSize=2120220672 -XX:MaxNewSize=706740224 -XX:MinHeapDeltaBytes=524288 -XX:NewSize=44564480 -XX:OldSize=89653248 -XX:+UseCompressedClassPointers -XX:+UseCompressedOops -XX:+UseFastUnorderedTimeStamps -XX:-UseLargePagesIndividualAllocation -XX:+UseParallelGC
Command line:  -Dvisualvm.id=1722941542355300 -javaagent:xx\idea_rt.jar=51761:xx\bin -Dfile.encoding=UTF-8
```

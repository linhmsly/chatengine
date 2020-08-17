# Compile and run nebula's open source server chatengine notes

> Reprinted with permission of the author [@robinfoxnan](https://me.csdn.net/robinfoxnan)
> 

The official said it runs under LINUX, but after a look, it basically uses pure GO to compile, and it should be able to run under WINDOWS.

I am using the home version of Windows 10 and cannot use docker, so I decided to install the service directly.

For telegramd, according to the author's statement, it is no longer supported, so I suggest you use chatengine.

## 1. Install mysql5.7.19

　[Download address:](https://dev.mysql.com/downloads/mysql/)

Use the built-in execution script. \chatengine\docker\mysql\init-sql\01-chatengine.sql

Note: I use Navicat to build the database and import the table structure, the lower version does not support data types, and 5.7 installation is more troublesome, you can refer to another article of mine.

Among them, 5.7 does not support the default value of the timestamp in the script. You need to add an option in the session:

```
set session sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
```

Otherwise, a lot of errors will be reported, causing the table to be lost, and errors will occur during later operation.

## 2. Install redis

[Help:](https://www.cnblogs.com/jylee/p/9844965.html)

[Download address:](https://github.com/MicrosoftArchive/redis/releases)

There is not much to say about this, it is relatively simple.

## 3. Install etcd

[Introduction:](https://blog.csdn.net/skh2015java/article/details/80712214)

[Download address:](https://github.com/etcd-io/etcd/releases)

Need to add a configuration file: named: etcd.conf.yml

```
name: etcd
listen-client-urls: http://0.0.0.0:2379
advertise-client-urls: http://0.0.0.0:2379
```

Execute commands at startup:

```
etcd.exe --config-file etcd.conf.yml> log.txt
```
 
I use golang 1.13.8

Set it to GOPATH in c:\godir

Note: The directory must be stored in accordance with the agreed method, such as

C:\godir\src\github.com\nebula-chat\chatengine

Otherwise, the library will not be found when compiling,

Go get / go build according to the manual one by one

Then change the address of each configuration file.

 

Starting each file is cumbersome, so make a batch file to start each EXE.

 
## Note
Note: The current open source version supports the 1.0 protocol, so when compiling the client, you need to follow the instructions of nubela, checkout to the specified version to patch and compile.

 Supports group, but does not support channel and secret chat.

The enterprise version (paid version) supports the current new functions. If you need it, contact the author on your own telegram.


For specific source code analysis, see my other articles.

# [ Error ]  java.net.SocketException - Too many open files 분석

> 온라인 고객센터 발생 Issue 원인 분석

## 원인

- WEB Server(Apache 등)를 활용하여  웹 서비스를 운영 시,
                                            **동접자가 많은 경우**,  구동되는 **process 수**와 **해당 process가 처리하게 되는 파일 수** 또한 증가하며 발생한 Error.
- 시스템이 많은 파일과 소켓을 사용하는 경우, 시스템 오동작 (설정 값을 넘어가면 open() 시스템 콜에서 'Too many open files' 에러를 발생 시킴)
                                        - 많은 파일 : 프로세스가 가질 수 있는  파일 개수을 의미
                                        - 소켓 : Java에서 소켓 통신(HTTP API, JDBC 커넥션 등)을 의미
                                             - 즉, open file =  process + socket 

```bash
톰캣 에러 로그 

2021-11-16 11:57:29 INFO  o.a.c.httpclient.HttpMethodDirector - I/O exception (java.net.SocketException) caught when processing request: 열린 파일이 너무 많음
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:333)
        at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:190)
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:157)
        at org.springframework.transaction.interceptor.TransactionInterceptor$1.proceedWithInvocation(TransactionInterceptor.java:99)
        at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:281)
        at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
        at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:92)
        at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
        at org.springframework.aop.interceptor.AsyncExecutionInterceptor$1.call(AsyncExecutionInterceptor.java:115)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
Caused by: java.io.FileNotFoundException: /home/cscenter/tomcat/webapps/ROOT/WEB-INF/lib/spring-tx-4.3.0.RELEASE.jar (열린 파일이 너무 많음)
        at java.util.zip.ZipFile.open(Native Method)
        at java.util.zip.ZipFile.(ZipFile.java:225)
        at java.util.zip.ZipFile.(ZipFile.java:155)
        at java.util.jar.JarFile.(JarFile.java:166)
        at java.util.jar.JarFile.(JarFile.java:130)
        at org.apache.tomcat.util.compat.JreCompat.jarFileNewInstance(JreCompat.java:197)
        at org.apache.tomcat.util.compat.JreCompat.jarFileNewInstance(JreCompat.java:182)
        at org.apache.catalina.webresources.AbstractArchiveResourceSet.openJarFile(AbstractArchiveResourceSet.java:308)
        at org.apache.catalina.webresources.AbstractSingleArchiveResourceSet.getArchiveEntry(AbstractSingleArchiveResourceSet.java:96)
        ... 45 more
```



## Solution

> 웹서버 구동 계정에 nofile의 limit 값을 늘려준다. 
>
> > *nofile : 해당 도메인(사용자, 그룹)이 오픈할 수 있는 최대 파일개수*

- 처리 1.  - limit값을 늘려주기 위해 현재 서버의 open files 개수 확인

  ```bash
  방법 1. 설정된 open file 값 확인하기
  $ ulimit -a | grep open  // 설정된 open file 값 확인하기
  -------------------------------------------------------------
   ex) open files                      (-n) 8192
  -------------------------------------------------------------
  
  방법 2. 설정된 open file 값 확인하기
  $ ulimit -n 
  -------------------------------------------------------------
   ex) 8192
  -------------------------------------------------------------
  
  방법 3. 늘릴 수 있는 최대 오픈 파일 수 확인 ('커널 파라미터' : fs.file-max, fs.file-nr)
  방법 3-1.
  $ cat /proc/sys/fs/file-max 
  : '열 수 있는 파일의 최대 수 확인'
  -------------------------------------------------------------
   ex) 94304
  -------------------------------------------------------------
  
  방법 3-2.
  $ cat /proc/sys/fs/file-nr :  
  : '(현재 열여있는 파일의 수 / 현재 열려 있으나 사용되지 않는 파일 수/ 열 수 있는 파일의 최대 개수 )'
  -------------------------------------------------------------
   ex)   10176   0   94304
  -------------------------------------------------------------
  
  ```
  
  ​	※ 크기 비교 :    ' /proc/sys/fs/file-max '      >=     '/proc/sys/fs/file-nr'     >=     'ulimit -n' 

  


- 처리 2.  - 서버 구동 사용자(user) - 파일 limit 늘리기

  
  - soft : 새로운 프로그램을 생성하면 기본으로 적용되는 한도
  - hard : 소프트한도에서 최대로 늘릴 수 있는 한도
  
    - soft <=  hard (주로 동일하게 설정)
  
  ```bash
  $ vi /etc/security/limits.conf
  
  -------------------------------------------------------------
  httpd soft nofile 524288
  httpd hard nofile 524288
  
  nginx soft nofile 524288
  nginx hard nofile 524288
  
  {사용자} soft nofile {변경할 오픈파일수}
  {사용자} hard nofile {변경할 오픈파일수}
  -------------------------------------------------------------
  
-- 파일 적용 갱신
  source /etc/security/limits.conf 

  -- 재로그인
  ```
  
  

--------

### 비고

- Linux를 비롯한 일반적인 Unix에서 Socket을 마치 File(Process)과 같은 취급을 함
  - open file =  process + socket 
  - 참고 : https://stackoverflow.com/questions/344203/maximum-number-of-threads-per-process-in-linux/344292#34429



- ### Java 와 Python 차이

  > Python은 soft 옵션까지 file 오픈 <> Java는 hard 옵션까지 file 오픈하는 차이가 있음

  - JVM 옵션 중 

    - -XX:+MaxFDLimit : Bump the number of file descriptors to max. (Relevant to Solaris only.)

      (파일 설명자 수를 최대값으로 범핑합니다(Solaris에만 해당).)

      ​	https://www.oracle.com/java/technologies/javase/vmoptions-jsp.html

      

    - openJDK 코드에서 MaxFDLimit  옵션이 true일 경우 setrlimit 메소드로 limit을 증가시킴

      https://github.com/unofficial-openjdk/openjdk/blob/c3f27ada97987466e9c6e33e02e676bd69b78664/src/hotspot/os/linux/os_linux.cpp#L4998

    - Java에서는 default값이 TRUE

      ### 즉, 리눅스 OS환경에서는 JDK 실행 시 자동으로 limit 사이즈를 증가시켜줌



- ##### 서버관련 프로세스관련 에러 정리

  - java.net.SocketException (Too many open Files)일 때 

    - 원인 : 시스템이 기준보다 많은 파일과 소켓을 사용하는 경우 

    - 해결책 : 

      - [open files] limit 확인 

      - nofile 값 limit 늘려주기

        ※ *nofile : 해당 도메인(사용자, 그룹)이 오픈할 수 있는 최대 파일개수*

    

  - java.lang.OutOfMemoryError (unable to create new native thread)일 때 

    - 원인 : 정해놓은 Thread 기준보다 더 많은 Thread를 생성할 때

    - 해결책 : 

      - [max user process] limit 확인 

        ※ *nproc : 해당 도메인(사용자, 그룹)의 최대 프로세스 개수* 



#### 참고자료

```markdown
### ulimit 이란?

ulimit는 프로세스의 자원 한도를 설정하는 명령
하나의 유저(shell, process)에 대해서 할당할 자원량의 한계를 정해줌으로써 
다중프로그램/사용자를 기본으로하는 리눅스 시스템에서 과부하를 막아주는 설정 파일 

soft한도,hard한도 두가지로 나뉨

- soft : 새로운 프로그램을 생성하면 기본으로 적용되는 한도
- hard : 소프트한도에서 최대로 늘릴 수 있는 한도

ulimit [옵션] 값 ( Centos , RHEL 기준)
-a : 모든 제한 사항을 보여줌.
-c : 최대 코어 파일 사이즈
-d : 프로세스 데이터 세그먼트의 최대 크기
-f : shell에 의해 만들어질 수 있는 파일의 최대 크기
-s : 최대 스택 크기
-p : 파이프 크기
-n : 오픈 파일의 최대수
-u : 오픈파일의 최대수
-v : 최대 가상메모리의 양
-S : soft 한도
-H : hard 한도
```



-----

※ 참고 링크

- https://techblog.woowahan.com/2569/
- https://meetup.toast.com/posts/54
- https://dev-syhy.tistory.com/68
- https://github.com/unofficial-openjdk/openjdk/blob/c3f27ada97987466e9c6e33e02e676bd69b78664/src/hotspot/os/linux/os_linux.cpp#L4998
- https://www.oracle.com/java/technologies/javase/vmoptions-jsp.html
- https://stackoverflow.com/questions/344203/maximum-number-of-threads-per-process-in-linux/344292#34429


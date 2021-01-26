 별도 위치의 jdk를 사용할 때 절대 경로 

```ini
-vm C:\Program Files\Java\jre1.8.0_181\bin\javaw.exe 
```



파일 인코딩 

```ini
-Dfile.encoding=UTF-8 
```



클래스 유효성 검사 생략, 그러나 나중에 어딘서 오류나는지 확인하기 위해 사용 추천  

```ini
-Xverify:none 
```



 jdk 버전으로 설정하면 속도 향상  

```ini
-Dosgi.requiredJavaVersion=1.8
```



JVM 시작히 힙 영역 크기 : 최소(ms), 최대(mx) 

```ini
-Xms128m  

-Xmx2048m 
```



Permanent(영구) 영역 : JVM 클래스와 메소드를 위한 공간, 'Out of Memory' 에러 발생시 크기 조절 = PermSize  ;

New/Young 영역 : 새로 생성된 개체들을 위한 공간 = NewSize  

Old 영역 : 만들어진지 오래된 객체들의 공간(New영역에서 이동) 

```ini
-XX:PermSize=64M  

-XX:MaxPermSize=512M 

-XX:NewSize=128M  

-XX:MaxNewSize=512M ;
```



 Heap Shrinkage를 수행하는 임계치를 지정한다. 예를 들어 이 값이 70이면 Heap의 Free 공간이 70% 이상이 되면 Heap 크기가 축소된다. MinHeapFreeRatio 옵션과 함께 Heap의 크기 조정을 담당한다. 기본값 70  

```ini
-XX:MaxHeapFreeRatio=70 ; 
```



병렬 GC 사용 

메모리가 충분하고 코어수 많을때 유리하다. 

```ini
-XX:+UseParallelGC  ;
```



CMS GC 사용  

응답속도가 중요할때 사용한다.  

GC Pause에 의한 사용자 응답시간 저하 현상을 줄인다.  

```ini
-XX:-UseConcMarkSweepGC  

-XX:+CMSIncrementalPacing  
```

 

G1 GC(Garbage-First Garbage Collector) 사용  

성능은 좋지만 더욱 안정화가 되었을때 사용하는 것이 좋다.  

 JDK 1.7.0_4 이후 사용하는것이 안정적  

```ini
-XX:+UnlockExperimentalVMOptions  

-XX:+UseG1GC  

-XX:MaxGCPauseMillis=10 
```



컴파일러의 소수점 최적화 기능을 작동시켜 빨라진다.  

```ini
-XX:+AggressiveOpts
```


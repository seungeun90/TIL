process 안에 연산은 

## os는 proess 에 cpu 와 ram(physical memory)  을 배정해주는데 
여기서 process 는 ram 을 직접 사용하지 않는다.  
ram 을 추상화해서 사용하는데 이를 vm(virtual memory) 이라고 한다. 

ram 1차 메모리 
hdd 2차 메모리

vm = ram+ hdd  두가지 종류의 메모리를 하나의 연속된 메모리로 추상화 한 것

process (작업)은 최소 1개의 스레드(연산)를 가진다.  
os은 vm 을 process 에 할당,  
process 에 속한 모든 스레드는 process 의 vm 로 공간이 제약된다.
 
 \
  ![default](/img/process.png)  


## 멀티스레드에는 동시성, 동기화라는 단어가 따라온다,

한 가구는 process,  
세대원은 thread,  
각 세대원의 방은 thread local storage,  
거실/화장실 공용공간은 heap s으로 비유할 수 있다.  

thread 를 나누지 않고 각 process 로 실행하지 않는 것은 각 OS 의 설계철학에 따라   
일을 분배할 때 multi thread 로 하느냐 multi process 로 처리하느냐 차이이다.  
window 는 thread 들에게 하나의 vm 을   
linux 는 각 thread 에 각각의 vm 을 할당한다.  
도커는 그런 점에서 리눅스에 더 적합하다고 할 수 있다.    
일의 특성에 따라 무엇이 더 효율적인 환경인지 다르다.

 \
  ![default](/img/vm.png)

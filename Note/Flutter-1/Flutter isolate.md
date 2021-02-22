<h2>Flutter isolate</h2>

<hr>

- 일반적인 프로그래밍은 순차적으로 작업을 처리한다. 
- 하나의 작업이 끝나야 다음 작업으로 넘어간다. 





1. Concurrency vs Parallelism



2. Synchronous vs Asynchronous



3. Non-blocking vs Blocking 



<hr>

> Isolate

- 모든 Dart 코드가 실행되는 곳으로 단일 스레드(Single Thread)가 이벤트 루프를 실행하고 있다. 
- 단일 스레드 내에 여러 개의 Isolate가 있는 형태 

- 일반적인 Thread와 유사한 개념이다. 

  - main isolate(thread)에서 무거운 작업으로 인해 performance나 반응성이 떨어진다면 다른 작업 thread를 만들어서 그곳에서 처리하게끔 하는 것이다. 

- isolate는 Single Thread이지만 Dart언어가 자체적인 비동기 프로그래밍을 지원하기 때문에 비동기 작업도 

  Event loop에 의해서 적절히 처리된다. 

- 그러나 기존 언어의 Thread와는 차이점이 존재한다. 

- 일반적인 Thread는 한 프로세스 내에서 메모리 영역의 **<i>"Code", "Data", "Heap"</i>** 영역을 공유하는 구조이다.
- 하지만 isolate는 이름처럼 말 그대로 "고립"


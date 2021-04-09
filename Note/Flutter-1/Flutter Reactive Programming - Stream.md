<h2>Flutter Reactive Programming</h2>

<hr>

<h2>1. Stream </h2>

<hr>

> What is Reactive Programming?

- 데이터 스트림과 변경 사항에 대한 Propagation를 중심으로 하는 프로그래밍
- 특정 동작이 일어난다면, 다른 부분에서도 이 특정 동작에 대한 반응 및 동적인 데이터 갱신을 하는 것이다.

- 반대되는 개념으로 Imperative Programming이 있다 

```dart
x = 1
y = 1
x + y = 2
x * y = 1
2 * x + y = 3
```

- Imperative Programming의 경우 x의 값을 2로 변경하면 연산의 결과인 x + y = 2과 같은 것들은 변하지 않는다.
- 일일이 직접 수정을 해줘야한다. 

- 그러나 Reactive Programming의 경우 x의 값을 2로 변경하는 순간 연산의 결과도 즉시 동시에 변경된다. 
- 값의 변경에 따라 반응하여 진행되는 것이다. 

<hr>

> Stream?

- 스트림은 데이터가 들어오고 나가는 파이프(pipe) 통로이다. 
- 함수에다가 리스너를 스트림에 연결을 한다. 
- 이 함수가 스트림에 구독(subscribe)을 해서 듣고 있을 때, 데이터가 오는 것이다. 
- 데이터가 들어오면 그 데이터를 처리한다. 
- 또 다른 작업을 처리하다가 데이터가 또 들어오면 그 데이터를 처리한다. 
- 구독을 하고 들어오는 데이터마다 데이터를 처리하는 것이다. 

- Future는 데이터를 단일적으로 데이터 "하나"만 처리하지만
- Stream은 list처럼 여러개의 데이터를 처리할 수 있다. 



- Stream은 한개의 Listener만 가질 수 있다. 
- 여러개의 Listener를 가지려면 Broadcast Stream을 사용하면 된다. 

- 구독이 안된 상태에서 데이터가 도착하면 Stream을 타고 들어오면 기다렸다가, 만약에 리스너가 구독을 하면
- 그 때 한꺼번에 데이터를 처리한다. 
- 에러 조차도 Stream을 타고 들어올 수 있다. 
- 에러가 들어왔을 때 에러를 처리하고 나서 Stream의 구독을 취소를 할 것인가 그래서 데이터를 더 이상 받지 않을 것인가, 아니면 계속 데이터를 받을 것인가에 대해 선택권을 준다. 

- Stream의 최고 장점인 "Manipulation"인 데이터가 도착했을 때 이 데이터를 바로 사용하기 전에 
- 중간에 데이터를 가공할 수가 있다. -> A라는 데이터가 Stream을 타고 들어왔는데 도착했더니 A`으로 도착함

- Stream을 통해 특정 데이터만을 받을 수가 있다. (제네릭) (그 이외의 데이터는 버림)
- 데이터가 도착했는데, 데이터들 중에 같은 데이터는 다 제거할 수가 있다. -> Distinct

<hr>

- 보통 UI의 변경작업을 setState() 메소드를 호출하는데, setState의 경우 동작하는 방식은
- build() 메소드를 호출하여, 즉 가장 위부터 전부 다 다시 그리는 것이다. 

- 그러나 Stream을 사용하면 위젯트리가 전부 그려지는게 아니라 Stream와 연결된 위젯만 다시 그려진다!

<hr>

> 실제 코드상에서 How?

```dart
Future<int> sumStream(Stream<int> stream) async{
    var sum = 0;
    await for(var value in stream){
        print(sum);
        sum += value;
    }
    return sum;
}
Stream<int> countStream(int to) async*{
    for(int i=1; i<= to; i++){
        await Future.delayed(const Duration(seconds : 1));
        yield i;
    }
}

main() async{
    var stream = countStream(10);
    var sum = await sumStream(stream);
    print(sum);
}
```





```dart
var transformer = StreamTransformer<int, String>.fromHandlers(handleData : (value, sink){
    sink.add("value : $value");
});

stream.transform(transformer).listen
```






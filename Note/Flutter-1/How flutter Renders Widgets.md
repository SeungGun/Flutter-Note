<h2>Flutter How flutter Reders Widgets</h2>

<hr>

- 위젯은 불변하지만, 위젯 트리는 변경 가능하다. 
- 위젯 트리에서 일부를 빼내고, 다른 위젯 구성으로 교체할 수 있다. 
- 하지만 위젯의 일부를 변경하기 위젯 트리 전체를 rebuild하는 것은 원하지도 않고 성능면에서 좋지 않다. 

**그렇다면 플러터는 어떻게 위젯 트리를 관리할까?**

> Three Trees of Flutter 

- 플러터에서는 하나의 트리(위젯트리)를 통해 위젯을 관리하는 것으로 보이지만 
- 실상 3가지의 트리로 구성되어 있다. 

```
Widget - Element - RenderObject
(Widget tree) - (Element tree) - (Render tree)
```

- 위젯 트리는 우리가 코드상에서 얼마든지 control할 수 있다. 
- 그러나 element tree와 render tree는 플러터가 내부적으로 control하는 것이다. 이 두개의 트리는 우리가 **만든 위젯 트리에 근거하여** 생성된다.
- 위젯 트리는 우리가 작성한 코드에 근거하여 플러터가 build 메소드를 호출해서 생성하는 것이다. 
- 이 위젯 트리는 하나의 구성일 뿐 직접적으로 화면에 그려지지는 않는다. 
- 그러므로 위젯 트리는 하나의 설계도역할로 플러터에게 화면에 이러한 순서와 모양으로 UI를 그려달라고 하는 역할이다. 



- 중요한 것은 Element tree로 이 Element tree는 중간에서 위젯트리와 Render트리를 연결하고 있다. 
- Element 트리는 플러터가 자동으로 우리가 만든 위젯트리에 근거하여 생성을 해주는 요소이며
- 위젯트리에 있는 모든 위젯 하나하나가 1대1로 Element tree와 링크되어있다. 



- Render tree는 직접적으로 화면에 그려주는 High Level System이다. 
- Element tree는 중간에서 Render tree가 실제적으로 렌더링하기 위해서 가지고 있는 render 객체와 1대1로 링크되어있다. 
- 눈으로 보이는 화면의 모든 요소들은 Render tree의 작업 결과이다. 
- 


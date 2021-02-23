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
```




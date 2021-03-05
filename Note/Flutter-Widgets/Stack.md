<h2>Flutter Widget</h2>

<hr>

<h2>Stack</h2>

<hr>

- Multi-child layout widget이다. 
- Row와 Column 혹은 Container기반의 레이아웃의 갑갑함을 해결하고
- 그리고 중복이 가능한 위젯을 지원한다.
- 즉, 이름처럼 위젯위에 위젯을 쌓고, 쌓는 중첩된 레이아웃을 지원해주는 위젯이다. 

- Stack 위젯의 children 속성을 통해 위젯들을 배치할 수 있다.
- 그럴 때, children 속성의 리스트에서 위에 있는(앞에 있는) 위젯은 아래로 깔리게 되고 그 다음 순차적으로 그 위에 위젯들이 깔리는 형식이다. 

- 위치 정렬을 설정해주지 않으면 각 하위 위젯요소들은 topStart로 default로 설정된다. 
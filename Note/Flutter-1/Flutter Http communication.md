<h2>Flutter Http communication with Rest API</h2>

<hr>

> Http method - CRUD

| method | function                                                     | example                |
| ------ | ------------------------------------------------------------ | ---------------------- |
| GET    | 데이터 읽기(Read), 검색(Retrieve)<br />form data를 URL에 포함 시킨다. (action URL - query string parameters) 요청에 body가 없음. 응답에 body가 있음. | 게시판 리스트 불러오기 |
| POST   | 새로운 리소스 생성(Create) 및 저장<br />추가적인 데이터를 body에 포함 시킨다. 응답에 body가 있음. | 회원가입, 로그인       |
| PUT    | 전체 데이터 수정(Update)                                     | 회원정보 전체 수정     |
| DELETE | 데이터 삭제(Delete)                                          | 회원정보 삭제          |
| PATCH  | 데이터 수정(Update)                                          | 회원정보 일부 수정     |



> Http Status Code (Header의 Entity header)

| code | state         | meaning                                                      |
| ---- | ------------- | ------------------------------------------------------------ |
| 1xx  | Informational | 요청 정보 처리 중                                            |
| 2xx  | Success       | 요청을 정상적으로 처리함                                     |
| 3xx  | Redirection   | 요청을 완료하기 위해 추가 동작 필요                          |
| 4xx  | Client Error  | 서버가 요청을 이해하지 못함 (클라이언트가 서버에 잘못된 요청을 했을 경우) |
| 5xx  | Server Error  | 서버가 요청 처리 실패함 (대부분의 에러 코드를 500 Error 처리) |

  

> Http Content-Type

- 헤더에 포함되는 속성; 리소스의 미디어 타입
- Application/x-www-form-urlencoded : HTML Form 형태
- Application/json : JSON 형태
- multipart/form-data : 파일 첨부
- text/* : 단순 html, css, js 파일 



<hr>

<h2>REST API</h2>

- Element들로 Resource, Method, Message 3가지로 구성

- name이 John인 사용자를 생성한다. 

  → 사용자 : 생성되는 resource

  → 행위 : method

  → name이 John인 사용자 : message

- HTTP POST, http://~~/users/{

  ​	"users" : {

  ​		"name" : "John"	

  ​	}

  }

https://bcho.tistory.com/953

https://meetup.toast.com/posts/92





<hr> 

<h2> Flutter에서의 사용</h2>

- Back-end는 php 사용

> 데이터 전송하기 POST

- Client

```dart
import 'package:http/http.dart' as http;

Future<void> _postRequest() async{
    String url = 'http://xxx/test1.php'; // 요청할 url
    
    http.Response response = await http.post(url, headers : <String, String>{
        'Content-Type' : 'application/x-www-form-urlencoded',
    },
        body : <String, String>{
            'user_id' : 'user_id_value',
            'user_name' : 'user_name_value',
            'user_age' : 'user_age_value'
        });
    // POST 방식으로 하기 때문에 body에 데이터를 같이 전송해줌. 헤더 정보와 url 넣어줌
    if(response.statusCode == 200){ // 요청 코드가 200, 즉, 요청에 성공했다면
        print('전송 성공');
    }
    else{
        print('문제 발생');
    }
}
```

- Server - test1.php

```php
<?php
$id = $_POST["user_id"]; // user_id_value 
$name = $_POST["user_name"]; // user_name_value
$age = $_POST["user_age"]; // user_age_value;

include "../db.php";
	
$sql = ("INSERT INTO test_table (id, name, age) VALUES ('$id', '$name', '$age')");

$result = mysql_query($sql);
echo mysql_error();
?>
```



> 데이터 가져오기 GET

- Client

```dart
import 'package:http/http.dart' as http;
Future<void> _getRequest() async{
    String uri = 'http://xxx/get_data.php'; // 데이터를 가져올 uri
    
    final response = await http.get(uri+'?id=user_id_value', header : <String, String>{
        'Content-Type' : 'application/x-www-form-urlencoded',
    });
    // get method로 요청 파라미터를 uri에 붙임 + 헤더 정보도 추가
    if(response.statusCode == 200){ // 요청 결과 코드가 200, 즉 성공이라면
        print(response.body); // 결과 내용 출력
   		// body에 결과 값이 들어 있음. 이 데이터를 가공하면 됨
    }
}
```

- Server - get_data.php

```php
<?php
include "../db.php"; // DB에 연결 (db.php는 DB에 연결하는 코드)

$id = $_GET["id"]; // GET METHOD로 값을 가져옴

$sql = ("SELECT age FROM test WHERE id = '$id'"); // DB에 query 실행
$result = mysql_query($sql); // 쿼리문 결과
echo mysql_fetch_row($result)[0]; // 결과 가공
echo mysql_error();

?>
```



- Response 객체 멤버
  1. body - 요청의 결과 값이 들어가 있음 검색결과, 데이터 전송 성공 여부, 추가로 화면에 뿌려지는 것들
  2. statusCode - http 요청 코드
  3. headers - 헤더 정보
  4. contentLength - 내용 길이

<hr>

- php에 존재하는 추가 기능

1. json_encode
2. curl
3. array
4. date
5. mysql_num_rows
6. str_replace
7. explode
8. sizeof
# ajax__prac

- json : 페이지 전환 없이 서버에서 데이터를 가져오는 방법(서버 -> 클라이언트)

- 클라이언트 -> 서버
    - GET : 통상적으로 데이터 조회(Read)
    - POST : 통상적으로, 데이터 생성(Create), 변경(Update), 삭제(Delete)

- GET 방식으로 데이터를 전달하는 방법
    - ? : 여기서부터 전달할 데이터가 작성된다는 의미
    - & : 전달할 데이터가 더 있다는 뜻
    - 예시 : google.com/search?q=아이폰&sourceid=chrome&ie=UTF-8
        > 위 주소는 google.com의 search 창구에 다음와 같은 정보를 전달한다 
        > q=아이폰 (검색어)
        > sourceid=chrome (브라우저 정보)
        > ie=UTF-8 (인코딩 정보)

- ajax는 jQuery를 import한 페이지에서만 작동한다.

- ajax 기본 골격
    $.ajax({
    type: "GET",
    url: "여기에URL을입력",
    data: {},
    success: function(response){
    console.log(response)
  }
})

url에 api를 입력하면 거기에 있는 모든 정보들이 response로 들어오게 되고 모든게 console에 찍히게 된다.

http://openapi.seoul.go.kr:8088/6d4d776b466c656533356a4b4b5872/json/RealtimeCityAir/1/99
이걸 url로 입력하고 아래처럼 치면
console.log(response['RealtimeCityAir']['row'][0])
중구에 관련된 미세먼지 정보가 나오게 된다.

$.ajax({
    type: "GET",
    url: "여기에URL을입력",
    data: {},
    success: function(response){
    let mise_list = response["RealtimeCityAir"]["row"]; 
    for (let i = 0; i < mise_list.length; i++) {
    let mise = mise_list[i];
    let gu_name = mise["MSRSTE_NM"]; 
    let gu_mise = mise["IDEX_MVL"]; 
    console.log(gu_name, gu_mise);
  }
})
이런식으로 반복문을 돌릴 수 있는 것을 정의로 담아두고 반복문을 돌려서 한개씩 모두 꺼내볼 수 있다.
그리고 변수 정의를 끝낸 시점에서 if문을 통해 원하는 값만 가지고 올 수 있기도 하다.
    - if (gu_mise < 70) {
        console.log(gu_mise);
    }
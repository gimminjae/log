이번 글에는 저번 글에 이어서 지도에 컨트롤러를 추가해 보려고 한다.
컨트롤러의 기능에는 지도의 타입을 스카이뷰로 변경할 수 있는 기능과 지도를 확대, 축소할 수 있는 기능이 있다.

# 지도에 컨트롤 올리기
먼저 '지도에 컨트롤 올리기' 코드를 보자
- [지도에 컨트롤 올리기](https://apis.map.kakao.com/web/sample/addMapControl/)

아래의 코드는 카카오에서 제공하는 샘플 코드에서 html을 제외한 코드이다.
```javascript
var mapContainer = document.getElementById('map'), // 지도를 표시할 div 
    mapOption = { 
        center: new kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
        level: 3 // 지도의 확대 레벨
    };

var map = new kakao.maps.Map(mapContainer, mapOption); // 지도를 생성합니다

// 일반 지도와 스카이뷰로 지도 타입을 전환할 수 있는 지도타입 컨트롤을 생성합니다
var mapTypeControl = new kakao.maps.MapTypeControl();

// 지도에 컨트롤을 추가해야 지도위에 표시됩니다
// kakao.maps.ControlPosition은 컨트롤이 표시될 위치를 정의하는데 TOPRIGHT는 오른쪽 위를 의미합니다
map.addControl(mapTypeControl, kakao.maps.ControlPosition.TOPRIGHT);

// 지도 확대 축소를 제어할 수 있는  줌 컨트롤을 생성합니다
var zoomControl = new kakao.maps.ZoomControl();
map.addControl(zoomControl, kakao.maps.ControlPosition.RIGHT);
```

여기서 다른 지도 구현 코드와 중복되는 코드들은 제외하고 컨트롤러를 추가하는데 필요한 코드만 뽑아내면 아래와 같다.
```javascript
// 일반 지도와 스카이뷰로 지도 타입을 전환할 수 있는 지도타입 컨트롤을 생성합니다
var mapTypeControl = new kakao.maps.MapTypeControl();

// 지도에 컨트롤을 추가해야 지도위에 표시됩니다
// kakao.maps.ControlPosition은 컨트롤이 표시될 위치를 정의하는데 TOPRIGHT는 오른쪽 위를 의미합니다
map.addControl(mapTypeControl, kakao.maps.ControlPosition.TOPRIGHT);

// 지도 확대 축소를 제어할 수 있는  줌 컨트롤을 생성합니다
var zoomControl = new kakao.maps.ZoomControl();
map.addControl(zoomControl, kakao.maps.ControlPosition.RIGHT);
```

이제 이 코드를 지난 글에서 다루었던 커스터마이징한 지도의 script에 추가하면 된다.
![](https://velog.velcdn.com/images/gimminjae/post/81ef4ac2-31dc-4a9d-863a-230a633a7972/image.png)

# 결과
![](https://velog.velcdn.com/images/gimminjae/post/9c34fd5f-01ae-48fc-ac0f-868f54e019ce/image.png)
다음과 같이 지도타입을 스카이뷰로 변경할 수 있고 확대, 축소를 간단히 할 수 있는 컨트롤러를 추가하였다.

이번 여행을 DAMDA 프로젝트를 진행하면서 전 글에서 '키워드로 장소 검색하여 표출하기'지도 라이브러리를 사용한 것을 포스팅하였다.

그 지도 라이브러리는 장소를 검색하여 자신의 플래너에 담는 기능을 구현하는데 사용되었다.
그럼 이제 그 담은 장소들을 플래너 상세 페이지에서 보여주어야 하는데, 각각 장소의 좌표를 받아서 처리할까 싶었지만, 카카오 맵 api에 주소로 장소 표시하기 샘플이 있어서 이것을 사용하기로 했다.

하지만 샘플은 하나의 장소만 표시 가능했기에 해당 일차의 모든 여행지를 마커로 표시하려면 api의 코드를 직접 수정해야 했다.
그리고 지도 범위 재설정도 해야했다.

이렇게 서비스를 위해 커스터마이징한 방법과 과정을 써보려 한다.

> 프로젝트와 관련지어서 설명하기엔 너무 장황하므로 간단한 장소 예제로 글을 작성할 것이다.

# 사용한 API
- [주소로 장소 표시하기](https://apis.map.kakao.com/web/sample/addr2coord/)
- [지도 범위 재설정하기](https://apis.map.kakao.com/web/sample/setBounds/)
- [여러 개 마커 표시하기](https://apis.map.kakao.com/web/sample/multipleMarkerImage/)

# 과정
## 주소로 장소 표시하기 코드 붙이기
- 주소로 장소 표시하기의 javascript + html 코드를 갖다 붙이고, 앱 키를 붙여넣는다.
![](https://velog.velcdn.com/images/gimminjae/post/f4212677-3844-4ab0-b759-b02f6a0f11b0/image.png)
결과는 이렇다 kakao스페이스 닷원의 주소가 기본 값으로 넣어져 있어 위와 같이 지도가 표시된다.

## 주소로 장소 표시하기 코드 분석
```java
<body>
<div id="map" style="width:100%;height:350px;"></div>

<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=53ca7ba233962018a7a8996d89d2622a&libraries=services"></script>
<script>
  var mapContainer = document.getElementById('map'), // 지도를 표시할 div
          mapOption = {
            center: new kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
            level: 3 // 지도의 확대 레벨
          };

  // 지도를 생성합니다
  var map = new kakao.maps.Map(mapContainer, mapOption);

  // 주소-좌표 변환 객체를 생성합니다
  var geocoder = new kakao.maps.services.Geocoder();

  // 주소로 좌표를 검색합니다
  geocoder.addressSearch('제주특별자치도 제주시 첨단로 242', function(result, status) {

    // 정상적으로 검색이 완료됐으면
    if (status === kakao.maps.services.Status.OK) {

      var coords = new kakao.maps.LatLng(result[0].y, result[0].x);

      // 결과값으로 받은 위치를 마커로 표시합니다
      var marker = new kakao.maps.Marker({
        map: map,
        position: coords
      });

      // 인포윈도우로 장소에 대한 설명을 표시합니다
      var infowindow = new kakao.maps.InfoWindow({
        content: '<div style="width:150px;text-align:center;padding:6px 0;">우리회사</div>'
      });
      infowindow.open(map, marker);

      // 지도의 중심을 결과값으로 받은 위치로 이동시킵니다
      map.setCenter(coords);
    }
  });
</script>
</body>
```
위의 지도 생성 코드를 나눠보면 
1. 지도가 표시될 div
2. 지도를 생성하는 부분
3. 주소를 좌표로 변환하는 객체
4. 위의 객체를 이용하여 주소를 좌표로 변환하고 그 좌표로 마커와 인포윈도우를 표시한다.

주소를 이용하여 여러개의 장소를 표시하려면 1, 2, 3의 코드는 반복될 필요가 없다.
4번만 우리가 추가할 장소 객체 배열의 수만큼 반복하면 되는 것이다.


## 장소의 정보들을 담을 positions 배열 생성
```java
  var positions = [
    {
      title: '카카오',
      address: '제주특별자치도 제주시 첨단로 242'
    },
    {
      title: '생태연못',
      address: '경기 남양주시 조안면 능내리 50'
    },
    {
      title: '근린공원',
      address: '경기 남양주시 별내면 청학로68번길 40'
    }
  ];
```

장소 객체 배열을 담은 positions 배열을 코드에 추가해준다.
![](https://velog.velcdn.com/images/gimminjae/post/12e24961-2b35-47ad-8516-075140a5569b/image.png)

## forEach 이용하여 여러개 마커 표시하기
몇 줄의 코드만 추가하면 된다.
위에 있던 4번의 과정을 forEach로 돌리면 된다.
아래의 코드로 확인하자.
```
<body>
<div id="map" style="width:100%;height:350px;"></div>

<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=53ca7ba233962018a7a8996d89d2622a&libraries=services"></script>
<script>
  var mapContainer = document.getElementById('map'), // 지도를 표시할 div
          mapOption = {
            center: new kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
            level: 3 // 지도의 확대 레벨
          };

  // 지도를 생성합니다
  var map = new kakao.maps.Map(mapContainer, mapOption);

  // 주소-좌표 변환 객체를 생성합니다
  var geocoder = new kakao.maps.services.Geocoder();

  var positions = [
    {
      title: '카카오',
      address: '제주특별자치도 제주시 첨단로 242'
    },
    {
      title: '생태연못',
      address: '경기 남양주시 조안면 능내리 50'
    },
    {
      title: '근린공원',
      address: '경기 남양주시 별내면 청학로68번길 40'
    }
  ];

  positions.forEach(function (position) { //추가한 코드
    // 주소로 좌표를 검색합니다
    geocoder.addressSearch(position.address, function(result, status) {

      // 정상적으로 검색이 완료됐으면
      if (status === kakao.maps.services.Status.OK) {

        var coords = new kakao.maps.LatLng(result[0].y, result[0].x);

        // 결과값으로 받은 위치를 마커로 표시합니다
        var marker = new kakao.maps.Marker({
          map: map,
          position: coords
        });

        // 인포윈도우로 장소에 대한 설명을 표시합니다
        //변경한 코드
        var infowindow = new kakao.maps.InfoWindow({
          content: '<div style="width:150px;text-align:center;padding:6px 0;">' + position.title + '</div>'
        });
        infowindow.open(map, marker);

        // 지도의 중심을 결과값으로 받은 위치로 이동시킵니다
        map.setCenter(coords);
      }
    });
  });
</script>
</body>
```
위와 같이 코드를 수정하면
마커는 모두 표시되나, 처음에는 한가지 장소의 마커를 중심으로 지도가 배치된다.
- 처음 화면
![](https://velog.velcdn.com/images/gimminjae/post/8672bf53-cdb6-4e9f-b195-60ad6bf35855/image.png)
- 축소시켰을 때
![](https://velog.velcdn.com/images/gimminjae/post/792ee5b6-fa2f-4f80-9ff6-404cc6f26cbc/image.png)

이제 이 문제를 해결하고자 '지도범위 재설정하기'의 코드를 일부 사용할 것이다.

## 지도 범위 재설정하기
지도 범위 재설정하기의 코드를 살펴보자
![](https://velog.velcdn.com/images/gimminjae/post/1a5ecda7-0304-48f2-81cd-7ceb58ec2226/image.png)

이미 있는 코드를 제외하고 우리가 필요한 코드는 다음과 같을 것이다.
- 지도를 재설정할 범위정보를 가지고 있을 객체 -> bounds
- marker 객체는 이미 있으므로 마커를 지도에 추가하는 marker.setMap(map); 함수
- bounds 객체에 좌표를 추가하는 함수 bounds.extend(points[i]);
- bounds 객체를 기준으로 지도 범위를 재설정하는 함수 setBounds()
```javascript
// 지도를 재설정할 범위정보를 가지고 있을 LatLngBounds 객체를 생성합니다
var bounds = new kakao.maps.LatLngBounds(); 

marker.setMap(map);

// LatLngBounds 객체에 좌표를 추가합니다
    bounds.extend(points[i]);
    
    function setBounds() {
    // LatLngBounds 객체에 추가된 좌표들을 기준으로 지도의 범위를 재설정합니다
    // 이때 지도의 중심좌표와 레벨이 변경될 수 있습니다
    map.setBounds(bounds);
}
```

이제 이  코드들을 아래와 같이 적절히 추가해주면 된다.
```
<body>
<div id="map" style="width:100%;height:350px;"></div>

<script type="text/javascript" src="//dapi.kakao.com/v2/maps/sdk.js?appkey=53ca7ba233962018a7a8996d89d2622a&libraries=services"></script>
<script>
  var mapContainer = document.getElementById('map'), // 지도를 표시할 div
          mapOption = {
            center: new kakao.maps.LatLng(33.450701, 126.570667), // 지도의 중심좌표
            level: 3 // 지도의 확대 레벨
          };

  // 지도를 생성합니다
  var map = new kakao.maps.Map(mapContainer, mapOption);

  // 주소-좌표 변환 객체를 생성합니다
  var geocoder = new kakao.maps.services.Geocoder();

  var positions = [
    {
      title: '카카오',
      address: '제주특별자치도 제주시 첨단로 242'
    },
    {
      title: '생태연못',
      address: '경기 남양주시 조안면 능내리 50'
    },
    {
      title: '근린공원',
      address: '경기 남양주시 별내면 청학로68번길 40'
    }
  ];

  // 지도를 재설정할 범위정보를 가지고 있을 LatLngBounds 객체를 생성합니다
  var bounds = new kakao.maps.LatLngBounds(); //추가한 코드

  positions.forEach(function (position) {
    // 주소로 좌표를 검색합니다
    geocoder.addressSearch(position.address, function(result, status) {

      // 정상적으로 검색이 완료됐으면
      if (status === kakao.maps.services.Status.OK) {

        var coords = new kakao.maps.LatLng(result[0].y, result[0].x);

        // 결과값으로 받은 위치를 마커로 표시합니다
        var marker = new kakao.maps.Marker({
          map: map,
          position: coords
        });
        marker.setMap(map); //추가한 코드

        // LatLngBounds 객체에 좌표를 추가합니다
        bounds.extend(coords); //추가한 코드, 현재 코드에서 좌표정보는 point[i]가 아닌 coords이다.

        // 인포윈도우로 장소에 대한 설명을 표시합니다
        var infowindow = new kakao.maps.InfoWindow({
          content: '<div style="width:150px;text-align:center;padding:6px 0;">' + position.title + '</div>'
        });
        infowindow.open(map, marker);

        // 지도의 중심을 결과값으로 받은 위치로 이동시킵니다
        // map.setCenter(coords); //제거한 코드
        setBounds(); //추가한 코드
      }
    });
  });
  function setBounds() { //추가한 함수
    // LatLngBounds 객체에 추가된 좌표들을 기준으로 지도의 범위를 재설정합니다
    // 이때 지도의 중심좌표와 레벨이 변경될 수 있습니다
    map.setBounds(bounds);
  }
</script>
</body>
```
결과는 아래와 같다.
![](https://velog.velcdn.com/images/gimminjae/post/613e698b-0e2c-498d-9b82-70f98f729a5d/image.png)

지도가 로드될 때 표시되는 마커의 위치에 따라 지도의 범위가 적절하게 재설정된다.


# 정리
이렇게 '주소로 장소 표시하기' api에 여러 개 마커를 표시하고 지도 범위를 마커들의 위치에 따라 재설정하는 기능들을 추가해 보았다.

난 javascript도 잘 모르고, 관련 정보들도 거의 없었다.
그래서 난 많은 시도와 시행착오를  통해 위와 같은 결과를 냈다.
이 글을 보고 나와 같은 것을 구현하려는 분들에게 조금이나마 도움이 되었으면 좋겠다.

다음 글에는 지금까지 커스터마이징한 지도에 지도뷰를 변경하거나 확대 축소를 편하게 할 수 있는 컨트롤러를 추가하는 과정을 작성하려 한다.

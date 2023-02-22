# 개요
이번 프로젝트에서 나는 플래너 설계 기능을 맡았다.
우선 여행을 계획하려면 장소를 검색하고, 그 장소가 어디인지 지도상에 나타나야지만 여행을 계획할 수 있다.
그래서 우리 팀은 지도를 카카오 맵 API를 채택했다.

이유는 단순하다.
사람들에게 친숙하고, 개발자가 사용하기에도 편하기 때문이다.
이 글에서는 카카오 맵 API를 자신의 프로젝트에 적용하는 방법을 써보고자 한다.

# Kakao Developers
![](https://velog.velcdn.com/images/gimminjae/post/9772fc73-5bb3-43ea-bd52-5f56086380a4/image.png)
카카오개발자 사이트이다.
이 사이트를 활용해 화면에 보이는 카카오 로그인, 소셜, 메시지, 지도, 검색, 그 이외에도 정말 유용하고 많은 API가 있다.

# 로그인 및 애플리케이션 생성
먼저 카카오 계정으로 로그인을 한다.(매우 간단)

그리고 상단의 내 애플리케이션으로 들어가 앱을 하나 생성한다.
![](https://velog.velcdn.com/images/gimminjae/post/75e14629-cdb1-45fb-9d90-f409556ad118/image.png)

앱이름과 사업자명을 적고 생성한다.
![](https://velog.velcdn.com/images/gimminjae/post/34018ceb-b02f-40e0-ab4e-60458aa9e2ff/image.png)
그리고 그 앱을 클릭해서 들어가면 위와 같은 페이지가 뜬다.
> 여기서 중요한 것은 앱키는 웬만하면 공개되지 않도록 하는 것이 좋다.
필자는 위 앱을 바로 삭제할 것이기에....

# 플랫폼 설정
좌측의 앱 설정에서 플랫폼으로 들어가 아래와 같이 도메인을 설정해준다.
필자는 로컬서버에서, 그리고 웹을 사용할 것이므로 웹의 http:/localhost:8080으로 하겠다.
![](https://velog.velcdn.com/images/gimminjae/post/2b51330d-f790-4ab8-b3f0-edeaef8c35bd/image.png)
도메인은 쵀대 10개까지 등록이 가능하다.
# 지도 유형 선택
그럼 이제 사용할 지도를 골라보자.
페이지 헤더의 큐브모양을 눌러 Maps API로 들어가자.
![](https://velog.velcdn.com/images/gimminjae/post/2fb19c8e-e8e9-4115-a23a-2d1a99201dfb/image.png)
그럼 아래와 같은 페이지로 이동한다.
필자는 web을 사용할 것이므로 web을 선택하겠다.
![](https://velog.velcdn.com/images/gimminjae/post/58353f1d-0ec5-4511-9825-932da33c4e39/image.png)
카카오 맵 API에서는 사용자가 쉽게 지도를 사용할 수 있도록 아래와 같은 wizard 기능과 sample지도 를 제공한다.
wizard화면에서 자신이 넣고 싶은 기능을 넣어 아래의 코드를 복사해 붙여넣기만 하면 그대로 사용이 가능하다. (샘플지도도 마찬가지)
![](https://velog.velcdn.com/images/gimminjae/post/22e25079-25c2-4680-b5be-4d9559f7a764/image.png)
![](https://velog.velcdn.com/images/gimminjae/post/10a6156f-c6ac-49d8-b0f5-383a85cb8d73/image.png)
필자는 지도 라이브러리 중 '키워드로 장소검색하고 목록으로 표출하기'를 사용하고자 한다.

# 지도 사용하기
![](https://velog.velcdn.com/images/gimminjae/post/3e500f64-9c36-4ded-a6fa-5de3e1b250a5/image.png)
그럼 이제 사이트 아래의 코드를 복사한다.
> 지도를 보여줄 html태그 요소가 있다면 javascript만 복사해 붙이면 된다.

![](https://velog.velcdn.com/images/gimminjae/post/f063d50d-bbcd-4f10-9f06-c3f8c3155cd4/image.png)
이제 이 코드를 프로젝트의 파일에 붙여넣기만 하면 된다.
![](https://velog.velcdn.com/images/gimminjae/post/4315bd82-fa9f-47e6-8214-9264a9daa809/image.png)
> 여기서 신나서 바로 실행시키면 지도가 나오지 않아 실망할 것이다..ㅋㅋ

코드의 앱키에 자신의 앱키를 넣어주어야 한다.
![](https://velog.velcdn.com/images/gimminjae/post/44e48e00-b5be-4758-8f18-6a535770ecb1/image.png)
![](https://velog.velcdn.com/images/gimminjae/post/6ef40de3-e896-4d3c-8bc2-3de1290230fb/image.png)
요자리에 이렇게 자신의 javascript앱키를 붙여주고 다시 실행시키면
![](https://velog.velcdn.com/images/gimminjae/post/82cd2e59-b6a9-44e3-be41-5cc579859847/image.png)
아래와 같이 지도가 표시된다.


오늘은 카카오 지도 api를 자신의 프로젝트에 적용하는 방법을 알아봤다.



Spring Boot를 사용하는 사람이라면, 스프링 컨트롤러에서 model로 html에 정보드을 넘겨주고 html에서 그 정보들을 사용하게 할 것이다.
난 프로젝트를 하면서 model에서 넘겨준 정보들을 javascript에서 사용해야 하는 경우가 많이 있었다.
그래서 질문과 구글링을 통해 두 개의 방법을 찾았다.
# 예제 코드
먼저 설명 전에 예제 코드를 간단하게 살펴보자.
> 예제코드에서는 thymeleaf, lombok을 사용한다.

- article 객체
```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class Article {
    private String subject;
    private String content;
    private LocalDateTime createDate;
}
```
- url 매핑
```java
@Controller
public class HomeController {

    @GetMapping("/test1")
    public String test1(Model model) {
        Article article = new Article("파이썬 vs 자바", "파이썬과 자바 중 어떤 언어가 코딩테스트에 유리할까?", LocalDateTime.now());
        model.addAttribute("article", article);
        return "article_detail";
    }
}
```
- article_detail.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
</head>
<body>
<h1 th:text="${article.subject}"></h1>
<br>
<div th:text="${article.content}"></div>
<br>
<div th:text="${article.createDate}"></div>
</body>
</html>
```
- localhost:8080/test1 접속시
![](https://velog.velcdn.com/images/gimminjae/post/69af572a-d55b-4422-9721-6e34939aec4d/image.png)
다음과 같은 페이지가 로드된다.

여기서 자바스크립트를 통해 위의 정보들을 alert창으로 띄워보자.
article_detail.html에 script문을 추가하자
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
</head>
<body>
<h1 th:text="${article.subject}"></h1>
<br>
<div th:text="${article.content}"></div>
<br>
<div th:text="${article.createDate}"></div>
<button onclick="articleMessage()">버튼</button>
<script>
    function articleMessage() {
        //article의 정보를 alert창으로 표시한다.
        // alert();
    }
</script>
</body>
</html>
```
이제 model로 넘겨받은 정보를 스크립트문 안에서 사용할 수 있게 해주면 된다.
# 첫 번째 방법
> 첫 번째 방법은 jQuery를 사용하므로 아래의 코드를 html내에 추가해 jQuery를 사용할 수 있도록 해야한다.

```javascript
<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>

```

첫 번째 방법은 아래의 코드를 이용하는 것이다.
```javascript
//script문에 추가
var article_subject = $('input[name=article_subject]').val();

//html에 추가
<input type="hidden" name="article_subject" th:value="${article.subject}">
```

위에 있는 코드는 script문에 추가하는 코드로 article_subject라는 이름의 변수에  html내에서 name이 article_subject인 태그의 value값을 저장한다는 의미이다.

아래의 코드 input태그는 type이 hidden이므로 html내의 아무 곳에나 넣어주면 된다.
- 변경된 코드
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
</head>
<body>
<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<input type="hidden" name="article_subject" th:value="${article.subject}">
<h1 th:text="${article.subject}"></h1>
<br>
<div th:text="${article.content}"></div>
<br>
<div th:text="${article.createDate}"></div>
<button type="button" onclick="articleMessage()">버튼</button>
<script>
    var article_subject = $('input[name=article_subject]').val();
    function articleMessage() {
        //article의 정보를 alert창으로 표시한다.
        alert('제목 : ' + article_subject);
    }
</script>
</body>
</html>
```
- 결과
![](https://velog.velcdn.com/images/gimminjae/post/1b02a03e-0576-406e-8ac6-e57c806b3b68/image.png)
- 주의 사항
article.subject같은 특정 값이 아닌 article객체 자체를 방금과 같은 방식으로 사용하면 안된다.
만약 아래의 코드와 같이 article 객체를 받아 처리하려고 하면 아래의 이미지와 같이 객체가 문자열화되지 않고 그대로 출력되고, 다른 값들도 undefined가 출력되게 된다.
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
</head>
<body>
<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<input type="hidden" name="article" th:value="${article}">
<h1 th:text="${article.subject}"></h1>
<br>
<div th:text="${article.content}"></div>
<br>
<div th:text="${article.createDate}"></div>
<button type="button" onclick="articleMessage()">버튼</button>
<script>
    var article = $('input[name=article]').val();
    function articleMessage() {
        //article의 정보를 alert창으로 표시한다.
        alert('article : ' + article + '제목 : ' + article.subject);
    }
</script>
</body>
</html>
```

![](https://velog.velcdn.com/images/gimminjae/post/21927787-e74e-465c-b93c-6b610dea7c84/image.png)

# 두 번째 방법
> 두번째 방법은 더 간단하고 심지어 객체도 받아 사용할 수 있다.

- 먼저 script문의 태그 앞부분에 다음과 같이 코드를 추가해준다.
```
<script th:inline="javascript">
//생략
</script>
```
- spring의 컨트롤러에서는 Article객체를 article이라는 이름으로 html내에서 사용할 수 있도록 넘겨주었다. script문 내에 다음과 같이 변수를 선언해주고 [[${____}]]안에 값을 넣어서 저장해주면 된다.
```
<script th:inline="javascript">
var articleObject = [[${article}]];
</script>
```
- 이렇게만 해주면 다음과 같은 코드에서 아래의 이미지와 같은 결과를 얻을 수 있다.
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Article</title>
</head>
<body>
<h1 th:text="${article.subject}"></h1>
<br>
<div th:text="${article.content}"></div>
<br>
<div th:text="${article.createDate}"></div>
<button type="button" onclick="articleMessage()">버튼</button>
<script th:inline="javascript">
    var articleObject = [[${article}]];

    function articleMessage() {
        //article의 정보를 alert창으로 표시한다.
        alert('article : ' + articleObject
            + '\n제목 : ' + articleObject.subject
            + '\n내용 : ' + articleObject.content
            + '\n시간 : ' + articleObject.createDate);
    }
</script>
</body>
</html>
```

![](https://velog.velcdn.com/images/gimminjae/post/23b286a5-4d54-4d5b-81f9-29af4120df8c/image.png)

# 정리
오늘은 spring boot에서 model로 html에 넘겨준 정보들을 javascript내에서 사용할 수 있도록 해주는 두 가지 방법에 대해서 글을 써보았다.

내가 정보를 얻은 사이트도 밑에 올려 놓을테니 참고하면 좋을 듯하다.
- [StackOverFlow](https://stackoverflow.com/questions/25687816/setting-up-a-javascript-variable-from-spring-model-by-using-thymeleaf)

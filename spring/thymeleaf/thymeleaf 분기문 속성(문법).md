# 개요
기본적인 형태는 th:action, th:each, th:text ... 등의 형태이다.
기존의 문법에 th:만 붙여주면 된다.
# 종류
- th:action
- th:each
- th:text
- th:href
- th:if
...더 있지만 이 글에서는 자주 사용되는 것만 다루도록 하겠다.

# Ex)
## Controller
컨트롤러에서 5개의 글을 생성해 model로 값을 넘겨준다.
```java
@Controller
public class HomeController {
    @GetMapping("/article/list")
    public String list(Model model) {
        List<Article> articleList = new LinkedList<>();
        for(long i = 1; i <= 10; i++) {
            articleList.add(new Article(i, i + "번째 제목", i + "번째 내용", LocalDateTime.now()));
        }
        model.addAttribute("articleList", articleList);
        return "article_list";
    }
}
```
## article_list.html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>article_list</title>
</head>
<body>
<h1 th:text="|글 개수 : ${#lists.size(articleList)}|"></h1>
<table>
    <thead>
    <tr>
        <th>번호</th>
        <th>제목</th>
        <th>내용</th>
        <th>작성일시</th>
    </tr>
    </thead>
    <tbody>
    <tr th:each="article, loop : ${articleList}">
        <td th:if="${article != null}" th:text="${loop.count}"></td>
        <td>
            <a th:href="@{#}" th:text="${article.subject}"></a>
        </td>
        <td th:text="${article.content}"></td>
        <!--아래와 같이 작성할 수도 있다.
        <td>
          <a th:href="@{#}">[[${article.subject}]]</a>
        </td>
        <td>[[${article.content}]]</td>
        -->
        <td th:text="${#temporals.format(article.createDate, 'yyyy-MM-dd HH:mm')}"></td>
    </tr>
    </tbody>
</table>
</body>
</html>
```
## 결과
![](https://velog.velcdn.com/images/gimminjae/post/a207d2b9-7184-4852-9e35-dbd82cb42085/image.png)

## 간단 설명
- th:each
반복문이라고 이해하면 된다.
- th:href="@{...}"
링크를 넣을 수 있다.
- th:if="조건"
조건문이 참일 때만 해당 태그를 화면에 로드한다.
- th:text="${...}", [[\${...}]]
해당 텍스트를 표시한다.

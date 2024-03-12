- `@Builder`  : 빌더 패턴
    - 롬북에서 지원하는 어노테이션
    - 빌더 패턴 사용 시 객체를 유연하고 직관적으로 생성할 수 있기 때문에 개발자들이 애용하는 디자인 패턴
    
    ```java
    @Builder
    public Article(String title, String content) {
    		this.title = title;
    		this.content = content;
    }
    
    //빌더 패턴 사용 시
    Article.Builder()
    			.title("블로그 제목")
    			.content("내용");
    ```
    

- 엔티티 생성
    
    ```java
    @Getter
    @Entity
    @NoArgsConstructor
    public class Article {
    		@Id
    		@GeneratedValue(strategy = GenerationType.IDENTITY)
    		@Column(name = "id", updatable = false)
    		private Long id;
    	
    		@Column(name = "title", nullable = false)
    		private String title;
    	
    		@Column(name = "content", nullable = false)
    		private String content;
    	
    		@Builder
    		public Article(String title, String content) {
    				this.title = title;
    				this.content = content;
    		}
    }
    ```
    
- 레포지토리
    - JpaRepository 클래스 상속받을 때 Article과 엔티티의 PK 타입인 Long을 인수로 넣음
    
    ```java
    public interface BlogRepository extends JpaRepository<Article, Long> {
    }
    ```
    
<br></br>
## API 구현

- `DTO(Data transfer object)`
    - 데이터를 전달하기 위해 사용하는 전달자 역할 객체
    - toEntity()메소드는 빌더 패턴을 사용하여 DTO를 엔티티로 만들어주는 메소드
    
    ```java
    @NoArgsConstructor
    @AllArgsConstructor
    @Getter
    public class AddArticleRequest { 
    		private String title;
    		private String content;
    		
    		public Article toEntity() {	// 생성자를 사용해 객체 생성
    				return Article.builder()
    						.title(title)
    						.content(content)
    						.build();
    		}
    }
    ```
    
- `Service 코드 구현`
    - @Service 애노테이션을 사용하여 해당 클래스를 빈으로 서블릿 컨테이너에 등록
    - save() 메소드는 **`JpaRepository` 에서 지원하는 저장 메소드**

- `Controller 코드 작성`
    - URL 매핑 어노테이션 @GetMapping, @PostMapping, @PutMapping, @DeleteMapping 등을 사용
    - @RestController 애노테이션을 클래스에 붙이면, HTTP 응답으로 객체 데이터를 JSON 형식으로 변환
    - @RequestBody 애노테이션은 HTTP 요청할 때 응답에 해당하는 값을 @RequestBody 어노테이션이 붙은 대상 객체에 매핑

```java
@RestController	
public class BlogController {
		private BlogService blogService;
	
		public BlogController(BlogService blogService) {
				this.blogService = blogService;
		}
		
	
		@PostMapping("/api/articles")
		public ResponseEntity<AddArticleResponse> addArticle(@RequestBody AddArticleRequest request) { 
        Article article = articleService.saveArticle(request);
        AddArticleResponse savedResponse = article.toResponse();
        return ResponseEntity.status(HttpStatus.CREATED)
                .body(savedResponse);
		}
}
```
<br></br>
## 🌟 HTTP status 코드

- 200 OK : 요청이 성공적으로 수행되었음
- 201 Created : 요청이 성공적으로 수행되었고, 새로운 리소스가 생성됨
- 400 Bad Request : 요청 값이 잘못되어 요청에 실패했음
- 403 Forbidden : 권한이 없어 요청에 실패했음
- 404 Not Found : 요청 값으로 찾은 리소스가 없어 요청에 실패했음
- 500 Internal Server Error : 서버 상에 문제가 있어 요청에 실패했음
- 503 Service Unavailable : 서버가 요청을 받을 수 없는 상태

<br></br>
## 테스트 코드 작성

아래와 같은 양식으로 작성 !

| given | 블로그 글을 저장합니다. |
| --- | --- |
| when | 저장한 블로그 글의 id를 가져오고 삭제 API를 호출합니다. |
| then | 삭제 API 호출 응답이 200 ok인지 검증 후 실제 데이터가 삭제되었는지 확인합니다. |

```java
 @DisplayName("블로그 글 삭제 성공")
    @Test
    public void testDeleteArticle() throws Exception {
        // given
        final String url = "/api/articles/{id}";
        String title = "제목1";
        String content = "내용1";

        Article article = blogRepository.save(new Article(title, content));
        Long savedId = article.getId();

        // when
        mockMvc.perform(delete(url, savedId)).andExpect(status().isOk());

        // then
        List<Article> afterDeleteList = blogRepository.findAll();
        assertThat(afterDeleteList).isEmpty();
    }
```

<br></br>
## 타임리프

- 서버에서 데이터를 받아 HTML 웹페이지에 데이터를 넣어 보여주는 도구 : `템플릿 엔진`

타임리프 선언문

```java
<html xmlns:th="http://www.thymeleaf.org">
```

타임리프 표현식

| 표현식 | 설명 |
| --- | --- |
| ${…} | 변수의 값 표현식 |
| #{…} | 속성파일 값 표현식 |
| @{…} | URL 표현식 |
| *{…} | 선택한 변수의 표현식. th:object에서 선택한 객체 접근 |

타임리프 문법

| 표현식 | 설명 | 예제 |
| --- | --- | --- |
| th:text | 텍스트를 표현할 때 사용 | th:text=${person.name} |
| th:each | 컬렉션을 반복할 때 사용 | th:each=”person : ${persons}” |
| th:if | 조건이 true일 때만 표시 | th:if=”${person.age}>=20” |
| th:unless | 조건이 false일 때만 표시 | th:unless=”${person.age}>=20” |
| th:with | 변수값으로 지정 | th:with=”name=${person.name}” |
| th:object | 선택한 객체로 지정 | th:object=”${person}” |
| th:href | 이동 경로 | th:href=”@{/person(id=${person.id})}” |

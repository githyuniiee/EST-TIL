# HTML-2

# **여러가지 태그들**

- aside
    - 문서의 내용과 간접적으로 연관된 부분을 나타냄

## Contents 요소들

- h1, h2, h3, h4, h5, h6
    - Heading : 제목
    - level 별 제목
    - 숫자 클수록 소제목
    - 블록 레벨 요소

- a [anchor]
    - URL로 연결할 수 있는 하이퍼링크를 만듦
    - `href` : hypertext reference
        - tel, mailto
    
    ```jsx
    <a href="**mailto**:google@gmail.com">mailto:google@gmail.com</a>
    <a href="**tel**:010-0000-0000">010-1234-1234</a>
    ```
    
    - target 속성값
        - `_self` : default 값
        - `_blank` : 새로운 탭으로 이동 (별도의 새로운 창이 열림)
    - download
        - 링크 이동 대신 사용자에게 URL에 위치하는 대상을 저장할지
    
    ![image](https://github.com/githyuniiee/EST-learn/assets/109260733/4c4b606b-e80d-4384-bab5-080b953fb327)

    
- p
    - paragraph의  하나의 문단 나타냄
    - **하나의 완결된 문장일 경우 사용**

- strong
    - 굵은 글꼴, 강조
    - inline
    - p 태그 안에서 사용 가능
    - `<b>` 태그 🤔(더 이상 사용 x)

- br
    - break의 약어로 줄을 나눈다는 뜻
    - 줄 바꿈을 위해 사용
    - 

- hr
    - 단락 구분 시 사용
    - `<p>` 태그 내의 사용은 하지 않음
    - 실무에서는 거의 사용
    - ❌

- code
    - 프로그래밍 코드 나타낼 경우

- pre
    - html 작성 표현 그대로
    - 의미 없는..❌
    

## 목록 태그

- ol
    - ordered list의 약자로 **순서 있는 목록**
    - 보통 순위 표현 시에 많이 사용
        - `type` : 순서 어떤식으로 지정할건지 ⇒ 거의 사용 x
        - `start` : 어디서부터 시작할건지 ↔ `reverse`
        
- ul
    - unordered list로 **비순차적 목록**

- li
    - **ol, ul의 자식 요소로만 사용 가능**

## Media

- img
    - 문서에 이미지 삽입
    - `src` : 경로
    - `alt` : 대체 텍스트, 이미지에 대한 설명
    

<aside>
💡 인라인 요소 ⇒ 텍스트를 표현하기 위한 요소

</aside>

코드 리뷰 

- <time datetime="2023-04-24">2023.04.24</time>
- html <time> ⇒ 컴퓨터가 날짜 인식

# **양식(form)**

- 입력한 데이터를 제출, 전송하기 위해 사용하는 태그
- 별도 제출할 필요가 없으면 사용 X
    - `method` : 양식을 제출할 때 사용할 HTTP 메서드 ⇒ GET, POST
    - POST
        - client → server 로 보낼 경우(request)
        - 브라우저에 의해 캐시되지 않음 ⇒ 기록되지 않음
        - 쿼리 문자열과는 별도로 데이터 전송
        - 데이터의 길이 제한 X
            - `enctype` : encodingtype, 양식 제출 시 데이터의 MIME 타입을 나타냄
            - `**application/x-www-form-urlencoded**`: 기본값
            - `**multipart/form-data**`: `<input **type="file"**>`이 존재하는 경우 사용
    
    - GET
        - 쿼리 형식으로 데이터 정송
        - GET 방식의 HTTP 요청은 브라우저에 의해 캐시에 저장
        

- action 속성
    - 데이터를 전송할 서버의 주소
    - `<form action=””method=”post”>`
    - form 요청 경우(새로 고침됨→ 자바스크림트를 통해 막을 수 있음) ⇒ UI 구성 시 form이 필요할 경우
    - ajax 요청 경우 ⇒  form 요청 필요 없을 경우
    
- autocomplete 속성
    - 입력요소 기본 값으로 설정가능하게

## label

- input과 함께 사용
- 사용자 인터페이스 항목을 나타냄

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/c092d06b-adda-483b-ba3d-c72abcf9257f)


⇒ 두 가지 동시 활성화를 연결하기 위해 for와 id 사용 or label안에 input 넣기

## button

- `type = “button”` default
- `type = “reset”` form안에 있는 내용 초기화
- `type = “submit”`  form 안에 있는 데이터 서버로 전송 ⇒ form태그 안에서의 button은 default type submit

## input

- `<button~>` == `<input type =”button”>` : 어떤걸 더 많이 사용할까 🤔 ⇒ <button>은 닫는 태그가 있으므로 다른 속성 가용해 <button> 주로 사용

### fieldset

- from 관련 요소 묶을 때
- `legend` : 제목’

### textarea

- 여러 줄의 데이터를 입력받을 수 있게 사용하는 요소

# **table(표)**

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/7ccd49da-6ac0-4f6a-bc1f-f76376aa4e4d)


# table

- `tr` : 테이블의 행
- `th` : 항목에 대한 제목 (table header)
- `td` : 데이터
- `caption` : 테이블의 제목이나 설명 의미

- `thead, tbody, tfoot` ⇒ 테이블의 구역을 나누는 요소로 사용
- `colspan, rowsapn`  ⇒ 셀 병합
- `colgroup` ⇒ 테이블 열 그룹을 만들고 싶을 때 사용

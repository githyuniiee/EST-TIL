# HTML

## **HTML (Hyper Text Message Language)**

- 웹페이지가 어떻게 구조화되어 있는지 브라우저로 하여금 알 수 있도록 하는 마크업 언어

**HTML 기본**

- HTML은 여는 태그 닫는 태그로 구성되어 있음`<>` → 하나의 태그
- 주석 표시

```jsx
<!-- 주석 -->
```

- 부모, 형제, 자식, 자손

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/5291f6e4-9445-48ea-87d9-8d3930c92644)


**HTML 문서해부**

- `<!DOCYTYPE html>`
    - 기본 브라우저가 알아서 처리
    - 문서의 타입에 대한 정보 제공

- `<html lang= “en”>`
    - 페이지의 주 언어 설정

- `head`
    - 기계가 식별할 수 있는 문서 정보를 담음

- `charset`

```jsx
  <meta charset="utf-8">
```

 문서가 깨질 수 있으니 문자 코드 종류 설정

- `title`
    - 브라우저의 제목 표시줄이나 페이지 탭에 보이는 문서 제목 정의

- `link`
    - 현재 문서와 외부 리소스의 관계 명시

- `body`
    - 사용자에게 보이는 영역

**블록 레벨 요소 vs 인라인 요소**

- `block`
    - 한 라인을 혼자 차지 ! / 가능한 모든 너비 차지 !
    - 이전, 이후 요소 사이 줄바꿈
    - 페이지의 구조적 요소를 나타날 때 사용 ⇒ 블록 레벨 목적
    - 블록요소는 인라인 요소 안에 중첩 될 수 없지만, 인라인 요소는 블록 요소 안에 중첩 될 수 있음
    - div, p, form … 등이 있음
    - **<p> → 어떠한 문장을 표현하고 싶을 때 ⇒ 줄바꿈을 위한 태그는 아님 // 줄바꿈은 ⇒ <br>, <div> ⇒ 의미는 없지만, 안에 있는 내용 구별 위해**

- i`nline`
    - 블록 레벨 요소 내에 포함
    - width, height 크기를 지정할 수 없고, [padding, border, margin] ⇒ box model 속성을 사용할 수 있지만, 상하 margin 속성은 사용할 수 없음
    - a, label, input, span 등

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/99f3980e-2369-490c-8db2-817df7803f77)


**여러가지 태그들**

- `div`
    - 콘텐츠 **분할** 요소
    - 프론트앤드 개발에서는 div 태그 사용은 **스타일 적용을 위한 용도**로 사용할 것 권장
    - 의미가 X ⇒ 의미 없는 태그를 사용하는 것을 지양해야함!
    

브라우저는 알지 못하는 태그는 inline 요소로 처리 

inline 요소는 css 처리 x ⇒ 사용자의 의도와 다르게 layout이 나옴

naver는 어떤 사용자든(어떠한 브라우저에서 열든) 우리 페이지를 잘 보이게 하기 위해 `<div></div>`를 많이 썼음 !

- `span`
    - 인라인 요소
    - div와 같이 의미가 없음 ⇒ 되도록 사용 지양
    - css로 스타일을 주기 전까지는 영향 x

- `Sections`
    - header
        - head태그(화면에 보여지지 않는 내용)와 혼동 X
        - 중첩으로 사용하거나 헤더 안에 푸터 사용 X
    - nav
        - 네비게이이션 역할
        - 메뉴, 목차, 브레드크럼(사용자가 현재 페이지의 어디 위치에 있는지 파악하기 위해 사용)으로 사용
        
        ![image](https://github.com/githyuniiee/EST-learn/assets/109260733/dfd020d9-75ce-425c-8b54-7d183a7418ea)

        
        ⇒ 브레드크럼 (사용자가 어디에 있는지!)
        
        <ul>은 순서가 없는 목록
        
        <ol> (ordered list) ⇒ 순서가 있는 목록 ⇒ 브레드크럼에는 ol !
        
        - 페이지의 주요 탐생 링크를 위한 태그
        
    - `footer`
    
    기본 틀
    
   ![image](https://github.com/githyuniiee/EST-learn/assets/109260733/b37bcfc1-07d5-45c7-add4-001ff10d8619)

    
    -`main`
        - html에서 딱 1번 사용 가능
    
    - `article`
        - **독립적**으로 구분해 배포하거나 재사용할 수 있는 구획
        
    - `section`
        - 구획 나누는데 사용함 , 제목 요소를 자식으로 포함해야함 → ** 의미가 있어야 함 ** ⇒ div와의 차이
        
        ![image](https://github.com/githyuniiee/EST-learn/assets/109260733/1ecbcad3-56a6-4776-9e42-ac6824855196)

        
        ⇒ 로그인과 핫딜 어떻게 제목을 해야할까? 🤔
        
        → 이런 경우 `<div> </div>` (제목 달기 애매한 부분에 사용)
        

<a href = “#”> ⇒ 내부 링크로 이동

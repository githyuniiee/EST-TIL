# CSS 기본

## CSS란?

- Cascading Style Sheets의 약자
- CSS는 스타일 적용 시 우선순위대로 적용됨

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/f1ed4cea-fe73-4158-9b71-a094c490ace1)

⇒ 가장 높은 우선순위 CSS applied by the user

## 작성방법

```jsx
선택자 { 속성 : 속성값; }
```

## 주석

```jsx
/* 주석 */
```

## ex)

```jsx
<style>

h1 {
color : #008080;
}

</style>
```

# CSS 적용하기

## 인라인 방식

- 태그 자체에 style 속성으로 스타일 주기
- 인라인 방식으로는 잘 사용하지 않음
- :hover ⇒ 어떤 요소에 마우스 올렸을 때 [가상클래스], ::before, ::after와 같은 가상요소[html에는 존재하지 않지만 css로 만들 수 있음]에는 사용 불가

```jsx
<p style=”color:yellow;”>Hello</p>
```

## 내부 스타일

```jsx
**<style>
		p {
				color:yellow; 
				background-color:black;
		}
	</style>**
```

## 외부 스타일

`link`

- 현재 문서와 외부 리소스의 관계 명시
- css는 되도록이면 외부 파일로 분리해서 사용 ⇒ 각각의 언어 독립적 사용 위해
- `rel` : css 파일은 stylesheet
- `href` : 연결 시 참조할 파일 위치

```jsx
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>외부 스타일</title>
	**<link rel="stylesheet" href="style.css">**
</head>
```

# CSS 상속

## 상속을 이용하여 텍스트 모두 빨간색으로 바꾸기 👍

```jsx
<div>
	<h1>Hello</h1>
	<h2>Hello</h2>
	<p>Hello</p>
</div>
```

```jsx
div{
	color:red;
}
```

## 상속

- `width, height, margin, padding`(요소 내부의 크기), boder와 같은 것은 상속
    
    ⇒ 요소의 크기와 관련된 것들은 상속되지 않음 ! 
    
- `button, input` 요소와 같은 form 관련 태그들은 상속받지 않음
    
    ⇒ 브라우저별로 적용된 스타일이 있음
    
- `inherit` : 상속받게 함
- `initial` : 브라우저 기본 스타일 속성 따름

# CSS 선택자

## 전체 선택자

```css
*{ }
```

## 타입 선택자

- 특정 태그 전부 선택

```css
h1 {
	font-weight:bold;
}
```

## 아이디 선택자

- HTML 페이지 내에 id는 유일해야 함

```html
<header id="header">
...
</header>
```

```css
#header {padding:10px;}
```

## 클래스 선택자

- 클래스 신택자 `.`
- 한 페이지에 동일한 클래스 값을 여러 개 가질 수 있음 (아이디 선택자와의 차이), 재사용성 높음
- id, class는 숫자로 시작하면 안됨
- -, _, 문자로만 시작 가능

```css
<p class="fc-red">Lorem ipsum dolor sit amt</p>
```

```css
.fc-red {
	color: red;
}
```

## 특정 선택자

- HTML의 attribute
- `[]`
- 주어진 특성을 가진 모든 요소 선택

## 그룹 선택자

- `,`로 묶어 여러개 요소 동시 선택

## 복합 선택자

- 자손 선택자
    - 공백 () 으로 구분
    - 직계자손, 자손 모두 선택
    
    ```css
    section p {
      border: 3px solid skyblue;
    }
    ```
    

- 자식 선택자
    - `>`
    - 직계자손만을 선택 !
    
- 일반 형제 선택자
    - `~` 를 통해 구분
    - 뒤에 오는 형제만 선택

- 인접 형제 선택자
    - `+` 를 통해 구분
    - 바로 뒤에 있는 형제만 선택

## 가상 클래스 선택자

- 존재하지 않는 클래스르 마치 있는 것 처름 사용

### 가상 클래스

| :link | 방문하지 않은 링크 |
| --- | --- |
| :visited | 방문한 링크 |
| :hover | 마우스 커서를 올려 놓았을 때 |
| :active | 마우스로 클릭했을 때 |
| :focus | 포커스 되었을때 |

### 구조적 가상 선택자

 `**:firtst-child**`

`**:last-child**`

### `:nth-child` : CSS 함수

- 형제 사이의 순서에 따라

```css
div input:first-child{
border: 3px solid pink;
}
```

**⇒ 위와 같은 예시의 경우 div 첫번째 요소가 Input 이여야만 설정됨 !**

```css
div:first-child{
border: 3px solid pink;
}
```

**⇒ body의 첫번째가 div인 경우에 적용됨 !**

```css
/* 홀수번째 li */
li:nth-child(odd) {
  color: lime;
}
```

```css
ul li:nth-child(3){
border: 3px solid pink;
}
```

**⇒ ul의 3번째 자식을 선택할건데 3번째 자식이 li라면 background color 주겠다!**

- 인덱스가 1부터 !

**`:not` ⇒ 부정 선택자**

# CSS 선택자 우선순위

## 후자 우선의 원칙

- 뒤에 나오는 CSS가 우선순위가 높다.
- 가중치가 같을 경우 적용됨

## 구체성(명시도)의 원칙 :

- 선택자가 구체적일수록 우선순위가 높다. ⇒ 어떤게 더 구체적인가**🤔🤔**

| inline-style | 1000점 |
| --- | --- |
| id 선택자 # | 100점 |
| class ., 가상클래스, 속성선택자 | 10점 |
| 타입, 가상요소 선택자 | 1점 |
| 전체선택자 * | 0점 |
- inline-style을 잘 사용하지 않는 이유도 우선순위가 너무 높기에 다른 sytle 겹쳐서 사용 못하기에 !

## 중요성의 원칙

`!important`

: 다른 어떤 CSS의 선언 보다도 우선한다.

# display 속성

- 박스의 유형 결정
- `inline-block`  ⇒ width, height, margin, padding 값 모두 설정 가능
- `flex` : 정의된 요소의 자식들의 x or y축 둘 중 한 방향으로 위치 정렬하기 위한 속성
- `grid` : .. x,y축 모두 정렬 ⇒ 입체적인 레이아웃으로 가능


# CSS Box Model

- HTML 요소를 감싸는 상자
    - 요소 : HTML 그 자체 !
    - 패딩 : 요소 주변 영역
    - 테두리 : 요소와 패딩을 감싸는 테두리
    - 마진 : 테두리 밖의 영역 ⇒ 요소의 영역으로 포함하지 않음
- inline 요소는 width, heihgt, 상하 margin 값이 적용되지 않는다.

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/028e6879-0c10-4ec9-851c-aeb5cd1f70d9)


## padding

- 요소 내부의 여백을 줄 때 주로 사용

## margin

- box 모델의 요소의 가장 바깥 공간
- 요소 넓이의 공간에 포함되지 않는다.
- 요소와 요소 사이의 여백을 줄 때 주로 사용
- margin : auto ⇒ 요소 가운데 정렬
- margin auto는 수평 정렬만 지원

## 마진병합 현상

- 요소와 요소 사이의 margin-top 혹은 margin-bottom의 공간이 있는 경우 더 높은 값의 마진 값이 적용되는 현상

![image](https://github.com/githyuniiee/EST-learn/assets/109260733/b72b224e-dd20-4d43-b194-708388af8566)



마진병합 현상 해결방법

- 부모 요소에 `overflow` 속성 값을 적용
- 부모 요소에 `display: inline-block` 값을 적용
- 부모 요소에 `border` 값을 적용
- 부모 요소에 `display:flow-root`을 사용

## border

- 테두리 적용
- 요소의 크기에 영향을 미침

## box-sizing

- `content-box` : 기본값. width, height에 border, padding 포함하지 않음.
- `border-box`: width, height에 border, padding  포함.

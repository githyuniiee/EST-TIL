# form 관련 가상 클래스 선택자

## `:enabled`, `:disabled`

- 활성화 /비활성화 상태

## `:read-only`, `:read-write`

- 사용자가 편집할수 없는/있는 상태

## `:checked`

- input `checkbox` `radio` 유형일때 선택된 상태

## `:required`

- 필수입력값일 경우

## `**::placeholder**`

- 입력에 대한 추가 정보가 있을 경우

<br></br>
# positon

## position: static

- position 값 따로 속성값을 주지 않으면 static 값을 가짐
- html에 쓴 태그 순으로 위치가 지정 ⇒ 위치 지정 X
- 부모의 positon 속성은 static이여서는 안됨

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/7b8cc343-be18-4943-a433-a61aeaa8dfc9)


## position: relative

- position 속성이 있는 요소는 position 속성이 없는 요소를 가려버림
- 원하는 위치로 지정
- 기준점 : 자신이 원래 있던 위치
- left, top, bottom right와 같은 속성이 있음

## position: absolute

- 기준점 : 부모요소
- 부모가 없을 경우 html의 root요소가 기준
- normal flow(html에 쓴 태그 순으로 위치가 지정)에서 벗어나짐

⇒ position 속성은 잘 사용하지 않음

- positon 속성은 위치를 속성하기 위해 요소의 위치를 정하는데 있어 써야하는 문법이 많음 top, left, position..
- 유지보수에 용이하지 않기에 layout 맞출 시 사용하지 않음
- 그렇다면 언제 사용 ? 🤔 : 화면을 겹쳐야할 경우 position 속성 사용, 모달 창 만들어야할 때..

## position: fixed

- 페이지가 스크롤 되어도 중요한 정보를 화면에 계속 노출시켜주기 위해 사용하는 속성

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/515c9be8-49a6-43a6-81e4-5b50dc57b55d)


## position: sticky

- 조상에 스크롤이 있다면 가장 가까운 부모 요소의 컨텐츠 영역에 달라붙음

```css
<!DOCTYPE html>
<html lang="ko">
<head>
    <style>
        section {
            height: 1000px;
            border: 3px solid black;
        }

        h2 {
            position: -webkit-sticky; //webkit 기반 브라우저에서만 작동
            position: sticky; //특정 브라우저에서는 지원 안할 수 있음
            top: 0px;
            background: greenyellow;
            margin: 0;
        }
    </style>
</head>

<body>
    <h1>sticky test</h1>
    (section>h2{오늘의 메뉴$}+ul>(li>lorem)*3)*3
</body>

</html>
```

## position: z-index

- 요소와 요소가 겹쳐보이는 일이 발생할 때 어떤 요소가 더 위로 나타나게 할지 결정할 때 사용
- z-index 값이 큰 요소가 더 앞으로 나옴
- 부모는 z-index값을 아무리 높여도 자식을 덮을 수 없음
- 부모의 z-index는 자식의 z-index에 영향을 줌

<br></br>
# flex

# flex-container에 사용하는 속성

- `dilpay:flex`
- 자식 요소들이 컨테이너 안 공간을 맞추기 위해서 크기를 키우거나 줄이는 방법 설정하는 법
- 부모요소 ⇒ `flex-container`, 자식요소 ⇒ `fliex-item`
- 자식 x or y축으로 정렬 가능

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        ul{
            list-style: none;
            margin: 0;
            padding: 0;
            display: flex;
        }
        li{
            background-color: royalblue;
            border: 2px solid black;
        }
    </style>
</head>
<body>
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
</ul>

</body>
</html>
```

flex 설정했을 경우

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/f9ae10c2-f217-4eb2-9ab9-400ef80dd7f5)


flex 설정 안 했을 경우

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/e06be9b7-530c-4467-aaf9-db6b12ff1b2c)


![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/0fbd9368-421e-4268-b47c-047b17563b93)

## fliex-direction

- 컨테이너 내 아이템 배치할 때 주측 및 방향 지정
- `row-reverse` : 오른쪽에서 왼쪽
- `column-reverse`  : 아래에서 위

## justify-content

- 주축을 기준으로 배열 위치 조절 및 아이템간 간격 설정

`justify-content: flex-start` :flex-start 위치에 두겠다

`justify-content: space-between` : 자식과 자식간의 공간을 최대한으로 

`justify-content: space-around`  :  요소 사이 사이 동일하게 동일하게 제공

`justify-content: space-evenly` :  시작부터 사이의 간격을 똑같이 제공

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/0c0d241c-df75-49cb-9bea-ed793773dbdb)

- 위의 이미지 코드
    
    ```css
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>flex</title>
        <style>
            .wrap{
                width:500px;
                height: 500px;
                background-color: lightgray;
                display: flex;
                justify-content: space-between;
            }
            .blue, .green, .yellow{
                width: 50px;
                height: 50px;
                text-align: center; //가운데 정렬
                line-height: 50px; //줄의 높이 값 설정
            }
            .blue{
                background-color: royalblue;
            }
            .green{
                background-color: teal;
            }
            .yellow{
                background-color: greenyellow;
            }
            .left_side, .center, .right_side{
                display: flex;
                flex-direction: column;
                justify-content: space-between;
            }
            .right_side{
                flex-direction: column-reverse;
            }
        </style>
    </head>
    <body>
    <article class="wrap">
        <div class="left_side">
            <div class="blue">a</div>
            <div class="green">b</div>
            <div class="yellow">c</div>
        </div>
        <div class="center">
            <div class="blue">d</div>
            <div class="yellow">e</div>
        </div>
        <div class="right_side">
            <div class="blue">f</div>
            <div class="green">g</div>
            <div class="yellow">h</div>
        </div>
    </article>
    </body>
    </html>
    ```
    

## align-items, align-content

- `align-items`: 교차 축을 기준으로 정렬
- `align-content`: 컨테이너의 교차 축의 아이템들이 여러 줄일때 사용
    - `flex-wrap:wrap` 일 때 사용(컨테이너가 자식들을 감쌀때)

## gap

- 아이템 사이 간격 설정

<br></br>
# flex-item에 사용하는 속성

## flex-basis

- 초기 크기 설정
- 축의 방향에 따라 달라진다는 것과 내부 콘텐츠에 따라 유연한 크기를 가짐
- flex-basis 값이 적용된다면 row일 경우 width 값 무시!

## flex-grow

- flex-grow : 1 → 자식 요소들이 모두 동일한 크기의 공간 할당
- flex-grow  : 2(2이상의 수) →  **특정한 하나의 자식에게만 줄 경우** 다른 자식요소보다 두배(배수로)의 **여백 공간을 할당** 만약 자식요소들의 컨텐츠 크기가 존재한다면 그 컨텐츠의 넓이에 따라 할당받는 값이 달라짐
- flex-basis : 0은 여백 공간이 아닌 전체 공간을 분할

⇒ fliex-basis보다 커지게 해라!

## flex-shrink

⇒ fliex-basis보다 작아지게 해라!

- flex-shrnk 값 기본적으로 1
- 0일 경우 갑이 줄어들지 않음

## align-self

- 부모의 align-items(교차축에서의 위치 정함 ⇒ flex container에서 사용) 속성을 덮어 flex-item 개개인에게 속성 부여

## flex

- 단축속성
- `flex-grow` `flex-shrink` `flex-basis`

```css
flex: 1 1 100px;
```

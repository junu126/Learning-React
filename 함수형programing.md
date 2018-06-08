# 함수형 프로그래밍

함수형 프로그래밍은 1930년대부터 시작되었다. 그 당시 발견한 람다 계산법이 시작이라고 할 수있다.  
17세기에 함수가 등장한 이래 함수는 계속해서 계산법의 일부였다. 함수를 함수로 넘기거나 함수가 함수를 결과로 내놓는 것도 가능하다.  
다른 함수를 조작하고, 함수를 인자로 받거나 반환하는 것이 가능한 복잡한 함수를 **고차 함수** 라고 한다.  

1950년대 *존 맥카시*는 람다 계산법에서 비롯된 개념을 활용해 새로운 프로그래밍 언어를 개발하는데 이름은 **리스프**이다.  

> 리스프는 고차함수라는 개념과 함수가 1급 시민 혹은 1급 멤버라는 개념을 구현했다. 1급 시민이 되려면 변수에 함수를 대입할 수 있고, 함수를 다른 함수에 인자로 넘길 수 있으며, 함수에서 함수를 만들어서 변환할 수 있어야 한다.

## 함수형이란?
자바스크립트에서는 함수가 1급 시민이기 때문에 함수형 프로그래밍을 지원한다고 할 수 있다.  
1급 시민이라는 말은 함수를 정수나 문자열 같은 다른 일반적인 값과 마찬가지로 취급할 수 있다는 뜻이다.  
ES6에는 함수형 프로그래밍 기법을 더 풍부하게 해주는 화살표 함수, 프라미스, 스프레드 연산자 등이 있다. ( 'ES6소개' 참조 ).  

> 자바스크립트에서는 함수가 애플리케이션의 데이터를 표현할 수도 있다. 문자열이나 수 또는 다른 모든 값과 마찬가지로 var 키워드를 사용해 함수를 정의할 수 있다.

```js
var log = function(message) {
    console.log(message);
}

log("자바스크립트에서는 함수를 변수에 넣을 수 있습니다.");

// 자바스크립트에서는 함수를 변수에 넣을 수 있습니다.
```

ES6에서는 화살표 함수를 사용해 같은 함수를 정의할 수 있다. 함수형 프로그래머들은 작은 함수를 아주 많이 작성하기 때문에 화살표 함수 구문을 사용할 수 있으면 코딩이 훨씬 더 간편해진다.
```js
const log = message () => console.log(message);
```
앞의 두 문장은 같은 일을 한다. 두 문장 모두 함수를 log라는 변수에 넣는다.  
추가로 두 번째 문장에서는 const 키워드를 사용했기 때문에 log를 덮어쓰지 못하게 막아준다.  

함수를 변수에 넣을 수 있는 것과 마찬가지로 객체에 넣을 수도 있다.
```js
const obj = {
    message: "함수를 다른 값과 마찬가지로 객체에 추가할 수도 있습니다.",
    log(message) {
        console.log(message);
    },
}

// 함수를 다른 값과 마찬가지로 객체에 추가할 수도 있습니다.
```
심지어 함수를 배열에 넣을 수도 있다.
```js
cosnt messages = [
    "함수를 배열에 넣을 수도 있습니다.",
    message => console.log(mesage),
    "일반적인 값과 마찬가지입니다.",
    message => console.log(message)
];

message[1](message[0]) // 함수를 배열에 넣을 수도 있습니다.
message[3](message[2]) // 일반적인 값과 마찬가지입니다.
```
다른 값과 마찬가지로 함수를 다른 함수에 인자로 넘길 수도 있습니다.
```js
const insideFn = logger => {
    logger("함수를 다른 함수에 인자로 넘길 수도 있습니다.");
}

insideFn(message => console.log(message));

// 함수를 다른 함수에 인자로 넘길 수도 있습니다.
```
함수가 함수를 반환할 수도 있다. 이 또한 일반적인 값과 마찬가지다.
```js
var createScream = logger => message => 
    logger(message.toUpperCase() + "!!!");

const scream = createScream(message => console.log(message));

scream('함수가 함수를 반환할 수도 있습니다.');
scream('createScream은 함수를 반환합니다.');
scream('scream은 createScream이 반환한 함수를 가르킵니다.');

// 함수가 함수를 반환할 수도 있습니다!!!
// CREATESCREAM은 함수를 반환합니다!!!
// SCREAM은 CREATESCREAM이 반환한 함수를 가리킵니다!!!
```
마지막 두 예제, 즉 함수를 인자로 받거나 함수를 반환하는 함수를 **고차함수**라고 부른다. 

## 명령형 프로그래밍과 선언적 프로그래밍 비교
함수형 프로그래밍은 **선언적 프로그래밍**이라는 더 넓은 프로그래밍 패러다임의 한 가지다.  
선언적 프로그래밍은 필요한 것을 달성하는 과정을 하나하나 기술하는 것보다 필요한 것이 어떤 것인지 기술하는데 방점을 두고 애플리케이션의 구조를 세워나가는 프로그래밍 스타일이다.  

**명령형 프로그래밍**은 코드로 원하는 결과를 달성해 나가는 과정에만 관심을 두는 프로그래밍 스타일이다. 어떤 문자열을 URL에서 사용할 수 있게 만드는 일반적인 작업을 살펴보면.  
공백은 URL에서 사용할 수 있는 문자가 아니므로 문자열을 URL에서 사용할 수 있게 (URL 친화적으로) 만들려면 모든 공백()을 하이픈(-)으로 바꿔야 한다.  
다음은 명령형 프로그래밍에서의 예시다.
```js
var string = "This is the midday show with Cheryl Waters";
var urlFriendly = "";

for(var i = 0; i<string.lengrh; i++) {
    if (string[i] === " ") {
        urlFriendly += "-";
    } else {
        urlFriendly += string[i];
    }
}

console.log(urlFriendly);
```
이 예제는 문자열의 모든 문자를 루프를 돌면서 공백을 만날 때마다 그 공백을 -로 바꾼다. 이런 구조의 프로그램은 우리가 원하는 것을 달성하는 방법에만 신경을 쓴다.  
이와 같은 문제를 선언적으로 풀어보면
```js
const string = "This is the midday show with Cheryl Waters";
const urlFriendly = string.replace(/ /g, "-");

console.log(urlFriendly);
```
여기서는 string.replace와 정규식을 사용해서 모든 공백을 하이픈으로 변경한다. string.replace를 사용하면 모든 공백이 하이픈으로 변경되어야 한다는 사실을 기술할 수 있다.  

선언적 프로그래밍의 코드 구문은 어떤 일이 발생해야 하는지 기술하고, 실제로 그 작업을 처리하는 방법은 추상화로 아랫단에 감춰진다.  

선언적 프로그램은 코드 자체가 어떤 일이 벌어질지 설명하기 때문에 좀 더 추론하기 쉽다. 다음 코드는 API에서 멤버를 가져온 다음 어떤 일을 해야 하는지 자세히 기술한다.
```js
const loadAndMapMembers = compose(
    combineWith(sessionStorage, "members"),
    save(sessionStorage, "members"),
    scopeMembers(window),
    logMemberInfoToConsole,
    logFieldsToConsole("name.first"),
    countMembersForMapping,
    save(sessionStorage, "map"),
    rederUSMap
);

getFakeMembers(100).then(loadAndMapMembers);
```
선언적 접근 방식이 더 읽기 쉽고, 그래서 더 추론하기 쉽다. 각 함수가 어떻게 구현되었는지는 함수라는 추상화 아래에 감춰진다.  
각각의 작은 함수에는 그 함수가 하는 일을 잘 설명하는 이름이 붙어 있고, 그런 함수들이 조합된 방식을 보면 멤버 데이터를 불러와서 맵에 저장하고 출력하는 과장이 잘 드러난다.  

이제 문서 객체 모델(DOM)을 만드는 과정을 살펴보면,  
명령형 접근 방식은 다음과 같이 구축한다.
```js
var target = document.getElementById('target');
var wrapper = document.createElement('div');
var headline = document.createElement('h1');

wrapper.id = "welcome";
headline.innerText = "hello World";

wrapper.appendChild(headline);
target.appendChild(wrapper);
```
이 코드는 엘리먼트를 만들고, 설정하고, 문서에 추가한다. 이런 식으로 DOM이 구축된 1만줄 되는 코드를 변경하거나 새로운 기능을 추가하거나 규모를 확장하는 것은 아주 어려운 일이다.  

리액트 컴포넌트를 사용해 DOM을 선언적으로 구성하는 방법을 살펴보면
```js
const { render } = ReactDOM;

const Welcome = () => (
    <div id="welcome">
        <h1>Hello World</h1>
    </div>
)

render(
    <Welcome />,
    document.getElementById('target');
)
```
리액트는 선언적이다. 여기서 welcome 컨포넌트는 렌더링할 DOM을 기술한다.  
render 함수는 컴포넌트에 있는 지시에 따라 DOM을 만든다. 이 과정에서 실제 DOM이 어떻게 렌더링되는지에 대한 내용은 추상화로 사라진다.  
이 코드를 보면 welcome 컨포넌트를 ID가 target인 엘리먼트 안에 렌더링하고 싶어 하는 의도가 명확히 드러난다.

## 함수형 프로그래밍의 개념
함수형 프로그래밍의 핵심 개념인 불변성, 순수성, 데이터 변환, 고차 함수, 재귀를 소개하는 단원이다.
> 불변성
- 'mutate'는 변한다느 뜻이다. 따라서 'immutable'은 변할 수 없다는 뜻이다.  
함수형 프로그래밍에서는 데이터가 변할 수 없다. 불변성 데이터는 결코 바뀌지 않는다.

원본 데이터 구조를 변경하는 대신 그 데이터 구조의 복사본을 만들고 그중 일부를 변경한다. 그리고 원본 대신 변경한 복사본을 사용해 필요한 작업을 진행한다.

다음은 불변성이 어떻게 작동하는지 이해하기 위해 데이터를 변경한다는 것이 어떤 의미인지 살펴보는 예시이다.  
잔디 색을 표현하는 객체를 생각해보자.
```js
let color_lawn = {
    title: "잔디",
    color: "00FF00",
    rating: 0
};
```
다음과 같이 색에 평점을 매기는 함수를 만든다. 이 함수는 넘겨받은 color 객체의 rating을 변경한다.
```js
rateColor = (color, rating) => {
    color.rating = rating;
    return color;
}

console.log(rateColor(color_lawn, 5).rating)    // 5
console.log(color_lawn.rating)                  // 5
```
자바스크립트에서 함수의 인자는 실제 데이터에 대한 참조다. rateColor 함수 안에서 color의 rating을 변경하면 원본 color_lawn 객체의 rating도 바뀐다.  
rateColor를 다음과 같이 고쳐쓰면 원본에는 아무런 해가 없이 색깔에 평점을 부여할 수 있다.
```js
var rateColor = (color, rating) => {
    return Object.assign({}, color, {rating:rating});
}

console.log(rateColor(color_lawn, 5).rating)    // 5
console.log(color_lawn.rating)                  // 0
```
여기서 Object.assign을 사용해 색의 평점을 바꿧다. Object.assign은 복사기와 같다.  

Object.assign은 빈 객체를 받고, color 객체를 그 빈 객체에 복사하고, 복사본에 있는 rating 파라미터의 값으로 변경한다.  

ES6의 화살표 함수와 ES7의 객체 스프레드 연산자르 활용해 같은 함수를 작성할 수도 있다.  
이렇게 만든 rateColor 함수는 스프레드 연산자를 사용해 원본 color를 새로운 객체 안에 복사한 다음 rating 프로퍼티를 덮어 쓴다.
```js
const rateColor = (color, rating) => ({
    // 객체 스프레드 연산자
    // 노드나 브라우저 버전에 따라 지원 여부가 달라짐
    ...color,
    rating
});
```
새로운 버전의 자바스크립트 언어로 작성한 rateColor 함수는 앞에서 본 예제의 rateColor함수와 똑같은 일을 한다.  
이 함수는 color를 변경 불가능한 객체로 취급하며, 더 짧고, 약간 더 명확해 보인다. 여기서 반환할 객체를 괄호 () 로 감쌌다는 점에 주의해야한다.  
화살표 함수의 본문에서 바로 중괄호를 사용해 객체를 반환할 수 없기 때문에 꼭 괄호가 필요하다.  

색의 이름으로 이루어진 배열을 생각해볼때,
```js
let colorArray= [
    {title: "과격한 빨강"},
    {title: "잔디"},
    {title: "파티 핑크"},
];
```
이 배열에 Array.push를 사용해 색을 추가하는 함수를 작성할 수 있다.
```js
var addColor = (title, colors) => {
    colors.push({title : title});
    return colors;
}

console.log(addColor("매력적인 초록", colorArray).length);   // 4
console.log(colorArray.length);     // 4
```
하지만 Array.push는 불변성 함수가 아니다. 이 addColor 함수는 원본 배열에 새로운 원소를 추가한다.  
원래의 colorArray 배열을 변화시키지 않고 유지하기 위해서는 Array.concat을 사용해야 한다.
```js
const addColor = (title, array) => arr.concat({title});

console.log(addColor("매력적인 초록", colorArray).length);   // 4
console.log(colorArray.length);      // 3
```
Array.concat은 두 배열을 붙여준다. 여기서는 Array.concat이 새로운 객체를 받는다.  
그 객체에는 새로운 색의 이름이 title이라는 이름의 프로퍼티로 들어 있다. Array.concat은 그 객체를 원래 배열을 복사한 새로운 배열 뒤에 추가한다.
```js
const addColor = (title, list) => [...list, {title}]
```
이 함수는 원본 리스트의 원소를 새로운 배열에 복사하고, title파라미터로 받은 값을 title프로퍼티로 하는 객체를 새 배열에 추가한다.  
이 함수는 인자로 받은 list를 변경하지 않기 때문에 list의 원본인  colorArray의 불변성을 지켜준다.

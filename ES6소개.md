# ES6 소개

## ES6란?
ECMAScript를 ES라 줄여 부르고, 버전에 따라서 ES뒤에 숫자가 붙는다. ES6는 2015년에 효울적인 코드작성을 위해 만들어진 새로운 기술이다.

---
## ECMAscript가 생긴 배경
자바스크립트(Javascript)가 넷스케이프(Netscape) 브라우져만이 아니라 다른 웹 브라우져들의 지원까지 받기 시작하면서 다양한 웹 브라우져에서 자바스크립트(Javascript)가 공통되게 잘 작동하기 위해서 표준 규격이 필요해졌는데, 이 때문에, ECMA 국제 기구에서 “ECMAScript Standard”라 불리는 스크립트 표준이 만들어지게 된다.  
자바스크립트와 비슷한 뜻으로 많이 들어본 사람들이 있을텐데, Javascript는 ECMAScript와 BOM(Browser Object Model) 와 DOM(Document Object Model)이라는 1개의 코어와, 2개의 모델로 이루어져 있다.  
ECMAScript 와 Javascript 는 비슷한 뜻으로 자주 쓰이나 작은 차이를 가지고 있다.

---
## ECMAscript란?

ECMAScript는 자바 스크립트를 이루는 코어(Core) 스크립트 언어로, 웹 환경에서만 호스트 되는 언어가 아니다.  
웹 환경은 ECMA 스크립트가 호스트되는 환경들 중 하나일 뿐이다.  
ECMA 스크립트 호스트 환경은 ECMA 스크립트 실행 환경이 구현되있고, 각각 그 환경에 알맞는 확장성을 가지고 있다.  
예를들어 웹 브라우져 환경에서는 BOM(Browser Object Model)과 DOM(Document Object Model)이 그 확장성이 되겠다.  
이러한 확장성들은 ECMA 스크립트의 문법과 기능에 맞춰 기능의 확장을 가능게 한다.  
자바스크립트의 document 객체가 좋은 예이다.

---
## ES6 트랜스파일링
모든 웹 브라우저가 ES6를 지원하지 않는다. 그리고 Es6를 지원하더라도 모든 ES6 기능을 지원하지 않는 경우도 많다. 그러니 브라우저에서 ES6코드를 실행하기 전에 ES5로 컴파일을 하면 ES6가 제대로 동작하도록 보장할 수 있다. - 이런 변환을 **트랜스파일링**이라고 한다. -
> 가장 유명한 트랜스파일링 도구는 **바벨**이 있다.  
> http://babeljs.io  
  
---  
## ES6 객체와 배열
ES6는 객체와 배열을 다루는 방법과 객체와 배열 안에서 변수의 영역을 제한하는 방법을 다양하게 제공한다. 그러한 기능으로는 *구조분해, 객체 리터럴 개선, 스프에드 연산자*등이 있다.

>  구조분해  
- 객체 안에 있는 필드 값을 원하는 변수에 대입할 수 있다.  
다음 sandwich 객체를 보면 sandwich에는 4개의 필드가 있다. 그중에서 bread와 meat필드의 값이 필요하다.
```js
var sandwich = {
    bread: "더치 크런치",
    meat:"참치",
    cheese:"스위스",
    toppings:["상추", "토마토", "머스타드"],
};

var {bread, meat} = sandwich;

console.log(bread, meat) // 더치 크런치 참치
```

이 코드는 sandwich를 분해해서 bread와 meat 필드를 같은 이름의 변수에 넣어준다. 두 변수의 값은 sandwich에 있는 같은 이름의 필드 값으로 초기화 되지만, 두 변수를 변경해도 원래의 필드 값은 바뀌지 않는다.

```js
var {bread, meat} = sandwich;

bread = "마늘";
meat = "칠면조";

console.log(bread) // 마늘
console.log(meat) // 칠면조

console.log(sandwich.bread, sandwich.meat) // 더치 크런치 참치
```
객체를 분해해서 함수의 인자로도 넘길 수 있다. 어떤 사람의 이름을 영주처럼 표현해주는 함수를 생각해볼때
```js
var lordify = regularPerson => {
    console.log(`캔터베리의 ${regularPerson.firstname}`);
}

var regularPerson = {
    firstname: "준우",
    lastname: "김",
};

lordify(regularPerson) // 캔터베리의 준우
```
객체의 필드에 접근하기 위해 점(.)과 필드 이름을 사용하는 대신 regularPerson에서 필요한 값을 구조 분해로 가져올 수 있다.
```js
var lordify = ({firstname}) => console.log(`캔터베리의 ${firstname}`);

lordify(regularPerson); // 캔터베리의 준우
```
구조 분해는 더 선언적이다. 따라서 코드를 작성한 사람의 의도를 더 잘 설명해준다. 구조 분해로 firstname을 가져옴으로써 객체의 필드 중에서 firstname만 사용한다는 사실을 선언한다.  

배열을 구조 분해해서 원소의 값을 변수에 대입할 수 도 있다. 배열의 첫 번째 원소를 변수에 대입하고 싶다고 할때

```js
var [firstResort] = ["용평", "평창", "강촌"];
console.log(firstResort) // 용평
```
불필요한 값을 콤마(,)를 사용해서 생략하는 리스트 매칭을 사용할 수도 있다. 무시하고 싶은 원소 위치에 콤마를 넣으면 리스트 매칭된다. 위 배열에서 첫 두 원소를 콤마로 대치하면 다음과 같다.

```js
var [,,thirdResort] = ["용평","평창","강촌"]
console.log(thirdResort) // 강촌
```
> 객체 리터럴 개선
- 구조 분해의 반대. 객체 리터럴 개선은 구조를 다시 만들어 내는 과정 또는 내용을 한데 묶는 과정이라 할 수 있다.  

객체 리터럴 개선을 사용하면 현재 영역에 있는 변수를 객체의 필드로 묶을 수 있다.

```js
var name = "탈락";      // 캘리포니아에 있는 산
var elevation = 9738;   // 높이(단위 : 피트)

var funHike = {name, elevation};

console.log(funHike);
```
이제 funHike 객체에는 name과 elevation이라는 필드가 들어 있다.  
객체 리터럴 개선 또는 객체 재구축으로 객체 메서드를 만드는 것도 가능하다.
```js
var name = "Tallac";
var elevation = 9738;
var print = () => {
    console.log(`${this.name} 산의 높이는 ${this.elevation}피트입니다.`);
}

var funHike = {name, elevation, print};

funHike.print() // Tallac 산의 높이는 9738피트입니다.
```
이때 객체의 키에 접근하기 위해 this를 사용했다는 사실에 유의해야한다.  
객체 메서드를 정의할 때는 더이상 function 키워드(화살표 함수)를 사용하지 않아도 된다.

```js
// 예전방식
var skier = {
    name : name,
    sound : sound,
    powderYell : function() {
        var yell = this.sound.toUpperCase();
        console.log(`${yell} ${yell} ${yell}!!!`);
    },
    speed : function(mph) {
    this.speed = mph;
    console.log('속력(mph) :', mph)
    },
}

// 새로운 방식
const skier = {
    name,
    sound,
    powderYell() {
        let yell = this.sound.toUpperCase();
        console.log(`${yell} ${yell} ${yell}!!!`);
    },
    speed(mph) {
        this.speed = mph;
        console.log('속력(mph) :', mph);
    },
}
```
객체 리터럴 개선으로 현재 영역에서 볼 수 있는 변수들을 객체의 필드에 대입할 수 있으며, function키워드를 입력하지 않아도 되기 때문에 입력해야 할 코드 양도 줄어든다.

> 스프레드 연산자
- 세 개의 점(...)으로 이루어진 연산자로, 몇 가지 다른 역할을 담당한다.  

먼저 스프레드 연산자를 사용해 배열의 내용을 조합할 수 있다. 예를 들어 두 배열이 있다면 스프레드 연산자를 적용하여 두 배열의 모든 원소가 들어간 세 번째 배열을 쉽게 만들 수 있다.
```js
var peaks = ["대청봉", "중청봉", "소청봉"];
var canyons = ["천불동계곡", "가야동계곡"];
var seoraksan = [...peaks, ...canyons];

console.log(seoraksan.join(', '));  // 대청봉, 중청봉, 소청봉, 천불동계곡, 가야동계곡
```
peaks와 canyons에 포함된 모든 원소가 seoraksan이라는 새 배열에 들어간다.  

위 예제에서 정의한 peaks 배열의 마지막 원소를 변수에 담고 싶을 때, Array.reverse 메서드를 사용해 배열을 뒤집고 구조 분해를 사용해 첫 번째 원소를 변수에 넣으면 된다.

```js
var peaks = ["대청봉", "중청봉", "소청봉"];
var [last] = peaks.reverse();   // 구조 분해

console.log(last)   // 소청봉
console.log(peaks.join(', '))   // 소청봉, 중청봉, 대청봉
```

위의 코드에는 문제점이 있다. reverse 메서드는 원본 배열을 변경한다. 하지만 스프레드 연산자를 사용하면 원본 배열을 변경하지 않고 복사본을 만들어서 뒤집을 수 있다.

```js
var peaks = ["대청봉", "중청봉", "소청봉"];
var [last] = [...peaks].reverse();

console.log(last)   // 소청봉
console.log(peaks.join(', '));  // 대청봉, 중청봉, 소청봉
```
스프레드 연산자를 사용해 배열의 원소를 복사했기 때문에 원본인 peaks는 변경되지 않고 그대로 남는다. 따라서 나중에 필요할 때 원본 peaks를 다시 사용할 수 있다.  

스프레드 연산자를 사용해 배열의 나머지 원소를 얻을 수도 있다.
```js
var lakes = ["경포호", "화진포", "송지호", "청초호"];
var [first, ...rest] = lakes;   // [first, ...rest]에 lakes에 있는 값을 넣어줌

console.log(lakes.join(', '));   // "화진포, 송지호, 청초호"
console.log(rest.join(', '));    // "화진포, 송지호, 청초호"
```
스프레드 연산자를 사용해 함수의 인자를 배열로 모을 수도 있다. 다음 예제는 n개의 인자를 스프레드 연산자를 사용해 배열로 모든 다음 그 배열을 사용해 여러 가지 내용을 콘솔 메시지로 찍는 함수를 보여준다.
```js
function directions(...args) {
    var [start, ...remaining] = args;
    var [finish, ...stops] = remaining.reverse();

    console.log(`${args.length} 도시를 운행합니다.`);   // 6 도시를 운행합니다.
    console.log(`${start}에서 출발합니다.`);    // 서울에서 출발합니다.
    console.log(`목적지는 ${finish}입니다.`);   // 목적지는 부산입니다.
    console.log(`중간에 ${stops.length}군데 들립니다.`);    // 중간에 4군데 들립니다.
}

directions(
    "서울",
    "수원",
    "천안",
    "대전",
    "대구",
    "부산"
)
```

스프레드 연산자를 객체에 사용할 수도 있다. 스프레드 연산자를 객체에 사용하는 방법은 배열에와 비슷하다. 다음 예제에서는 두 배열을 세 번째 배열로 합쳤던 과정을 배열 대신 객체를 사용해 수행한다.

```js
var morning = {
    breakfast: "미역국" ,
    lunch: "삼치구이와 보리밥",
};

var dinner = "스테이크 정식";

var backpackingMeals = {
    ...morning,
    dinner,
};

console.log(backpackingMeals);
// {breakfast: "미역국", lunch: "삼치구이와 보리밥", dinner: "스테이크 정식"};
```
---
## 프라미스
**프라미스**는 비동기적인 동작을 다루기 위한 방법이다.  
비동기 요청을 보내면 모든 것이 바라는 대로 잘 작동해서 성공하거나 또는 오류가 생긴다.  

요청이 성공하거나 실패하는 데도 다양한 유형이 있을 수 있다.  
예를 들어 데이터 얻기에 성공할 때까지 여러 가지 방법을 시도해 볼 수 있다. 또한 여러 유형의 오류가 발생할 수 있다. 

프라미스를 사용하면 이런 여러 가지 성공이나 실패를 편리하게 단순한 성공이나 실패로 환원할 수 있다.  
</br>

---
</br>

randomuser.me API로 부터 데이터를 가져오는 비동기 프라미스를 하나 만들때, 이 API에는 가짜 멤버에 대한 전자우편 주소, 이름, 전화번호, 집주소 등의 정보가 들어 있으며, 그런 데이터를 더미로 활용하기 좋다.  

_**getFakeMembers**_ 함수는 새로운 프라미스를 반환한다. 그 프라미스는 randomuser.me API에 요청을 보낸다. 프라미스가 성공한 경우에는 데이터를 제데로 받아올 것 이고, 실패한 경우에는 오류가 발생할 것 이다.

```js
const getFakeMembers = const => new Promise((resolves, rejects) => {
    const api = `https://api.randomuser.me/?nat=US&result=${count}`;
    const request = new XMLHttpRequest();
    request.open('GET', api);
    request.onload = () => {
        (request.status === 200) ?
        resolves(JSON.parse(request.response).result) :
        reject(Error(request.statusText))
    };
    request.onerror = (err) => rejects(err);
    request.send();
});
```
이 함수로 프라미스를 만들 수 있게 되었지만 아직 프라미스를 사용한 것은 아니다. 가져오고 싶은 멤버 수를 getFakeMembers 함수에 전달해 호출하면 실제 프라미스를 사용할 수 있다.  
프라미스가 성공한 경우에 처리할 작업을 기술하기 위해 then 함수를 프라미스 뒤에 연쇄 (체이닝) 시킨다.  
이때 오류를 처리하기 위한 콜백도 함께 제공한다.

```js
getFakeMembers(5).then(
    members => console.log(members),
    err => console.error(new Error("randomuser.me에서 멤버를 가져올 수 없습니다."));
)
```
프라미스는 비동기 요청을 더 쉽게 처리할 수 있게 해준다.  
자바스크립트에서는 비동기로 데이터를 처리하는 경우가 많기 때문에 비동기 요청을 쉽게 처리할 수 있으면 좋다.  
노드에서도 프라미스를 많이 사용하는 것을 볼 수있다.  
따라서 프라미스를 잘 이해하는 것은 최신 자바스크립트 개발자에게 필수적인 덕목이다.

---

## 클래스

이전 자바스크립트에는 공식적으로 클래스가 없었다. 타입은 함수로 정의했었다. 과거에는 다음과 같이 함수를 정의하고 그 함수 객체에 있는 프로토타입을 사용해 메서드를 정의 했다.

```js
function Vacation(destination, length) {
    this.destination = destination;
    this.length = length
}

Vacation.prototype.print = () => {
    console.log(this.destination + "은(는)" + this.length + "일 걸립니다.");
}

var maui = new Vacation("마우이", 7);   // new를 사용해서 maui라는 객체를 생성

maui.print()    // 마우이은(는) 7일 걸립니다.
```
ES6에는 클래스 선언이 추가되었다. 하지만 자바스크립트는 여전히 기존 방식으로 작동한다. 함수는 객체며 상속은 프로토타입을 통해 처리된다.

```js
class Vacation {
    contructor(destination, length) {
        this.destination = destination;
        this.length = length;
    }

    print() {
        console.log(`${this.destination} 은(는) ${this.length}일 걸립니다.`);
    }
}
```
    대문자 관습  
    -> 모든 타입의 이름은 대문자로 시작하는 규칙을 흔히들 사용한다.

클래스를 정의하고 나면 new 키워드를 사용해 해당 클래스의 새로운 인스턴스를 만들 수 있다.  
그 후 그 인스턴스의 메서드(클래스에 정의된)를 호출할 수 있다.

```js
const trip = new Vacation("칠레 산티아고", 7);  // new를 사용해서 Vacation이라는 class에 trip이라는 객체를 생성
console.log(trip.print())   // 칠레 산티아고은(는) 7일 걸립니다.
```
클래스 객체를 만들고 나면 새로운 객체를 생성하기 위해 원하는 만큼 new를 호출할 수 있다.  
클래스를 확장할 수도 있다. 기존의 클래스를 확장한 새로운 클래스는 상위 클래스의 모든 프로퍼티와 메서드를 상속한다.  
이렇게 상속한 프로퍼티나 메서드를 하위 클래스 선언 안에서 변경할 수도 있다.  

Vacation을 여러 가지 휴가 타입을 정의하기 위한 추상 클래스로 사용할 수도 있다. 예를 들어 EXpedition은 Vacation 클래스를 확장하여 장비를 표현하는 프로퍼티(gear)를 더 가진다.
```js
class Expedition extends Vacation { // class 자녀클래스 extends 부모클래스
    constructor(destination, length, gear) {    // destination, length, gear과 함께 부모 클래스의 생성자를 호출
        super(destination, length); // 파생클래스에서 super()를 먼저 사용해야 'this'를 사용 가능
        // 부모 객체의 함수를 호출하는데 사용
        this.gear = gear;
    }

    print() {
        super.print();  // Vacation 함수의 print함수를 실행
        console.log(`당신의 ${this.gear.join("와(과) 당신의 ")}를(을) 가져오십시오.`);
    }
}
```
여기서 하위 클래스는 상위 클래스의 프로퍼티를 상속한다는 간단한 상속 관계를 볼 수 있다.  
print() 에서는 상위 클래스에 있는 print()를 호출한 다음 Expedition에 있는 추가 정보를 출력했다.  
상속을 사용해 만든 하위 클래스의 인스턴스를 생성할 때도 상위 클래스의 인스턴스를 생성할 때와 마찬가지로 new 키워드를 사용한다.

```js
const trip2 = new Expedition("한라산", 3, ["선글라스", "오색깃발", "카메라"]);
trip2.print();
// 한라산은(는) 3일 걸립니다.
// 당신의 선글라스와(과) 당신의 오색 깃발와(과) 당신의 카메라를(을) 가져오십시오.
```

    클래스 상속과 프로토타입 상속
    -> class 키워드를 사용하더라도 여전히 자바스크립트의 프로토타입 상속을 사용하고 있는 것이다. Vacation.prototype을 콘솔에 log로 찍으면 프로토타입에 들어 있는 생성자와 print메서드를 볼 수 있다.  

객체 지향을 알고넘어가는 이유는 리액트 컴포넌트를 만들 때 클래스를 활용하기 위해서이다.

## ES6 모듈
**자바스크립트 모듈**은 다른 자바스크립트 파일에서 쉽게 불러서 활용할 수 있는 재사용 가능한 코드 조각을 말한다. 최근까지 자바스크립트를 모듈화하는 방법은 모듈의 임포트와 익스포트를 처리하는 라이브러리를 활용하는 것뿐이었다. 하지만 ES6부터는 자바스크립트 자체에서 모듈을 지원하기 시작했다.

자바스크립트는 각각의 모듈을 별도의 파일로 저장한다. 모듈을 만들고 외부에 익스포트하는 방법에는 한 모듈에서 여러 자바스크립트 객체를 외부에 노출시키는 방법과 모듈당 하나의 자바스크립트 객체를 노출시키는 방법이 있다.

아래의 **text-helper.js**에 있는 모듈은 두 함수를 외부에 노출시킨다.

```js
export const print(message) => log(message, new Date())

export const log(message, timestamp) => console.log(`${timestamp.toString()}: ${message}`);
```
export를 사용해 다른 모듈에서 활용하도록 이름(함수, 객체, 변수, 상수)을 외부에 익스포트한다. text-helper.js에 정의된 다른 선언은 이 모듈 내부에 한정되됨(즉, 로컴 선언이 됨)

모듈에서 단 하나의 이름만 외부에 익스포트하고 싶을 때도 있다. 이러한 경우 export default를 사용한다.

```js
const freel = new Expedition("Mt. Freel", 2, ["water", "snack"]);
export default freel
```

export defalut는 오직 하나의 이름만 노출하는 모듈에서 사용할 수 있다. 다시 말하지만 export나 export defalut에서는 기본 타입, 객체, 배열, 함수 등 모든 타입의 자바스크립트 이름을 외부에 노출시킬 수 있다.

모듈은 import 명령을 사용해 다른 자바스크립트 파일을 불러와 사용할 수 있다. 외부에 여러 이름을 노출한 모듈은 임포트할 때는 객체 구조 분해를 활용할 수 있다. export default를 사용해 한 이름만 노출한 경우에는 노출된 대상을 구조분해 없이 한 이름으로 부를 수 있다.

```js
import {print, log} from './text-helpers'
import freel form './mt-freel'

print('메시지를 print');
log('메시지를 log');

freel.print();
```
모듈에서 가져온 대상의 다른 이름을 부여할 수 도있다.

```js
import { print as p, log as l} from 'text-helpers'
// print의 이름을 p로 바꾸겠다. ( as의 이용 )

p('메시지를 print');
l('메시지를 log');
```

import *를 사용하면 다른 모듈에서 가져온 이름을 사용자가 정한 로컬 이름 공간 안에 가둘 수 있다.

```js
import * as fns from './text-helpers'
```
아직은 모든 브라우저가 ES6 모듈을 완전히 지원하지는 않는다. 바벨은 ES6 모듈을 지원한다.

## 커먼JS

**커먼JS**는 모든 버전의 노드에서 지원하는 일반적인 모듈 패턴이다. 이 모듈은 바벨이나 웹팩에서 여전히 사용할 수 있으며 커먼 JS를 사용하면 자바 객체를 module.exports를 사용해 익스포트 할 수 있다.
```js
const print(message) => log(message, new Date());

const log(message, timestamp) => console.log(`${timestamp.toString()}: ${message}`); 
// toString은 숫자를 문자열로 바꿔서 출력해줌
// EX) toString()을 하면 10진수,
// EX) toString(2)을 하면 2진수,
// EX) toString(8)을 하면 8진수,
// EX) toString(16)을 하면 16진수,

module.exports = {print, log};
```
커먼JS는 import 문을 지원하지 않는다. 대신 require 함수로 모듈을 임포트 할 수있다.

```js
const {log, print} = require('./txt-helpers');
```
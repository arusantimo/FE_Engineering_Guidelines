
# TypeScript 스타일 가이드 및 코딩 규칙

> DevPMO실의 타입스크립트로 작성된 코딩 스타일 가이드 입니다. (버전 0.0.1) `typescript-book Repo` `구글 타입스크립트` `Airbnb 가이드` 를 참고 했습니다.

* [ 기본 규칙 ](#기본-규칙)
* [ Naming 규칙 ](#네이밍-규칙-(identifiers))
* [ 변수 ](#변수)
* [ 함수 ](#함수)
* [ 객체 ](#객체-&-q배열)
* [ 클래스 ](#클래스)
* [ type & interface ](#type-(Alias)-&-interface)
* [ 모듈 ](#모듈)
* [ 네임스페이스 ](#네임스페이스)
* [ `enum` 열거형 ](#enum)
* [ 연산자 ](#연산자)
* [ 조건문 ](#조건문)
* [ 반복문 ](#반복문)
* [ 주석 ](#주석)

## 기본 규칙

### 내부 로직에선 `any` 유형을 사용하지 않는다.
> 이유 : 해당 코드 이외에도 `any`유형과 연관된 다른 로직에서도 추론이 힘들어진다.
---
### 들여쓰기는 space2를 사용한다.
> 이유 : 많은 기업과 팀에서 사용하는 컨벤션이다. [eslint 공백](https://eslint.org/docs/latest/rules/indent)
---
### 문자열은 `''`작은 따움표로 통일한다.
> 이유 : 글로벌 컨벤션을 따른다.
```ts
const name = 'poll';
```
---
### 다른 타입의 구문의 경우 빈칸의 띄어쓰기를 한다.
> 이유 : 코드 가독성이 올라간다.
```ts
const value = 10;
// 공백
function fun(): number {
  let some = 1;
  // 공백
  if (condition) {
    some = 2;
  } else {
    some = 3;
  }
  // 공백
  return some;
}
```
---
### 한줄에 하나의 문장만 허용한다. 문장 종료 시에는 반드시 세미콜론`;`을 사용한다.
> 이유: 문법 오류가 나지 않지만, 개발자가 오류를 일으킬수 있다.
```ts
✅ const gold = 'gold';
🚫 const gold = 'gold' silver = 'silver'
```
---
### 블록 구문에는 세미콜론을 사용하지 않는다. 한줄짜리 블록도 생략하지 않는다.
> 이유: 문법 오류가 나지 않지만, 개발자가 오류를 일으킬수 있다.
```ts
✅ if (condition) {
  ...
} else {
  ...
}
🚫 if(condition) doSomething();
```
---
### 객체의 경우 줄바꿈으로 구분해서 선언한다. 배열은 한 요소가 길어지면 줄바꿈으로 구분한다.
> 이유: 가독성을 높일 수 있다.
```ts
const me: {
  [key: string]: string | number
} = {
  age: 1,
  name: 'roby'
};
const list = [1, 2, 3];
const list2: Array<string | number> = [
  'goldgoldgoldgoldgoldgoldgold', 
  'silver, silver,silversilversilversilver', 
  3
];
```
---
### 기본 타입으로 `undefined`는 선언하지 않는다. ?옵셔녈 선언으로 대체 한다.
> 이유 : 코드의 품질에 저하된다. 기본적으로 `undefined`은 필요한 경우가 없다. ?선언으로 모든 경우 커버 가능하다.

```ts
let foo: { x: number, y?: number } = { x:123 };
```
---
&nbsp;&nbsp;

## 네이밍 규칙 (identifiers)

[구글코딩스타일 - 변수](https://google.github.io/styleguide/tsguide.html#identifiers)

### 의미와 기능을 유추할수 있는 이름 짖는다. (너무 길면 X)
> 이유: 코드 가독성이 올라간다.
```ts
const name = '강동원';
let age = 12;
const sum: number = (a: number, b: number) => a + b;
```
---
### 변수 및 함수 이름에 `lowerCamelCase` 사용한다.
> 이유: 불필요한 '_' 필요 없이 코드 작성 가능하고 많은 팀에서 사용하고 있다.
```ts
const fooConst;
let fooVar;
function barFunc() {...}
```
---
### `Global const`와`enum`의 경우 `CONSTANT_CASE`를 사용한다.
> 이유: 글로벌 표준에 따름 / 타입스크립트 표준이다.  
```ts
const SERVICE_CODE = '0112';
enum GAME_TYPE {
  MMO = 'mmo',
  PUZZLE = 'Puzzle'
}
```
---
### interface / Class / TypeAlias / namespace  이름에 `UpperCamelCase` 를 사용한다.
> 이유: 표준 자바스크립트 문법 /  타입스크립트 표준이다.
```ts
type SomeTypeAlias = 'A' | 'B';
class  Foo { }
interface Food { }
namespace Fad {}
```
---
### interface / TypeAlias   이름에 `I` `T` 접두사를 사용 하지 않는다.
> 이유: 현재 d.ts에서 사용하지 않고 타입스크립트 스타일 대체적인 흐름이다.
```ts
interface Food {}

🚫 interface IFood {}
```
---
### 클래스 / interface 멤버 및 메서드는 `lowerCamelCase`를 사용한다.
> 이유: 표준 자바스크립트 문법 /  타입스크립트 표준이다.
```ts
class Foo {
  bar: number;
  baz() { }
}
interface Food {
  foo: string;
  bar: string;
};
type Foo = number | { someProperty: number }
```
---
&nbsp;&nbsp;

## 변수

### `var` 사용 하지 않는다. `const` `let`을 그룹화 해서 선언한다.
> 이유: const, let으로 인해 사용 빌요성 없어졌다.  
> [구글코딩스타일 - 변수선언](https://google.github.io/styleguide/tsguide.html#variables)
```ts
const fooConst = 10;
const name = 'hill';
let fooVar;
let age = 11; 

🚫 var fooVar; 
```
---
### 문자열 computed value 사용시 템플릿 문자열을 사용한다.
> 이유 : + 를 사용하는 것 보다 가독성이 좋다. 글로벌 컨벤션을 따른다. (구글, Airbnb)
```ts
const talk = `How are you, ${name}?`;
```
---
### 기본유형 클래스 인스턴스화 해서 선언하지말고 `리터럴 표기법`으로 선언한다.
> 이유: 더 명확하고 선언적이며, 성능에도 도움이된다.
```ts
const age = 10;
const list = [];
const name = '';
const isGood = true;

🚫 var isBad = new Boolean(false); 
🚫 var address = new String('음...'); 
```
---
### 그룹화 선언을 하지 않고, 개별 선언한다.
> 이유: 가독성이 떨어지고, 오류 찾기 힘들어지고, 해당 변수가 const, let인지 한번에 알수 없다.
```ts
const age = 10;
const list = [];
const name = '';
const isGood = true;

🚫 const address = '10',
  hool = 10; 
```
---
### 변수 선언시 타입 추론이 되는 선언은 타입선언을 생략한다.
> 이유: 컴파일러에서 자동으로 추론 가능한 선언문은 굳이 타입을 선언하지 않아도 된다.
```ts
const num = 15;  // Type inferred.
let maxNum: bigint;
maxNum = BigInt(3145) * 10n;

🚫 const age: number = 10;
```
---
### `const` 선언시 값을 선언과 동시에 할당한다.
> 이유: const는 선언할때만 값을 할당할 수 있다.
```ts
const num = 15;
```
---
&nbsp;&nbsp;

## 함수

### 함수 내에서 특정 변수의 값 반환은 한번만 한다.
> 이유: 코드를 예측하기 쉬워지고 흐름이 간결해 진다.
```ts
🚫
function getResult() {
  const gold = 'gold';
  
  if (condition) {
    
    return someDataInTrue;
  }
  
  return someDataInFalse;
}

function getResult(isValid) {
  
  if (!isValid) {
    
    return;
  }
  
  return someDataInTrue;
}

// Good
function getResult() {
  let resultData;

  if (condition) {
    
    ...
    resultData = someDataInTrue;
  } else {
    
    ...
    resultData = someDataInFalse;
  }

  return resultData;
}
```
---
### 익명함수 / arrow  함수 사용시 클로저를 사용하지 않도록 한다.
> 이유: 스코프 체인이 늘어나 성능저하되고, 코드 관리와 가독성이 저하된다. 글로벌 컨벤션(Air bnb)
```ts
let data;

🚫 Array.forEach(arr, function(ar) {
  
  data = ar / 10;
});

✅ Array.forEach(arr, (ar) => {
  
  const data = ar / 10;
});
```
---
### 모듈화된 공용 함수의 경우 JSDoc를 사용해서 함수 설명한다.
> 이유 : 함수를 빠르게 파악할수 있고, IDE를 통해 불러오기할때도 빠르게 확인할 수 있다.
```ts
/**
 * @desc 함수 설명
 * @param 파라미터 설명 얘)rowSize 가로사이즈 1300 ~ 1920
 * @returns 리턴 설명 예) 실제 가로 사이즈
 */
export const getReakRowsize = (
  rowSize: number,
): string => {
  
  return rowSize + 100;
};
```
---
### 함수(표현)식 or 익명함수의 경우 arrow 함수를 사용한다.
> 이유 : 함수표현식 함수에 비해 불필요한 this 바인딩이 되지 않다. 효율적이고, 코드 가독성 코드량이 적다.
```ts
[1, 2, 3].map(x => {
  
  return x * 10;
});
```
---
### arrow 함수 한줄 표현 가능하고, 구문이 길어질 경우 소괄호를 넣어준다.
> 이유 : 코드 가독성이 높아지고, 코드량을 줄일 수 있다.
```ts
[1, 2, 3].map(number => (
  `As time went by, the string containing the ${number} became much ` +
  'longer. So we needed to break it over multiple lines.'
));

[1, 2, 3].map(number => `A string containing the ${number}.`);
```
---
### 파라미터 기본값은 사용가능하나 순서상 가장 뒤 인자로 넣고, 기본값에 수식 조건등을 넣지 않는다.
> 이유 : 사이드 이팩트를 방어한다.
```ts
🚫 function count(a = b++) {
  ...
}

✅ function handleThings(name, opts = {}) {
  ...
}

```
---
### 함수 선언시 `parameter`와 `return`의 타입을 정의해 준다.
> 이유 : 타입스크립트 기본 가이드에 따른다.
```ts
const sum = (a: number, b: number): number {
  return a + b;
}
```
---
### 함수 `parameter`에 괄호를 쓴다.
> 이유 : 코드 가독성과 일관성을 위해서, 글로벌 컨벤션에 따른다 (Air bnb)
```ts
[1, 2, 3].map((x) => x * x);
```
---
### 매개변수로 객체를 넘기는 것은 지양하자! 사용시 함수 매게변수 `interface` 필수!
> 이유 : 매개변수 정의가 힘들고, 파악이 어렵다. 컴팩트한 순수함수를 만들어내기 힘들다.
```ts
// 🚫 
const getPokemon = (Pokemon) => {
  console.log(`The pokemon is $(Pokemon.pokemonName) the weigth is $(Pokemon.pokemonWeight)`)
}

// ✅ 
const getPokemon = (pokemonName, pokemonWeight) => {
  console.log(`The pokemon is $(pokemonName) the weigth is $(pokemonWeight)`)
}
```
---
&nbsp;&nbsp;

## 객체 & 배열

### 객체 메****소드 선언(정의)의 경우 메소드 단축 구문 사용하자.
> 이유 : 더 직관적이고 기독성이 높다.
```ts
const obj = {
  ✅ foo() {
    // …
  },
  🚫 bar: function () {
    // …
  },
};
```
---
### 얕은 복사(1 depth)시 `전개 연산자(확장연산자)` 를 사용한다.  
> 이유 : 적은 코드량으로 편하게 복사 가능하다.
```ts
const obj = {
  a: 10
};
const obj2FromObj = {
  ...obj
}
const list = [1, 2, 3];
const list2 = [...list2, 4, 5];
```
---
### 객체의 속성 / 배열의 요소 값을 참조 할당할때는 `구조분해할당`을 사용한다.
> 이유 : 코드량을 효율적으로 줄일 수 았다.
```ts
const [first, second, ...rest] = [10, 20, 30, 40, 50];
const {
  age, name, ...rest2
} = {
  age: 10, 
  name: 'gill', 
  height: 30, 
  size: 40
};
```
---
### 객체 타입 선언시 `Type alias`를 사용한다.
> 이유 : 향후 활용 범위가 넓어 지고 코드 가독성이 높아진다.
```ts
type profile = {
  age: number;
  name: string;
}

const myProfile: profile = {
  age: 11,
  name: '고길동'
}
```
---
### 배열 타입 선언시 `Generic`타입을 사용한다.
> 이유 : 향후 활용 범위가 넓어 지고 코드 가독성이 높아진다.
```ts
type profile = {
  age: number;
  name: string;
}

const ages: Array<Number> = [1, 2, 3];
const member: Array<profile> = [
  {
    age: 11,
    name: '고길동'
  }
];
```
---
### 객체 할당 시 단춘구문을 사용한다.
> 이유 : 코드 가독성과 효율적으로 코드를 작성 할수 있다. Airbnb 컨벤션 참고
```ts
const lukeSkywalker = 'Luke Skywalker';
const obj = {
  lukeSkywalker,
};
```
---
&nbsp;&nbsp;

---

## 클래스

### `static` 속성 유형을 사용 할 수 있다.
> 이유 : 타입스크립트에서 호환된다.
```ts
class Rect {
  static count: number;
  
  constructor(width, height) {
    
    Rect.count++;
  }
}
```
---
### `readonly` 속성 유형을 사용 할 수 있다.
> 이유 : 타입스크립트에서 호환된다.
```ts
class Rect {
  readonly name: number;
  
  constructor(name: string) {

    this.name = name;
  }

  set name(name) {
    this.name = name; // ERROR: Left-hand side of assignment expression cannot be a constant or a read-only property.
  }
}
```
---
### 비공개 속성 유형의 경우 `#` 식별자 사용하지말고 `_` `private`를 앞에 붙인다.
> 이유: ES2015 이전 코드 호환성 문제와, 실질적으로 타입스크립트 시스템에서는 유효하지 않다.
```ts
class Foo {
  private _bar: number;

  🚫 #foo: string;
}
```
---
### `public` 속성의 경우 public을 쓰지 않는다.
> 이유 : 기본적 속성은 공개값고 널리 알고 있기 때문에 코드가 불필요 하다.
```ts
class Foo {
  bar: number;

  🚫 public foo: string;
}
```
---
### 상속은 `extends` 를 사용한다. 프로토타입 체인을 사용하지 않도록 하자.
> 이유 : 타입스크립트 문법을 따른다.
```ts
class PeekableQueue extends Queue {
  peek() {
    return this._queue[0];
  }
}
```
---
### `overwriting`은 되도록 하지 않도록 하자. (이것은 협의 필요할듯...)
> 이유 : 많은 개발자가 참여한 프로젝인 경우 사이드 이팩트를 일으킬 수 있다.
```ts
```
---
### `getter` 메서드를 단순히 속성 접근 제한(보안)을 위해서 쓰지 않는다. 아니라면 `readonly` 사용하자.
> 이유 : 사이드 이팩트를 방지한다.
```ts
class Foo {
  private wrappedBar = '';
  ✅ get bar() {
    return this.wrappedBar || 'bar'; // getter의 처리가 필요 아니라면 readonly 사용하자.
  }
  🚫 get bar() {
    return this.wrappedBar;
  }
}
```

---
&nbsp;&nbsp;

## type (Alias) & interface

### `TypeAlias` 에 기본 타입을 포함 하지 않도록 한다.
> 이유 : 타입의 명확성이 떨어진다. 구글 코드스타일을 따름.
```ts
type CoffeeResponse = Latte|Americano;

class CoffeeService {
  getLatte(): CoffeeResponse|undefined { ... };
}
```
---
### 대부분 `interface`를 사용하고 객체 이외 정의시 `type`을 쓰자. 
> 이유: [설명 영상](https://www.youtube.com/watch?v=IXAT3If0pGI)  
> type은 computed value 선언이 된다. (좋은것인진 모르겠지만.)  
> interface의 선언 병합이 가능하다.  
> interface는 객체에만 사용이 가능하다.
> 
```ts
type names = 'firstName' | 'lastName';
type NameTypes = {
  // computed value의 사용
  [key in names]: string
}

interface NameInterface {
  // error > 그럼으로 성능 향상이 된다.
  [key in names]: string
}

interface Foo {
  foo: string;
}
interface FooBar extends Foo {
  bar: string;
}
class X implements FooBar {
  foo: string;
  bar: string;
}
```
---
### `union type`인터페이스와 같은 타입을 다룰 때, 논리적 사고(유니온 타입은 OR, 인터섹션은 AND)를 주의하자.
> 이유 : 명확한 정의가 되지 않아 코드 품질이 저하된다. 어느 타입이 올지 알 수 없는 추측 불가능한 코드가 생성될수 있다.
```ts
🚫 const sum =  (num: number | string, num2: number): number => {
  return  num + num2; // type error 
}

✅ const dir: 'right' | 'left' = 'right';
```
---
### `intersection Types` (교차 타입)을 통해 타입을 믹스인 하지 않는다. (되도록 사용 하지 않는다.)
> 이유 : 선언 병합은 interface로 하는것이 바람직하고, 교차 타입은 사용하는 곳의 이유가 합집합의 케이스를 위해서 존재한다. 다양한 문제를 일으킬수 있음.
```ts
type names = string & number; // type error 
```
---
### `interface`는 추상 클래스와 혼용하여 쓰지 않도록 한다.
> 명확하게 사용하는 방향이 다름으로 상속을 위해서는 interface 는 사용하지 않는다.
```ts
// Abstract class
abstract class AbstractBird {
    // 추상 멤버 변수
    abstract birdName: string;
    abstract habitat: string;
    
    // 추상 메서드
    abstract flySound(sound: string);
    
    // 구현 메서드
    fly(): void {
    	this.flySound('파닥파닥');
    }
    
    // 구현 메서드
   	getHabitat(): void {
    	console.log(`<${this.birdName}>의 서식지는 <${this.habitat}> 입니다.`);
    }
}

class WildGoose extends AbstractBird {
    // 추상 멤버 변수를 상속함
    constructor(public birdName: string, public habitat: string) {
    	super();
    }
    
    // 추상 메서드를 오버라이딩
    flySound(sound: String) {
    	console.log(`<${this.birdName}>가 <${sound}> 날아갑니다.`);
    }
}



// interface
interface Dog { 
  run(): void;
  getStatus(): { runningSpeed: number; };
}

interface Bird {
  fly(): void;
  getStatus(): { flightSpeed: number; };
}

interface DogBird extends Dog, Bird {
  getStatus(): { runningSpeed: number, flightSpeed: number; }
}

class NewAnimal implements DogBird {
  run(): void { }
  fly(): void { }
  getStatus(): { runningSpeed: number, flightSpeed: number; } {
    return { runningSpeed: 10, flightSpeed: 20 }
  }
}

```
---
&nbsp;&nbsp;

## 모듈

### `require`는 사용을 지양하고, 모든 가져오기 불러오기는 `import, export` 구문을 이용한다.
> 이유 : 최근 `import, export`로 글로벌 스탠다드로 정해지고 있고, 최신 자바스크립트 스택과 타입스크립트에서 지원한다.
```ts
import { es6 } from './AirbnbStyleGuide';

export default es6;
```
---
### `import`문으로부터 직접 `export`하지 않는다.
> 이유 : 간결성 보단 코드 가독성과 일관성 유지가 더 중요하다.
```ts
export { es6 as default } from './airbnbStyleGuide';
```
---
### `default export` 가져오기시 `wildcard import`는 사용하지 않는다.
> 이유 : 모듈 변경시에 식별자 출돌이 있을수 있다.
> [기본 가져오기 단점 링크](ttps://yceffort.kr/2020/11/avoid-default-export)
```ts
🚫
import * from './AirbnbStyleGuide';

✅ 
import * as AirbnbStyleGuide from './AirbnbStyleGuide';
```
---
### `export let`과 같은 변경 가능한 내보내기는 금지한다.
> 이유 : 이해하기 어려운 코드를 생산하고, 사이드 이팩트를 야기한다.
```ts
🚫 export let foo = 3;
// In pure ES6, foo is mutable and importers will observe the value change after a second.
// In TS, if foo is re-exported by a second file, importers will not see the value change.
window.setTimeout(() => {
  foo = 4;
}, 1000 /* ms */);
```
--- 
### `tpye` `interface`정의코드를 가져오기 할때 `type import`로 구분하자.
> 이유 : 불러오기 오버라이딩이 될수있어 오류를 야기할 수 있고, 불러오기시 명확성이 올라간다.
```ts
import { es6 } from './AirbnbStyleGuide';
import type { events } from './AirbnbStyleGuide';
```
---
### `export` 단축 구문 사용을 지향한다.
> 이유 : 코드 가독성과 코드량을 줄일 수 있다. Airbnb 컨벤션 참고
```ts
const lukeSkywalker = 'Luke Skywalker';

export {
  lukeSkywalker,
};
```
---
&nbsp;&nbsp;

## 네임스페이스

### `namespace`는 하나의 주제로 묶어서 그룹관리(내부모듈)할때 사용하며, 중복되지 않는 큰주제(primary name)로 통합니다. 상속을 이용한 구조화를 위해선 `class`를 사용하자.
> 이유 : `namespace` 하나의 공간으로 인터페이스를 통합하는것이지 상속은 지원하지 않는다.
```ts
namespace Events{
  // 내부에서만 사용
  type EventType = 'click' | 'push';
  
  const lettersRegexp = /^[A-Za-z]+$/;
  
  // 외부 노출용
  export interface EventHandlers {
    click(): void;
    push(): void;
  }
  
  export class Handler implements EventHandlers {
    
    click() {
      ...  
    }
    
    push() {
      ...
    };
  }
}
```

### 다중 파일 네임스페이스는 사용을 지양한다.
> 이유 : 기능이 너무 암시적이기 때문에 개발자 오류가 날 수 있다.
```ts
test.d.ts
namespace SomeTest{
    export class test {}
}

test2.d.ts
namespace SomeTest{
  export interface test{}
}

test.ts
/// <reference path="test.d.ts" />
/// <reference path="test2.d.ts" />

const test = new SomeTest.test(); // 암시적 오류를 발생 시킴
```
---
&nbsp;&nbsp;

## enum

### string 값 을 가진 `enum` 선언

> 이유: 컴파일된 결과물에서도 어떤 열거형인지 디버깅 가능
```ts
export enum EvidenceTypeEnum {
  UNKNOWN = 'unknown',
  PASSPORT_VISA = 'passport_visa',
  PASSPORT = 'passport',
  SIGHTED_STUDENT_CARD = 'sighted_tertiary_edu_id',
  SIGHTED_KEYPASS_CARD = 'sighted_keypass_card',
  SIGHTED_PROOF_OF_AGE_CARD = 'sighted_proof_of_age_card',
}
```
---
### 대부분의 경우 `enum` 대신 `union Type`을 사용하고, 특정 지칭 사항일때 Enum으로 특정 KeyList로써 사용하자.
> 이유 : `enum`은 컴파일된 파일을 보면 불필요한 코드가 많다. `union Type`이 대부분의 기능을 대체할 수 있다.
```ts
type ScaleType = 'display1' | 'display2' | ... ;

type Props = {
...
  scale: ScaleType
...
}
```
---
&nbsp;&nbsp;

## 연산자

### 단항 증감 연산자(++, --)를 사용하지 말자.
> 이유 : 코드 명확성을 위해서는 대신 +=1 을 사용하는것이 좋다.
```ts
🚫 num++;
✅ num += 1;
```
---
### 삼항 연산자는 중첩하여 사용하지 않는다.
> 이유 : 코드 가독성을 위해서 하나의 연산자만 사용을 권장하고 있다. 
```ts
🚫 const foo = maybe1 > maybe2
  ? "bar"
  : value1 > value2 ? "baz" : null;

✅ const foo2 = maybe1 > maybe2 ? 'bar' : maybeNull;
```
---
### 다중 연산자를 사용할때는 괄호를 사용한다.
> 이유 : 순서가 모호해 질수 있고 가독성을 위해서 괄호를 사용해준다.
```ts
if (a || (b && c)) {
  return d;
}

const foo = (a && b < 0) || c > 0 || (d + 1 === 0);
```
---
### 연산자 사이에 공백을 넣는다.
> 이유 : 코드 가독성을 위해서.
```ts
🚫const x=y+5;
✅const x2 = y + 5;
```
---
&nbsp;&nbsp;

## 조건문
### (`boolean`)논리연산자를 조건으로 사용할때 암시적 조건을 사용하지 말자. 조건 확인 유틸을 작성하여 활용하자.
> 이유 : 코드의 명확성을 위해서이고, 개발자의 휴먼 에러를 방어하고자 함이다.
> `null`, `undefined`, `0(Number)`, `''(String)`, `false` ,`[]Array` 모두 거짓으로 평가 된다.
```ts
🚫 if (!string) // 이런식으로 빈문자열 확인 보다는
  
✅  if (isEmpty(string)) {...} // 빈 문자열 
✅  if (isEmpty(list)) // 빈 배열
...
```
---
### 조건식은 한줄 짜리 구문을 사용하지 않는다.
> 이유 : 코드의 통일성과 명확성을 위해서.
```ts
🚫 if (condition) doSomething()
✅ if (condition) {
  ...
}
```
---
### `swith case`는 `default` 케이스를 필수로 작성한다. `()` `{}` 사용도 필수로 한다.
> 이유 : 에러를 방어하기 위해서.
```ts
switch (conditionValue) {
  case (value1): {
    ...
    break;
  }
  case (value2): {
    ...
    break;
  }
  default: {
    ...;
    break;
  }    
}
```
---
&nbsp;&nbsp;

## 반복문

### for-in문 안에서는 hasOwnProperty 조건 검사를 권장한다.
> 이유: 예상치 않게 상속받은 프로퍼티로 인해 문제가 생길 수 있다.
```ts
for (const prop in object) {
  
  if (object.hasOwnProperty(prop)) {
    
    ...
  }
}
```
---
&nbsp;&nbsp;

## 주석
### 한줄 주석은 `//` 를 통해서만 주석을 작성한다. 시작때 공백을 넣어준다.
> 이유 : 가독성을 높여준다. 글로벌 컨벤션에 따른다.
```ts
🚫
const active = true;  // is current tab

✅
// is current tab
const active = true;
```
---
### 협업(코드리뷰등)을 위해서 사용하는 주석에는 목적 `FIXME:` `TODO:` 를 주석에 붙여준다.
> 이유 : 다른 개발자의 주석에 대한 이해를 빠르게 해준다.
```ts
class Calculator extends Abacus {
  constructor() {
    super();

    // FIXME: 전역 변수를 사용해서는 안 됨
    total = 0;
  }
}

class Calculator extends Abacus {
  constructor() {
    super();

    // TODO: total은 옵션 파라메터로 설정해야함
    this.total = 0;
  }
}
```

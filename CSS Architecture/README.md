# CSS Architecture

# CSS Architecture

## 1. CSS Architecture란?

1. CSS
   - CSS의 목적은 HTML 요소를 대상으로 선택자를 정의하고 스타일을 적용하는 것이다.
   - 대규모의 복잡한 프로젝트로 갈수록 무분별한 CSS는 혼돈을 줄 수 있다.
   - 이것이 CSS 아키텍쳐가 유용한 이유이다.
2. CSS 아키텍쳐
   - CSS 작성을 이유 있는 방향으로 이끌어 주는 역할을 해준다.
   - 개발자의 코드 예측을 용이하게 해준다.
   - 유지 보수성과 확장성, 재사용성에 도움이 되는 가이드라인을 제시해준다.

## 2. CSS Architecture의 목적

1. CSS 아키텍쳐의 주요 목적 4가지

   - Predictable (예측 가능하게):
     - 예측 가능한 CSS는 예상대로 작동해야 함을 의미한다.
     - 새로운 규칙을 추가하거나 변경할 때 다른 부분에 예상치 못한 영향을 주지 않아야한다.
     - 대규모 웹 사이트에서 매우 중요하다.
   - Reusable (재사용 가능하게):
     - CSS의 규칙은 충분히 추상적이면서 독립적이어야 한다.
     - 새로운 웹 구성요소를 만들 때 기존에 만들어 놓은 CSS를 재사용 가능하게 해야한다.
   - Scalable (확장 가능하게):
     - 웹 사이트의 규모와 복잡성이 증가해도 유지보수하기 쉬어야한다.
   - Maintainable (유지 보수 가능하게):
     - 새로운 구성 요소나 기능이 추가, 수정 또는 재배치될 때 기존의 CSS를 다시 작성할 필요가 없어야 한다.

1. 이러한 목적을 달성하기 위해서는?
   - 일관된 코딩 스타일
     - 코드 컨벤션 도입
   - 모듈화된 CSS 구조
     - 각 컴포넌트 또는 모듈에 해당하는 CSS 파일을 분할
   - 주석 활용
     - 목적, 역할, 중요 정보를 설명
   - 선택자의 특수성 관리
     - 선택자 특수성
       - 스타일 규칙이 어떤 요소에 적용되는지 우선 순위를 결정하는 방식
     - 선택자의 특수성을 최소화하고 효율적으로 관리해야한다.
       - 불필요하게 과도한 특수성은 예상치 않은 스타일 우선 순위 문제를 일으킬수 있다.
     - 가급적이면 ID 선택자를 피하고 클래스 또는 요소 선택자를 사용해야 한다.
       - ID 선택자는 특정한 요소에 대한 스타일을 정의하므로 재사용 가능한 스타일 규칙을 작성하는 데 적합하지 않다.
   - CSS 전처리기의 활용
     - CSS 전처리기(Sass,Less)를 사용하여 변수, 믹스인, 네스팅, 상속 등을 활용하여 CSS를 보다 모듈화하여 관리하기 쉽게 한다.
     - DRY원칙을 지킬 수 있고, 스타일을 유연하게 수정 가능하다.
   - CSS 아키텍쳐 패턴 적용
     - OOCSS(Object-Oriented CSS)
     - BEM(Block Element Modifier)
     - SMACSS(Scalable and Modular Architecture for CSS)

# 예시

## 1. 깊은 선택자 사용

1. 선택자가 복잡할수록 HTML과 밀접하게 연결된다.

   ```css
   #main-search ul li ul li div {
   }
   #content-block article h1:first-child {
   }
   #footer > div > h1 + p {
   }
   ```

2. 문제점
   - 만약 다른 HTML 구조를 가진 다른 컴포넌트가 같은 스타일을 재사용해야 한다면, 전체 스타일을 다시 만들어야 한다.
   - HTML이 수정될 경우 깊은 선택자 사용은 예측이 어렵다.
   - 유지보수가 힘들고, 확장 가능하지 않다.
3. CSS 선택자가 원하지 않은 요소에 스타일을 적용하지 않도록 하는 가장 좋은 방법은 그런 기회를 제공하지 않는 것이다.
   - 클래스 선택자를 이용하여 원치 않는 요소에 적용되는것을 피하여 예측 가능하게 유지해야한다.

## 2. 관심사 분리

1. CSS 코드를 작성할 때 스타일과 레이아웃 및 위치 관련 관심사를 분리해야 한다.

   ```css
   .left-block {
     position: absolute;
     top: 10px;
     left: 10px;
     background-color: black;
     font-size: 15px;
     text-transform: uppercase;
   }
   ```

   - 스타일과 레아아웃 및 위치를 모두 처리하고 있다.
     - 재사용하려고 하면 스타일 외에도 위치 및 레이아웃 정보도 함께 복사해야 하므로 중복 코드가 발생한다.
   - 스타일만 다루는 클래스와 레이아웃 및 위치 관련 스타일을 별도의 클래스로 분리하자
     - 다른 컴포넌트에서 각각의 클래스를 활용할 수 있어 코드 중복을 방지할 수 있다.
     - 유지보수성 및 협업에 대한 효율성이 증가된다.

## 3. 클래스의 Namespace

1. 거의 모든 웹 사이트에서는 일반적으로 동일한 디자인 요소가 여러 곳에서 사용된다.

   - 몇몇의 구역에서 특정한 경우를 제외하고 디자인을 조금 다르게 적용해야 할 때, 별도의 부모 요소를 찾거나 만들고 그 부분을 처리하는 새로운 CSS를 만드는 경우가 있다.

   ```css
   .widget {
     background-color: yellow;
     border: 1px solid black;
     color: black;
     width: 50%;
   }

   #sidebar .widget {
     width: 200px;
   }

   body.homepage .widget {
     background: white;
   }
   ```

1. 위 코드에 대한 문제점

   - `widget`의 스타일은 예측하기 어렵다.
     - `sidebar`나 `homepage`에서 `widget`을 사용하면 동일한 마크업임에도 불구하고 다르게 보일것이다.
   - 재사용성과 확장성이 떨어진다.
     - 다른 페이지에서 `widget`을 `hompage widget`처럼 보이도록 하려면 새로운 CSS를 추가해야 한다.
   - 관리가 어렵다.
     - `widget`의 디자인이 변경되면 여러 위치에서 수정해야 한다.

1. 더 나은 방법은 클래스에 Namespace를 부여하는것

   ```css
   .widget {
   }
   .widget-title {
   }
   .widget-content {
   }
   ```

   - 컴포넌트 내에서 모든 하위 요소 클래스가 동일한 이름을 공유하게 한다.
     - 컴포넌트의 하위 요소를 스타일링할 때 필요한 특수성을 줄이고 기존 클래스와의 충돌 가능성을 줄일 수 있다.
   - 이러한 방식을 통해 CSS 코드를 예측 가능하게 만들고 스타일링을 일관성있게 유지하면서도 다양한 상황에서 재사용 가능하고 유지 보수성을 높일 수 있다.

## 4. 수정된 클래스로 컴포넌트 확장

1. 특정 환경에서 스타일을 조금 다르게 보이도록 하려면 기존 컴포넌트를 확장하기 위한 수정자 클래스를 만들자

   ```css
   /* Bad */
   .button {
   }
   #primary .button {
   }

   /* Good */
   .button {
   }
   .button-primary {
   }
   ```

   - 수정자 클래스는 어디서든 사용될 수 있고 필요한 만큼 자주 사용될 수 있다.
   - 개발자의 의도를 명확하게 보여준다.

<aside>
💡 클래스의 Namespace와 수정된 클래스로 컴포넌트 확장의 차이점

클래스의 Namespace은 그들이 속한 컴포넌트의 이름으로 그룹화하여 스타일을 구조화하고 특정성 충돌을 방지하는데 사용된다.

수정된 클래스는 특정 컴포넌트를 확장하거나 변경하여 다른 환경에서 더 특정한 스타일을 적용할 때 사용된다.

따라서 Namespace를 사용하는 것은 주로 컴포넌트의 스타일을 구조화하고 충돌을 방지하기 위한 것이며, 수정자 클래스는 특정 컴포넌트를 다양한 상황에 맞게 확장하거나 수정하는데 사용된다.

두가지 모두 CSS코드를 더 모듈화하고 유지관리하기 쉽게 만들어준다.

</aside>

## 5. CSS 방법론 사용

1. CSS 방법론

   - CSS 코드를 보다 효과적으로 구조화하고 유지 관리하기 위한 접근 방식이다.
   - 장점
     - 확장성: 프로젝트가 성장하더라도 CSS 코드를 쉽게 관리할 수 있다.
     - 유지보수성: 코드를 수정하거나 업데이트할 때 문제가 발생할 가능성을 줄일 수 있다.
     - 재 사용성: 디자인 요소를 다른 프로젝트에서도 재 사용할 수 있다.

1. 종류

   [**OOCSS (Object Oriented CSS)**](./OOCSS/README.md)

   [**BEM (Block Element Modifier)**](./BEM/README.md)

   - **SMACSS (Scalable and Modular Architecture for CSS)**

## 6. **preprocessors 사용**

1. preprocessors란?
   - CSS의 기본 기능을 확장하는 스크립트 언어.
     - CSS 코드에서 변수, 믹스인, 네스팅, 수학 연산, 이스케이핑을 사용할 수 있다.
     - 반복적인 작업을 자동화하고 코드의 중복과 오류를 방지하며 재사용 가능한 코드 조각을 작성할 수 있다.
     - 역하위 호환성(이전 버전과 호환성을 유지하면서 구현하거나 사용될 수 있는 능력을 가르키는 개념)을 보장할 수 있다.
2. 주요 기능

   - 변수

     ```sass
     $width: 10px;
     $height: @width + 10px;

     #header {
     	width: @width;
     	height: @height;
     }

     // compiled
     #header {
     	width: 10px;
     	height: 20px;
     }
     ```

   - 믹스인

     - 하나의 rule-set에서 다른 rule-set으로 스타일을 포함하는 방법이다.

     ```sass
     .bordered {
     	border-top: dotted 1px black;
     	border-bottom: solid 2px black;
     }

     #menu a {
     	color: #111;
     	.bordered();
     }

     .post a {
     	color: red;
     	.bordered();
     }
     ```

     - `.bordered`의 스타일은 `#menu a` 및 `.post a`에 모두 나타난다.

   - 네스팅

     - 캐스케이딩을 중첩과 결합하여 사용할 수 있다.
       - 캐스케이딩 (Cascading)
         - CSS에서 사용되는 스타일 규칙을 적용하고 관리하는 방식을 나타내는 개념

     ```sass
     #header {
     	color: black;
     }

     #header .navigation {
     	font-size: 12px;
     }

     // 네스팅

     #header {
     	color: black;
     	.navigation {
     		font-size: 12px;
     	}
     }
     ```

   - 중첩된 At-Rules 및 버블링

     ```sass
     .component {
         width: 300px;
         @media (min-width: 768px) {
             width: 600px;
             @media (min-resolution: 192dpi) {
                 background-color: yellow;
             }
         }
         @media (min-width: 1280px) {
             width: 800px;
         }
     }

     // output
     .component {
         width: 300px;
     }
     @media (min-width: 768px) {
         .component {
             width: 600px;
         }
     }
     @media (min-width: 768px) and (min-resolution: 192dpi) {
         .component {
             background-color: yellow;
         }
     }
     @media (min-width: 1280px) {
         .component {
             width: 800px;
         }
     }
     ```

     - @media 또는 @supports와 같은 At-Rules는 선택자와 같은 방식으로 중첩될 수 있다.
     - 버블링
       - 중첩된 At-Rules의 작동 방식을 나타낸다.
       - At-Rules은 기존 스타일 규칙과 동일한 ruleset 내에서 중첩될 수 있으며, 이것은 At-Rule이 다른 스타일 규칙에 영향을 미치는 방식을 설명한다.
         - At-Rule이 위에서 아래로 "버블링"되며, 조건이 맞으면 해당 At-Rule 내에 선언된 스타일 규칙이 적용됩니다.
     - 이것은 웹 페이지를 다양한 환경에서 반응적으로 만드는데 도움을 주며, 특정 조건에 따라 스타일을 조절할 때 유용하다.

   - 수학연산

     - 수학 연산인 `+, -, *, /`는 숫자, 색상 또는 변수에 대해 활용할 수 있습니다.
     - 결과 값의 단위는 가장 왼쪽에 사용된 단위를 갖는다.
       - 변환이 불가능하거나 의미가 없는 경우 단위는 무시다.
         - ex) px → cm 변환, rad → % 변환은 불가능하다.
       - 길이와 길이를 곱하거나 나눌시 CSS는 면적을 지원하지 않기 때문에 단위 그대로를 사용한다

     ```sass
     $conversion-1: 5cm + 10mm; // 6cm
     $conversion-1: 2 - 3cm - 5mm; // -1.5cm

     $incompatible-units: 2 + 5px - 3cm; // 4px

     $base: 5%;
     $filler: $base * 2; // 10%
     $other: $base + $filler // 15%

     $base2: 2cm * 3mm; // 6cm
     $color: #224488 / 2; // #112244
     ```

   - 이스케이핑

     - 임의의 문자열을 속성 또는 변수 값으로 사용할 수 있게 해준다.

     ```sass
     $min768: unquote("(min-width:768px)");
     .element {
         @media #{$min768} {
             font-size: 1.2em
         }
     }

     //result

     @media (min-width: 768px) {
         .element {
             font-size: 1.2em
         }
     }
     ```

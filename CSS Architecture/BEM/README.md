# BEM (Block Element Modifier)

# BEM이란 무엇인가?

- BEM (Block, Element, Modifier)은 웹 개발의 컴포넌트 요소 중심적인 접근 방식이다.
- Block, Element, Modifier 요소를 더블 언더바 (`__`)와 더블 하이픈 (`--`)으로 구분지어 작성한다.
  ```css
  .header__navigation--navi-text {
    ...;
  }
  ```
  - header는 Block, navigation은 Element, navi-text는 Modifier=

# Block, Element, Modifier

## 1. Block

1. 재사용이 가능하고 종속되지 않은 기능적으로 독립적인 컴포넌트를 말한다.
   - 독립적으로 사용되니 여백 또는 위치값(margin, position)은 선언하지 않는것이 좋다.
2. 블록의 이름은 그 목적을 설명해야 한다.

   - **“무엇인가”**를 설명해야지 어떻게 보이는가가 아니다.

   ```html
   <!-- 올바른 방식. `error` "무엇인가" -->
   <div class="error"></div>

   <!-- 잘못된 방식. 외관을 설명합니다 "어떻게 보이는가"-->
   <div class="red-text"></div>
   ```

3. 블록은 서로 중첩 가능하며 우선순위 또는 계층 구조가 없다.

   ```html
   <!-- `header` 블록 -->
   <header class="header">
     <!-- 중첩된 `logo` 블록 -->
     <div class="logo"></div>

     <!-- 중첩된 `search-form` 블록 -->
     <form class="search-form"></form>
   </header>
   ```

## 2. Element

1. 블록의 구성 요소로 독립적으로 사용할 수 없는 부분이다.
   - 엘리멘트는 의존적이며 자신이 속한 블록내에서 의미를 가지기 때문에 다른곳에서 재사용 하는건 불가능하다.
2. 더블 언더바 (`__`)로 구분한다.

   ```html
   <!-- `search-form` 블록 -->
   <form class="search-form">
     <!-- `search-form` 블록 내의 `input` 엘리먼트 -->
     <input class="search-form__input" />

     <!-- `search-form` 블록 내의 `button` 엘리먼트 -->
     <button class="search-form__button">검색</button>
   </form>
   ```

3. 엘리멘트는 서로 중첩될 수 있으며 중첩 레벨 수에 제한이 없다.

   ```html
   <!--
       올바른 방식. 전체 엘리먼트 이름의 구조는 다음 패턴을 따릅니다:
       `block-name__element-name`
   -->
   <form class="search-form">
     <div class="search-form__content">
       <input class="search-form__input" />

       <button class="search-form__button">검색</button>
     </div>
   </form>

   <!--
       잘못된 방식. 전체 엘리먼트 이름의 구조가 다음 패턴을 따르지 않음:
       `block-name__element-name`
   -->
   <form class="search-form">
     <div class="search-form__content">
       <!-- 권장: `search-form__input` 또는 `search-form__content-input` -->
       <input class="search-form__content__input" />

       <!-- 권장: `search-form__button` 또는 `search-form__content-button` -->
       <button class="search-form__content__button">검색</button>
     </div>
   </form>
   ```

## 3. Modifier

1. 모디파이어는 블럭이나 엘리먼트의 외관, 상태 및 동작과 관련된 속성을 담당하며 더블 하이픈(`--`)으로 구분한다.
2. Modifier의 유형
   - Boolean
     -
   - Key-value

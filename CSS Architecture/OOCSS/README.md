# OOCSS (Object Oriented CSS)

# OOCSS란 무엇인가?

- 객체 지향 설계 원칙을 적용하여 동적 CSS를 더 관리하기 쉽게 만드는 것이 목표인 객체 지향 CSS(OOCSS)이다.
- OOCSS를 사용하여 재사용 가능하고 확장 가능하며 관리하기 쉬운 CSS를 얻을 수 있다.
- 단일 책임 원칙과 관심사 분리를 비롯한 객체 지향 프로그래밍의 여러 개념을 활용한다.
- 목표는 유연하고 모듈식이며 교체 가능한 컴포넌트를 생성하는 것이다.

# OOCSS의 두가지 원칙

## 1. 구조(structure)와 모양(skin)의 분리

1. 구조 (structure)

   - 사용자에게 보이지 않는 요소
     - Height
     - Width
     - Margins
     - Padding
     - Overflow

1. 모양 (skin)
   - 요소의 시각적 요소
     - Colors
     - Fonts
     - Shadows
     - Gradients

<aside>
💡 OOCSS는 이들을 분리하여 정의한다.

</aside>

1. 예시

   ```sass
   .button {
       width: 150px;
       height: 50px;
       background: #FFF;
       border-radius: 5px;
   }

   .button-2 {
       width: 150px;
       height: 50px;
       background: #000;
       border-radius: 5px;
   }
   ```

   `width, height, border-radius` 같이 반복되는 코드가 많으면 스타일을 혼란스럽게 만든다. OOCSS를 사용하여 동일한 속성을 상속하는 모든 스킨에서 공통 패턴을 추출할 수 있다.

   ```sass
   .button {
       background: #FFF;
   }
   .button-2 {
       background: #000;
   }
   .skin {
       width: 150px;
       height: 50px;
       border-radius: 5px;
   }
   ```

   프로젝트가 커질 수록 모든 요소를 클래스로 따로 정의함으로써 구조에 대한 재사용 가능한 스킨을 만들 수 있다.

   ```html
   <a class="button skin" href="#">홈</a>
   <a class="button-2 skin" href="#">블로그</a>
   ```

## 2. 컨테이너와 컨텐츠의 분리

1. 컨테이너와 컨텐츠를 분리하면 더 일관적이고 예측 가능한 코드를 작성 할 수 있다.

   ```css
   #sidebar {
     padding: 2px;
     left: 0;
     margin: 3px;
     position: absolute;
     width: 140px;
   }

   #sidebar .list {
     margin: 3px;
   }

   #sidebar .list .list-header {
     font-size: 16px;
     color: red;
   }

   #sidebar .list .list-body {
     font-size: 12px;
     color: #fff;
     background-color: red;
   }

   /* 컨테이너와 컨텐츠를 분리 */
   .sidebar {
     padding: 2px;
     left: 0;
     margin: 3px;
     position: absolute;
     width: 140px;
   }

   .list {
     margin: 3px;
   }

   .list-header {
     font-size: 16px;
     color: red;
   }

   .list-body {
     font-size: 12px;
     color: #fff;
     background-color: red;
   }
   ```

   자식 선택자를 피하는 것은 컨테이너와 컨텐츠를 분리하기 위한 좋은 전략이다. 고유한 요소에 고유한 클래스를 할당하는 것이 중요하다.

# OOCSS의 장점

1. 속도
   - OOCSS를 사용하면 DRY원칙을 따르게 되고 결과적으로 CSS 파일을 작아져서 다운로드 속도가 빠르게 된다.
2. 확장성
   - 요소의 컨텍스트에 크게 신경 쓰지 않고 다른 요소에 자유롭게 클래스를 혼합하고 다시 적용할 수 있다.
3. 유지관리성
   - HTML 마크업을 추가하거나 재 배치할 때 CSS 흐름을 생각할 필요가 없다.
   - 대규모 프로젝트에 유용하다.

# OOCSS의 단점

1. 요소에 사용되는 클래스 수의 증가
   - 여러 스타일을 추가하기 위해 하나의 요소에 여러 클래스를 작성해 혼란을 줄수 있다

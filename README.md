# 프론트엔드 CS #1 브라우저

#### I - 1. 브라우저의 주요 기능

---

- 브라우저의 주요 기능 = 사용자가 선택한 자원을 서버에 요청하고 브라우저에 표시하는 것
- 브라우저는 HTML과 CSS에 따라 HTML 파일을 해석해서 표시



#### I - 2. 브라우저의 기본 구조

---

- 사용자 인터페이스 - 주소 표시줄, 이전/ 다음 버튼 등 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분
- 브라우저 엔진 - 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어
- 렌더링 엔진 - 요청한 콘텐츠를 표시
- 통신 - HTTP 요청과 같은 네트워크 호출에 사용
- UI 백엔드 - 콤보 박스와 창 같은 기본적인 장치를 그림
- 자바스크립트 해석기 - 자바스크립트 코드를 해석하고 실행
- 자료저장소 - 자료를 저장하는 계층. 쿠키를 저장하는 것과 같이 모든 종류의 자원을 하드 디스크에 저장할 필요가 있다.

#### I - 3. 렌더링 엔진과 동작과정

---

- 크롬과 사파리는 Webkit 엔진을, 파이어폭스는 Gecko 엔진을 사용
- 동작과정

1.  DOM 트리구축을 위한 HTML 파싱
2. 렌더 트리 구축
3. 렌더 트리 배치
4. 렌더 트리 그리기



![helloworld-59361-3](README.assets/helloworld-59361-3.png)



#### I - 4. 파싱

- 문서 파싱은 브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것
- 파싱 결과는 보통 문서 구조를 나타내는 노드 트리인데 이를 파싱 트리 혹은 문법 트리라고 한다

- 파싱은 문서에 작성된 언어 또는 형식의 규칙을 따른다. 이를 문맥 자유 문법이라고 한다



##### 파서-어휘 분석기 조합

- 파싱은 어휘 분석과 구문 분석이라는 두 가지로 구분할 수 있다
- 어휘 분석 = 자료를 토큰으로 분해하는 과정 
- 토큰은 유효하게 구성된 단위의 집합체로 예를 들자면 사전에 등장하는 모든 단어와 같다
- 파서는 자료를 유효한 토큰으로 분해하는 어휘분석기가 있고 언어 구문 규칙에 따라 문서 구조를 분석함으로써 파싱 트리를 생성하는 파서가 있다. 
- 어휘 분석기는 공백과 줄 바꿈같은 의미없는 문자를 제거한다.



![helloworld-59361-6](README.assets/helloworld-59361-6.png)

- 파싱을 반복하면서 어휘 분석기로부터 새 토큰을 받아서 구문 규칙과 일치하는지 확인하고 맞으면 토큰에 해당하는 노드를 파싱트리에 추가
- 맞지 않으면 파서는 토큰을 내부적으로 저장하고 토큰과 일치하는 규칙이 발견될 때 까지 요청한다. 맞는 규칙이 없는 경우 예외로 처리한다.

##### 변환

소스 코드를 기계 코드로 만드는 컴파일러는 파싱 트리 생성 후 이를 다시 기계 코드 문서로 변환한다

##### 파서의 종류

파서는 하향식 파서와 상향식 파서로 나뉜다.

- 하향식 파서

  - 구문의 상위 구조로부터 일치하는 부분을 찾는다

  - ex) 

    2+3-1을 파싱할 때

    1. 하향식 파서는 2+3과 같은 표현식에 해당하는 높은 수준의 규칙을 먼저 찾는다.
    2. 그 다음 표현식으로 2+3-1을 찾는다. 
    3. 표현식을 찾는 과정은 일치하는 다른 규칙을 점진적으로 더 찾아내는 방식인데 가장 높은 수준의 규칙을 먼저 찾는다

- 상향식 파서

  - 구문의 낮은 수준에서 점차 높은 수준으로 찾는다
  - ex)
    1. 입력 값이 규칙에 맞을 때까지 찾아서 맞는 입력 값을 규칙으로 바꾼다. 이 과정을 입력 값의 끝까지 진행된다
    2. 상향식 파서는 입력 값의 오른쪽으로 이동하면서 구문 규칙으로 갈수록 남는 것이 점차 감소하기 때문에 이동-감소 파서라고 부른다.

  

  ##### HTML 파서

  HTML 파서는 HTML 마크업을 파싱 트리로 변환한다.

  전통적인 파서는 HTML에 적용할 수 없다. HTML은 파서가 요구하는 문맥 자유 문법에 의해 쉽게 정의할 수 없기 때문이다!!!

  

  - 파싱은 대신 CSS와 자바스크립트를 파싱하는데 사용된다

  

  HTML 정의를 위한 공식적인 형식으로 DTD가 있지만 문맥 자유 문법이 아니다.

  

  ##### DOM

  DOM은 문서 객체 모델(Document Object Model)이다. 파싱트리는 DOM 요소와 속성 노드의 트리로서 출력 트리가 된다.

  

  DOM은 HTML 문서의 객체 표현이고 외부를 향하는 자바스크립트와 같은 HTML 요소의 연걸 지점이다. 트리의 최상위 객체는 문서이다.

  

  ###### !! DOM은 마크업과 1:1의 관계를 맺는다.



##### HTML의 파싱 알고리즘

- HTML은 일반적인 하향식이나 상향식 파서로 파싱이 불가하다!

- HTML의 파싱 알고리즘은 토큰화와 트리 구축의 2단계!
- 

![helloworld-59361-9](README.assets/helloworld-59361-9-16661673834362-16661673848104.png)



##### 토큰화 알고리즘

결과물로 HTML 토큰을 생성한다.

알고리즘은 상태 기계(state machine)이라고 볼 수 있다!

각 상태는 하나 이상의 연속된 문자를 입력받아 문자에 따라 다음 상태를 갱신한다.

- ###### 결과는 현재의 토큰화 상태와 트리 구축 상태의 영향을 받는다!!!

- ###### 같은 문자여도 현재 상태에 따라 다음 상태의 결과가 다르게 나오는 것!!

1. 초기 상태는 자료 상태이다. < 문자를 만나면 태그 열림 상태로 변한다.
2. a부터 z까지의 문자를 만나면 시작 태그 토큰을 생성하고 상태는 태그 이름 상태로 변한다.
3. `>` 문자를 만나면 현재 토큰이 발행되고 상태가 다시 자료 상태로 바뀐다.



##### 트리 구축 알고리즘

파서가 생성되면 문서 객체가 생성된다. 트리 구축이 진행되는 동안 문서 최상단에는 DOM 트리가 수정되고 요소가 추가된다. 토큰화에 의해서 발행된 각 노드가 트리 생성자에 의해 처리된다. DOM 트리에 요소를 추가하는 것이 아니라면 열린요소는 스택(임시 버퍼 저장소)에 추가된다. 이 스택은 부정확한 중첩과 종료되지 않은 태그를 교정한다.



트리구축 단계의 입력값은 토큰화 단계에서 만들어지는 토큰이다.

![helloworld-59361-11](README.assets/helloworld-59361-11-16662760135977.png)



##### 파싱이 끝난 후

이 단계에서 브라우저는 문서와 상호작용할 수 있게 되고 문서 파싱 이후 실행하는 지연 모드 스크립트를 파싱 시작한다. 문서 상태는 완료가 되고 로드 이벤트가 발생





#### I - 5 CSS 파싱

CSS는 문맥자유문법이기 때문에 기본적인 파서 유형으로 파싱이 가능하다



##### 웹킷 CSS 파서

웹킷은 CSS 문법 파일로부터 자동으로 파서를 생성하기 위해 플렉스와 바이슨 파서 생성기를 사용한다. 바이슨은 상향식 이동 감서 파서를 생성하고 파이어폭스는 하향식 파서를 사용한다. 



두 경우 모두 각 CSS 파일은 스타일 시트 객체로 파싱되고 각 객체가 CSS 규칙을 포함한다!

![helloworld-59361-12](README.assets/helloworld-59361-12-16666206765712.png)



##### 스크립트와 스타일 시트의 진행 순서



###### 스크립트 

웹은 파싱과 실행이 동시에 수행되는 동기화 모델

파서가 <script>태그를 만나면 즉시 파싱하고 실행하고, 스크립트가 실행되는 동안 파싱은 중단된다.HTML5는 스크립트를 비동기로 처리하는 속성을 추가했기 때문에 별도의 맥락에 의해 파싱되고 실행된다.



###### 예측 파싱

웹킷과 파이어폭스는 예측파싱과 같은 최적화를 지원한다. 스크립트를 실행하는 동안 다른 스레드는 네트워크로부터 다른 자원을 내려받고 문서의 나머지 부분을 파싱한다. 

즉 병렬로 자원을 연결하여 받아 전체적인 속도를 개선한다. 예측 파서는 DOM 트리는 수정하지 않고 메인파서의 일로 넘긴다. 예측 파서는 외부 스크립트, 외부 스타일스트와 같이 참조된 외부 자원을 파싱한다.



###### 스타일 시트

스타일 시트는 DOM트리를 변경하지 않기 때문에 문서 파싱을 기다리거나 중단할 이유가 없다. 하지만 스크립트가 문서를 파싱하는 동안 스타일 정보를 요청하는 경우면 문제가 된다!! 

==> 스타일이 파싱되지 않은 상태라면 스크립트는 잘못된 결과를 내놓기 때문!

- 파이어폭스는 아직 로드 중이거나 파싱중인 스타일 시트가 있는 경우 모든 스크립트의 실행을 중단한다

- 웹킷은 로드되지 않은 스타일 시트 가운데 문제가 될만한 속성이 있을 때만 스크립트를 중단한다.



#### 렌더 트리 구축

DOM 트리가 구축되는 동안 브라우저는 렌더 트리를 구축

파이어폭스는 이 시각적인 구성 요소를 형상(frames)라고 부르고 웹킷은 렌더러 혹은 렌더 객체(render object)라고 한다



각 렌더러는 css2 명세에 따라 노드의 css 박스에 부합하는 사각형을 표시한다. 렌더러는 기하학적 정보를 포함한다.

박스 유형은 display 스타일 속성의 영향을 받는다.

##### DOM 트리와 렌더 트리의 관계

렌더러는 DOM 요소에 부합하지만 1:1 대응 관계는 아님!

Head와 같은 비시각적 DOM 요소는 렌더트리에 추가 되지 않고 display 속성이 none 인 요소는 트리에 나타나지 않는다

여러개의 시각 객체와 대응하는 DOM 요소

ex) select( 표시 영역, 드롭다운 목록, 버튼) 

도 있다.



##### 트리를 구축하는 과정

파이어폭스: 프레젠테이션은 DOM 업데이트를 위한 리스너로 등록된다. 프레젠테이션이 형상 만들기를 FrameConstructor에 위임하고 이것이 스타일을 결정하고 형상을 만든다.



웹킷: 스타일을 결정하고 렌더러를 만드는 과정을 attachment라고 한다. 모든 DOM 노드에 attach 메서드가 있다. 어테치먼트는 동기적이다. DOM 트리에 노드를 추가하면 새 노드의 attach 메서드를 호출한다.



HTML 태그와 BODY 태그를 처리함으로써 렌더 트리 루트를 구성

루트렌더 객체는 포함 블록과 일치한다.

파이어폭스는 ViewPortFrame, 웹킷은 RenderView라고 한다.



##### 스타일 계산

렌더 트리를 구축하려면 각 요소의 스타일 속성을 계산함으로서 각 렌더 객체의 시각적 속성을 계산한다.



스타일은 인라인 스타일요소,  HTML 시각적 속성과 같은 다양한 스타일 시트를 포함한다.



###### 스타일 시트를 계산하는 것의 문제점!

1. 스타일 데이터 구성이 매우 광범위해서 메모리 문제 발생 가능
2. 최적화되어 있지 않다면 각 요소에 할당된 규칙을 찾는 것은 성능 문제를 야기할 수 있다.
3. 규칙을 적용하는 것은 계층 구조를 파악해야하는 꽤나 복잡한 다단계 규칙을 수반한다.

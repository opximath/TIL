# 시퀸스 다이어그램 (SequenceDiagram)
## 정의
시퀸스 다이어그램이란 객체 지향의 소프트웨어 표준 설계 방법인 UML(Unified Modeling Language)의 하나로, 시계열로 정렬된 객체 상호작용을 보여준다. 시나리오 기능을 수행하는데 필수적인 객체들 간에 교환되는 일련의 메시지들과 시나리오에 수반되는 객체와 클래스를 표현한다.
일반적으로 개발 중인 시스템의 논리적 뷰의 유즈 케이스 실현화와 관련된다. 시퀸스 다이어그램은 이벤트 다이어그램, 이벤트 시나리오라고도 부른다 [1].
## 툴
UML 툴은 정말 많지만, 학부생때 수업으로 StarUML을 사용해본 경험이 있다 [2]. 아울러, 전문연구요원으로 일하면서 연구과제의 보고서 작성시 웹 기반의 Lucid Chart를 사용해보았었다 [3]. 좀 더 조사해보니 Microsoft의 Visio도 UML에 작성에 활용한다고한다 [4].
## 구성
시퀸스 다이어그램은 라이프 라인(Life line), 활성 박스(Activation Box), 메시지(Message), 가드(Guard), 프래그먼트(Fragment)로 구성되어있다.  

<img width="100%" src="https://github.com/opximath/TIL/blob/main/Software%20Engineering/Image/SeqDiagram.png"/>  

**그림 1. 시퀸스 다이어그램 구성**

그림 1을 통해 시퀸스 다이어그램의 구성을 살펴볼 수 있다.

- 라이프 라인 : 모델링이 되는 인스턴스를 표현하는데, 객체의 관점으로 표현한다면 클래스, 서비스 관점으로 표현한다면 컴포넌트가 된다.
- 활성 박스 : 라이프 라인의 인스턴스가 다른 인스턴스와 상호 작용을 하며 활성화 되어있는 상태를 나타낸다.
- 메시지 : 인스턴스 간 주고 받은 데이터를 표현한다. 일반적으로 요청과 응답으로 표현한다.

<img width="100%" src="https://github.com/opximath/TIL/blob/main/Software%20Engineering/Image/SeqDiagram_message.png"/>  

**그림 2. 메시지의 유형**  

그림 2를 통해 시퀸스 다이어그램의 메시지 유형을 살펴볼 수 있다.

- 동기 메시지(Sync message) : 요청을 보낸 후 반환이 올때까지 대기
- 비동기 메시지(Async message) : 요청을 보낸 다음 반환을 기다리지 않고 다른 작업을 수행
- 자체 메시지(Self message) : 자기 자신에게 요청을 보냄
- 반환 메시지 (Reply/Return message) : 요청에 대해 메시지를 반환

## 흐름 제어
앞서 살펴본 메시지를 활용하여 충분히 시퀸스 다이어그램을 그릴 수 있다. 하지만 조건문, 반복문 등 시간 순으로 인스턴스 간 상호작용을 표현하기 때문에 제어문이 필요할 경우가 있다. 이 경우, 가드(Guard)와 복합 프래그먼트(Combined fragment)를 활용할 수 있다.

- 가드 : 단일 메시지에 대해 조건을 명시할 수 있는 방법이며, 메시지의 앞 쪽에 대괄호([])를 감싸서 조건을 명시한다.
- 복합 프래그먼트 : 범위로 조건을 명시할 수 있다. 특정 부분에 대해 메시지를 반복하거나 조건을 명시할 때 사용된다.

|명칭|기호|처리내용|
|---|---|---|
|Alternatives|alt|조건에 의한 분기 처리(if else)|
|Assertion|assert|절대 처리(정의된 로직이 반드시 성립되는 처리)|
|Parallel|par|병렬처리|
|Consider|consider|중심이 되는 중요한 처리|
|Option|opt|조건이 만족될 때만 실행되는 처리 (if)|
|Reference|ref|다른 시퀀스 다이어그램의 참고|
|Loop|loop|반복처리|
|Break|break|조건이 만족되는 시점에 중단되는 처리|
|Negative|neg|부정 처리(보통 발생하지 않는 처리)|
|Critival Region|critical|인터럽트와 중단을 허용하지 않는 배타처리|
|Ignore|ignore|실행시에 무시하는 처리 (이 시퀀스 다이어그램 중에서는 관계없다는 것을 명시적으로 표시할 때에 사용)|  

**표 1. 복합 프래그먼트의 분류 [6]**  

<img width="100%" src="https://github.com/opximath/TIL/blob/main/Software%20Engineering/Image/SeqDiagram_combinedFragment.png"/> 

**그림 3. 복합 프래그먼트의 예시** 

그림 3과 같이 복합 프래그먼트를 활용하여 다양한 표현이 가능하다.

## 시퀸스 다이어그램 작성시 주의점  
### 반드시 시나리오를 명확히한 후에 작성한다.  
- 시나리오가 명확하지 않은 상황에서 시퀸스 다이어그램을 작성한다면 정밀도가 낮은 결과가 나오기 때문이다.

### 시퀸스 다이어그램 1개당 하나의 시나리오가 기본이다.
- 가독성을 위해 1개 시퀸스 다이어 그램에 1개의 시나리오를 작성하는 것이 일반적이다.

### 길어질 것 같은 시퀸스 다이어그램은 분리하자.
- 시나리오에 따라 시퀸스 다이어그램이 옆으로 길어져 버리는 경우가 있는데, ref 등의 복합 프래그먼트를 활용하여 분리한다.

### 메시지의 작성법을 정의해두자.
- 메시지를 받는 관점에서 작성할 것인지 송신하는 쪽에서 작성할 것인지 정의가 필요하다. 명확하게 정의해두지 않으면 개발자 입장에서 혼란스럽다.
- 일반적으로 받는 쪽의 관점에서 작성하는 경우가 잦다.

### 어디까지 자세히 적을지 미리 정의해두자.
- 상세히 작성하고자 한다면 변수, 메소드, 파라미터 등 끝없이 자세히 적을 수 있다. 얼마나 구체적으로 작성할지 정의해두고 접근하자.


## Reference
[1] https://ko.wikipedia.org/wiki/시퀸스_다이어그램  
[2] https://staruml.io/  
[3] https://lucidchart.com/  
[4] https://www.microsoft.com/ko-kr/microsoft-365/visio/flowchart-software  
[5] https://brownbears.tistory.com/511  
[6] https://engineer-mole.tistory.com/131  

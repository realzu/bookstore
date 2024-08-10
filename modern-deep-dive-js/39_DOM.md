# DOM

Document Object Model  
HTML 문서의 계층적 구조와 정보 표현. 및 제어할 수 있는 API(프로퍼티 및 메서드) 제공하는 트리 자료구조

### 노드

- HTML 요소와 노드 객체
  - HTML 요소: HTML 문서를 구성하는 개별적인 요소
    - 렌더링 엔진에 의해 파싱되어 DOM 구성하는 요소 노드 객체로 변환 -> attribute node. text content는 text node..
  - 요소간 부자 관계를 반영하여 모든 노드 객체를 트리 자료로 구성
  - 노드 객체들로 구성된 트리 자료구조 = DOM (= DOM 트리)
- 노드 객체의 타입
  - 문서 노드(document node)
    - document 객체
    - 브라우저가 렌더링한 HTML 문서 전체를 가리키는 객체 (HTML 문서당 document 객체는 유일)
  - 요소 노드(element node)
    - HTML 요소를 가리키는 객체
    - 부자 관계 -> 정보 구조화 (= 문서 구조화)
  - 어트리뷰트 노드(attribute node)
    - 속성이 지정된 HTML 요소의 요소 노드와 연결
  - 텍스트 노드(text node)
    - HTML 요소의 텍스트를 가리키는 객체
    - DOM 트리의 최종단

### 요소 노드 취득

- id
  - `getElementById`
  - id값은 HTML 문서 내에서 유일한 값
  - id 요소 존재하지 않으면 null 반환

### 노드 탐색

### 노드 정보 취득

### 요소 노드의 텍스트 조작

### DOM 조작

### 어트리뷰트

### 스타일

### DOM 표준

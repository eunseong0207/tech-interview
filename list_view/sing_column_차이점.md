# ListView, ListView.builder, SingleChildScrollView + Column 3가지의 차이점은 무엇인가요? 


## ListView (기본)
- children 속성을 사용하여 리스트를 생성
### 주요 특징
- 코드가 직관적이고 간결하
- 모든 자식 위젯을 즉시 렌더링

### 장점
- 구현이 매우 간단
- 아이템 간의 구분선을 넣거나 정적인 메뉴를 구성할 때 편리 
- 구분선 넣을때는 ListView.separated 사용한다

### 단점
- 리스트의 아이템 개수가 많아지면 메모리 사용량이 급증
- 화면에 보이지 않는 아래쪽 아이템까지 모두 그리기에 성능에 좋지 않음

---

## ListView.builder (가장 권장)
- 화면에 보이는 부분과 스크롤 할 때 나타날 일부 영역만 그림
### 주요 특징
- `itemBuilder` 콜백 함수를 통해 필요할 때만 위젯을 생성
- `itemCount` 속성으로 리스트의 전체 개수를 지정
- `itemExtent` 속성으로 아이템의 높이를 지정하면 성능 향상
- `prototypeItem` 속성으로 아이템의 높이를 지정하면 성능 향상
- 스크롤되어 화면 밖으로 나간 위젯은 메모리에서 해제

### 장점
- 데이터가 많아도 메모리 사용량 일정
- 앱의 초기 로딩속도 빨라짐

### 단점
- 코드가 복잡함
- 아이템 간의 구분선을 넣기 어려움

---

## SingleChildScrollView + Column
- 스크롤이 불가능한 Column을 스크롤 가능하게 만듬
### 주요 특징
- 모든 자식 위젯을 즉시 렌더링
- 범용적인 레이아웃 구성 방식

### 장점
- 리스트 형태가 아닌 서로 다른 크기와 종류의 위젯들을 자유롭게 배치하고 전체를 스크롤 되게 할 때 유용
- Column의 mainAxisAlignment, crossAxisAlignment 속성을 활용해 정렬하기 편리

### 단점
- 데이터 목록을 표시하는 용도로는 성는상 부적합


---

| 구분 | 렌더링 방식 | 메모리 효율 | 주요 용도 | 데이터 크기 |
| :--- | :--- | :--- | :--- | :--- |
| **ListView.builder** | Lazy Rendering (지연 렌더링) | 최상 | 데이터가 많은 리스트, 무한 스크롤, 뉴스 피드 | 대량 / 무제한 |
| **ListView (기본)** | Eager Rendering (즉시 렌더링) | 낮음 | 설정 화면, 메뉴 목록 등 아이템 개수가 적고 고정된 경우 | 소량 (약 50개 미만) |
| **SingleChildScrollView + Column** | Eager Rendering (즉시 렌더링) | 낮음 | 폼(Form) 입력 화면, 스크롤 필요한 복합 레이아웃 | 소량 |


## 결론
- 데이터가 많거나 동적인 리스트 : ListView.builder
- 아이템 개수가 적고 고정된 리스트 : ListView
- 리스트 형태가 아닌 복합 레이아웃 : SingleChildScrollView + Column

![alt text](list_view.png)
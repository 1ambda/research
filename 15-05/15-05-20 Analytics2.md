## SpreadSheet를 이용해서 편하게 살기.

Box & Whisker 황찬주님

GA 를 쓰고, SpreadSheet 로 대쉬보드를 만드는 일.

### 지표

다양한 지표들이 나오게 되고,

Retention 은 게임 자체의 재미에는 별 도움이 안됌.
마케팅에 집중하게 되고, 푸시, 출석이벤트, 데일리 이벤트 불라불라

### Evenet, State 를 정의하기


- **state:** 게임의 Scene 과 팝업을 page 로 만들고
- **event:** 버튼클릭

#### 캔디크러시 Ex

/title -> Start
/maps -> Life, Message, Stage
/stage1/ready => Start, Item1~3, Rank, cancle
/stage1/play -> Item2Use, Item3Use
/stage1/end

### SpreadSheet 부가기능

복잡한 차트 라이브러리 없이 GA 로그를 기반으로
Query 형태로 SpreadSheet 에서 땡겨 사용 가능.

심지어 스케쥴러도 가능하고, 웹에도 게시 가능

즉, GA 를 DB 처럼 사용

- 약 4시간의 딜레이
- 월 1000만건 제한
- 통계는 가능하지만 개별 분석은 힘듦. 만약 스테이지형 게임에서 이유없이 한 스테이지만 계속하는 유저가 평균을 바꿀 수 있음

SDK 를 추천하지만, SDK 도 일인데,
POST 형식으로 measurement API 에 제공

https://developers.google.com/analytics/devguides/collection/

https://developers.google.com/analytics/devguides/config/mgmt/v3/

#### 측정기준, 측정항목

- Dimensions(측정 기준)
- Metrics (측정 항목): 얼마나 머물렀는가?

#### Ex: 튜토리얼이 얼마나 도움이 되는가?

9장을 다 페이지로 만듬.
/tutorial/1, 2, ...

ga:pageviews
ga:uniquePageViews

#### Ex: 게임을 끝냈는가?

ga:exitPagePath Dimensions(측정기준)
- 세션 안의 마지막 페이지가 어딘가.

ga:exits Metrics(측정항목)
- 갯수는 몇개인가.

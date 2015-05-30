### GA 로 게임 로그 분석하기

- GA 를 활용하여 게임 데이터를 수집 / 분석
- 게임 로그를 GA 에 잘 매핑하기

GA 는 게임에 더 적합.
딱 하루면 Lean 에서 이야기하는 Build -> Measure -> Learn.

### Desktop vs Mobile 환경에서 난이도가 다를까?

### A/B 테스팅

Parameterized 해서 게임 version 을 여러개 준비.

몰랐는데 Google API 에서 지원해줌.

http://techcrunch.com/2013/06/04/googles-content-experiments-api-a-b-testing/

https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&ved=0CCoQFjAB&url=https%3A%2F%2Fdevelopers.google.com%2Fanalytics%2Fdevguides%2Fplatform%2Fexperiments-overview&ei=oeBbVdfLF8758QXY-IGwAg&usg=AFQjCNEmj8L0TX9OYQL1Av-2yzo09pn0kA&sig2=Gs8yhqwwL9BerU90FUmSsQ&bvm=bv.93756505,d.c2E&cad=rja

https://developers.google.com/analytics/devguides/config/mgmt/v3/mgmtExperimentsGuide

https://developers.google.com/analytics/devguides/platform/experiments-overview

### 1부 Summary

핵심 이벤트를 작은 단위로 분리하고,
개별적으로 프로토타이핑하고 데이터를 모으는 방식도 가능할듯.

### 2부 게임로그를 GA 에 맞게 설계하기.

- 웹페이지에서 주요한 상태변화는 웹주소(URL) 의 전환
  앱에선서는 화면의 전환

- 따라서 우리에게 가장 중요한 상태 변화가 무엇인지 결정하고,
  그것에 따라 URL 을 매핑하는 것.

- 우리 게임은 URL 은 안쓰니까 이벤트를 전송해야지, 하면 이상해짐
 URL 을 매핑할 것.

#### 캔디크러시

/main
/map
/s11/302/enetry
/s11/302/field
/s11/302/lose, /s11/302/win

#### 카트라이더

/speed/track_a/lap-1
/speed/track_a/lap-2
/item/track_b/lab-1

#### MMORPG

필드, 주요 NPC, 인던, 포탈등에 URL 을 부여
필드가 넓다면 grid 로 나누고 filed_a/x-y 등으로 분류해서 heatmap 을 그릴 수 있음

이정도만 해도 온갖 유용한 정보가 나온다.

Q. A 트랙은 플레이하지만, B 트랙은 플레이 하지 않는 사람들의 특징은?
Q. 패치 이전 / 이후 랩타임은?
Q. 트랙별 lap-time 은?
Q. 완주 안하고 중간에 나가버리는 플레이어 트랙은?

### 주요하지 않은 상태변화는?

캐릭터/직업/레벨 등 게임 고유의 특화된 상태는 Custom Dimension
경험치나 골드 등 게임 고유의 수치는 Custom Metric
플레이어 사망 아이템 획득 등 게임 고유의 사건은 Custom Event

상태는 **길이**가 있음. (랩 타임)
이벤트는 **점** (e.g 아이템 획득, 플레이어 사망)

모두다 event, stats 를 때려넣지 않아야.

- 간이 맞을때 그만 졸이면 돼요.

### 스테이지형 퍼즐게임 예시

구글시트와 연동해서 파생지표 및 Custom Metric 을 엮어서 보여주기

                      abandon gold spent
Success 95% ||||||||      ||| ||||

Funnel,

웹이라는 결에 맞추어

![](http://www.boxnwhis.kr/img/posts/2014-09-15-analyze_game_using_ga_1/heatmap.png)

![](http://www.boxnwhis.kr/img/posts/2014-09-15-analyze_game_using_ga_1/motion_chart.png)

### 2부 Summary

- 기능이 부족하면 API 를 써서 확장


### 참고자료

https://developers.google.com/analytics/devguides/collection/protocol/v1/

https://ga-dev-tools.appspot.com/dimensions-metrics-explorer/
https://developers.google.com/analytics/devguides/reporting/core/dimsmets

https://developers.google.com/analytics/solutions/google-analytics-spreadsheet-add-on

GA 로 게임 분석하기 1, 2, 3
http://www.boxnwhis.kr/2014/09/15/analyze_game_using_ga_1.html

http://www.ecogwiki.com/Google_Analytics%EB%A1%9C_%EA%B2%8C%EC%9E%84_%EB%B6%84%EC%84%9D%ED%95%98%EA%B8%B0_2

http://www.boxnwhis.kr/2015/04/12/analyze_game_using_ga_3.html




### Q&A

- GA 의 단점은 평균, 최대값만 보여줌
- GA Relay 등을 이용해서
- 실제 세션길이보다 약간 짧음. Finish 이후 에는 점(event) 가 없이 때문

- Custom Dimension, Metric Slot 20개를 재활용

### API, SDK

- Android, iPhone, Web
- Mesurement API 를 이용하면 매장이건 어디건
//

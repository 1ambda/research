
Volume -> Variety(비정형, 반정형: Log), Velocity(실시간) -> Veracity, Value

5V + 1V(Value) = 6V


### Volumn

고비용 DBMS, TB 단위 -> PB 급 처리, Commodity 서버, Scale out (not up)

### Variety

정형데이터 처리, 내부 Transaction -> 반정형+비정형, 외부데이터 활용(?)

### Velocity

주기에따른 Batch -> almost real-time, streaming, EDA
의사결정(DSS, BI) 에 활용 -> Time to Market BIZ

### Veracity

신뢰성 높은 TR, 기준 메타 정보 -> Garbage Data 비중 높음.


### Summary

분석 유연성 확보: CDA -> EDA, Visualization
데이터 직접 활용: DSS -> Open API, 추천, 타게팅, FDS

### Process

- 수집: ETL, 크롤링, 로거

로그기반은 Flume, Chukwa
DB 기반은 Sqoop

- 저장: DBMS, HDFS, NOSQL

- 처리: MR, Pig, Hive

Oozie, Cascading

Oozie is a workflow scheduler system to manage Apache Hadoop jobs.

- 분석: R, ML, NLP

- 활용: Report, Visual, DaaS

시각화: Tableau (http://www.tableau.com)


기존의 분석계(DW) 와 유사한 아키텍쳐


### EDA

복잡한 통계적 모델 수립, 검증 대신에
빠르고 유연한 분석 + Visualziation

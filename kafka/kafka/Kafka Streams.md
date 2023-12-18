# 1. 카프카 스트림즈란?

- 카프카 클러스터의 이벤트 스트림에 대해 스트리밍 처리를 용이하게 구현할 수 있도록 도움을 주는 자바 라이브러리
- 자바의 stream api 와 같이 데이터 스트림 처리를 위한 고수준 추상화 API 를 제공하는 Streams DSL
- 세세한 제어가 필요할 때 사용하는 저수준의 Processor API
- 이벤트 스트림을 테이블(Ktable & GlobalKTable), 스트림(KStream) 로 추상화(데이터 모델링) 가능
- 데이터 변환, 보강, 조인, 집계 등의 기능 제공
- 상태가 있는 스트림 처리가 가능
- 윈도우 처리와 주기적인 함수 실행 등 시간-기반 연산 지원
- 쉬운 설치, 단순 자바 라이브러리이기 때문에 별도 설치할 것이 없음
- 높은 확장성, 신뢰성, 유지 보수성

# 2. 프로세서 토폴로지 (Processor Topology)

![processor topology](https://docs.confluent.io/platform/current/_images/streams-architecture-topology.jpg)
[그림 1] 카프카 스트림즈 프로세서 토폴로지 _(출처 https://docs.confluent.io/platform/current/streams/architecture.html)_

- 소스 프로세서 (Source Processor)
	- 카프카 스트림즈 애플리케이션으로 레코드를 흘려보내는 역할
	- 카프카 토픽으로부터 데이터를 읽고, 하나 이상의 스트림 프로세서로 전달
- 스트림 프로세서 (Stream Processor)
	- 데이터 처리 (변환/보강/필터 등) 로직을 실행하고 하나 이상의 스트림 프로세서 혹은 싱크 프로세서로 전달
-  싱크 프로세서 (Sink Processor)
	- 소스/스트림 프로세서를 통해 전달받은 데이터(레코드)를 다시 카프카 클러스터의 특정 토픽으로 내보내는 역할
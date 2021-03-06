# 역정규화

- https://bellog.tistory.com/125

## 역정규화(Denormalization)란?

- 정규화된 릴레이션을 다시 통합하거나 분할하여 구조를 재조정하는 과정
- 정규화를 한다는 것은 하나의 릴레이션을 여러 개의 릴레이션으로 분해한다는 것을 의미
- 원하는 데이터를 얻기 위해서는 다수의 릴레이션을 참조해야 한다
- 이는 데이터베이스에서 저장된 자료를 검색하는 시간을 증가시키고 성능 저하의 결과를 초래할 수 있다
- 때문에 데이터베이스의 물리적 설계 과정에서 성능을 향상시키기 위해서는 역정규화의 과정이 필요

## 역정규화의 종류

1. 릴레이션 역정규화

- 두 릴레이션을 합하거나 하나의 릴레이션을 분할하는 방법
- 릴레이션 병합 : 두 릴레이션 간의 잦은 참조로 성능이 저하될 경우 이 문제점을 해결하기 위해 병합
- 릴레이션 분할 : 자주 사용하는 속성이나 튜플을 분해하여 성능을 향상 시키는 방법
  - 릴레이션의 데이터를 검색할 때는 목록을 순차적으로 조회
  - 이 때 자주 사용하지 않는 속성이나 튜플이 있다면 검색이 느려짐
  - 수직 분할 : 자주 사용하는 속성과 그렇지 않은 속성 분할
  - 수평 분할 : 자주 사용하는 튜플과 그렇지 않은 튜플 분할

2. 속성 역정규화

- 검색 성능을 향상시키기 위해 속성을 추가하거나 필요한 속성을 만듬
- 속성 추가 : 자주 사용하는 외래키 속성 추가
- 파생 속성 추가 : 현재 릴레이션에 없는 속성이지만 작업 효율을 위해 새로운 속성 추가

## 해시 함수

- 해시 함수는 어떤 값을 입력받아 고정된 길이의 문자열로 반환하는 함수.
- 예시 : `SHA-256`

## 해시 테이블

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/1200px-Hash_table_3_1_1_0_1_0_0_SP.svg.png" alt="hash-table" />
(이미지 출처 : https://en.wikipedia.org/wiki/Hash_table)

<br >

- 키와 값의 쌍으로 이루어진 자료 구조. 키가 주어지면 이 키가 해시 함수를 통하여 일련의 값으로 변경되고, 이 값을 테이블의 인덱스로 사용하는 형태이다. 정리하자면 **{키 : 값} 중 키를 해시 함수를 통하여 배열의 인덱스를 계산하고, 이 인덱스에 값을 저장하는 자료구조** 이다.
- 해시 테이블은 [해시 함수](https://ko.wikipedia.org/wiki/%ED%95%B4%EC%8B%9C_%ED%95%A8%EC%88%98)를 사용하여 색인(index)을 버킷(bucket)이나 슬롯(slot)의 배열로 계산한다.
- 해시 테이블은 시간 복잡도 - 공간 복잡도의 trade-off 관계를 사용한 예라고 할 수 있다.

## 해시의 성능 평가

- 이론 상으로 삽입, 삭제, 변경 등의 연산이 O(1)에 일어나나, 충돌 등의 문제로 인해 O(n)까지 시간이 걸릴 수도 있다.
- 해시의 성능을 향상시키기 위하여 좋은 해시 함수를 설계하는 것이 중요하다.

### 좋은 해시 함수를 설계하는 방법

- 좋은 해시 함수는 데이터를 **균일하게 분산**시켜 충돌을 최소화하고, **계산이 빠르고**, 간단하며, 해시 값을 예측하기 어려워야 합니다.

## 해시 충돌

### 충돌 방지 기법

<img src="https://static.javatpoint.com/ds/images/hashing-open-addressing-for-collision-handling.png" alt="open addressing" />

- **Open Addressing** : Probing 을 이용하여, 어떤 인덱스에서 해시 충돌이 일어났을 때 값을 다른 곳에 저장하는 방법
  - **Linear Probing** : 선형으로 값을 저장. 즉, 충돌이 발생하면 바로 오른쪽 칸에 값을 저장한다.
    - 장점 : Cache hit rate 가 높다. 구현이 간단하다.
    - 단점 : Clustering 의 문제가 생긴다. 바로 옆에 값을 저장하는 특성 상, Clustering이 생성될 위험성이 크고, 이 근처에 값을 삽입하게 된다면 인덱스가 그 만큼 이동해야 하므로 성능상 좋지 않은 영향을 준다.
  - **Qudratic Probing** : 충돌이 발생하면 인덱스를 제곱 식으로 (1, 2, 4, ..) 이동한다.
    - 장점 : Cache hit rate 가 나쁘지 않다. Linear Probing 에 비해서 Clustering 의 위험성이 낮다.
    - 단점 : Clustering 에 대해 완전한 해결책이 되지 못한다.
  - **Double Probing** : 해시 함수를 하나 더 둬서, 충돌이 일어날 경우 몇 칸 더 이동할지를 이 해시 함수를 통해 결정한다.
    - 장점 : Clustering 을 효과적으로 회피할 수 있다.
    - 단점 : Cache hit rate 가 좋지 않다.

<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2015/07/hashChaining1.png" alt="chaining" />

- **Separate Chaining** : 각 해시 테이블에 값을 저장할 떄, 이 테이블을 연결리스트 혹은 Tree를 통해 구현한다. 즉, **해시 함수의 충돌이 생기면 그 인덱스에 새로운 키 : 값을 노드로 추가하는 방식**이다. 이 방법은 키가 어마나 많이, 자주 삽입되거나 삭제될지 알 수 없는 경우에 사용된다.
  - 장점 : 일반적으로 Open Addressing 에 비하여 속도가 빠르다. 해시 함수에 덜 민감하다.
  - 단점 : 값이 linked list로 저장되므로 cache 성능이 좋지 않다. 공간이 낭비 된다.

## 해시의 활용 사례

- 디지털 서명 : 디지털 서명 과정에서 원본 데이터에 대해 해시를 생성하고, 이 해시에 개인 키를 사용하여 서명이 생성됩니다. 수신 측에서는 공개 키를 사용하여 해시 값을 복원하고 원본 데이터의 해시 값과 비교함으로써 데이터의 무결성과 송신자의 신원을 검증할 수 있습니다.
- 데이터 무결성 확인

### 언어별 특징

- JavaScript : Object와 ES6 이후로 도입된 Map 의 해시 기반 자료 구조를 제공한다.
  - Obejct : 키에는 문자열 또는 심볼 형태만 가능하며, 숫자 키가 문자열로 변환된다.
  - Map: ES6부터 도입되었으며, 키의 타입에 제약이 없으며 삽입 순서를 유지한다.
  - 참고로, JavaScript의 경우 엔진별로 구현이 다를 수 있다. 예를 들어 V8 엔진 (Chrome)에서는 성능 향상을 위해 해시 테이블 대신 히든 클래스를 사용한다.
    > `Map`의 명세는 "평균적으로 집합 내 요소의 수에 따라 하위 선형인 접근 시간을 제공하는" 맵을 구현해야 한다고 기술되어 있습니다. 따라서 복잡성이 O(N)보다 더 나은 경우 내부적으로 해시 테이블(O(1) 룩업), 검색 트리(O(log(N)) 룩업) 또는 기타 데이터 구조로 표현될 수 있습니다.
    > Map -JavaScript | MDN

## 참고 자료

- [Map - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [Open Addressing Collision Handling technique in Hashing | GeeksForGeeks](https://www.geeksforgeeks.org/open-addressing-collision-handling-technique-in-hashing/)
- [Separate Chaining Collision Handling Technique in Hashing | GeeksForGeeks](https://www.geeksforgeeks.org/separate-chaining-collision-handling-technique-in-hashing/)

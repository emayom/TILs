# 해시(Hash)
> 해시 함수에 의해 얻어지는 값을 **해시 값, 해시 코드, 해시 체크섬** 또는 간단하게 **해시**라고 한다.   
> i.e., 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑(mapping)한 값

## 해시 함수(Hash Function)

해시 함수는 임의의 길이의 데이터를 **고정된 길이의 데이터**로 매핑하는 함수이다.  
가장 기본적이고, 대표적인 해시 함수로는 **모듈러 연산 기반의 해시 함수**($hash(x) = x \ mod \ N$)가 있다. 

#### 해시 함수 특징
- 어떤 입력 값에도 항상 **고정된 길이의 결괏값**을 출력한다.
- 동일한 입력 값에 대해서는 언제나 **동일한 출력값**을 반환한다.
- 입력 값이 조금만 달라져도 결괏값은 크게 달라진다.
- 결괏값을 토대로 입력 값을 찾는 것이 계산상 어렵다.

### 해시 충돌(Hash Collision)
> [비둘기집 원리(Pegionhole Principle)](https://ko.wikipedia.org/wiki/%EB%B9%84%EB%91%98%EA%B8%B0%EC%A7%91_%EC%9B%90%EB%A6%AC) 참고 

해시 충돌은 **해시 함수가 서로 다른 입력값으로부터 동일한 출력값을 생성하는 상황**을 의미한다.    
해시 함수의 고정된 길이의 출력값으로 매핑되므로, 입력값의 범위는 무한할 수 있지만 출력값의 범위는 유한하다.  
이로 인해 어떤 입력값들은 동일한 해시 값을 생성할 가능성이 존재하므로 해시 충돌은 피할 수 없다.

#### 해시 충돌 해결 전략 
- **체이닝(Separate Chaining)**  
    > 해시 테이블의 각 버킷에 `링크드 리스트`를 할당하여 동일한 해시 값을 가진 항목들을 연결하여 저장하는 방식  

- **개방 주소법(Open Addressing)**
    > 충돌이 발생한 경우, 해시 테이블 내에서 다른 빈 공간을 찾아 데이터를 저장하는 방식  
    > i.e., 모든 원소가 반드시 자신의 해시 값과 일치하는 주소에 저장된다는 보장이 없다. 

    - 선형 탐사(Linear Probing)
    - 이차 탐사(Quadratic Probing)
    - 더블 해싱(Double Hashing)

## 해시 테이블(Hash Table)(=해시 맵)

> 연관 배열(Associative Array)이란 키-값 쌍을 저장하는 추상 자료형(ADT)  
> e.g., 자바스크립트의 `Map` 객체, 파이썬의 `Dictionary`

해시 테이블은 연관 배열 추상 자료형(ADT)을 구현하는 자료구조이다.  
해시 함수를 기반으로 하여, 저장된 원소의 양과 상관없이 탐색, 삽입, 삭제 연산이 **상수 시간**에 이루어지도록 설계되었다.

해시 함수를 사용하여 키를 해시 값으로 매핑하는 과정 자체를 **해싱(Hashing)** 이라고 하며, 해시 값을 색인(index)으로 삼아 키와 값을 함께 저장한다. 이때, 데이터가 저장되는 곳을 **버킷(bucket)** 또는 **슬롯(slot)** 이라고 한다. 

해시 테이블에서는 삽입에 따른 키의 순서를 유지하지 않기 때문에 삽입 순서에 따른 데이터 접근이 중요하다면, 자바의 `LinkedHashMap`과 같은 별도의 자료구조를 사용하는 것이 필요하다.  

#### 해시 테이블과 해시 충돌 

> 적재율(Load Factor)이란 해시 테이블의 크기 대비, 키의 개수를 말한다. 

해시 테이블에서는 테이블의 크기가 키의 개수보다 작을 수 있기 때문에 적재율이 1을 초과하여 충돌이 발생 할 수 있다.  
즉, 가능한 모든 키의 숫자는 테이블 인덱스의 개수보다 많기 때문에 해시 충돌을 피할 수는 없다.

충돌이 발생하지 않는다면 해시 테이블의 탐색, 삽입, 삭제 연산은 모두 상수 시간(O(1))에 수행되지만, 충돌이 발생할 경우 탐색 및 삭제 연산이 최악의 경우 선형 시간 복잡도(O(n))로 증가할 수 있다. 이렇듯 해시 테이블에서의 충돌은 연산 효율성이 크게 감소시킬 수 있며, 충돌의 최소화하는 것이 해시 테이블의 핵심이다. 

> 해시 테이블의 로드 팩터(Load Factor)가 높아지면 크기를 동적으로 리사이징 해주는 것이 필요하다. 

#### 해시 테이블에서의 좋은 해시 함수의 조건
- 충돌(Collision) 발생 최소화
- 균등한 분포
- 빠른 연산 

#### 해시 테이블의 기본 시간 복잡도
> 충돌이 발생하지 않은 경우, 평균적으로 O(1) 시간 복잡도로 연산을 수행할 수 있지만,   
> 충돌 처리 방식과 해시 함수의 품질에 따라 최악의 경우 O(n) 시간 복잡도까지 크게 증가할 수 있다.

| `Case` | `Time Complexity` |
| :--- | :----: | 
| 탐색(Search)   | O(1) | 
| 삽입(Insertion)   | O(1) | 
| 삭제(Deletion)   | O(1) | 

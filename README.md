# 키친포스

## 퀵 스타트

```sh
cd docker
docker compose -p kitchenpos up -d
```

## 요구 사항
**메뉴그룹**

- [ ]  메뉴 그룹명을 관리한다
- [ ]  메뉴 그룹명은 비속어와 빈 문자열이 등록될 수 없고 16자 이하여야 한다
- [ ]  메뉴 그룹은 전체 조회가 가능하다

**메뉴**

- [ ]  메뉴판에 등록된 메뉴의 가격을 변경할 수 있다
- [ ]  이미 등록된 메뉴의 가격만 변경할 수 있다
- [ ]  메뉴에 등록된 상품을 조회할 수 있다
- [ ]  메뉴는 상품 정보를 노출한다
- [ ]  메뉴를 추가하기전 메뉴 그룹과 상품이 요구된다
- [ ]  메뉴는 메뉴 그룹, 금액, 메뉴 상품을 필요로 한다
- [ ]  수량이 0개 이하인 상품은 메뉴로 등록할 수 없다
- [ ]  메뉴의 가격은 수량과 가격의 총합으로 등록된다
- [ ]  메뉴에 등록되는 상품의 가격은 0원 이상이어야 한다
- [ ]  메뉴의 상품 노출 여부를 결정할 수 있다 (숨김/표출)

**상품**

- [ ]  상품은 [등록/가격변경/조회]가 가능하다
- [ ]  상품은 상품명과 가격을 보유해야 한다
- [ ]  상품명은 비속어가 포함될 수 없다
- [ ]  가게의 전체 상품목록을 조회할 수 있다
- [ ]  상품의 가격은 0보다 커야한다
- [ ]  상품명이 비어있는 상품은 등록될 수 없다
- [ ]  상품의 가격을 변경할 땐 메뉴에서 해당 상품의 가격을 전부 변경해야 한다
- [ ]  변경된 상품 가격이 0원 이상이면 메뉴에서 일시적으로 노출하지 않는다

**테이블**
- [ ]  테이블은 [착석 가능 여부 변경/조회/손님 등록/테이블 등록]가 가능하다   
- [ ]  처음 테이블을 등록할 때는 착석 여부와 손님 여부가 기본값으로 설정된다 (착 가능 석여부 : false, 손님 수 : 0)
- [ ]  테이블엔 이미 착석한 손님이 없을때만 착석이 가능하다
- [ ]  테이블의 착석 가능여부를 허용 해야만 해당 테이블에 착석할 수 있다
- [ ]  테이블에서 손님이 떠나면 좌석을 비워야 한다 (착석 가능 여부 : false, 손님 수 : 0)
- [ ]  매장 취식 손님을 테이블에 지정할 때 테이블은 착석 가능 여부가 true여야 한다 
- [ ]  매장의 전체 테이블 정보를 조회할 수 있다

**주문** 
- 주문
  - [ ]  메뉴에 노출된 상품만 주문할 수 있다
  - [ ]  주문 상태는 대기(WAITING), 승인(ACCEPTED), 서빙됨(SERVED), 배달중(DELIVERING), 배달완료(DELIVERED), 완료(COMPLETED)가 존재한다
  - [ ]  주문 타입은 배달(DELIVERY), 포장(TAKEOUT), 매장취식(EAT_IN)가 존재한다
  - [ ]  주문한 메뉴의 수와 실제 등록된 메뉴의 수가 일치하지 않으면 거절된다
  - [ ]  주문 타입이 포함되지 않은 주문은 거절된다
  - [ ]  메뉴가 포함되지 않은 주문은 거절된다
  - [ ]  존재하지 않는 메뉴를 주문하면 거절된다
  - [ ]  배달주문은 주소가 필수로 요구된다
  - [ ]  테이블이 존재하지 않으면 매장에서 취식 할 수 없다
- 주문 수락
  - [ ]  대기상태가 아닌 주문은 수락되지 않는다
  - [ ]  주문타입이 DELIVERY이면 배달을 요청한다
  - [ ]  주문이 성공적으로 수락(accept)되면 주문 상태를 ACCEPTED로 변경한다
- 서빙
  - [ ]  수락(ACCEPTED)된 주문이 아니면 서빙하지 않는다
  - [ ]  서빙이 완료되면 주문 상태를 SERVED로 변경한다
- 배달
  - [ ]  등록된 주문만 배달이 가능하다
  - [ ]  주문 상태가 DELIVERY가 아니라면 배달을 시작할 수 없다
  - [ ]  SERVED 상태로 변경된 주문만 배달이 가능하다
  - [ ]  배달처리가 승인되면 주문 상태를 DELIVERING으로 변경한다
  - [ ]  배달이 완료된 주문은 DELIVERED 상태로 변경한다
  - [ ]  주문 상태가 DELIVERING인 주문만 DELIVERED 상태로 변경할 수 있다
- 주문 완료
-  [ ] 존재하는 주문만 주문 완료 상태로 변경할 수 있다
-  [ ] 배달 주문 상태가 DELIVERED가 아니라면 주문을 완료할 수 없다
-  [ ] TAKEOUT과 EAT_IN 상태는 SERVED 상태가 아니라면 주문 완료 처리를 ㅏㅎㄹ 수 없다
-  [ ] 주문 완료처리가 성공하면 주문의 상태를 COMPLETED로 변경한다
-  [ ] EAT_IN 주문은 주문이 완료되면 취식한 테이블의 상태를 변경한다 [Guest = 0, Occupied = false] 

## 용어 사전

| 한글명     | 영문명           | 설명             |
|---------|---------------|----------------|
| 상품      | product       | 판매할 상품         |
| 메뉴      | menu          | 가게의 상품을 표현하는 수단 |
| 주문 테이블  | orderTable    | 매장 취식 고객의 주문 단위 |
| 주문      | order         | 상품을 주문 행위      |
| 주문타입    | orderType     | 주문 방식          |
| 가격      | price         | 상품의 가격         |
| 수량      | price         | 상품의 가격         |
| 상품 표시 여부 | displayed     | 메뉴에 상품을 표시할지 결정 |
| 주문 정보   | orderLine | 고객이 주문한 상품들의 정보 |
| 상품 수량   | quantity | 고객이 주문한 상품의 수량 |

## 모델링

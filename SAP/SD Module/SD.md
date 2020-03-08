# SD란?
쉽게 말해서 '물건 주문'을 하는 모듈이다.
- SD = Sales and Distribution

SAP 에서 영업 및 물류 관리를 수행하는 모듈이다.
![Alt text](/image/sd_process.gif)

## SD를 구성하는 3 요소
1. 기업구조 : Enterprise Structure
2. 마스터 데이터 : Master data
3. 트랜잭션 : Transaction

```
- SIS                       Sales Information System (영업 정보 시스템)
- Presales                  주문 이전에 일어나는 모든 행위.
                            (영업활동, 계약, 견적요청, 견적 등이 포함된다.)
- Sales Activity            영업활동
- Contract                  계약
- Inquiry                   견적요청
- Quotation                 견적
- Scheduling Agreement      납품 일정 계약 (계약의 한 종류)
- Order                     영업 주문
- Delivery                  납품 문서
- Good Issue                출고
- Transfer Order            이전 오더 (자재를 창고간 이동할 때 사용)
- Shipment                  선적 (자재의 운송경로, 방법을 결정하고 
                                  그 비용을 산출, 정산하는데 사용)
- Billing document          대금 청구문서
- Account Receivable        외상 매출금 
                            (회계 용어 입니다, 
                            흔히 AR,AP 라고 말하는데 
                            AP는 - Account Payable, 외상 매입금)
- Material Stock Account    직역하면 자재 재고 계정, 
                            그냥 자재원장 정도로 생각 하시면 될 것 같내요.
- MM                        MM 모듈 (자재관리)
- PP                        PP 모듈 (생산관리)
```

# SD Master Data
- 고객마스터
- 자재마스터
- 조건 마스터(가격)

> 고객마스터

주문, 배송, 청구서 및 고객지불처리에 필요한 모든 정보가 들어있다.
모든 고객은 반드시 마스터 레코드가 있어야한다.

고객마스터 정보는
 - General Data
 - Compnay code Data
 - Sales Area Data

> 자재마스터

회사가 재료에 대해 관리해야하는 모든 정보를 포함한다.

자재 관리와 관련된 만큼 SAP 시스템의 대부분의 영역에서 사용되는 부분이다.

기본 데이터, 영업, 구매, 자재계획, 재고, 회계, 관리 등의 데이터는 자재 마스터에 포함되어 있다.

> 조건 마스터

물가, 할증료, 할인, 화물, 세금 관련 데이터들이 포함되어 있다.
가격을 정하기도 한다.

특정 재료별로도 정의를 할 수도 있고, 고객별로도 정의를 할 수 있는 데이터이다.

>> 운송비와 세금은 여기 CONDITIONING에서 마음대로 바꿀 수 없다.



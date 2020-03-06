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
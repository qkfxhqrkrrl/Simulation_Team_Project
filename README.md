# Plant Simulation 을 이용한 물류배치 최적화
- 사용 프로그램 : https://www.plm.automation.siemens.com/global/ko/products/manufacturing-planning/plant-simulation-throughput-optimization.html

## 기본규칙

위 보이는 트랙이 하차, 그 아래에 위치한 트랙들이 저장 창고, 마지막 아래쪽에 위치한 트랙들이 상차입니다.

<center><img src="https://user-images.githubusercontent.com/53500865/149169258-e1340ad5-a082-4c7d-9f56-b08a4569f8e3.png" width="600" height="800"></center>


여기서 들어오는 수화물들은 하나 하나가 서울,인천,부산으로 고유값을 가지며 정해진 임시 저장소에 저장됩니다.
실제 구현한 시뮬레이션은 1,2,3,4 가 서울이고 5,6이 부산, 7이 인천으로 할당하였습니다.
![image](https://user-images.githubusercontent.com/53500865/149172191-1482f4e4-4c80-4e36-bf82-d5509f6b7e9a.png)

물건을 다 옮기고나면 아래에서 대기중인 직원이 자신이 옮길 수 있는 물류량이 다 할당될 떄 까지 대기하다가 제일 아래쪽에 위치한 선반부터 하나씩 물건을 채우러 출발합니다.
여기서 물건을 다 채우고 나면 반대트랙으로 가서 다시 물건을 받을 수 있는 위치에서 대기합니다.

![image](https://user-images.githubusercontent.com/53500865/149172811-3056a743-b168-43cf-9771-f02e20a6e1fe.png)

상차트럭들은 각자 창고에서 물건을 가지고 갈 작업자 한명이 있습니다.(사진에선 빨간색)
도착하고 난 뒤에 앞에 이미 상차중인 트럭이 있으면 작업이 마칠때까지 대기합니다.
작업자가 모든 물건을 싣고 나면 트럭은 빠져나가게 됩니다.

![image](https://user-images.githubusercontent.com/53500865/149174214-dc7c2589-0580-4d16-a458-0d0593927a94.png)


## 실험내용
수화물을 저장하는 배지 방식에 따라 상차 효율이 달라질 것이라는 생각에서부터 시작했습니다.
한 트랙에 저장될 수 있는 수화물의 수에는 한계가 있으므로, 자신의 트랙에서 할당된 수화물을 모두 처리했다면 옆에 트랙에서 수화물을 가져와야 하는 상황이 생기게 됩니다.
이러한 상황을 가정하고 물건을 가지러 가는 시간이 배치 레이아웃을 바꾸면 변화가 있을거라고 생각했습니다.
이러한 시간 변화는 결국 효율로 직결되기에 이 시간을 단축시키는 레이아웃을 찾기위해 실험에 착수했습니다.

- I자 모형: 작업자들은 트랙들 사이를 움직이지 않습니다. 즉, 직원은 현재 물량이 부족하더라도 하차에서 물량이 들어올 떄까지 대기합니다.
<img src="https://user-images.githubusercontent.com/53500865/149169258-e1340ad5-a082-4c7d-9f56-b08a4569f8e3.png" width="100%" height="100%">


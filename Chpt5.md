# Computer_structure
2021 1학기 컴퓨터구조론 내용정리



딜레이와 CPI
Stall : 멀티사이클로 구동하였을 시 해저드로 인해서 딜레이가 발생한다.

이때, 딜레이는 CPI 가 증가하는 방향으로 보인다.

Hit : 찾고 있는 데이터가 상위 레벨 메모리에서 엑세스 할 수 있을 때

hit rate : 발견에 성공한 비율
hit time : 해당 데이터에 엑세스 하기 위해 필요했던 시간

Miss : Lower 레벨에 데이터가 있다. 즉 상위 레벨에서 데이터를 찾는 데 실패하였다.

miss rate : 1 - hit rate
miss penalty : 상위 레벨의 블럭 대신 하위 레벨의 블럭으로 대체하는데 걸린 시간



캐시 : 임시 메모리의 저장 공간이라고 한다. 빠르고 집적도도 좋고.

Direct mapped cache : 4 bit 데이터가 주어진다.
ㄴ> 0000 0001 0100 ...
ㄴ> 좌측의 두 비트는 데이터
ㄴ> 우측의 두 비트는 1열로 나열된 데이터 주소


만약, 0 4 0 4 와 같은 패턴이 들어오게 된다면, 계속해서 그것은 0이 나오게 된다.
ㄴ> 이것을 핑퐁 효과라고 한다.


1. 찾는 주소에 해당 주소가 들어있다면 Hit
2. 없다면 Miss & 주어진 명령어에 근거하여 그 데이터를 찾고자 하는 데이터로 대체한다.???

맨 처음에는 모두 비어 있는 Empty Cache 로 시작한다.

PPT 58페이지
Multiword block direct mapped cache - 핑퐁 효과를 막기 위한 모델
- 마찬가지로 일련의 정수가 입력이 되고 있다


1. 좌측의 2 비트로 태그의 값을 판정한다.
2. 주소는 오른쪽에서 두번째 index 1비트로 판정한다.

3. 가장 오른쪽의 1비트는 오프셋 비트이다.
ㄴ> 만약 0 이면, miss 일때 우측에서부터 입력된 정수 n, n+1 이 들어간다.
ㄴ> 만약 1 이면, miss 일때 우측에서부터 n, n-1 이 들어간다.

===================

Split Cachesd

Unified Cache(=Single Cache) 는 Structure Hazard 가 발생할 우려가 있다
ㄴ> 따라서 Split 하여 캐시를 사용 하기로 한다.

ㄴ> miss rate 가 더 낮아야 한다.

Instruction Cache / Data Cache / Unified Cache 로 구 성된다.

Miss per instruction 이 주어졌다고 가정하자.

Miss rate (16KB, Inst) = Instruction Cache / MPI * 1
Miss rate (16KB, Data) = Data Cache / MPI * Data Transfer Instruction 36%

Total Miss rate = Miss rate(Inst) * 1/1+0.36  +  Miss rate(Data) * 0.36 / 1 + 0.36


==========================
62페이지의 식
64페이지의 식

==========================
72 페이지의 식

Ping Pong 이펙트 해결하기
ㄴ> 정수가 입력된다. 다만, 블럭이 4블럭으로 나누어져 있다.
ㄴ> 위 아래 2블럭씩 번갈아가면서 판정이 발생한다.


좌측의 3비트가 태그 비트로 사용된다.
최우측의 1비트가 인덱스 비트로 사용된다.

======================
CPI - new

1. CPU 사이클 횟수에 이제 Stall 로 인한 Missed 사이클 횟수가 추가된다. 
2. 사이클 횟수는 I * (C/I) * s/C 인데, 여기서 CPI 에 해당하는 C/I 가 Missed case 의 영향을 받아 변동이 일어난다.

Memory Stall Cycles : (Instructions/Program) * (Misses/instruction) * Miss Penalty


               



# rock-paper-scissors-Game

기존 가위바위보 게임은 createRoom이나 joinRoom에서 hand를 0~2로 받아 트랜잭션 input에서 방장의 hand를 알 수 있고 참가자는 이를 알고 패를 결정할 수 있다는 단점이 있었습니다.

<개발 내용>

1. 가위바위보게임에서 방장(originator)이 createRoom을 할 때 미리 낸 패를 숨길 수 있다.

2. 이후에 joinRoom으로 방에 참여한 참가자(taker)의 패도 숨길 수 있다.

3. 방장이 낸 배팅금액과 같은 금액을 참가자가 배팅해야 입장 할  수있다.

4. use~함수를 이용해서 방장과 참여자 둘다 자신이 낸 진짜 패를 해독하여 저장시킨다.

5. 둘다 해독하여 완벽히 저장되어야 compare를 통해 payout이 가능하다.

<조건>

1. createRoom 또는 joinRoom에서 _hand는 keccak함수를 통해 만들어진 bytes32의 값을 넣어야한다.
2. payout전 방장과 참여자의 진짜 hand값을 저장하기 위해 use~ 함수를 각자 사용하여 진짜 hand값을 저장해야한다.
3. use~함수에 의해 진짜 hand가 저장되고 방장과 참여자의 정보에 count가 1이 되어야만 payout내의 compare함수가 정상작동한다.
4. payout은 방장과 참여자만 실행 할 수 있다.

<문제점>

1. use~함수를 방장과 참여자중 먼저 실행 한 사람의 input을 통해 어떤 진짜패를 냈는지, 
실행하지 않은 자가 확인 할 수 있고 결과를 안 다음 본인이 패배했다면 payout을 못 사용하게 할 수 있다. 배팅금이 영원히 잠긴다.

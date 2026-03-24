1. 락의 안전한 획득과 해제 패턴
<details>
<summary>ReentrantLock 사용 시 lock() 호출을 try 블록 외부에서 해야 하는 이유는 무엇인가요?</summary>
<div markdown="1">
lock() 호출을 try 블록 **직전(외부)**에 두는 이유는 락 획득 과정에서 예외(예: Error나 RuntimeException)가 발생했을 때, finally 블록에서 획득하지도 않은 락을 해제(unlock)하려는 시도를 방지하기 위해서입니다.

만약 try 블록 내부에서 lock()을 호출했다가 락을 얻기 전에 예외가 발생하면, finally에서 unlock()이 호출되면서 IllegalMonitorStateException이 추가로 발생하여 진짜 원인이 되는 예외를 덮어버릴 수 있습니다. 따라서 락 획득 성공이 보장된 시점에 try 블록으로 진입하는 것이 안전한 관례입니다.

</div>
</details>

2. AQS의 상태값과 재진입성(Reentrancy)
<details>
<summary>ReentrantLock에서 '재진입 가능'하다는 것은 내부적으로 어떤 변수를 통해 관리되나요?</summary>
<div markdown="1">
ReentrantLock은 내부적으로 AQS(AbstractQueuedSynchronizer)의 state 값을 이용하여 재진입을 관리합니다.

처음에 락을 획득하면 state는 0에서 1이 됩니다.

동일한 스레드가 다시 lock()을 호출하면, 현재 스레드가 락 소유자임을 확인하고 state 값을 1씩 증가시킵니다.

unlock()이 호출될 때마다 state 값을 1씩 감소시키며, 이 값이 다시 0이 되는 순간에만 실제로 락이 완전히 해제되어 다른 스레드가 획득할 수 있게 됩니다.

</div>
</details>

3. Condition 객체를 활용한 정교한 대기/통지
<details>
<summary>synchronized의 wait/notify 대비 ReentrantLock이 가지는 '복잡한 대기 구조'의 이점은 무엇인가요?</summary>
<div markdown="1">
synchronized는 하나의 객체당 하나의 대기 셋(Wait Set)만 가질 수 있어 notifyAll() 호출 시 깨어날 필요가 없는 스레드까지 모두 깨어나는 '신호 손실'이나 성능 저하가 발생할 수 있습니다.

반면, ReentrantLock은 Condition 객체를 여러 개 생성할 수 있습니다. 예를 들어, 생산자-소비자 패턴에서 notFull과 notEmpty라는 두 개의 Condition을 만들어, 생산자는 notFull에서 기다리고 소비자는 notEmpty에서 기다리게 함으로써 특정 조건의 스레드만 선택적으로 깨우는(signal) 정교한 스케줄링이 가능합니다.

</div>
</details>
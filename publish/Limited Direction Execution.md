중간에 멈춘 위치를 하드웨어에 커널스텍에 저장을 하는게 이 개념과 관련된 protocol이다,

## 문제점
중첩적인 interrupt가 발생하면 Os는 어떻게 하지? 
1. interrupt를 처리하는 중에는 해당 interrupt를 무시한다. 
2. locking schemes를 사용? 
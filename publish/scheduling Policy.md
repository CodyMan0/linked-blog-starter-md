자원을 어떤 시점에 어떤 프로세스에게 할당할지를 결정

## Scheduling 기준
1. CPU utilization ->  
2. 처리율 -> 시간당 몇개의 프로세스를 처리 할 수 있는지
3. Turnaround time -> 요청시간으로부터 완료 시간까지의 시간 
4. Waiting time -> 해당 큐에서 얼만큼 기다리고 있는 시간
5. Response time -> CPU를 할당 받기 위한 요청을 한 시간으로부터 처음으로 응답을 받은 시간 

scheduling 알고리즘이 1,2 는 최대한으로 설계하고 3,4,5는 최소화하여 설계하는게 성능이 좋은 scheduling 
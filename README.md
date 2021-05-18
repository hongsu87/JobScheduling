# Job Scheduling
작업 스케줄링 문제는 n개의 작업, 각 작업의 수행 시간, m개의 동일한 기계가 주어질 때, 모든 작업이 가장 빨리 종료되도록 작업을 기계에 배정하는 문제이다. 
단, 한 작업은 배정된 기계에서 연속적으로 수행되어야 하고 기계는 1번에 하나의 작업만 수행할 수 있다.
- 근사해 구하기 : greedy 알고리즘을 이용하여 현재까지 배정된 작업에 대해서 가장 빨리 끝나는 기계에 새 작업을 배정한다.
- 최적해 구하기 : brute force 알고리즘을 이용하여 작업이 기계에 배정될 수 있는 모든 경우의 수를 구한다.

## 코드 설명
: 주어진 작업의 개수만큼 작업 수행 시간을 랜덤으로 생성한 후, greedy 알고리즘으로 주어진 기계에 작업을 배정하여 모든 작업이 종료되는 시간을 반환한다.
- 입력 : 작업의 개수, 기계의 개수, 각 작업 수행 시간
- 출력 : 모든 작업이 종료된 시간

![1](https://user-images.githubusercontent.com/81207799/118443829-57d33880-b727-11eb-9c12-5f351539469f.png)

## 시간복잡도
### greedy
1. 가장 빨리 끝나는 기계 찾기 : m-1    
n개의 작업이므로 n x O(m)    
2. 가장 마지막으로 종료되는 시간 찾기 : O(m)    

-> n x O(m) + O(m) = **O(nm)**    

### brute force
1. 모든 경우의 수 찾기 : m^n    
2. 가장 마지막으로 종료되는 시간 찾기 : O(m)    

-> O(m^n) + O(m) = **O(m^n)**    

## 근사비율
근사해를 OPT', 최적해를 OPT라고 할 때, OPT'<=2 x OPT 이다.
- 증명)    
![2](https://user-images.githubusercontent.com/81207799/118639863-52ebb300-b813-11eb-9288-b3960eb7a1c9.png)    
OTP' = T + ti    
T' = 작업 i를 제외한 모든 작업의 수행시간의 합을 기계의 수 m으로 나눈 값 (평균 종료 시간)    
-> T <= T'    
![3](https://user-images.githubusercontent.com/81207799/118639886-5848fd80-b813-11eb-96aa-b6822756f74e.png)    

## 예제
n = [2, 3, 4, 5]    
m = 2    
n이 2일 때, t : 2, 4    
n이 3일 때, t : 6, 4, 9    
n이 4일 때, t : 2, 4, 5, 8    
n이 5일 때, t : 9, 4, 6, 8, 10    
### 시간복잡도
- 파랑 : greedy
- 검정 : bruteforce

![4](https://user-images.githubusercontent.com/81207799/118443305-b4822380-b726-11eb-865e-985e0550e351.png)

### 근사비율
근사비율 = 근사해 / 최적해
  | n | 2   | 3   | 4   | 5   |
  | ---- | ---- | ---- | ---- | ---- |
  | 근사해 | 4    | 13    | 12    | 20    |
  | 최적해 | 4    | 10    | 10    | 19    |
  | 근사비율 | 1    | 1.3    | 1.2    | 1.05    |
#### greedy 알고리즘을 이용한 근사해
![5](https://user-images.githubusercontent.com/81207799/118443788-4853ef80-b727-11eb-8f2b-75c1a54cf3ea.png)
![6](https://user-images.githubusercontent.com/81207799/118443803-4d18a380-b727-11eb-8a49-1557e41e338c.png)
![7](https://user-images.githubusercontent.com/81207799/118640939-82e78600-b814-11eb-821c-16fa10f5f573.png)
![8](https://user-images.githubusercontent.com/81207799/118443829-57d33880-b727-11eb-9c12-5f351539469f.png)
#### brute force 알고리즘을 이용한 최적해
<img src="https://user-images.githubusercontent.com/81207799/118640341-d3aaaf00-b813-11eb-8958-5c5fd200d261.png" height="500px" width="500px">

### 결론    
시간복잡도에서 brute force 알고리즘은 n이 커질수록 시간이 급격히 증가하고 greedy 알고리즘과의 시간 차이가 커졌다. 
즉, bruteforce 알고리즘은 정확한 해(최적해)를 구할 수 있지만 m과 n이 커지면 해를 구할 수 없다. 
그렇기 때문에 m과 n이 큰 경우에는 greedy 알고리즘을 이용하여 근사해를 구해야 한다. 
위에서 구한 근사비율을 보면 대부분 1에 가까운 값으로 거의 정확했다. 
일반적으로 근사비율을 구할 때는 최적해를 구할 수 없기 때문에 간접적인 최적해를 이용한다. 
이처럼 NP 완전 문제에서는 다항식 시간에 최적해를 구할 수 없으므로 근사비율과 함께 근사해를 이용한다. 
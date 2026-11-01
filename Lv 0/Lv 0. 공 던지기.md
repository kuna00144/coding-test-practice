---
title: 공 던지기
aliases: [공 던지기]
platform: 프로그래머스
level: Lv.0
category: 코딩테스트 입문
problem_type: 함수 작성
language: Python
tags: [코딩테스트, 반복문, 원형순회, 나머지연산]
status: 성공
help: 혼자 해결
---

# 공 던지기 (프로그래머스 Lv.0)

## 문제 요약
- 1번부터 번호가 붙은 사람들이 **원형**으로 서 있음
- 공은 1번부터 시작해서 **한 명 건너뛰고** 그다음 사람에게 던짐
- k번째로 공을 **던지는** 사람의 번호 반환

> [!info] 유형
> 반복문 시뮬레이션 / **원형(끝에서 처음으로 돌아가기)** / 나머지 연산

---

## 내 코드 (통과)
```python
def solution(numbers, k):
    answer = 1
    for _ in range(1, k):            # k-1번 던짐
        answer += 2                  # 한 명 건너뛰기
        if answer > max(numbers):    # 끝을 넘어가면
            answer -= max(numbers)   # 처음으로 돌아감
    return answer
```

> [!success] 잘한 점
> - "k번째로 던지는 사람" = 공이 **k−1번** 이동한 위치 → `range(1, k)`로 정확히 처리
> - 끝을 넘어가면 빼서 처음으로 돌리는 **원형 처리**를 스스로 생각해냄

---

## 개선할 점

> [!tip] 1. `max(numbers)`를 반복문 안에서 매번 계산
> `max()`는 리스트 전체를 훑는 O(N) 작업 → 반복마다 하면 **O(N·K)**
> 번호가 1부터 순서대로이니 `n = len(numbers)`를 **반복문 밖에서 한 번만** 구하면 O(K)

> [!tip] 2. 번호 대신 인덱스로 생각하면 더 일반적
> 지금 코드는 "번호가 1부터 연속"이라는 조건에 기대고 있음
> 인덱스로 계산하고 `numbers[인덱스]`로 꺼내면 번호가 어떻게 생겼든 동작

### 개선 버전
```python
def solution(numbers, k):
    n = len(numbers)
    idx = 0                          # 0번 인덱스(1번 사람)부터
    for _ in range(k - 1):
        idx = (idx + 2) % n          # 나머지 연산으로 원형 처리
    return numbers[idx]
```

### 한 줄 버전 (참고)
```python
def solution(numbers, k):
    return numbers[2 * (k - 1) % len(numbers)]
```
k−1번 던질 때마다 2칸씩 → 총 `2 * (k - 1)`칸 이동 → 원형이니 `% n`

### 복잡도
- 내 코드: **O(N·K)** → 개선 버전: **O(K)** → 한 줄 버전: **O(1)**

---

## 핵심 개념 정리

> [!important] 1. 원형 순회 = 나머지 연산 `%`
> `(idx + 2) % n` → n을 넘어가면 자동으로 0부터 다시
> 원형 큐, 시계, 요일 계산 등에 계속 나옴

> [!important] 2. 반복문 안에서 매번 같은 계산을 하지 않기
> 바뀌지 않는 값(`len`, `max`)은 **반복문 밖에서 한 번만** 구해두기

> [!important] 3. "k번째" 문제는 off-by-one 주의
> k번째 행동 = 이동은 k−1번 → 작은 예시로 손으로 세어보기

---

## 공부해야 할 부분
- [ ] 나머지 연산 `%`로 원형 처리하기
- [ ] 반복문 안 불필요한 계산 줄이기 (시간 복잡도 감각)

## 관련 문제
- 프로그래머스 Lv.0 **배열 회전시키기** — 원형 이동

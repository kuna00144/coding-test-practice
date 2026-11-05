---
title: "[PCCE 기출문제] 9번 / 지폐 접기"
aliases: [지폐 접기, PCCE 9번 지폐 접기]
platform: 프로그래머스
level: Lv.1
category: PCCE 기출문제
problem_type: 함수 작성 (문제에 의사코드 제공)
language: Python
tags: [코딩테스트, while, 시뮬레이션, min-max]
status: 성공
help: AI 도움 많이 받음 → 다시 풀기 필요
---

# [PCCE 기출문제] 9번 / 지폐 접기 (프로그래머스 Lv.1)

## 문제 요약
- 지갑 크기 `wallet`, 지폐 크기 `bill` (각각 [가로, 세로])
- 지폐가 지갑에 들어갈 때까지 **긴 쪽을 반으로** 접음 (홀수면 소수점 버림)
- 그대로 또는 **90도 돌려서** 들어가면 멈춤
- 최소 접는 횟수 반환
- 문제 설명에 **의사코드가 함께 제공됨**

> [!info] 유형
> `while` 시뮬레이션 / 조건이 만족될 때까지 반복 / **min, max로 회전 처리**

---

## 풀이 과정
- **AI 도움을 많이 받아서** 해결 → 혼자 설계한 풀이는 아님
- 막혔던 포인트(추정):
  - "90도 돌려서 넣기"를 조건으로 어떻게 표현할지
  - while 조건을 "들어갈 때까지"가 아니라 "**안 들어가는 동안**"으로 뒤집어 쓰는 것

---

## 내 코드 (통과)
```python
def solution(wallet, bill):
    answer = 0
    wallet_min, wallet_max = min(wallet), max(wallet)
    bill_min, bill_max = min(bill), max(bill)

    while bill_min > wallet_min or bill_max > wallet_max:   # 안 들어가는 동안
        if bill[0] > bill[1]:            # 긴 쪽을
            bill[0] = bill[0] // 2       # 반으로 (소수점 버림)
        else:
            bill[1] = bill[1] // 2
        bill_min, bill_max = min(bill), max(bill)   # 접은 뒤 다시 계산
        answer += 1

    return answer
```

### 다듬은 버전 (참고)
```python
def solution(wallet, bill):
    w_small, w_big = sorted(wallet)
    b_small, b_big = sorted(bill)
    answer = 0
    while b_small > w_small or b_big > w_big:
        b_big //= 2                          # 항상 긴 쪽을 접음
        b_small, b_big = sorted([b_small, b_big])   # 다시 짧은/긴 쪽 정렬
        answer += 1
    return answer
```
- 처음부터 "짧은 쪽, 긴 쪽"으로 정리해두면 `bill[0] > bill[1]` 비교가 필요 없음

### 복잡도
- 시간: **O(log B)** (B = 지폐의 큰 변, 매번 절반), 공간: **O(1)**

---

## 핵심 개념 정리

> [!important] 1. "90도 회전" = 짧은 변끼리, 긴 변끼리 비교
> 돌려 넣을 수 있다는 건 방향이 상관없다는 뜻
> → `min(지폐) <= min(지갑)` **그리고** `max(지폐) <= max(지갑)`이면 들어감

> [!important] 2. while 조건은 "멈출 조건"의 반대
> - 멈출 조건: 짧은 변 ≤ 짧은 변 **and** 긴 변 ≤ 긴 변
> - 반복 조건: 짧은 변 > 짧은 변 **or** 긴 변 > 긴 변
> - **and의 반대는 or** (드모르간 법칙) → [[Lv 1. 공원 산책]]의 범위 밖 검사와 같은 원리

> [!important] 3. 반복문 안에서 바뀌는 값은 다시 계산
> 접을 때마다 bill이 바뀌니 `bill_min`, `bill_max`도 **반복문 안에서** 다시 구해야 함
> (밖에서 한 번만 구하면 무한 루프!)

> [!important] 4. `//` 몫 연산
> `17 // 2` → `8` (소수점 버림)

---

## 공부해야 할 부분
- [ ] **AI 없이 다시 풀기** (우선순위 높음)
- [ ] "멈출 조건 → 반복 조건"으로 뒤집기 (and ↔ or)
- [ ] 반복문 안에서 갱신해야 하는 변수 vs 밖에서 한 번만 구하는 변수 구분

## 관련 문제
- [[Lv 0. PCCE 4번 저축]] — 조건 만족까지 while 반복
- [[Lv 1. 공원 산책]] — 범위 밖 조건(or)

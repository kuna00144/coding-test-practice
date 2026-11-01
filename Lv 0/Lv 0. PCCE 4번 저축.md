---
title: "[PCCE 기출문제] 4번 / 저축"
aliases: [저축, PCCE 4번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 빈칸 채우기
language: Python
tags: [코딩테스트, 기초문법, 반복문, while, 시뮬레이션]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 4번 / 저축 (프로그래머스 Lv.0)

## 문제 요약
- 목표 금액 100만 원(코드에선 100)
- 첫 달 `start`만큼 저축 → 70 미만이면 매달 `before`씩 → 70 이상부터는 매달 `after`씩
- 100 이상 모일 때까지 걸리는 **개월 수** 출력

> [!info] 유형
> 빈칸 채우기 / `while` 반복문 / 단순 시뮬레이션

---

## 내 코드 (통과)
```python
start = int(input())
before = int(input())
after = int(input())

money = start
month = 1
while money < 70:          # 70 미만인 동안
    money += before
    month += 1
while money < 100:         # 100 미만인 동안
    money += after
    month += 1

print(month)
```

---

## 핵심 개념 정리

> [!important] 1. `for` vs `while`
> - `for` → **몇 번** 반복할지 알 때 (`range(n)`)
> - `while` → **언제까지** 반복할지(조건)만 알 때
> - 이 문제는 "몇 달 걸릴지"가 답이라 미리 모름 → `while`

> [!important] 2. 두 단계 while
> 첫 while이 끝나면 money는 이미 70 이상 → 두 번째 while이 이어서 진행
> 처음부터 70 이상이면 첫 while은 **한 번도 실행 안 됨** (입출력 예 #2)

> [!important] 3. 카운터 변수
> `month += 1`처럼 반복할 때마다 1씩 늘려서 횟수 세기

---

## 공부해야 할 부분
- [ ] while 조건이 처음부터 거짓이면 아예 실행 안 된다는 점 (엣지 케이스)

## 관련 문제
- [[Lv 1. PCCE 9번 지폐 접기]] — 조건이 만족될 때까지 반복하는 while

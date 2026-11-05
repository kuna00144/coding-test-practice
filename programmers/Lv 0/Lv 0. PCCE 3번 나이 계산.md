---
title: "[PCCE 기출문제] 3번 / 나이 계산"
aliases: [나이 계산, PCCE 3번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 빈칸 채우기
language: Python
tags: [코딩테스트, 기초문법, 조건문, 입출력]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 3번 / 나이 계산 (프로그래머스 Lv.0)

## 문제 요약
- 출생 연도 `year`와 나이 종류 `age_type`이 입력으로 주어짐
- 2030년 기준 나이를 출력
  - `"Korea"` → 한국식 나이: 현재 연도 − 출생 연도 + 1
  - `"Year"` → 연 나이: 현재 연도 − 출생 연도

> [!info] 유형
> 빈칸 채우기 / 조건문 분기 / 표준 입력

---

## 내 코드 (통과)
```python
year = int(input())
age_type = input()          # 문자열은 int() 없이 그대로

if age_type == "Korea":
    answer = 2030 - year + 1
elif age_type == "Year":
    answer = 2030 - year

print(answer)
```

---

## 핵심 개념 정리

> [!important] 1. `input()`은 항상 문자열
> - 숫자로 쓸 거면 `int(input())`
> - 문자열 그대로 쓸 거면 `input()`

> [!important] 2. 문자열 비교는 따옴표 + 철자 정확히
> `age_type == "Korea"` → 대소문자, 철자 하나만 달라도 False
> ([[Lv 0. 캐릭터의_좌표]]에서 `"rignt"` 오타로 키가 무시됐던 것과 같은 함정)

> [!important] 3. `if` / `elif` 구조
> 경우가 서로 겹치지 않으면 `elif`로 연결 → 하나가 참이면 나머지는 검사 안 함

---

## 공부해야 할 부분
- [ ] `input()` 결과의 자료형 의식하기
- [ ] 문자열 비교 시 철자 확인 습관

## 관련 문제
- [[Lv 0. PCCE 2번 피타고라스의 정리]] — 표준 입력
- [[Lv 0. PCCE 7번 가습기]] — 조건문 분기 심화

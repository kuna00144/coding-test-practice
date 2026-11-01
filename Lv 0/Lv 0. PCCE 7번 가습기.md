---
title: "[PCCE 기출문제] 7번 / 가습기"
aliases: [가습기, PCCE 7번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 빈칸 채우기
language: Python
tags: [코딩테스트, 기초문법, 조건문, 함수]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 7번 / 가습기 (프로그래머스 Lv.0)

## 문제 요약
- 가습기 모드 `mode_type`("auto", "target", "minimum"), 습도 `humidity`, 설정값 `val_set`
- 모드별 규칙에 따라 현재 가습 단계(0~5) 반환
  - auto: 습도 구간(10 단위)에 따라 5 → 0단계
  - target: 설정값 미만 3단계, 이상 1단계
  - minimum: 설정값 미만 1단계, 이상 0단계

> [!info] 유형
> 빈칸 채우기 / 조건문 분기 / **함수 나누기**

---

## 내 코드 (통과)
```python
def func1(humidity, val_set):        # target 모드
    if humidity < val_set:
        return 3
    return 1

def func2(humidity):                 # auto 모드
    if humidity >= 50:
        return 0
    elif humidity >= 40:
        return 1
    elif humidity >= 30:
        return 2
    elif humidity >= 20:
        return 3
    elif humidity >= 10:
        return 4
    else:
        return 5

def func3(humidity, val_set):        # minimum 모드
    if humidity < val_set:
        return 1
    return 0

def solution(mode_type, humidity, val_set):
    answer = 0
    if mode_type == "auto":
        answer = func2(humidity)
    elif mode_type == "target":
        answer = func1(humidity, val_set)
    elif mode_type == "minimum":
        answer = func3(humidity, val_set)
    return answer
```

> [!success] 잘한 점
> 함수 이름(func1/2/3)만 보고 어떤 모드인지 **함수 내용을 읽어서** 연결함 → 코드 읽기 능력

---

## 핵심 개념 정리

> [!important] 1. 큰 값부터 검사하는 elif 사다리
> `>= 50` → `>= 40` → … 순서로 쓰면 각 구간의 **아래쪽 경계만** 쓰면 됨
> (위에서 이미 걸러졌으니 "40 이상 50 미만"을 다 쓸 필요 없음)

> [!important] 2. `return`을 만나면 함수 즉시 종료
> `func1`에서 `if`가 참이면 `return 3`으로 끝 → 그래서 `else` 없이 `return 1`만 써도 됨

> [!important] 3. 함수로 나누기
> 복잡한 조건을 모드별 함수로 나누면 읽기 쉬움 → 싸피 시뮬레이션처럼 긴 코드에서 유용

---

## 공부해야 할 부분
- [ ] 구간 조건을 elif로 간결하게 쓰는 순서 감각
- [ ] 함수 분리해서 코드 짜보기

## 관련 문제
- [[Lv 0. PCCE 3번 나이 계산]] — 조건문 분기 기초

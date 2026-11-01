---
title: "[PCCE 기출문제] 5번 / 산책"
aliases: [산책, PCCE 5번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 빈칸 채우기
language: Python
tags: [코딩테스트, 기초문법, 문자열순회, 방향이동, 시뮬레이션]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 5번 / 산책 (프로그래머스 Lv.0)

## 문제 요약
- `"N"`, `"S"`, `"E"`, `"W"`로 이루어진 문자열 `route`대로 한 칸씩 이동
- 최종 위치를 `[동쪽으로 떨어진 거리, 북쪽으로 떨어진 거리]`로 반환
- 서쪽·남쪽은 **음수**로 표현

> [!info] 유형
> 빈칸 채우기 / 문자열 순회 / 방향 이동 (맵 경계 없음)
> [[Lv 0. 캐릭터의_좌표]], [[Lv 1. 공원 산책]]의 가장 기초 버전

---

## 내 코드 (통과)
```python
def solution(route):
    east = 0
    north = 0
    for i in route:            # 문자열을 한 글자씩
        if i == "N":
            north += 1
        elif i == "S":
            north -= 1
        elif i == "E":
            east += 1
        elif i == "W":
            east -= 1
    return [east, north]
```

### 딕셔너리 버전 (캐릭터의 좌표에서 배운 방식)
```python
def solution(route):
    move = {"N": (0, 1), "S": (0, -1), "E": (1, 0), "W": (-1, 0)}
    east, north = 0, 0
    for d in route:
        de, dn = move[d]
        east, north = east + de, north + dn
    return [east, north]
```

### 복잡도
- 시간: **O(L)** (L = route 길이), 공간: **O(1)**

---

## 핵심 개념 정리

> [!important] 1. 문자열도 for문으로 한 글자씩 순회 가능
> `for i in "NSE":` → `"N"`, `"S"`, `"E"` 차례로

> [!important] 2. 이 문제는 **수학 좌표** (북쪽 = +)
> [[Lv 1. 공원 산책]]은 **2차원 리스트** (북쪽 = 행 번호 −)
> → 문제마다 좌표계가 다를 수 있으니 **방향 부호를 꼭 확인!**

> [!important] 3. 방향 문제 3단계 성장
> 1. 산책: 경계 없이 이동만
> 2. [[Lv 0. 캐릭터의_좌표]]: 경계 + 무시
> 3. [[Lv 1. 공원 산책]]: 경계 + 장애물 + 여러 칸

---

## 공부해야 할 부분
- [ ] 수학 좌표 vs 2차원 리스트 좌표의 방향 차이

## 관련 문제
- [[Lv 0. 캐릭터의_좌표]]
- [[Lv 1. 공원 산책]]

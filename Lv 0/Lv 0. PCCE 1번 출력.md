---
title: "[PCCE 기출문제] 1번 / 출력"
aliases: [출력, PCCE 1번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 빈칸 채우기
language: Python
tags: [코딩테스트, 기초문법, 자료형, 형변환]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 1번 / 출력 (프로그래머스 Lv.0)

## 문제 요약
- 빈칸 3개에 값을 넣어서, 주어진 print 3줄이 예시와 똑같이 출력되게 만들기
- 핵심: `int_val + 10`은 **숫자 덧셈**, `string_val + "10"`은 **문자열 이어붙이기**

> [!info] 유형
> 빈칸 채우기 / 자료형(int, str) 구분

---

## 내 코드 (통과)
```python
string_msg = "Spring is beginning"
int_val = 3
string_val = str(3)

print(string_msg)
print(int_val + 10)       # 3 + 10 = 13
print(string_val + "10")  # "3" + "10" = "310"
```

> [!success] 잘한 점
> `string_val`에 `str(3)`을 넣어 **형 변환**으로 해결 → `"3"`이라고 써도 같은 결과

---

## 핵심 개념 정리

> [!important] 1. 같은 `+`라도 자료형에 따라 다르게 동작
> - 숫자 + 숫자 → 덧셈: `3 + 10` → `13`
> - 문자열 + 문자열 → 이어붙이기: `"3" + "10"` → `"310"`
> - 숫자 + 문자열 → **에러** (`TypeError`)

> [!important] 2. 형 변환
> - `str(3)` → `"3"`
> - `int("3")` → `3` ([[Lv 1. 공원 산책]]에서 `int(v)`로 다시 사용)

> [!important] 3. 리스트·튜플의 `+`, `*`도 "이어붙이기/반복"
> `[1, 0] + [0, 1]` → `[1, 0, 0, 1]`, `(0, 1) * 2` → `(0, 1, 0, 1)` ([[Lv 1. 공원 산책]]에서 빠졌던 함정)

---

## 공부해야 할 부분
- [ ] 자료형에 따라 연산자가 다르게 동작한다는 감각 → 공원 산책의 `start + move[k]` 실수와 연결

## 관련 문제
- [[Lv 1. 공원 산책]] — `int(v)` 형 변환, 리스트+튜플 함정

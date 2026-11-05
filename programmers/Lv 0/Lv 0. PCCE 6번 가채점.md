---
title: "[PCCE 기출문제] 6번 / 가채점"
aliases: [가채점, PCCE 6번]
platform: 프로그래머스
level: Lv.0
category: PCCE 기출문제
problem_type: 한 줄 수정 (디버깅)
language: Python
tags: [코딩테스트, 기초문법, 리스트인덱스, 디버깅]
status: 성공
help: 혼자 해결
---

# [PCCE 기출문제] 6번 / 가채점 (프로그래머스 Lv.0)

## 문제 요약
- `numbers`: 문의하려는 학생 **번호** 리스트
- `our_score`: 그 학생들이 가채점한 점수 (numbers와 같은 순서)
- `score_list`: 실제 성적 (**1번 학생부터** 순서대로)
- 같으면 `"Same"`, 다르면 `"Different"`를 순서대로 담아 반환 → **한 줄 수정**

> [!info] 유형
> 한 줄 수정(디버깅) / 리스트 인덱스 / **번호(1부터) vs 인덱스(0부터)**

---

## 내 코드 (통과)
```python
def solution(numbers, our_score, score_list):
    answer = []
    for i in range(len(numbers)):
        if our_score[i] == score_list[numbers[i] - 1]:   # 핵심 줄
            answer.append("Same")
        else:
            answer.append("Different")
    return answer
```

---

## 핵심 개념 정리

> [!important] 1. 학생 번호 ≠ 리스트 인덱스
> - 학생 번호는 **1번부터**, 리스트 인덱스는 **0번부터**
> - 3번 학생의 실제 성적 → `score_list[3 - 1]` = `score_list[2]`
> - 번호를 인덱스로 쓸 땐 **−1** 잊지 말기!

> [!important] 2. 인덱스를 두 단계로 따라가기
> `score_list[numbers[i] - 1]`
> → i번째 문의 학생의 **번호**를 꺼내고 → 그 번호로 실제 성적을 찾음
> **값 vs 좌표**([[Lv 0. 안전지대]]) 감각과 연결: `numbers[i]`는 값이지만, 여기선 그 값이 다시 **위치 번호**로 쓰임

> [!important] 3. 결과를 모을 땐 `append`
> 반복문 안에서 `=`로 쓰면 덮어쓰기 ([[Lv 1. 공원 산책]]에서 했던 실수)

---

## 공부해야 할 부분
- [ ] 1부터 세는 번호 ↔ 0부터 세는 인덱스 변환
- [ ] 인덱스 안에 인덱스가 들어간 코드 읽기

## 관련 문제
- [[Lv 0. 안전지대]] — 값 vs 좌표
- [[Lv 1. 공원 산책]] — append vs 덮어쓰기

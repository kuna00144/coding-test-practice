---
title: JadenCase 문자열 만들기
aliases: [JadenCase 문자열 만들기, JadenCase]
platform: 프로그래머스
level: Lv.2
category: 연습문제
problem_type: 함수 작성
language: Python
tags: [코딩테스트, 문자열, split, join, 엣지케이스]
status: 성공
help: 설계 혼자, capitalize는 검색, 엣지 케이스는 질문 힌트 받음
---

# JadenCase 문자열 만들기 (프로그래머스 Lv.2)

## 문제 핵심 (내 말로)
- 문자열의 각 단어를 **첫 글자는 대문자, 나머지는 소문자**로 바꾸기
- 단어 사이 공백은 **연속으로 여러 칸** 나올 수 있고, 그대로 유지해야 함
- 첫 글자가 숫자면 그대로 두고 나머지만 소문자

> [!info] 유형
> 문자열 처리 / `split`과 `join` / **엣지 케이스(연속 공백)**
> 격자·위치 문제에서 벗어난 첫 **문자열** 유형

---

## 내 분석
- s를 공백 기준으로 나눠서 리스트에 저장
- 각 단어의 첫 글자는 대문자, 나머지는 소문자로 바꾸기
- 반복문 돌면서 리스트를 다시 문자열로 합쳐서 반환
- 원래는 첫 글자 `upper()`, 나머지 `lower()`로 처리하려 했는데, 검색해서 `capitalize()` 발견
  - 실전에서 까먹으면 `upper`, `lower` 조합으로 처리할 것

> [!success] 잘한 점
> - 전체 흐름(나누기 → 변환 → 합치기)을 혼자 설계
> - 검색으로 더 간단한 도구(`capitalize`)를 찾고, **까먹었을 때의 대안**까지 생각해둠

---

## 풀이 과정

### 1차 ❌ 연속 공백과 반복 단어에서 틀림
```python
def solution(s):
    s_list = list(s.split())
    answer = ""
    for i in range(len(s_list)):
        if s_list[i] != s_list[0]:       # 첫 단어가 아니면 공백 추가
            answer += " "
        answer += s_list[i].capitalize()
    return answer
```

**놓친 것 1: 연속 공백이 사라짐**
```python
print("for  the".split())       # ['for', 'the']          ← 공백 두 칸 정보가 사라짐
print("for  the".split(" "))    # ['for', '', 'the']      ← 빈 문자열로 공백이 보존됨
```
- `split()` (괄호 비움) → 공백이 몇 칸이든 **하나로 취급**하고 빈 값은 버림
- `split(" ")` → 공백 **한 칸마다** 나눔 → 연속 공백은 빈 문자열 `''`로 남음
- 그래서 `"for  the"`가 `"For The"`(한 칸)가 되어버림

**놓친 것 2: 값으로 "첫 번째"를 판단함** ⚠️ 값 vs 좌표
- `s_list[i] != s_list[0]` → "**몇 번째**인지"가 아니라 "**무슨 단어**인지"를 비교
- `s = "a a a"`면 두 번째, 세 번째 `"a"`도 `s_list[0]`과 같아서 **공백이 안 붙음** → `"AAA"`
- 위치를 비교하려면 값이 아니라 **인덱스 `i`**를 써야 함 (`i != 0`)

### 2차 → 성공 🎉
- `split(" ")`로 연속 공백을 빈 문자열로 보존
- 각 원소를 `capitalize()`로 변환 (빈 문자열은 그대로 빈 문자열)
- `" ".join()`으로 합치면 빈 문자열 자리에 공백이 다시 살아남
- `join`이 사이사이에만 공백을 넣어주니 **"첫 단어인지" 판단하는 if문 자체가 필요 없어짐**

---

## 최종 코드 (통과)
```python
def solution(s):
    s_list = list(s.split(" "))          # 공백 한 칸 기준 → 연속 공백은 '' 로 보존
    answer = ""
    for i in range(len(s_list)):
        s_list[i] = s_list[i].capitalize()   # 첫 글자 대문자, 나머지 소문자

    answer = " ".join(s_list)            # 사이사이에 공백 한 칸씩 → 원래 공백 복원

    return answer
```

### 동작 예시 (손으로 따라가기)
```text
s = "3people  unFollowed me"

split(" ")   → ['3people', '', 'unFollowed', 'me']
capitalize   → ['3people', '', 'Unfollowed', 'Me']
" ".join     → "3people  Unfollowed Me"     ← 공백 두 칸 유지
```
- `'3people'.capitalize()` → 첫 글자가 숫자라 대문자 변환 없음, 나머지는 소문자
- `''.capitalize()` → 빈 문자열 그대로

### 복잡도
- 시간: **O(L)** (L = 문자열 길이), 공간: **O(L)**

---

## 다듬은 버전 (참고)
```python
def solution(s):
    return " ".join(word.capitalize() for word in s.split(" "))
```
- `s.split(" ")`는 이미 리스트를 반환하므로 `list()`로 감쌀 필요 없음
- `answer = ""` 초기화는 사용되지 않으므로 삭제 가능
- 변환과 합치기를 한 줄로 (리스트 컴프리헨션과 같은 문법, [[Lv 1. 모의고사]] 참고)

### `capitalize()`를 까먹었을 때
```python
def solution(s):
    words = s.split(" ")
    for i in range(len(words)):
        if words[i]:                                   # 빈 문자열이 아닐 때만
            words[i] = words[i][0].upper() + words[i][1:].lower()
    return " ".join(words)
```
- 빈 문자열에서 `words[i][0]`을 꺼내면 **에러** → `if words[i]:`로 먼저 확인 필요
- `capitalize()`는 이걸 알아서 처리해줌 → 도구를 알면 엣지 케이스가 줄어듦

---

## 틀렸던 부분 한눈에 보기

| 실수 | 왜 틀렸나 | 바른 방법 |
|---|---|---|
| `s.split()` | 연속 공백을 하나로 합치고 빈 값은 버림 | `s.split(" ")` |
| `s_list[i] != s_list[0]` | **값**으로 첫 번째를 판단 → 같은 단어 반복 시 오작동 | 위치로 판단 `i != 0`, 또는 `join` 사용 |
| 반복문에서 공백을 직접 붙임 | 공백 규칙을 직접 관리해야 해서 복잡 | `" ".join()`이 사이사이에 자동 삽입 |
| `list(s.split(" "))` | `split`은 이미 리스트 | `s.split(" ")` |

---

## 핵심 개념 정리

> [!IMPORTANT]
> **1. `split()` vs `split(" ")`**
>
> | 코드 | `"a  b"` 결과 | 특징 |
> |---|---|---|
> | `split()` | `['a', 'b']` | 공백 여러 칸 = 하나, 빈 값 버림 |
> | `split(" ")` | `['a', '', 'b']` | 공백 한 칸마다 나눔, 빈 값 유지 |
>
> **공백 개수를 지켜야 하면 `split(" ")`**, 단어만 필요하면 `split()`

> [!IMPORTANT]
> **2. `join`은 split의 반대**
> `" ".join(['a', '', 'b'])` → `"a  b"`
> `split(" ")` 후 `" ".join()`하면 **원래 공백 구조가 그대로 복원**됨

> [!IMPORTANT]
> **3. 값 vs 좌표 ⚠️ (또 등장)**
> "첫 번째인지"는 **위치(인덱스)**의 문제 → 값끼리 비교하면 같은 값이 반복될 때 깨짐
> [[Lv 0. 안전지대]], [[Lv 1. 공원 산책]], [[Lv 1. 키패드 누르기]]에 이어 문자열에서도 등장

> [!IMPORTANT]
> **4. 문자열 메서드**
> - `capitalize()` → 첫 글자 대문자, **나머지 소문자**
> - `upper()` / `lower()` → 전체 대문자 / 소문자
> - `title()` → 단어마다 첫 글자 대문자 (단, 숫자·특수문자 뒤 글자도 대문자로 바꿔서 이 문제엔 부적합)

> [!IMPORTANT]
> **5. 엣지 케이스는 제한사항에 숨어 있다**
> "공백이 연속해서 나올 수 있다" 같은 한 줄이 정답을 가름
> → 문제 읽을 때 **제한사항을 엣지 케이스 목록**으로 보기

---

## 공부해야 할 부분
- [ ] `split()`과 `split(" ")` 차이 → 직접 `print`로 실험해본 것처럼 헷갈리면 실험
- [ ] 제한사항에서 엣지 케이스 뽑아내는 습관
- [ ] 값 vs 좌표 — 문자열·리스트에서도 똑같이 적용
- [ ] `capitalize` 없이 `upper` + 슬라이싱으로도 풀어보기 (빈 문자열 처리 포함)

## 회고
- Lv.2지만 설계는 바로 나옴 → 막힌 건 **도구의 세부 동작**(`split` 인자 유무)
- 힌트로 받은 `print` 실험 두 줄로 차이를 직접 확인 → 모르면 **실험해보는 습관**
- `join`을 쓰니 if문이 통째로 사라짐 → 좋은 도구는 코드와 실수를 함께 줄여줌

## 비슷한 유형 추천
- 프로그래머스 Lv.1 **이상한 문자 만들기** — 단어별 짝/홀 인덱스 대소문자 변환, **연속 공백** 함정 동일
- 프로그래머스 Lv.1 **시저 암호** — 문자 단위 변환

## 관련 문제
- [[Lv 1. 키패드 누르기]] — 문자열 만들기 (`+=`, `join`)
- [[Lv 1. 모의고사]] — 컴프리헨션 문법

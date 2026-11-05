---
title: SWEA 입출력 템플릿
aliases: [SWEA 입출력, SWEA 템플릿]
tags: [코딩테스트, SWEA, 입출력, 템플릿, Python, SSAFY대비]
---

# SWEA 입출력 템플릿 (Python)

> [!NOTE]
> SW Expert Academy(SWEA) 문제를 Python으로 풀 때 쓰는 입출력 정리입니다.
> 프로그래머스와 달리 SWEA는 **직접 입력을 읽고, 정해진 형식으로 출력**해야 합니다.
> 문제를 풀 때마다 옆에 띄워두고 참고하세요.

## 목차
1. [프로그래머스 vs SWEA](#1-프로그래머스-vs-swea)
2. [기본 뼈대](#2-기본-뼈대)
3. [입력 패턴 6가지](#3-입력-패턴-6가지)
4. [출력 패턴 3가지](#4-출력-패턴-3가지)
5. [자주 틀리는 함정](#5-자주-틀리는-함정)
6. [로컬 테스트 방법](#6-로컬-테스트-방법)
7. [복사해서 쓰는 전체 템플릿](#7-복사해서-쓰는-전체-템플릿)
8. [제출 전 체크리스트](#8-제출-전-체크리스트)

---

## 1. 프로그래머스 vs SWEA

| 구분 | 프로그래머스 | SWEA |
|---|---|---|
| 입력 | 함수 인자로 주어짐 `solution(board)` | `input()`으로 **직접 읽기** |
| 출력 | `return` | `print()`로 **형식 맞춰 출력** |
| 테스트케이스 | 함수가 케이스마다 따로 호출됨 | 한 번 실행에 **여러 케이스를 반복 처리** |
| 출력 형식 | 값만 반환 | `#번호 답` |

### 입력은 이렇게 들어옵니다
문제의 입력 설명 예시:
```text
첫 줄에 테스트케이스 개수 T가 주어진다.
각 테스트케이스의 첫 줄에 N과 M이 주어지고,
다음 N줄에 걸쳐 N개의 숫자가 공백으로 구분되어 주어진다.
```
실제 입력 (통째로 들어옴):
```text
2
3 2
1 3 5
2 4 6
7 8 9
4 2
...
```
출력:
```text
#1 23
#2 41
```

---

## 2. 기본 뼈대

```python
T = int(input())
for tc in range(1, T + 1):
    # ① 입력 받기
    # ② 풀이
    # ③ 출력
    print(f"#{tc} {answer}")
```

> [!TIP]
> `range(1, T + 1)`로 쓰는 이유: 출력 번호가 **1부터** 시작하기 때문

---

## 3. 입력 패턴 6가지

거의 모든 SWEA 문제는 아래 패턴의 조합입니다.

| # | 입력 모양 | 코드 |
|---|---|---|
| ① | 숫자 하나 `5` | `n = int(input())` |
| ② | 숫자 여러 개 → 변수 `3 2` | `n, m = map(int, input().split())` |
| ③ | 숫자 여러 개 → 리스트 `1 3 5 7` | `arr = list(map(int, input().split()))` |
| ④ | 격자, **공백 있음** `1 0 1` | `board = [list(map(int, input().split())) for _ in range(n)]` |
| ⑤ | 격자, **공백 없음** `101` | `board = [list(map(int, input().strip())) for _ in range(n)]` |
| ⑥ | 문자열 한 줄 `hello` | `s = input().strip()` |

```python
# ① 숫자 하나
n = int(input())

# ② 한 줄에 숫자 여러 개 → 변수로 나눠 담기
n, m = map(int, input().split())

# ③ 한 줄에 숫자 여러 개 → 리스트로
arr = list(map(int, input().split()))

# ④ 격자 (숫자가 공백으로 구분된 N줄)
board = [list(map(int, input().split())) for _ in range(n)]

# ⑤ 격자 (공백 없이 붙어 있는 N줄, 예: "01101")
board = [list(map(int, input().strip())) for _ in range(n)]

# ⑥ 문자열 한 줄
s = input().strip()
```

> [!WARNING]
> **④와 ⑤를 헷갈리면 바로 틀립니다.**
> 입력 예시에서 **숫자 사이에 공백이 있는지** 반드시 확인하세요.
> 공백 없는 `"01101"`에 `split()`을 쓰면 `["01101"]` 한 덩어리가 됩니다.

> [!TIP]
> `.strip()`은 줄 끝의 공백·줄바꿈을 지워주는 **안전장치**입니다.
> 문자열을 읽을 때는 습관적으로 붙이세요.

---

## 4. 출력 패턴 3가지

```python
# ① 답 하나
print(f"#{tc} {answer}")
# → #1 23

# ② 답이 여러 개 (한 줄에 공백으로)
print(f"#{tc}", *result)            # result = [3, 1, 2]
# → #1 3 1 2

# ③ 답이 격자 (번호 줄 + 격자 줄들)  예: 달팽이 숫자
print(f"#{tc}")
for row in board:
    print(*row)
# → #1
#   1 2 3
#   8 9 4
#   7 6 5
```

> [!TIP]
> `*리스트`는 리스트를 풀어서 **공백으로 띄워** 출력합니다. (대괄호·쉼표 없이)
> `print(*[1, 2, 3])` → `1 2 3`

---

## 5. 자주 틀리는 함정

> [!CAUTION]
> **1. `[S/W 문제해결 기본]` 시리즈는 T가 주어지지 않습니다.**
> 1208 Flatten, 1206 View 등은 테스트케이스가 **10개로 고정**이고,
> 각 케이스 첫 줄에 테스트케이스 번호 등 다른 값이 먼저 옵니다.
> ```python
> for tc in range(1, 11):          # T = int(input()) 없음!
>     case_no = int(input())       # 문제에 따라 첫 줄 형태가 다름
>     ...
> ```
> → **입력 설명을 항상 먼저 읽기**

> [!CAUTION]
> **2. 출력 형식은 글자 하나까지 정확해야 합니다.**
>
> | 출력 | 결과 |
> |---|---|
> | `#1 23` | ✅ |
> | `#1: 23` | ❌ 콜론 |
> | `# 1 23` | ❌ `#` 뒤 공백 |
> | `#1  23` | ❌ 공백 두 개 |

> [!CAUTION]
> **3. `input()` 안에 안내 문구를 넣지 마세요.**
> `input("숫자 입력: ")` → 문구까지 출력으로 잡혀서 오답

> [!WARNING]
> **4. 테스트케이스마다 변수를 초기화하세요.**
> 정답 변수, 방문 배열 등을 `for tc` **바깥**에서 만들면 이전 케이스 값이 남습니다.
> → 케이스마다 새로 써야 하는 변수는 **반복문 안**에서 만들기

---

## 6. 로컬 테스트 방법

SWEA 문제의 입력 예시를 `input.txt`로 저장하고, 코드 맨 위에 추가:

```python
import sys
sys.stdin = open("input.txt", "r")
```

매번 입력을 손으로 칠 필요 없이 파일에서 읽어옵니다.

> [!CAUTION]
> **제출 전에 반드시 이 두 줄을 지우거나 주석 처리!**
> 서버에는 `input.txt`가 없어서 에러가 납니다. (실제로 정말 많이 하는 실수)

### (참고) 입력이 많을 때 빠르게 읽기
```python
import sys
input = sys.stdin.readline
```
- 입력 줄 수가 아주 많은 문제에서 시간 초과를 줄여줍니다.
- 이때 문자열을 읽으면 끝에 줄바꿈이 붙으므로 **반드시 `.strip()`**

---

## 7. 복사해서 쓰는 전체 템플릿

```python
# import sys
# sys.stdin = open("input.txt", "r")   # 로컬 테스트용 — 제출 전 주석 처리!

T = int(input())
for tc in range(1, T + 1):
    # ===== 입력 =====
    n, m = map(int, input().split())
    board = [list(map(int, input().split())) for _ in range(n)]

    # ===== 풀이 =====
    answer = 0

    # ===== 출력 =====
    print(f"#{tc} {answer}")
```

### 격자 문제용 (방향 리스트 포함)
```python
T = int(input())
for tc in range(1, T + 1):
    n = int(input())
    board = [list(map(int, input().split())) for _ in range(n)]

    dr = [-1, 1, 0, 0]          # 상 하 좌 우
    dc = [0, 0, -1, 1]

    answer = 0
    for r in range(n):
        for c in range(n):
            for k in range(4):
                nr, nc = r + dr[k], c + dc[k]
                if 0 <= nr < n and 0 <= nc < n:     # 범위 검사 (좌표 숫자!)
                    pass                            # board[nr][nc] 활용

    print(f"#{tc} {answer}")
```

### BFS 문제용
```python
from collections import deque

T = int(input())
for tc in range(1, T + 1):
    n = int(input())
    board = [list(map(int, input().strip())) for _ in range(n)]

    dr = [-1, 1, 0, 0]
    dc = [0, 0, -1, 1]
    dist = [[0] * n for _ in range(n)]      # 방문 체크 겸 거리 (케이스마다 새로!)

    q = deque()
    q.append((0, 0))                        # 시작점
    dist[0][0] = 1

    while q:
        r, c = q.popleft()
        for k in range(4):
            nr, nc = r + dr[k], c + dc[k]
            if 0 <= nr < n and 0 <= nc < n and board[nr][nc] == 0 and dist[nr][nc] == 0:
                dist[nr][nc] = dist[r][c] + 1
                q.append((nr, nc))

    answer = 0                              # 문제에 맞게 dist에서 계산
    print(f"#{tc} {answer}")
```

---

## 8. 제출 전 체크리스트

- [ ] 입력 설명을 읽고 **T가 주어지는지** 확인했다
- [ ] 격자 입력에 **공백이 있는지 없는지** 확인했다 (`split()` 여부)
- [ ] 케이스마다 써야 하는 변수를 **`for tc` 안에서** 초기화했다
- [ ] 출력이 `#번호 답` 형식과 **정확히** 같다
- [ ] `sys.stdin = open(...)` 줄을 **지우거나 주석 처리**했다
- [ ] `input()` 안에 안내 문구가 없다
- [ ] 입력 예시로 돌려서 출력 예시와 **완전히 같은지** 확인했다

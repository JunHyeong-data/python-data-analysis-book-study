# Python `re` 모듈 정리

Python의 `re` 모듈은 정규 표현식(Regular Expression)을 사용해 문자열에서 패턴을 검색, 치환, 분리할 수 있도록 도와주는 내장 모듈입니다.

---

## 🔧 주요 함수

| 함수 | 설명 |
|------|------|
| `re.compile(pattern)` | 정규표현식을 객체로 컴파일 (재사용에 유리) |
| `re.match(pattern, string)` | 문자열 **시작**부터 패턴이 일치하는지 검사 |
| `re.search(pattern, string)` | 문자열 전체에서 **처음** 일치하는 부분 검색 |
| `re.findall(pattern, string)` | 패턴과 일치하는 **모든 문자열 리스트** 반환 |
| `re.finditer(pattern, string)` | 패턴과 일치하는 모든 부분을 **Match 객체 반복자**로 반환 |
| `re.sub(pattern, repl, string)` | 일치하는 부분을 `repl`로 **치환** |
| `re.split(pattern, string)` | 패턴을 기준으로 **문자열 분리** |

---

## 🧱 자주 쓰는 정규표현식 패턴

| 패턴 | 의미 | 예시 |
|------|------|------|
| `.` | 임의의 한 문자 (줄바꿈 제외) | `"a.c"` → "abc", "a1c" 등 |
| `^` | 문자열 **시작** | `"^a"` → "apple" 매치 |
| `$` | 문자열 **끝** | `"z$"` → "buzz" 매치 |
| `*` | 0번 이상 반복 | `"ab*"` → "a", "ab", "abbb" |
| `+` | 1번 이상 반복 | `"ab+"` → "ab", "abbb" |
| `?` | 0 또는 1번 반복 | `"ab?"` → "a", "ab" |
| `{n}` | n번 반복 | `"a{3}"` → "aaa" |
| `{n,m}` | n~m번 반복 | `"a{2,4}"` → "aa", "aaa", "aaaa" |
| `[abc]` | a 또는 b 또는 c |
| `[^abc]` | a, b, c를 제외한 문자 |
| `[0-9]` | 숫자 |
| `\d` | 숫자 (`[0-9]`) |
| `\D` | 숫자가 아닌 문자 (`[^0-9]`) |
| `\w` | 단어 문자 (`[a-zA-Z0-9_]`) |
| `\W` | 단어 문자가 아닌 것 |
| `\s` | 공백 문자 (스페이스, 탭 등) |
| `\S` | 공백이 아닌 문자 |
| `|` | OR 조건 | `"cat|dog"`은 "cat" 또는 "dog" |

---

## 🔍 Match 객체

`re.match()` 또는 `re.search()`는 **Match 객체**를 반환하며, 다음 메서드 사용 가능:

- `group()` : 매치된 전체 문자열
- `start()` : 시작 인덱스
- `end()` : 끝 인덱스
- `span()` : (시작, 끝) 튜플 반환

```python
import re

m = re.search(r'\d+', 'Age: 21')
print(m.group())   # 21
print(m.start())   # 5
print(m.end())     # 7
print(m.span())    # (5, 7)
```

---

## 🧪 예제 코드

```python
import re

text = "My phone number is 010-1234-5678"

# 전화번호 추출
pattern = r'\d{3}-\d{4}-\d{4}'
match = re.search(pattern, text)
if match:
    print(match.group())  # 010-1234-5678

# 모든 숫자 추출
numbers = re.findall(r'\d+', text)
print(numbers)  # ['010', '1234', '5678']

# 문자열 분리
parts = re.split(r'[-\s]', text)
print(parts)  # ['My', 'phone', 'number', 'is', '010', '1234', '5678']
```

---

## 📌 팁

- 정규표현식은 `r''` **raw 문자열** 형식으로 쓰는 것이 안전합니다. (`\\` 처리 방지)
- 자주 쓰는 패턴은 `re.compile()`로 컴파일하여 반복 사용 시 효율적입니다.
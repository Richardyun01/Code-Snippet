# 띄어쓰기 비교
## 출처
[프로그래머즈 PCCP 인증시험 Python3](https://certi.programmers.co.kr/about/pccp)

## 목적
- 원 문제: 두 단어 원본과 비교군의 일치 비교
- 이때 비교군은 대문자/소문자의 오용이 가능하고 띄어쓰기가 생략될 경우 동일한 것으로 간주
- 그 외의 오류는 틀린 것으로 간주(띄어쓰기가 잘못된 경우도 포함)
- ex
  - 원본: Hello World
  - 비교군 1: HELLOWORLD -> 동일
  - 비교군 2: heLLo wORld -> 동일
  - 비교군 3: Hel loWor ld -> 틀림
  
## 해결
- 대문자/소문자의 오용은 casefold()로 해결이 가능
- 띄어쓰기의 생략은 replace()로 해결이 가능하나 이 경우 띄어쓰기의 오용은 판별 불가
- 원본 띄어쓰기는 유지하거나 삭제할 수 있으므로
  - 유지: 동일 위치에서 공백-공백 매칭
  - 삭제: 원본 공백만 건너뜀
- 두 포인터를 진행
  - 원본이 공백일 경우:
    - 후보도 공백이면 -> 공백 유지: i, j를 둘 다 1칸 전진
    - 후보가 글자면 -> 공백 삭제: i만 1칸 전진(원본 공백 삭제)
  - 원본이 글자일 경우
    - 후보도 공백이면 -> 원래 없던 공백이 추가되었으므로 실패
    - 후보가 글자면 -> 두 글자가 같아야 함, 같으면 둘 다 1칸 전진, 다르면 실패
- 원본에 남은 것이 공백이면 모두 삭제 가능하므로 i를 끝까지 밀기
- 후보에 문자가 남아 있으면 공백 추가로 간주해 실패
- i가 원본 끝에 도달해야 성공

## 코드
```
def solution(s, arrs):
    def is_ok(ori, can):
        o = ori.casefold()
        c = can.casefold()
        i = j = 0
        n, m = len(o), len(c)

        while i < n and j < m:
            oi, cj = o[i], c[j]
            if oi.isspace():
                if cj.isspace():
                    i += 1
                    j += 1
                else:
                    i += 1
            else:
                if cj.isspace():
                    return False
                if oi != cj:
                    return False
                i += 1
                j += 1
        while i < n and o[i].isspace():
            i += 1
        if j < m:
            return False
        return i == n

    answer = [is_ok(s, arr) for arr in arrs]
    return answer

print(solution('Hello World', ['HELLOWORLD', 'heLLo wORld', 'Hel loWor ld']))
```

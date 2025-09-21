# ���� ��
## ����
- �� ����: �� �ܾ� ������ �񱳱��� ��ġ ��
- �̶� �񱳱��� �빮��/�ҹ����� ������ �����ϰ� ���Ⱑ ������ ��� ������ ������ ����
- �� ���� ������ Ʋ�� ������ ����(���Ⱑ �߸��� ��쵵 ����)
- ex
  - ����: Hello World
  - �񱳱� 1: HELLOWORLD -> ����
  - �񱳱� 2: heLLo wORld -> ����
  - �񱳱� 3: Hel loWor ld -> Ʋ��
  
## �ذ�
- �빮��/�ҹ����� ������ casefold()�� �ذ��� ����
- ������ ������ replace()�� �ذ��� �����ϳ� �� ��� ������ ������ �Ǻ� �Ұ�
- ���� ����� �����ϰų� ������ �� �����Ƿ�
  - ����: ���� ��ġ���� ����-���� ��Ī
  - ����: ���� ���鸸 �ǳʶ�
- �� �����͸� ����
  - ������ ������ ���:
    - �ĺ��� �����̸� -> ���� ����: i, j�� �� �� 1ĭ ����
    - �ĺ��� ���ڸ� -> ���� ����: i�� 1ĭ ����(���� ���� ����)
  - ������ ������ ���
    - �ĺ��� �����̸� -> ���� ���� ������ �߰��Ǿ����Ƿ� ����
    - �ĺ��� ���ڸ� -> �� ���ڰ� ���ƾ� ��, ������ �� �� 1ĭ ����, �ٸ��� ����
- ������ ���� ���� �����̸� ��� ���� �����ϹǷ� i�� ������ �б�
- �ĺ��� ���ڰ� ���� ������ ���� �߰��� ������ ����
- i�� ���� ���� �����ؾ� ����

## �ڵ�
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
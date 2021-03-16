# Pythonic Way

----------

> [toc]

<br>

## Cornell Notes [link](https://www.notion.so/dinoryong/Pythonic-Way-2ec2f926c8494ad8a504bd828990b79c)

<br>

## Unpacking

파이썬으로 알고리즘 문제를 좀 풀다보면 이 문법은 친숙할겁니다.

```
a, b = map(int, input().split())
```

이것은 iterable (모든 반복 가능한 객체를 iterable 하다고 합니다! 리스트, 튜플, 문자열 등등...) 한 데이터엔 모두 가능한 문법입니다.

그런데 이런 상황이 있을 겁니다.

> 입력 받은 list에서 첫번째, 마지막 값만 얻고 싶어!

또는

> 입력 받은 list에서 첫번째, 마지막 값을 제외하고 싶어!

이런 경우는 어떻게 해야 할까요?

```
_list = [1, 2, 3, 4, 5]
first_index, *rest, last_index = _list
print(rest) # 2 3 4
```

간단하네요? 파이썬은 *(asterisk)를 다음과 같은 상황에 사용합니다.

- 곱셈, 거듭제곱
- List형 컨테이너를 반복해서 확장
- 가변 인자
- Unpacking

위에서 rest에 사용한 것은 가변인자 입니다. 즉, 인자의 갯수가 몇개가 될지 확실하지 않을때 사용하는 거죠. first_index와 last_index가 앞과 끝을 가져가면, rest가 나머지를 가져가는 겁니다.

그렇다면 Unpacking은 뭘까요? 일단 아래 예시를 보겠습니다.

```
_list = [1, 2, 3, 4, 5]
for num in _list:
    print(num, end = ' ') # 1 2 3 4 5
```

_list내 원소들을 출력하는 평범한 코드입니다. 그렇다면 이건 어떨까요?

```
_list = [1, 2, 3, 4, 5]
print(*_list) # 1 2 3 4 5
```

놀랍게도 동일한 결과를 얻을 수 있습니다. 이것을 **List Unpacking** 이라고 부릅니다.

사실 list뿐만이 아니라, 컨테이너형 구조에선 모두 적용할 수 있습니다. 튜플에서도 되고, set에서도 가능해요.

Unpacking을 이야기 했으니 살짝 다른 이야기를 해보겠습니다. 이건 어떤가요?

```
a, b, c = [1, 2, 3]
d = a, b, c
print(d) # (1, 2, 3)
```

오잉? 첫번째 줄은 알겠는데 두번째 줄은 뭔가요?

저런식으로 하나의 변수에 여러 값을 할당하게 되면 튜플로 묶이게 됩니다. 위에서 튜플로 Unpacking을 할 수 있다고 했으니, 이건 Packing이라고 생각하면 되겠네요.

------

## List Comprehension

파이썬의 꽃 중에 하나로, 한국어로는 **지능형 리스트** 라고도 합니다.

그래도 List Comprehension은 워낙 유명해서 아시는 분들이 조금 많은 것 같지만, 그래도 중요한 내용이니 한 번은 이야기 하고 넘어가겠습니다.

먼저 기본형을 보면,

```
_list = [i for i in range(10)] # 0 1 2 3 4 5 6 7 8 9
```

이런 구조를 띄고 있습니다. 사실 이런 구조는 보기 쉬우니까 처음 보는 사람들도 적당히 이해하고 넘어갈 수 있습니다.

그렇다면 이건 어떨까요?

```
## 백준 온라인 저지 1920번 "수 찾기" (http://boj.kr/1920)
import sys
input = sys.stdin.readline

_ = input()
_set = set(map(int, input().split()))
q = input()
_list = list(map(int, input().split()))

print(*[1 if dt in _set else 0 for dt in _list], sep = '\n')
```

어... 이해가 잘 가시나요? 가신다면 그냥 스크롤을 아래로 쭉~~ 내리시면 됩니다.

우선 List Comprehension은 다음과 같은 구조를 띄고 있습니다.

> (변수를 활용해 만들 값) for (변수 명) in (순회할 수 있는 값)

그렇기 때문에 List Comprehension으로 된 코드를 읽을 때는, 앞에부터 읽는게 아니라, for 뒤 부터 읽으면 꽤 편해요.

이걸 인지하고 위 코드를 다시 보면, _list에 있는 원소를 dt라고 하고, 앞에 있는 `1 if dt in _set else 0`에 대입한다는 이야기네요.

해당 내용은 _set에 원소가 들어있으면 1, 아니면 0을 리턴하라는 말이네요? 휴! 드디어 해석했습니다.

물론 다차원 배열도 사용할 수 있습니다.

```
square = [[x ** 2 for x in range(3)] for _ in range(3)]
print(square) # [[1, 4, 9], [1, 4, 9], [1, 4, 9]]
```

코드의 길이를 확실히 줄일 수 있다는 장점이 있지만, 너무 길면 가독성도 해치고, 코드를 작성하는 본인도 "내가 뭘 하고 있지?" 라는 생각이 들 수 있습니다. 예를 들자면...

```
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print([[x for x in row if x % 3 == 0] for row in matrix if sum(row) >= 10]) # [[6], [9]]
```

제발 이러진 마세요...

참고로, 리스트 뿐만이 아니라 tuple, set, dict도 만들 수 있습니다. dict의 경우 뒷 부분에서 zip을 배우고 나면 정말 요긴하게 쓸 수 있습니다. (즉, 다음에 다룬다는 이야기입니다.) 사용법 자체는 List Comprehension과 유사합니다.

------

## Dictionary 잘 쓰기

파이썬을 교양수업으로 듣던, 책으로 조금만 공부하던, Dictionary와 Set에 대해서는 접해봤을 것 입니다.

다만 처음 배우는 입장에선 '굳이 이걸 사용해야 할까?' 라는 생각을 많이 하더라고요. 어디에 사용하면 좋은지, 그리고 어떻게 해야 잘 사용할 수 있을지 한 번 알아봅시다.

Dictionary와 Set은 *Hash Table* 구조를 띄고 있습니다. (해시에 대해 잘 모르신다면, [여기](https://github.com/VSFe/Algorithm_Study/blob/main/Concept/05_Heap_Hash/Ch.05_힙_해시_Python.pdf)를 봅시다.) 그래서 삽입, 삭제, 탐색 연산의 시간복잡도는 O(1) 입니다.

초보자분들이 가장 많이 하는 실수가, **값을 찾기 위해 list에서 in을 사용한다는 것** 입니다. 아니 그게 뭐가 문제냐고요?

```
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for i in range(100):
    if i in data:
        print(1)
```

해당 코드는 데이터를 순차적으로 탐색합니다. 그러니까 여기선 하나의 숫자를 찾기 위해 최대 10번 데이터를 확인해야 한다는 이야기겠죠.

뭐 데이터 양이 작다면 모르겠지만, 데이터양이 많으면 많아질수록 엄청나게 시간이 많이 소요됩니다. 당장 리스트에 100,000개의 원소가 있는데 20,000개의 랜덤 데이터가 여기 안에 있는지 찾는다고 생각해보세요.

이럴땐 set을 사용해야 합니다.

```
data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
_data_set = set(data)

for i in range(100):
    if i in data:
        print(1)
```

실제로 몇 백만개의 데이터가 있는 set에 약 10만 번 정도의 in 연산을 시행해도 1초도 안 걸리는 시간에 완료하는데, list를 사용하게 되면 몇 시간 이상 걸릴 수 있습니다.

또한 set의 구조상, 같은 값이 들어올 수 없다는 것은 모두가 아실겁니다. 이걸 응용하면 다음과 같은 것도 가능합니다.

```
i_want_to_erase_duplicate_element = [21, 31, 65, 21, 58, 94, 13, 31, 58]
completed_list = list(set(i_want_to_erase_duplicate_element)) # 21, 31, 65, 58, 94, 13

test_list = ['Test', 'test', 'TEST', 'tteesstt']
converted_list = list(set(map(lambda string: string.lower(), test_list))) # test, tteesstt
```

set은 iterable한 데이터를 기반으로 만들 수 있으니, 그걸 다시 list로 바꿔주면 중복된 값이 제거된 list가 만들어집니다.

아래 코드는 조금 어려울텐데, 우리는 lambda를 **익명 함수**라고 합니다. 뒤에 있는 `string`은 각각의 값을 string이라고 지칭하겠다고 선언하는 겁니다. 즉, 각각의 데이터를 소문자로 바꾸고, 그걸 set으로 바꾸고, 다시 list로 돌린거죠.

set은 끝난 것 같고, 이제 dictionary를 다뤄보겠습니다.

dictionary는 키와 쌍으로 이루어져 있습니다. 그렇다면 어떻게 생성할까요?

```
fruit = ['apple', 'grape', 'orange', 'banana']
price = [3200, 15200, 9800, 5000]
_dict = {}

for i in range(len(price)):
    _dict.append((fruit[i], price[i])) # {'apple' : 3200, 'grape' : 15200, 'orange' : 9000, 'banana' : 5000}
```

혹시 이렇게 하시나요?

여기서 **zip**에 대해 나옵니다. zip에 대해 파이썬 레퍼런스는,

> 각 iterables 의 요소들을 모으는 이터레이터를 만듭니다.

라고 하고 있습니다. 즉, 리스트를 묶어준다는 이야기겠네요. zip은 다양하게 활용할 수 있지만, dictionary를 만들 때도 유용하게 쓰일 수 있습니다.

```
fruit = ['apple', 'grape', 'orange', 'banana']
price = [3200, 15200, 9800, 5000]

_dict = dict(zip(fruit, price)) # {'apple' : 3200, 'grape' : 15200, 'orange' : 9000, 'banana' : 5000}
```

이제 생성은 다 되었네요!

일반적으로 딕셔너리에서 없는 값을 찾으려고 하면, 오류가 납니다.

```
fruit = ['apple', 'grape', 'orange', 'banana']
price = [3200, 15200, 9800, 5000]
_dict = dict(zip(fruit, price))

print(_dict['strawberry']) # Error!
```

그래서 이걸 회피하기 위해, 처음 배우는 분들은 in 옵션을 사용해서 데이터가 있는지 확인하고, 없으면 값을 추가하고, 있으면 출력하는 방식으로 넘어갑니다. 그런데, 꼭 if를 써야 할까요?

```
fruit = ['apple', 'grape', 'orange', 'banana']
price = [3200, 15200, 9800, 5000]
_dict = dict(zip(fruit, price))

print(_dict.setdefault('strawberry', 0)) # 0
```

`setdefault`는 딕셔너리에 값이 있을 땐 해당 값을 리턴하고, 값이 없을 땐 두번째 인자로 넘겨준 값을 추가하고 추가한 값을 리턴합니다.

참고로 해당 메소드를 활용한 *유사* dictionary가 있습니다. 우리는 이것을 **defaultdict** 라고 부르는데요,

```
from collections import defaultdict

movie_review = [('Train to Busan', 4), ('Clementine', 5), ('Parasite', 4.5), ('Train to Busan', 4.2), ('Train to Busan', 4.5), ('Clementine', 5)]

index = defaultdict(list)

for review in movie_review:
    index[review[0]].append(review[1]) # {'Train to Busan': [4, 4.2, 4.5], 'Clementine': [5, 5], 'Parasite': [4.5]}
```

defaultdict에서 값을 검색할 때, 값이 없으면 인자로 넘겨준 값이 default 값이 됩니다. 결국 찾을 때 마다 setdefault를 암묵적으로 실행해준다고 생각하면 될 것 같아요.

위에서 unpacking을 배울 때, 리스트나 튜플에서 사용할 수 있는 방법을 배웠습니다. 그런데 dictionary는 원소가 쌍이잖아요? 이걸 어떻게 해야 unpacking을 잘 할 수 있을까요?

```
fruit = ['apple', 'grape', 'orange', 'banana']
price = [3200, 15200, 9800, 5000]
_dict = dict(zip(fruit, price))

print(*_dict.keys()) # apple grape orange banana
print(*_dict.values()) # 3200 15200 9800 5000
print(*_dict.items()) # ('apple', 3200) ('grape', 15200) ('orange', 9800) ('banana', 5000)
```

다음과 같은 keys, values, items를 통해 내부 값을 unpacking 할 수 있습니다.

------

## Sorting

정렬은 **sort()** 라는 메소드가 있고, **sorted()** 라는 함수가 있습니다.

어? 하나는 메소드고 하나는 함수라고요? 정확히 말하자면 전자의 경우 **리스트를 내부 정렬하는 메소드** 이고, 후자는 **컨테이너형 데이터를 받아 정렬된 리스트를 돌려주는 함수** 입니다.

예시를 보면 다음과 같습니다.

```
_list = [5, 6, 4, 8, 2, 3]
sorted_list = sorted(_list) # 2, 3, 4, 5, 6, 8
_list.sort()
print(_list) # 2, 3, 4, 5, 6, 8

_set = {65, 12, 15, 156, 31, 54, 94, 82, 31}
_set.sort() # Error!!!!
print(sorted(_set)) # 12, 15, 31, 54, 65, 82, 94, 156
```

sorted()의 출력값이 **리스트**라는 것에 주목하세요. 애초에 dictionary와 셋은 순서가 없습니다.

내림차순 정렬은 쉽죠.

```
_list = [5, 6, 4, 8, 2, 3]
sorted_list = sorted(_list, reversed = True) # 8, 6, 5, 4, 3, 2
```

그런데... 이런 경우는 어떻게 정렬해야 할까요?

> 튜플의 리스트를 정렬하고 싶은데, 첫번째 값으로 오름차순 정렬을 하는데 값이 같으면 두번째 값으로 내림차순 정렬하고 싶어...

정렬 기준이 복잡하네요... 우선 이 문제를 해결하기 전에, 정렬 함수의 또 다른 옵션을 봅시다.

```
_list = [(1, 3), (8, 2), (2, 5), (4, 7)]
sorted_list = sorted(_list, key = lambda dt: dt[1]) # (8, 2), (1, 3), (2, 5), (4, 7)
```

lambda가 뭐죠? 우선 key는 함수를 입력 받습니다. 즉, lambda가 함수라는 것을 알 수 있습니다.

정확히 말해서, lambda는 **익명 함수**라는 것으로, 함수의 이름을 명시하지 않고 일회성으로 사용하기 위해 정의하는 것입니다. 여기서 *dt*는 함수에서 사용할 변수명으로, dt는 각각의 튜플을 저런식으로 사용하겠다는 겁니다.

즉, 저 문구를 정리하면, **튜플의 첫번째 값을 기준으로 정렬하겠다.** 라는 것이죠.

그렇다면 위에서 제기한 상황에선 어떻게 정렬을 해야할까요?

```
_list = [(1, 3), (8, 2), (2, 5), (4, 7)]
sorted_list = sorted(_list, key = lambda dt: (dt[1], -dt[0])) # (8, 2), (1, 3), (2, 5), (4, 7)
```

이런식으로 해주면 됩니다. 조건이 여러개인 경우 다음과 같이 튜플 형태로 묶어주는데, 음수가 되면 내림차순으로 정렬한다고 생각하면 됩니다. (사실은 각각의 값이 음수가 되면 대소관계가 반전되기 때문에, 음수로 변환해서 대소관계를 비교해서 정렬하는 것입니다.)

lambda를 사용하면 정말 다양한 방식으로 정렬을 할 수 있습니다.

```
_list = ["CHicken", "hamburger", "Sushi", "chocolate"]

print(sorted(_list)) # ['CHicken', 'Sushi', 'chocolate', 'hamburger']
print(sorted(_list, key = lambda dt: dt.lower())) # ['CHicken', 'chocolate', 'hamburger', 'Sushi']
```

일반적으로 문자열은 대소관계를 비교하기 때문에, 다음과 같이 모두 소문자로 바꿔버리면 대소관계 상관 없이 정렬을 할 수 있습니다.

------

## 문자열

코딩테스트를 파이썬으로 보시는 분들의 일부는 문자열 처리의 장점을 내세웁니다. 실제로 파이썬은 다른 언어보다 문자열 처리가 좀 편한 편이죠. 대부분의 문자열 처리는 다들 아실테니, 많은 분들이 잘 모르는 내용을 이야기 해보려고 합니다.

`strip()`에 대해서는 들어보셨을 겁니다. 공백을 제거하는 함수죠?

```
print('     asdasd     '.strip()) # asdasd
```

사실 이건 공백을 제거하는 함수가 아닙니다.

```
print('===chicken==='.strip('=')) # chicken
```

쨔잔! 양 끝에 있는 문자열을 제거하는 함수였습니다. 넘겨주지 않으면 공백 문자로 인식해서 공백을 제거했던 것일 뿐입니다. 참고로, 두개 이상의 문자열을 넣어주면, 두개를 모두 지워버립니다. and 조건이 아니라 or 조건이에요!

문자열을 뒤집고 싶을 땐, 두 가지 방법이 있습니다. (사실 이건 iterable한 데이터에선 모두 사용할 수 있지만, 두번째 때문에 일부러 문자열에서 설명합니다.)

```
string = 'I am Hungry...'
print(string[::-1])
print("".join(reversed(string)))
```

전자의 경우, 모든 iterable한 데이터에서 사용 가능합니다. (즉, 리스트도, 튜플도 가능한거죠.) 잘 모르시는 분들은 슬라이싱을 할 때 두개의 변수만 활용하지만, 세번째를 활용하면 슬라이싱이 더 무궁무진해집니다.

슬라이싱은 `string[시작:종료(포함 안 함):간격]` 구조를 띄고 있습니다. 즉, 마지막이 2이면 0, 2, 4... 번째 문자열을 꺼내오겠죠. -1은? 역순으로 뽑아옵니다. 간격도 물론 조정할 수 있습니다.

두번째의 경우 역순으로 뒤집은 iterator (iterable이 아닙니다!)을 리턴하는데, 그냥 출력하면 메모리 주소가 나오기 때문에 `for i in ~` 구조를 사용하거나 join을 사용합니다. (join 활용법은 아래에서 볼 수 있습니다!)

------

## Combination/Permutation

가끔 모든 경우를 탐색해야 하는 상황이 있습니다. 대표적으로 이런 문제가 있겠네요?

> 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열을 모두 구하시오.

일반적으로 백트래킹을 활용해서 문제를 풉니다. 그렇지만, 다음과 같은 기능을 공부하면 굳이 백트래킹을 할 필요가 없습니다.

```
import itertools
_list = [1, 2, 3, 4]
iter = itertools.combinations(_list, 2) # 12 13 14 23 24 34

iter = itertools.permutations(_list, 2) # 12 13 14 21 23 24 31 32 34 41 42 43

iter = itertools.combinations_with_replacement(_list, 2) # 11 12 13 14 22 23 24 33 34 44

iter = itertools.product(_list, repeat=2) # 11 12 13 14 21 22 23 24 31 32 33 34 41 42 43 44
```

`combination`은 모든 조합을 출력합니다. 즉, 중복이 없고, 순서를 구분하지 않습니다. `permutation`은 순열입니다. 중복은 없지만, 순서를 구분합니다.

`combination_with_replacement`는 중복이 가능한 조합입니다. 그래서 combination과 구분하여 11, 22, 33, 44가 새로 들어오죠. 마지막으로 `product`는 모든 가능한 경우의 수를 출력합니다. (**Cartesian Product**라고 합니다!)

combination을 활용하면 다음과 같은 문제도 해결할 수 있습니다.

> 전체 리스트에서 3개를 추출하여 곱했을 때, 그 곱의 최댓값을 출력하는 프로그램을 작성하시오.

방법은 굳이 알려드리지 않아도 알겠죠?

이처럼 단순히 순열, 조합을 구하는 것이 아닌, 다양한 완전탐색 상황에서 사용될 수 있으니 꼭 기억해두길 바라요.

------

## 기타 짤막한 도움말

### sum

파이썬에는 `reduce()`라는 함수가 있습니다. 예전 Python 2 시절에는 꽤 많이 썼는데, iterable한 값에 연속적으로 연산을 해 하나의 결과물을 출력하는 함수입니다.

```
from functools import reduce
_list = [1, 2, 3, 4, 5]
def sum(a, b):
    return a + b

reduce(sum, _list) # 15
```

뭔가 쓸만할 것 같은 함수죠? 다만 Python 3 에서는 사용하지 않기를 권하고 있고, 이를 대체하기 위한 함수가 여럿 나왔습니다. (all(), any() 등등...)

저기에서 떨어져 나온 함수 중에 하나가 `sum()` 입니다. 뭐냐고요?

```
_list = [1, 2, 3, 4, 5]
print(sum(_list)) # 15
```

이겁니다. 위에 있는 reduce()를 사용하는 것 보다 이게 몇 배는 더 쉽죠?

### join

리스트를 출력하고 싶은데, 출력 형태가 좀 특이합니다.

`1, 2, 3, 4, 5, 6, 7, 8` 처럼 출력을 하라고 하네요.

우선 이런 방법을 떠올릴 수 있지 않을까요?

```
_list = [1, 2, 3, 4, 5, 6, 7, 8]
print(*_list, sep=', ') # 1, 2, 3, 4, 5, 6, 7, 8
```

음... 나쁘지 않습니다. 다만 sep은 출력 할 때만 사용할 수 있기 때문에, 문자열 조작과정에선 사용할 수 없습니다. 다른 방법은 없을까요?

```
_list = [1, 2, 3, 4, 5, 6, 7, 8]
print(', '.join(_list))
```

오? 이게 뭘까요? join에 대한 정의를 봅시다.

> iterable 의 문자열들을 이어 붙인 문자열을 돌려줍니다.

정확히 말하면 str 클래스의 메소드인데, iterable한 데이터들 사이 사이에 문자열을 붙여서 문자열로 되돌려 줍니다. 그렇기 때문에 굳이 출력할 때가 아니더라도 사용할 수 있다는 장점이 있습니다.

### swap하기

C 스타일의 언어를 사용하다 보면, 두 값을 서로 바꿔야 할 때가 있습니다.

```
int a = 3, b = 5;
int tmp = a;
a = b;
b = tmp;
```

이런식으로 임시 변수를 만들어서 값을 바꾸곤 하는데, 파이썬은 그냥

```
a, b = b, a
```

하면 됩니다. 정말 쉽죠?

### for, while문 에서의 else

팁으로 넣어놓긴 하지만, 사용할 땐 좀 신중하게 사용해야 합니다.

이중 이상의 반복문을 사용하다가 중간에 break를 해야 할 때가 있습니다. 흔히 C 스타일의 언어는 다음과 같이 사용하죠.

```
for (int i = 0; i < N; i++) {
    bool tmp = true;
    for (int j = 0; j < N; j++) {
        if (sample[i][j] != 1) {
            tmp = false;
            break;
        }
    }
    if(tmp) {
        // Some Code...
    }
}
```

이런식으로, flag에 해당하는 변수를 하나 만들어서 참/거짓 여부를 판단합니다. 파이썬은 이걸 다음과 같이 사용할 수 있습니다.

```
for i in range(N):
    for j in range(N):
        if sample[i][j] != 1:
            break
    else:
        # Some Code...
```

어? 굉장히 낯선 코드입니다. for와 while 구문을 진행하다가 else가 나오면, **반복문을 break로 탈출하지 않았다면 진입**하는 구간으로 의미가 변경됩니다.

다만, 코드를 줄이는덴 좋긴 하지만, 상황에 따라 본인도 코드를 헷갈려 할 수 있습니다. 이걸 사용하기 전엔 한 번 생각해보고 (익숙해지고 싶다면 주석을 쓰셔도 되겠네요.) 사용해보는걸 권장합니다.

### Enumerate

for 를 사용하면 일반적으로 `range`를 사용해서 범위를 표시하거나, iterable한 데이터를 가져와서 내용물을 꺼냅니다.

다만 이런 경우가 있죠.

```
_list = [a, b, c, d, e, f, g]
# 목표: (1, a), (2, b), (3, c)...
```

분명 iterable하게 for를 쓰고 싶지만, 앞에 있는 숫자 때문에 할 수 없이

```
_list = [a, b, c, d, e, f, g]
for i in range(len(_list)):
    print(i, _list[i])
```

이렇게 쓰곤 합니다. 이걸 개선해보죠.

```
_list = [a, b, c, d, e, f, g]
for idx, val in enumerate(_list):
    print(idx, val)
```

`enumerate`라는 단어는 **열거하다** 라는 의미를 갖고 있습니다. enumerate를 사용하면 **(인덱스, 값)** 의 형태의 튜플을 돌려줍니다. 즉, 힘들게 range()를 사용하지 않아도 되는거죠!

### Counter

가끔, 문자열에 들어간 글자를 셀 필요가 있습니다. 일반적으로는 딕셔너리를 사용해서 해결하곤 하죠.

```
def countLetters(word):
    counter = {}
    for letter in word:
        counter.setdefault(letter, 0)
        counter[letter] += 1
    return counter

countLetters('Hello World') # {'H': 1, 'e': 1, 'l': 3, 'o': 2, ' ': 1, 'W': 1, 'r': 1, 'd': 1}
```

사실 이것도 충분히 쓸만합니다. 그런데 이걸 더 줄일 순 없을까요?

```
from collections import Counter
Counter('hello world') # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})
```

Counter는 다양한 메소드를 지원합니다.

```
from collections import Counter
Counter('hello world').most_common() # [('l', 3), ('o', 2), ('h', 1), ('e', 1), (' ', 1), ('w', 1), ('r', 1), ('d', 1)]
Counter('hello world').most_common(2) # [('l', 3), ('o', 2)]
```

`most_common()`을 사용하면 전체 결과를 튜플의 리스트로 리턴하고, 숫자를 명시하면 상위 n개에 해당하는 결과만 출력합니다.

---------------

# Part 2-3 Python

- [Generator](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#generator)
- [클래스를 상속했을 때 메서드 실행 방식](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#클래스를-상속했을-때-메서드-실행-방식)
- [GIL 과 그로인한 성능 문제](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#gil-과-그로인한-성능-문제)
- [GC 작동 방식](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#gc-작동-방식)
- [Celery](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#celery)
- [PyPy 가 CPython 보다 빠른 이유](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#pypy가-cpython보다-빠른-이유)
- [메모리 누수가 발생할 수 있는 경우](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#메모리-누수가-발생할-수-있는-경우)
- [Duck Typing](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#Duck-Typing)

[뒤로](https://github.com/JaeYeopHan/for_beginner)

## Generator

[Generator(제네레이터)](https://docs.python.org/3/tutorial/classes.html#generators)는 제네레이터 함수가 호출될 때 반환되는 [iterator(이터레이터)](https://docs.python.org/3/tutorial/classes.html#iterators)의 일종이다. 제네레이터 함수는 일반적인 함수와 비슷하게 생겼지만 `yield 구문`을 사용해 데이터를 원하는 시점에 반환하고 처리를 다시 시작할 수 있다. 일반적인 함수는 진입점이 하나라면 제네레이터는 진입점이 여러개라고 생각할 수 있다. 이러한 특성때문에 제네레이터를 사용하면 원하는 시점에 원하는 데이터를 받을 수 있게된다.

### 예제

```
>>> def generator():
...     yield 1
...     yield 'string'
...     yield True

>>> gen = generator()
>>> gen
<generator object generator at 0x10a47c678>
>>> next(gen)
1
>>> next(gen)
'string'
>>> next(gen)
True
>>> next(gen)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

### 동작

1. yield 문이 포함된 제네레이터 함수를 실행하면 제네레이터 객체가 반환되는데 이 때는 함수의 내용이 실행되지 않는다.
2. `next()`라는 빌트인 메서드를 통해 제네레이터를 실행시킬 수 있으며 `next()` 메서드 내부적으로 iterator 를 인자로 받아 이터레이터의 `__next__()` 메서드를 실행시킨다.
3. 처음 `__next__()` 메서드를 호출하면 함수의 내용을 실행하다 yield 문을 만났을 때 처리를 중단한다.
4. 이 때 모든 local state 는 유지되는데 변수의 상태, 명령어 포인터, 내부 스택, 예외 처리 상태를 포함한다.
5. 그 후 제어권을 상위 컨텍스트로 양보(yield)하고 또 `__next__()`가 호출되면 제네레이터는 중단된 시점부터 다시 시작한다.

> yield 문의 값은 어떤 메서드를 통해 제네레이터가 다시 동작했는지에 따라 다른데, `__next__()`를 사용하면 None 이고 `send()`를 사용하면 메서드로 전달 된 값을 갖게되어 외부에서 데이터를 입력받을 수 있게 된다.

### 이점

List, Set, Dict 표현식은 iterable(이터러블)하기에 for 표현식 등에서 유용하게 쓰일 수 있다. 이터러블 객체는 유용한 한편 모든 값을 메모리에 담고 있어야 하기 때문에 큰 값을 다룰 때는 별로 좋지 않다. 제네레이터를 사용하면 yield 를 통해 그때그때 필요한 값만을 받아 쓰기때문에 모든 값을 메모리에 들고 있을 필요가 없게된다.

> `range()`함수는 Python 2.x 에서 리스트를 반환하고 Python 3.x 에선 range 객체를 반환한다. 이 range 객체는 제네레이터, 이터레이터가 아니다. 실제로 `next(range(1))`를 호출해보면 `TypeError: 'range' object is not an iterator` 오류가 발생한다. 그렇지만 내부 구현상 제네레이터를 사용한 것 처럼 메모리 사용에 있어 이점이 있다.

```
>>> import sys
>>> a = [i for i in range(100000)]
>>> sys.getsizeof(a)
824464
>>> b = (i for i in range(100000))
>>> sys.getsizeof(b)
88
```

다만 제네레이터는 그때그때 필요한 값을 던져주고 기억하지는 않기 때문에 `a 리스트`가 여러번 사용될 수 있는 반면 `b 제네레이터`는 한번 사용된 후 소진된다. 이는 모든 이터레이터가 마찬가지인데 List, Set 은 이터러블하지만 이터레이터는 아니기에 소진되지 않는다.

```
>>> len(list(b))
100000
>>> len(list(b))
0
```

또한 `while True` 구문으로 제공받을 데이터가 무한하거나, 모든 값을 한번에 계산하기엔 시간이 많이 소요되어 그때 그때 필요한 만큼만 받아 계산하고 싶을 때 제네레이터를 활용할 수 있다.

### Generator, Iterator, Iterable 간 관계

[![img](https://camo.githubusercontent.com/b9f263e15badcde98f562297225d770eac1f0ef29291a822e01d09d43239945e/687474703a2f2f6e7669652e636f6d2f696d672f72656c6174696f6e73686970732e706e67)](https://camo.githubusercontent.com/b9f263e15badcde98f562297225d770eac1f0ef29291a822e01d09d43239945e/687474703a2f2f6e7669652e636f6d2f696d672f72656c6174696f6e73686970732e706e67)

#### Reference

- [제네레이터 `__next__()` 메서드](https://docs.python.org/3/reference/expressions.html#generator.__next__)
- [제네레이터 `send()` 메서드](https://docs.python.org/3/reference/expressions.html#generator.send)
- [yield 키워드 알아보기](https://tech.ssut.me/2017/03/24/what-does-the-yield-keyword-do-in-python/)
- [Generator 와 yield 키워드](https://item4.github.io/2016-05-09/Generator-and-Yield-Keyword-in-Python/)
- [Iterator 와 Generator](http://pythonstudy.xyz/python/article/23-Iterator와-Generator)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## 클래스를 상속했을 때 메서드 실행 방식

인스턴스의 메서드를 실행한다고 가정할 때 `__getattribute__()`로 bound 된 method 를 가져온 후 메서드를 실행한다. 메서드를 가져오는 순서는 `__mro__`에 따른다. MRO(method resolution order)는 메소드를 확인하는 순서로 파이썬 2.3 이후 C3 알고리즘이 도입되어 지금까지 사용되고있다. 단일상속 혹은 다중상속일 때 어떤 순서로 메서드에 접근할지는 해당 클래스의 `__mro__`에 저장되는데 왼쪽에 있을수록 우선순위가 높다. B, C 를 다중상속받은 D 클래스가 있고, B 와 C 는 각각 A 를 상속받았을 때(다이아몬드 상속) D 의 mro 를 조회하면 볼 수 있듯이 부모클래스는 반드시 자식클래스 이후에 위치해있다. 최상위 object 클래스까지 확인했는데도 적절한 메서드가 없으면 `AttributeError`를 발생시킨다.

```
class A:
    pass

class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass

>>> D.__mro__
(__main__.D, __main__.B, __main__.C, __main__.A, object)
```

[![img](https://camo.githubusercontent.com/6440fe7ffb2f7bf1bea228e4adc4dcd61dbe027f9ea80ec402856e557bba6d12/68747470733a2f2f6d616b696e612d636f727075732e636f6d2f626c6f672f6d65746965722f323031342f707974686f6e2d6d726f2d636f6e666c696374)](https://camo.githubusercontent.com/6440fe7ffb2f7bf1bea228e4adc4dcd61dbe027f9ea80ec402856e557bba6d12/68747470733a2f2f6d616b696e612d636f727075732e636f6d2f626c6f672f6d65746965722f323031342f707974686f6e2d6d726f2d636f6e666c696374)

Python 2.3 이후 위 이미지와 같은 상속을 시도하려하면 `TypeError: Cannot create a consistent method resolution` 오류가 발생한다.

#### Reference

- [INHERITANCE(상속), MRO](https://kimdoky.github.io/python/2017/11/28/python-inheritance.html)
- [What does mro do](https://stackoverflow.com/questions/2010692/what-does-mro-do)
- [Python 2.3 이후의 MRO 알고리즘에 대한 파이썬 공식 문서](https://www.python.org/download/releases/2.3/mro/)
- [What is a method in python](https://stackoverflow.com/questions/3786881/what-is-a-method-in-python/3787670#3787670)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## GIL 과 그로인한 성능 문제

GIL 때문에 성능 문제가 대두되는 경우는 압축, 정렬, 인코딩 등 수행시간에 CPU 의 영향이 큰 작업(CPU bound)을 멀티 스레드로 수행하도록 한 경우다. 이 땐 GIL 때문에 멀티 스레드로 작업을 수행해도 싱글 스레드일 때와 별반 차이가 나지 않는다. 이를 해결하기 위해선 멀티 스레드는 파일, 네트워크 IO 같은 IO bound 프로그램에 사용하고 멀티 프로세스를 활용해야한다.

### GIL(Global Interpreter Lock)

GIL 은 스레드에서 사용되는 Lock 을 인터프리터 레벨로 확장한 개념인데 여러 스레드가 동시에 실행되는걸 방지한다. 더 정확히 말하자면 어느 시점이든 하나의 Bytecode 만이 실행되도록 강제한다. 각 스레드는 다른 스레드에 의해 GIL 이 해제되길 기다린 후에야 실행될 수 있다. 즉 멀티 스레드로 만들었어도 본질적으로 싱글 스레드로 동작한다.

[![img](https://camo.githubusercontent.com/e2e6b345dc114675c9b3bfd9daa371806055e696c090310bc8429c4453b076d1/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a6871575845516d794d5a43477a4141787264304e30672e706e67)](https://camo.githubusercontent.com/e2e6b345dc114675c9b3bfd9daa371806055e696c090310bc8429c4453b076d1/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a6871575845516d794d5a43477a4141787264304e30672e706e67)

*출처 [mjhans83 님의 python GIL](https://medium.com/@mjhans83/python-gil-f940eac0bef9)*

### GIL 의 장점

코어 개수는 점점 늘어만 가는데 이 GIL 때문에 그 장점을 제대로 살리지 못하기만 하는 것 같으나 이 GIL 로 인한 장점도 존재한다. GIL 을 활용한 멀티 스레드가 그렇지 않은 멀티 스레드보다 구현이 쉬우며, 레퍼런스 카운팅을 사용하는 메모리 관리 방식에서 GIL 덕분에 오버헤드가 적어 싱글 스레드일 때 [fine grained lock 방식](http://fileadmin.cs.lth.se/cs/education/eda015f/2013/herlihy4-5-presentation.pdf)보다 성능이 우월하다. 또한 C extension 을 활용할 때 GIL 은 해제되므로 C library 를 사용하는 CPU bound 프로그램을 멀티 스레드로 실행하는 경우 더 빠를 수 있다.

#### Reference

- [동시성과 병렬성](https://www.slideshare.net/deview/2d4python)
- [Understanding the Python GIL](http://www.dabeaz.com/python/UnderstandingGIL.pdf)
- [Threads and the GIL](http://jessenoller.com/blog/2009/02/01/python-threads-and-the-global-interpreter-lock)
- [Python GIL](https://medium.com/@mjhans83/python-gil-f940eac0bef9)
- [Old GIL 과 New GIL](https://blog.naver.com/parkjy76/30167429369)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## GC 작동 방식

파이썬에선 기본적으로 [garbage collection](https://docs.python.org/3/glossary.html#term-garbage-collection)(가비지 컬렉션)과 [reference counting](https://docs.python.org/3/glossary.html#term-reference-count)(레퍼런스 카운팅)을 통해 할당 된 메모리를 관리한다. 기본적으로 참조 횟수가 0 이된 객체를 메모리에서 해제하는 레퍼런스 카운팅 방식을 사용하지만, 참조 횟수가 0 은 아니지만 도달할 수 없는 상태인 reference cycles(순환 참조)가 발생했을 때는 가비지 컬렉션으로 그 상황을 해결한다.

> 엄밀히 말하면 레퍼런스 카운팅 방식을 통해 객체를 메모리에서 해제하는 행위가 가비지 컬렉션의 한 형태지만 여기서는 순환 참조가 발생했을 때 cyclic garbage collector 를 통한 **가비지 컬렉션**과 **레퍼런스 카운팅**을 통한 가비지 컬렉션을 구분했다.

여기서 '순환 참조가 발생한건 어떻게 탐지하지?', '주기적으로 감시한다면 그 주기의 기준은 뭘까?', '가비지 컬렉션은 언제 발생하지?' 같은 의문이 들 수 있는데 이 의문을 해결하기 전에 잠시 레퍼런스 카운팅, 순환 참조, 파이썬의 가비지 컬렉터에 대한 간단한 개념을 짚고 넘어가자. 이 개념을 알고 있다면 바로 [가비지 컬렉션의 작동 방식 단락](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#가비지-컬렉션의-작동-방식)을 읽으면 된다.

#### 레퍼런스 카운팅

모든 객체는 참조당할 때 레퍼런스 카운터를 증가시키고 참조가 없어질 때 카운터를 감소시킨다. 이 카운터가 0 이 되면 객체가 메모리에서 해제한다. 어떤 객체의 레퍼런스 카운트를 보고싶다면 `sys.getrefcount()`로 확인할 수 있다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;"><span>&nbsp;</span><code style="box-sizing: border-box; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-size: 13.6px; padding: 0.2em 0.4em; margin: 0px; background-color: var(--color-markdown-code-bg); border-radius: 6px;">Py_INCREF()</code>와<span>&nbsp;</span><code style="box-sizing: border-box; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-size: 13.6px; padding: 0.2em 0.4em; margin: 0px; background-color: var(--color-markdown-code-bg); border-radius: 6px;">Py_DECREF()</code>를 통한 카운터 증감</summary></details>

#### 순환 참조

순환 참조의 간단한 예제는 자기 자신을 참조하는 객체다.

```
>>> l = []
>>> l.append(l)
>>> del l
```

`l`의 참조 횟수는 1 이지만 이 객체는 더이상 접근할 수 없으며 레퍼런스 카운팅 방식으로는 메모리에서 해제될 수 없다.

또 다른 예로는 서로를 참조하는 객체다.

```
>>> a = Foo()  # 0x60
>>> b = Foo()  # 0xa8
>>> a.x = b  # 0x60의 x는 0xa8를 가리킨다.
>>> b.x = a  # 0xa8의 x는 0x60를 가리킨다.
# 이 시점에서 0x60의 레퍼런스 카운터는 a와 b.x로 2
# 0xa8의 레퍼런스 카운터는 b와 a.x로 2다.
>>> del a  # 0x60은 1로 감소한다. 0xa8은 b와 0x60.x로 2다.
>>> del b  # 0xa8도 1로 감소한다.
```

이 상태에서 `0x60.x`와 `0xa8.x`가 서로를 참조하고 있기 때문에 레퍼런스 카운트는 둘 다 1 이지만 도달할 수 없는 가비지가 된다.

#### 가비지 컬렉터

파이썬의 `gc` 모듈을 통해 가비지 컬렉터를 직접 제어할 수 있다. `gc` 모듈은 [cyclic garbage collection 을 지원](https://docs.python.org/3/c-api/gcsupport.html)하는데 이를 통해 reference cycles(순환 참조)를 해결할 수 있다. gc 모듈은 오로지 순환 참조를 탐지하고 해결하기위해 존재한다. [`gc` 파이썬 공식문서](https://docs.python.org/3/library/gc.html)에서도 순환 참조를 만들지 않는다고 확신할 수 있으면 `gc.disable()`을 통해 garbage collector 를 비활성화 시켜도 된다고 언급하고 있다.

> Since the collector supplements the reference counting already used in Python, you can disable the collector if you are sure your program does not create reference cycles.

### 가비지 컬렉션의 작동 방식

순환 참조 상태도 해결할 수 있는 cyclic garbage collection 이 어떤 방식으로 동작하는지는 결국 **어떤 기준으로 가비지 컬렉션이 발생**하고 **어떻게 순환 참조를 감지**하는지에 관한 내용이다. 이에 대해 차근차근 알아보자.

#### 어떤 기준으로 가비지 컬렉션이 일어나는가

앞에서 제기했던 의문은 결국 발생 기준에 관한 의문이다. 가비지 컬렉터는 내부적으로 `generation`(세대)과 `threshold`(임계값)로 가비지 컬렉션 주기와 객체를 관리한다. 세대는 0 세대, 1 세대, 2 세대로 구분되는데 최근에 생성된 객체는 0 세대(young)에 들어가고 오래된 객체일수록 2 세대(old)에 존재한다. 더불어 한 객체는 단 하나의 세대에만 속한다. 가비지 컬렉터는 0 세대일수록 더 자주 가비지 컬렉션을 하도록 설계되었는데 이는 [generational hypothesis](http://www.memorymanagement.org/glossary/g.html#term-generational-hypothesis)에 근거한다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">generational hypothesis의 두 가지 가설</summary></details>

주기는 threshold 와 관련있는데 `gc.get_threshold()`로 확인해 볼 수 있다.

```
>>> gc.get_threshold()
(700, 10, 10)
```

각각 `threshold 0`, `threshold 1`, `threshold 2`을 의미하는데 n 세대에 객체를 할당한 횟수가 `threshold n`을 초과하면 가비지 컬렉션이 수행되며 이 값은 변경될 수 있다.

0 세대의 경우 메모리에 객체가 할당된 횟수에서 해제된 횟수를 뺀 값, 즉 객체 수가 `threshold 0`을 초과하면 실행된다. 다만 그 이후 세대부터는 조금 다른데 0 세대 가비지 컬렉션이 일어난 후 0 세대 객체를 1 세대로 이동시킨 후 카운터를 1 증가시킨다. 이 1 세대 카운터가 `threshold 1`을 초과하면 그 때 1 세대 가비지 컬렉션이 일어난다. 러프하게 말하자면 0 세대 가비지 컬렉션이 객체 생성 700 번만에 일어난다면 1 세대는 7000 번만에, 2 세대는 7 만번만에 일어난다는 뜻이다.

이를 말로 풀어서 설명하려니 조금 복잡해졌지만 간단하게 말하면 메모리 할당시 `generation[0].count++`, 해제시 `generation[0].count--`가 발생하고, `generation[0].count > threshold[0]`이면 `genreation[0].count = 0`, `generation[1].count++`이 발생하고 `generation[1].count > 10`일 때 0 세대, 1 세대 count 를 0 으로 만들고 `generation[2].count++`을 한다는 뜻이다.

[gcmodule.c 코드로 보기](https://github.com/python/cpython/blob/master/Modules/gcmodule.c#L832-L836)

#### 라이프 사이클

이렇듯 가비지 컬렉터는 세대와 임계값을 통해 가비지 컬렉션의 주기를 관리한다. 이제 가비지 컬렉터가 어떻게 순환 참조를 발견하는지 알아보기에 앞서 가비지 컬렉션의 실행 과정(라이프 사이클)을 간단하게 알아보자.

새로운 객체가 만들어 질 때 파이썬은 객체를 메모리와 0 세대에 할당한다. 만약 0 세대의 객체 수가 `threshold 0`보다 크면 `collect_generations()`를 실행한다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">코드와 함께하는 더 자세한 설명</summary></details>

`collect_generations()`이 호출되면 모든 세대(기본적으로 3 개의 세대)를 검사하는데 가장 오래된 세대(2 세대)부터 역으로 확인한다. 해당 세대에 객체가 할당된 횟수가 각 세대에 대응되는 `threshold n`보다 크면 `collect()`를 호출해 가비지 컬렉션을 수행한다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">코드</summary></details>

`collect()` 메서드는 **순환 참조 탐지 알고리즘**을 수행하고 특정 세대에서 도달할 수 있는 객체(reachable)와 도달할 수 없는 객체(unreachable)를 구분하고 도달할 수 없는 객체 집합을 찾는다. 도달할 수 있는 객체 집합은 다음 상위 세대로 합쳐지고(0 세대에서 수행되었으면 1 세대로 이동), 도달할 수 없는 객체 집합은 콜백을 수행 한 후 메모리에서 해제된다.

이제 정말 **순환 참조 탐지 알고리즘**을 알아볼 때가 됐다.

#### 어떻게 순환 참조를 감지하는가

먼저 순환 참조는 컨테이너 객체(e.g. `tuple`, `list`, `set`, `dict`, `class`)에 의해서만 발생할 수 있음을 알아야한다. 컨테이너 객체는 다른 객체에 대한 참조를 보유할 수 있다. 그러므로 정수, 문자열은 무시한채 관심사를 컨테이너 객체에만 집중할 수 있다.

순환 참조를 해결하기 위한 아이디어로 모든 컨테이너 객체를 추적한다. 여러 방법이 있겠지만 객체 내부의 링크 필드에 더블 링크드 리스트를 사용하는 방법이 가장 좋다. 이렇게 하면 추가적인 메모리 할당 없이도 **컨테이너 객체 집합**에서 객체를 빠르게 추가하고 제거할 수 있다. 컨테이너 객체가 생성될 때 이 집합에 추가되고 제거될 때 집합에서 삭제된다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;"><span>&nbsp;</span><code style="box-sizing: border-box; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, monospace; font-size: 13.6px; padding: 0.2em 0.4em; margin: 0px; background-color: var(--color-markdown-code-bg); border-radius: 6px;">PyGC_Head</code>에 선언된 더블 링크드 리스트</summary></details>

이제 모든 컨테이터 객체에 접근할 수 있으니 순환 참조를 찾을 수 있어야 한다. 순환 참조를 찾는 과정은 다음과 같다.

1. 객체에 `gc_refs` 필드를 레퍼런스 카운트와 같게 설정한다.
2. 각 객체에서 참조하고 있는 다른 컨테이너 객체를 찾고, 참조되는 컨테이너의 `gc_refs`를 감소시킨다.
3. `gc_refs`가 0 이면 그 객체는 컨테이너 집합 내부에서 자기들끼리 참조하고 있다는 뜻이다.
4. 그 객체를 unreachable 하다고 표시한 뒤 메모리에서 해제한다.

이제 우리는 가비지 콜렉터가 어떻게 순환 참조 객체를 탐지하고 메모리에서 해제하는지 알았다.

#### 예제

> 아래 예제는 보기 쉽게 가공한 예제이며 실제 `collect()`의 동작과는 차이가 있다. 정확한 작동 방식은 아래에서 다시 서술한다. 혹은 [`collect()` 코드](https://github.com/python/cpython/blob/master/Modules/gcmodule.c#L797-L981)를 참고하자.

아래의 예제를 통해 가비지 컬렉터가 어떤 방법으로 순환 참조 객체인 `Foo(0)`과 `Foo(1)`을 해제하는지 알아보겠다.

```
a = [1]
# Set: a:[1]
b = ['a']
# Set: a:[1] <-> b:['a']
c = [a, b]
# Set: a:[1] <-> b:['a'] <-> c:[a, b]
d = c
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b]
# 컨테이너 객체가 생성되지 않았기에 레퍼런스 카운트만 늘어난다.
e = Foo(0)
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> e:Foo(0)
f = Foo(1)
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> e:Foo(0) <-> f:Foo(1)
e.x = f
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> e:Foo(0) <-> f,Foo(0).x:Foo(1)
f.x = e
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> e,Foo(1).x:Foo(0) <-> f,Foo(0).x:Foo(1)
del e
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> Foo(1).x:Foo(0) <-> f,Foo(0).x:Foo(1)
del f
# Set: a:[1] <-> b:['a'] <-> c,d:[a, b] <-> Foo(1).x:Foo(0) <-> Foo(0).x:Foo(1)
```

위 상황에서 각 컨테이너 객체의 레퍼런스 카운트는 다음과 같다.

```
# ref count
[1]     <- a,c      = 2
['a']   <- b,c      = 2
[a, b]  <- c,d      = 2
Foo(0)  <- Foo(1).x = 1
Foo(1)  <- Foo(0).x = 1
```

1 번 과정에서 각 컨테이너 객체의 `gc_refs`가 설정된다.

```
# gc_refs
[1]    = 2
['a']  = 2
[a, b] = 2
Foo(0) = 1
Foo(1) = 1
```

2 번 과정에서 컨테이너 집합을 순회하며 `gc_refs`을 감소시킨다.

```
[1]     = 1  # [a, b]에 의해 참조당하므로 1 감소
['a']   = 1  # [a, b]에 의해 참조당하므로 1 감소
[a, b]  = 2  # 참조당하지 않으므로 그대로
Foo(0)  = 0  # Foo(1)에 의해 참조당하므로 1 감소
Foo(1)  = 0  # Foo(0)에 의해 참조당하므로 1 감소
```

3 번 과정을 통해 `gc_refs`가 0 인 순환 참조 객체를 발견했다. 이제 이 객체를 unreachable 집합에 옮겨주자.

```
 unreachable |  reachable
             |    [1] = 1
 Foo(0) = 0  |  ['a'] = 1
 Foo(1) = 0  | [a, b] = 2
```

이제 `Foo(0)`와 `Foo(1)`을 메모리에서 해제하면 가비지 컬렉션 과정이 끝난다.

### 더 정확하고 자세한 설명

`collect()` 메서드는 현재 세대와 어린 세대를 합쳐 순환 참조를 검사한다. 이 합쳐진 세대를 `young`으로 이름 붙이고 다음의 과정을 거치며 최종적으로 도달 할 수 없는 객체가 모인 unreachable 리스트를 메모리에서 해제하고 young 에 남아있는 객체를 다음 세대에 할당한다.

```
update_refs(young)
subtract_refs(young)
gc_init_list(&unreachable)
move_unreachable(young, &unreachable)
```

`update_refs()`는 모든 객체의 레퍼런스 카운트 사본을 만든다. 이는 가비지 컬렉터가 실제 레퍼런스 카운트를 건드리지 않게 하기 위함이다.

`subtract_refs()`는 각 객체 i 에 대해 i 에 의해 참조되는 객체 j 의 `gc_refs`를 감소시킨다. 이 과정이 끝나면 (young 세대에 남아있는 객체의 레퍼런스 카운트) - (남아있는 `gc_refs`) 값이 old 세대에서 young 세대를 참조하는 수와 같다.

`move_unreachable()` 메서드는 young 세대를 스캔하며 `gc_refs`가 0 인 객체를 `unreachable` 리스트로 이동시키고 `GC_TENTATIVELY_UNREACHABLE`로 설정한다. 왜 완전히 `unreachable`이 아닌 임시로(Tentatively) 설정하냐면 나중에 스캔될 객체로부터 도달할 수도 있기 때문이다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">예제 보기</summary></details>

0 이 아닌 객체는 `GC_REACHABLE`로 설정하고 그 객체가 참조하고 있는 객체 또한 찾아가(traverse) `GC_REACHABLE`로 설정한다. 만약 그 객체가 `unreachable` 리스트에 있던 객체라면 `young` 리스트의 끝으로 보낸다. 굳이 `young`의 끝으로 보내는 이유는 그 객체 또한 다른 `gc_refs`가 0 인 객체를 참조하고 있을 수 있기 때문이다.

<details style="box-sizing: border-box; display: block; margin-top: 0px; margin-bottom: 16px; color: rgb(36, 41, 46); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer;">예제 보기</summary></details>

`young` 리스트의 전체 스캔이 끝나면 이제 `unreachable` 리스트에 있는 객체는 **정말 도달할 수 없다**. 이제 이 객체들을 메모리에서 해제되고 `young` 리스트의 객체들은 상위 세대로 합쳐진다.

#### Reference

- [Instagram 이 gc 를 없앤 이유](https://b.luavis.kr/python/dismissing-python-garbage-collection-at-instagram)
- [파이썬 Garbage Collection](http://weicomes.tistory.com/277)
- [Finding reference cycle](https://www.kylev.com/2009/11/03/finding-my-first-python-reference-cycle/)
- [Naver D2 - Java Garbage Collection](http://d2.naver.com/helloworld/1329)
- [gc 의 threshold](https://docs.python.org/3/library/gc.html#gc.set_threshold)
- [Garbage Collection for Python](http://www.arctrix.com/nas/python/gc/)
- [How does garbage collection in Python work](https://www.quora.com/How-does-garbage-collection-in-Python-work-What-are-the-pros-and-cons)
- [gcmodule.c](https://github.com/python/cpython/blob/master/Modules/gcmodule.c)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## Celery

[Celery](http://www.celeryproject.org/)는 메시지 패싱 방식의 분산 비동기 작업 큐다. 작업(Task)은 브로커(Broker)를 통해 메시지(Message)로 워커(Worker)에 전달되어 처리된다. 작업은 멀티프로세싱, eventlet, gevent 를 사용해 하나 혹은 그 이상의 워커에서 동시적으로 실행되며 백그라운드에서 비동기적으로 실행될 수 있다.

#### Reference

- [Spoqa - Celery 를 이용한 긴 작업 처리](https://spoqa.github.io/2012/05/29/distribute-task-with-celery.html)
- [[번역\]셀러리 입문하기](https://beomi.github.io/2017/03/19/Introduction-to-Celery/)
- [Python Celery with Redis](http://dgkim5360.tistory.com/entry/python-celery-asynchronous-system-with-redis)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## PyPy 가 CPython 보다 빠른 이유

간단히 말하면 CPython 은 일반적인 인터프리터인데 반해 PyPy 는 [실행 추적 JIT(Just In Time) 컴파일](https://en.wikipedia.org/wiki/Tracing_just-in-time_compilation)을 제공하는 인터프리터기 때문이다. PyPy 는 RPython 으로 컴파일된 인터프리터인데, C 로 작성된 RPython 툴체인으로 인터프리터 소스에 JIT 컴파일을 위한 힌트를 추가해 CPython 보다 빠른 실행 속도를 가질 수 있게 되었다.

### PyPy

PyPy 는 파이썬으로 만들어진 파이썬 인터프리터다. 일반적으로 파이썬 인터프리터를 다시 한번 파이썬으로 구현한 것이기에 속도가 매우 느릴거라 생각하지만 실제 PyPy 는 [스피드 센터](http://speed.pypy.org/)에서 볼 수 있듯 CPython 보다 빠르다.

### 실행 추적 JIT 컴파일

메소드 단위로 최적화 하는 전통적인 JIT 과 다르게 런타임에서 자주 실행되는 루프를 최적화한다.

### RPython(Restricted Python)

[RPython](https://rpython.readthedocs.io/en/latest/index.html)은 이런 실행 추적 JIT 컴파일을 C 로 구현해 툴체인을 포함한다. 그래서 RPython 으로 인터프리터를 작성하고 툴체인으로 힌트를 추가하면 인터프리터에 실행추적 JIT 컴파일러를 빌드한다. 참고로 RPython 은 PyPy 프로젝트 팀이 만든 일종의 인터프리터 제작 프레임워크(언어)다. 동적 언어인 Python 에서 표준 라이브러리와 문법에 제약을 가해 변수의 정적 컴파일이 가능하도록 RPython 을 만들었으며, 동적 언어 인터프리터를 구현하는데 사용된다.

이렇게 언어 사양(파이썬 언어 규칙, BF 언어 규칙 등)과 구현(실제 인터프리터 제작)을 분리함으로써 어떤 동적 언어에 대해서라도 자동으로 JIT(Just-in-Time) 컴파일러를 생성할 수 있게 되었다.

#### Reference

- [RPython 공식 레퍼런스](https://rpython.readthedocs.io/en/latest/)
- [PyPy - wikipedia](https://en.wikipedia.org/wiki/PyPy)
- [PyPy 가 CPython 보다 빠를 수 있는 이유 - memorable](https://memorable.link/link/188)
- [PyPy 와 함께 인터프리터 작성하기](https://www.haruair.com/blog/1882)
- [알파희 - PyPy/RPython 으로 20 배 빨라지는 아희 JIT 인터프리터](https://www.slideshare.net/YunWonJeong/pypyrpython-20-jit)
- [PyPy 가 CPython 보다 빠를 수 있는 이유 - 홍민희](https://blog.hongminhee.org/2011/05/02/5124874464/)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## 메모리 누수가 발생할 수 있는 경우

> 메모리 누수를 어떻게 정의하냐에 따라 조금 다르다. `a = 1`을 선언한 후에 프로그램에서 더 이상 `a`를 사용하지 않아도 이것을 메모리 누수라고 볼 수 있다. 다만 여기서는 사용자의 부주의로 인해 발생하는 메모리 누수만 언급한다.

대표적으로 mutable 객체를 기본 인자값으로 사용하는 경우에 메모리 누수가 일어난다.

```
def foo(a=[]):
    a.append(time.time())
    return a
```

위의 경우 `foo()`를 호출할 때마다 기본 인자값인 `a`에 타임스탬프 값이 추가된다. 이는 의도하지 않은 결과를 초래하므로 보통의 경우 `a=None`으로 두고 함수 내부에서 `if a is None` 구문으로 빈 리스트를 할당해준다.

다른 경우로 웹 애플리케이션에서 timeout 이 없는 캐시 데이터를 생각해 볼 수 있다. 요청이 들어올수록 캐시 데이터는 쌓여만 가는데 이를 해제할 루틴을 따로 만들어두지 않는다면 이도 메모리 누수를 초래한다.

클래스 내 `__del__` 메서드를 재정의하는 행위도 메모리 누수를 일으킬 수 있다. 순환 참조 중인 클래스가 `__del__` 메서드를 재정의하고 있다면 가비지 컬렉터로 해제되지 않는다.

#### Reference

- [Is it possible to have an actual memory leak?](https://stackoverflow.com/questions/2017381/is-it-possible-to-have-an-actual-memory-leak-in-python-because-of-your-code)
- [파이썬에서 메모리 누수가 발생할 수 있는 경우 - memorable](https://memorable.link/link/189)
- [약한 참조 사용하기](https://soooprmx.com/archives/5074)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## Duck Typing

Duck typing이란 특히 동적 타입을 가지는 프로그래밍 언어에서 많이 사용되는 개념으로, 객체의 실제 타입보다는 객체의 변수와 메소드가 그 객체의 적합성을 결정하는 것을 의미한다. Duck typing이라는 용어는 흔히 [duck test](https://en.wikipedia.org/wiki/Duck_test)라고 불리는 한 구절에서 유래됐다.

> If it walks like a duck and it quacks like a duck, then it must be a duck.
>
> 만일 그 새가 오리처럼 걷고, 오리처럼 꽥꽥거린다면 그 새는 오리일 것이다.

동적 타입 언어인 파이썬은 메소드 호출이나 변수 접근시 타입 검사를 하지 않으므로 duck typing을 넒은 범위에서 활용할 수 있다. 다음은 간단한 duck typing의 예시다.

```
class Duck:
    def walk(self):
        print('뒤뚱뒤뚱')

    def quack(self):
        print('Quack!')

class Mallard:  # 청둥오리
    def walk(self):
        print('뒤뚱뒤뒤뚱뒤뚱')

    def quack(self):
        print('Quaaack!')

class Dog:
    def run(self):
        print('타다다다')

    def bark(self):
        print('왈왈')


def walk_and_quack(animal):
    animal.walk()
    animal.quack()


walk_and_quack(Duck())  # prints '뒤뚱뒤뚱', prints 'Quack!'
walk_and_quack(Mallard())  # prints '뒤뚱뒤뒤뚱뒤뚱', prints 'Quaaack!'
walk_and_quack(Dog())  # AttributeError : 'Dog' object has no attribute 'walk'
```

위 예시에서 `Duck` 과 `Mallard` 는 둘 다 `walk()` 와 `quack()` 을 구현하고 있기 때문에 `walk_and_quack()` 이라는 함수의 인자로서 **적합하다**. 그러나 `Dog` 는 두 메소드 모두 구현되어 있지 않으므로 해당 함수의 인자로서 부적합하다. 즉, `Dog` 는 적절한 duck typing에 실패한 것이다.

Python에서는 다양한 곳에서 duck typing을 활용한다. `__len__()`을 구현하여 *길이가 있는 무언가* 를 표현한다던지 (흔히 [listy](https://cs.gmu.edu/~kauffman/cs310/w04-2.pdf)하다고 표현한다), 또는 `__iter__()` 와 `__getitem__()` 을 구현하여 [iterable](https://docs.python.org/3/glossary.html#term-iterable)을 duck-typing한다. 굳이 `Iterable` (가명) 이라는 interface를 상속받지 않고 `__iter__()`와 `__getitem__()`을 구현하기만 하면 `for ... in` 에서 바로 사용할 수 있다.

이와 같은 방식은 일반적으로 `interface`를 구현하거나 클래스를 상속하는 방식으로 인자나 변수의 적합성을 runtime 이전에 판단하는 정적 타입 언어들과 비교된다. 자바나 스칼라에서는 `interface`, c++는 `template` 을 활용하여 타입의 적합성을 보장한다. (c++의 경우 `template`으로 duck typing과 같은 효과를 낼 수 있다 [참고](http://www.drdobbs.com/templates-and-duck-typing/184401971))

#### Reference

- [Templates and Duck Typing](http://www.drdobbs.com/templates-and-duck-typing/184401971)
- [Strong and Weak Typing](https://en.wikipedia.org/wiki/Strong_and_weak_typing)
- [Python Duck Typing - or, what is an interface?](https://infohost.nmt.edu/tcc/help/pubs/python/web/interface.html)
- [Quora : What is duck typing in python?](https://www.quora.com/What-is-Duck-typing-in-Python)
- [Duck Test](https://en.wikipedia.org/wiki/Duck_test)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)



## Timsort : Python의 내부 sort

python의 내부 sort는 timsort 알고리즘으로 구현되어있다. 2.3 버전부터 적용되었으며, merge sort와 insert sort가 병합된 형태의 안정정렬이다.

timsort는 merge sort의 최악 시간 복잡도와 insert sort의 최고 시간 복잡도를 보장한다. 따라서 O(n) ~ O(n log n)의 시간복잡도를 보장받을 수 있고, 공간복잡도의 경우에도 최악의 경우 O(n)의 공간복잡도를 가진다. 또한 안정정렬으로 동일한 키를 가진 요소들의 순서가 섞이지 않고 보장된다.

timsort를 좀 더 자세하게 이해하고 싶다면 [python listsort](https://github.com/python/cpython/blob/24e5ad4689de9adc8e4a7d8c08fe400dcea668e6/Objects/listsort.txt) 참고.

#### Reference

- [python listsort](https://github.com/python/cpython/blob/24e5ad4689de9adc8e4a7d8c08fe400dcea668e6/Objects/listsort.txt)
- [Timsort wikipedia](https://en.wikipedia.org/wiki/Timsort)

[뒤로](https://github.com/JaeYeopHan/for_beginner)/[위로](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python#part-2-3-python)

*Python.end*





------

refs

> [VSFe_github](https://github.com/Algorithm-box/Algorithm_Study/blob/main/Concept/00_Special/Pythonic_Code_For_Coding_Test.md)
>
> [JaeYeopHan_github](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Python)
>
> []()
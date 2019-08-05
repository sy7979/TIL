# Weakness

월말평가 : 다섯 문제/ ★클래스★ 파트 공부 하세요/ problem문제들 잘 보세요

### 슬라이싱, 인덱싱

##### 1. problem1 - 개인정보 보호

[-4:] : 뒤에서 4번째부터 마지막까지 쭉

delfual는 +1씩 커지게

defualt를 바꾸려면 [-4​ :  : -1 ​] 이런식으로 가장 마지막 값을 지정해줘야한다.



##### 2. ★ problem2 - 정중앙

슬라이싱

[n:m]

n이상 번째부터 m 미만 번째 까지!

```python
# question1
num = [1, 2, 3, 4, 5, 6, 7, 8, 9]
n = num[5:5]
print(n)
```

```python
# result1
[]
```

```python
# question2
n2 = num[4:5]
```

```python
# result2
[5]
```



### 딕셔너리

1. problem2 - 모든코인 상승장? 하락장?

   딕셔너리 안에 딕셔너리가 있는 구조

   for 문과 get을 이용해서 value(dictionary)의 value 값을 가져오는데, get('key')에서 'key'가 있는게 있고 없는게 있으면 for문이 제대로 돌지 않는다.



### if

1. ##### problem2 -혈액형★딕셔너리에 대한 이해!! 다시 한 번 꼭 풀어보기

   if와 elif의 차이점은? 파이썬 튜터를 활용해서 보자!!
   
   if - if - if - if -하면 if문을 다~~ 돎.
   
   if - elif - elif - 하면 순차적으로 걸러져 와서 위에서 조건을 만족하면 아래로 내려오지 않는다.






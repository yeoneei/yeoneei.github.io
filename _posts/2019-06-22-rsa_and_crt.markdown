---
layout: RSA and CRT
title:  "[알고리즘] RSA and CRT"
date:   2019-06-22 17:58:07
categories: algorithm
tags: algorithm
image: 
---
# RSA


# CRT

### CRT란?
- CRT == The Chinese Remainder Theorem [중국인의 나머지 정리]
- 어떤 쌍마다 서로소 자연수들에 대한 연립 합동식의 해의 유일한 존재에 대한 정리

### 왜 중국인의 나머지 정리인가?
5세기 중국 수학에서 손자산경에 연립합동식이 문제가 처음 등장했기 때문에
> "  개수를 알지 못하는 것들이 있다. 셋씩 센다면 두 개가 남고, 다섯씩 센다면 세 개가 남고, 일곱씩 센다면 두 개가 남는다. 질문: 총 몇 개인가?  "

### 과정
- x ≡ 1 (mod 3)
- x ≡ 3 (mod 5)
- x ≡ 2 (mod 7)
위를 만족하는 x를 구해보자

x ≡ 1 (mod 3)
> x = 3n +1

x ≡ 3 (mod 5)
> 3n+1 ≡ 3 (mod 5)  
> 3n+1 -1 ≡ 3 -1 (mod 5)
> 3n ≡ 2 (mod 5)

덧셈, 뺄셈, 곱셈은 modular 연산에서 닫혀있기 때문에 양변에 -1을 취해도 성립한다.

3n을 n으로 만들기 위해서는 3으로 나눠야 하지만 모듈러 연산에서는 나눗셈을 할 수없다. 그래서 3의 역원을 곱해줘야 한다.

### 역원

역원을 구하기 전에 모듈러 연산에 대해 알아야 한다.

- 덧셈 : (a + b) % M = (( a % M ) + ( b % M )) % M
- 뺄셈 : (a - b) % M = (( a % M ) -( b % M ) + M ) % M
- 곱셈 : (a * b) % M = (( a % M ) * ( b % M)) % M
- 나눗셈 : (a / b) % M = (( a % M ) / ( b % M)) % M ..?

나눗셈은 이렇게 모듈러 연산을 하지 않는다! 그럼 어떻게 해야할까?
>  ( a / b) % M  = ( a * b<sup>-1</sup> ) % M  
>  = (( a % M) * (b<sup>-1</sup> % M)) % M  

여기서 b<sup>-1</sup>은 b와 역원관계에 있다.
하지만 b<sup>-1</sup>은 모듈러 영역에서 알맞은 값이 아니다.   
 b * b<sup>-1</sup> ≡ 1 (mode M)&nbsp;&nbsp;&nbsp; 0 <=b<sup>-1</sup> < M 일때  b<sup>-1</sup>의 값은 얼마인가?

 ### 페르마의 소정리
 역원은 모듈러를 취했을 때 1이 나오는 값을 찾으면 된다
 > a<sup>p-1</sup> ≡ 1 (mod p)  
 > 단, p는 소수이고 a가 p의 배수가 아닌 경우  
 > a<sup>p-1</sup> = a * a<sup>p-2</sup> ≡ 1 (mod p)
 
 결론 : a * a<sup>-1</sup> ≡ 1 (mod p)일 때 a<sup>-1</sup>은 a<sup>p-2</sup>가 된다.

> (( a % M) * (b<sup>-1</sup> % M)) % M 
> = (( a % M) * (b<sup>M-2</sup> % M)) % M  

곱셈은 모듈러 연산의 분배법칙이 가능하기 때문에 오버플로우가 나지 않도록 M으로 나눠주면서 b<sup>M-2</sup>를 계산하면 된다.


### 과정 이어서  
3n ≡ 2 (mod 5)
> n ≡ 3<sup>-1</sup> * 2 (mod 5)  
> n ≡ 3<sup>3</sup> (mod 5) * 2 (mod 5)  
> n ≡ 2 * 2  (mod 5)  
> n ≡ 4 (mod 5)  
> n = 5m +4

이 식을 아까 구한 x = 3n +1 에 대입한다
> x = 3 ( 5m + 4) +1  = 15m + 13

x ≡ 2 (mod 7)
> 15m + 13 ≡ 2 (mod 7)  
> 15m ≡ -11 (mod 7)  
> 15m ≡ 3 (mod 7)  
> m ≡ 15<sup>-1</sup> * 3 (mod 7)  
> m ≡ 1 * 3 (mod 7)  
> m ≡ 3 (mod 7)  
> m = 7k +3

이식을 x = 15m +13에 대입
> x = 15(7k + 3) + 13 = 105k + 58  
> x = 105k + 58 &nbsp;&nbsp;&nbsp;( k = 0,1,2 ...)

### 정리
x ≡ ∑<sup>n</sup><sub>i=1</sub> M<sub>i</sub>(M−1<sub>i</sub> mod m<sub>i</sub>)a<sub>i</sub> (mod M)
- M = m<sub>1</sub>m<sub>2</sub>m<sub>3</sub>...m<sub>n</sub>  
- M<sub>i</sub> = M / m<sub>i</sub>  






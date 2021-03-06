# 제 1장 빅오 표기법

- O(1)은 신성하다
- 하미드 티주쉬(Hamid Tizhoosh)

- 알고리즘을 구현하는 법을 학습하기 전에 알고리즘이 얼마나 효과적인지 분석하는 법을 이해해야 한다
- 1장에서는 실행 시간과 사용된 메모리 관점에서 알고리즘 구현을 분석하는 방법을 배워본다

## 빅오 표기법 기초

- 빅오 표기법은 알고리즘의 최악의 경우 복잡도를 측정한다
- 여기서 O(n)에서 n은 입력 갯수를 뜻한다
- "n이 무한으로 증가할 때 알고리즘의 시간 복잡도는 어떻게 되는가"

## 일반적인 예

- O(1)은 입력 공간에 대해 변하지 않는다 => 상수 시간 => 배열에 있는 항목을 인덱스를 사용해 접근
- O(n) => 선형 시간 => 최악의 경우에 n번의 연산을 수행

- O(n) => 1중 for 문
- O(n^2) => 2중 for 문
- O(n^3) => 3중 for 문
- O(logn) => 2, 4, 8, 16, 32, 64를 출력하는 알고리즘

```
O(logn) 시간 복잡도를 가진 로직

function exampleLogarithmic(n) {
    for (let i = 2; i <= n; i *= 2) {
        console.log(i);
    }
}
```

## 빅오 표기법 규칙

- 알고리즘의 시간 복잡도를 f(n)이라고 표현해보자 (n = 입력의 개수)
- 박오 표기법은 개발자들이 f(n)에 관해 계산하는데 도움이 되는 기본적인 규칙을 제공한다

1. 계수 법칙
   - f(n) = O(g(n)) => kf(n) = O(g(n))
   - 입력 크기 n과 관련되지 않은 계수를 제거
   - n이 무한에 가까워지는 경우 다른 계수는 무시헤도 괜찮다
2. 합의 법칙
   - f(n) = O(h(n)), g(n) = O(p(n)) => f(n) + g(n) => O(h(n) + p(n))
   - 시간 복잡도가 두 개의 다른 시간 복잡도의 합이라면 빅오 표기법 역시 두 개의 다른 빅오 표기법의 합이라는 것을 의미
3. 곱의 법칙
   - f(n) = O(h(n)), g(n) = O(p(n)) => f(n) _ g(n) => O(h(n) _ p(n))
   - 마찬 가지로 곱의 법칙은 두 개의 다른 시간 복잡도를 곱할 때 빅오 표기법 역시 곱해진다
4. 전이 법칙
   - f(n) = O(g(n)), g(n) = O(h(n)) 이면 => f(n) = O(h(n))
   - 교환 법칙은 동일한 시간 복잡도는 동일한 빅오 표기법을 지님을 나타내기 위한 간단한 방법이다
5. 다항 법칙
   - f(n)이 k차 다항식이면 f(n)은 O(n^k)
   - 직관적으로 다항 법칙은 다항 시간 복잡도가 동일한 다항 차수의 빅오 표기법을 지님을 나타낸다

- 첫 번째 3가지 법칙과 다항 법칙이 가장 일반적으로 사용된다
- 각 법칙에 대해서 좀더 자세히 알아보자

  ### 계수 법칙 : "상수를 제거하라"

  - 단순히 입력 크기와 연관되지 않은 상수를 전부 무시하면 된다
  - 빅오에서 입력 크기가 클 때 계수를 무시할 수 있다
  - 이는 5f(n)과 f(n)이 모두 동일한 O(f(n))이라는 빅오 표기법을 지님을 의미한다
  - 예) 1부터 n까지 반복 하는 for문을 1부터 5n까지 반복하게 해도, 빅오 표기법은 O(5n) = O(n)과 같다
  - n이 무한대에 가까워질수록 추가된 연산은 무시할 수 있게 된다

  ### 합의 법칙 : "빅오를 더하라"

  - 합의 법칙은 쉽게 이해할 수 있다 => 시간 복잡도를 더할 수 있다는 것이다
  - 합의 법칙을 적용한 다음 계수 법칙을 적용해야 한다는 점에 주의하자

  ```
    function a(n) {
        let count = 0;

        for (let i = 0; i < n; i++) {
            count += 1;
        }

        for (let i = 0; i <  5 * n; i++) {
            count += 1;
        }

        return count;
    }
  ```

  - 위의 코드는 두 개의 메인 루프를 포함한다
  - 각 루프의 시간 복잡도는 개별적으로 계싼된 다음 더해져야 한다
  - 합의 법칙을 적용하면, f(n) = n + 5n = 6n 이다
  - 계수 법칙을 적용한 최종 결과는 O(n) = n이다

  ### 곱의 법칙 : "빅오를 곱하라"

  - 간단한 중첩 루프를 살펴보자

  ```
  function a(n) {
      let count = 0;

      for (let i = 0; i < n; i++) {
          count += 1;

          for (let i = 0; i < 5 * n; i++) {
              count += 1;
          }
      }

      return count;
  }
  ```

  - 위의 예에서 f(n) = 5n \* n = 5n^2이다
  - 내부 루프에 의해 5n번 실행되고 내부 루프가 외부 루프에 의해 n번 실행되기 떄문이다
  - 따라서 결과는 5n^2번 연산이 일어난다
  - 계수 법칙을 적용해 마무리하면 O(n) = n^2이 된다

  ### 다항 법칙 : "빅오의 k승"

  - 다항 법칙은 다항 시간 복잡도가 동일한 다항 차수를 지닌 빅오 표기법을 지님을 나타낸다

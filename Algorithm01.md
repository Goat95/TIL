# Algorithm With Javascript
원래는 백준이나 프로그래머스에서 알고리즘 문제를 풀려고 했는데, 전혀 감이 안와서 차라리 알고리즘 공부를 하자 라고 생각해서 구글에 Javascript  
알고리즘을 쳐보니 [github](https://github.com/trekhleb/javascript-algorithms/blob/master/README.ko-KR.md)페이지가 나와서 정리된 글을 보고 한 문제씩  
공부를 해보기로 했다.

## 피보나치 수
수학에서 피보나치 수는 피보나치 수열이라고 하는 다음 정수 수열의 수이며   처음 두 수 이후의 모든 수는 앞의 두 수의 합이라는 사실을 특징으로 합니다.  
```
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...
```
```javascript
function fibonacci(n) {
	const fibSequence = [1];

	let currentValue = 1;
	let previousValue = 0;

	if (n === 1) {
		return fibSequence;
	}

	let iterationsCounter = n - 1;

	while (iterationsCounter) {
		currentValue += previousValue;
		previousValue = currentValue - previousValue;

		fibSequence.push(currentValue);

		iterationsCounter -= 1;
	}

	return fibSequence;
}
```

## 팩토리얼
수학에서 n!으로 표시되는 음이 아닌 정수 n의 계승은 n보다 작거나 같은 모든 양의 정수의 곱입니다. 예를 들어:
```
5! = 5 * 4 * 3 * 2 * 1 = 120
```
```javascript
function factorial(number) {
	let result = 1;

	for (let i = 2; i <= number; i++) {
		result *= i;
	}

	return result;
}
```

## 소수 판별(trial division 방식)
소수는 두 개의 작은 자연수를 곱하여 만들 수 없는 1보다 큰 자연수입니다. 소수가 아닌 1보다 큰 자연수를 합성수라고 합니다.   예를 들어, 5는 1 × 5 또는 5 × 1과 같은 곱으로 쓰는 유일한 방법이 5 자체를 포함하기 때문에 소수입니다. 그러나 6은 6보다 작은 두 수(2 × 3)의 곱이기 때문에 합성수입니다.
```javascript
function trialDivision(number) {
	// 숫자가 정수인지 확인
	if (number % 1 !== 0) {
		return false;
	}

	if (number <= 1) {
		// 숫자가 1보다 작으면 정의상 소수가 아닙니다.
		return false;
	}

	if (number <= 3) {
		// 2부터 3까지의 모든 숫자는 소수입니다.
		return true;
	}

	// 숫자를 2로 나누지 않으면 더 이상 모든 짝수 나누기를 제거할 수 있습니다.
	if (number % 2 === 0) {
		return false;
	}

	// n의 제곱근까지 분할기가 없으면 더 높은 분할기도 없습니다.
	const dividerLimit = Math.sqrt(number);
	for (let divider = 3; divider <= dividerLimit; divider += 2) {
		if (number % divider === 0) {
			return false;
		}
	}

	return true;
}
```

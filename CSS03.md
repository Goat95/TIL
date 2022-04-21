# CSS 속성

## 플렉스(정렬) Container
"display: flex": Flex Container의 화면 출력(보여짐) 특성  
- flex-direction: 주 축을 설정
	- row: 행축(좌 => 우), 기본값
	- row-reverse: 행축(우 => 좌)
	- column: 열축(위 => 아래)
	- column-reverse: 열축(아래 => 위)
- flex-wrap: Flex Items 묶음(줄 바꿈) 여부
	- nowrap: 묶음(줄 바꿈) 없음, 기본값
	- wrap: 여러 줄로 묶음
	- wrap-reverse: wrap의 반대 방향으로 묶음
- justify-content: 주 축의 정렬 방법(수평 정렬)
	- flex-start: Flex Items를 시작점으로 정렬, 기본값
	- flex-end: Flex Items를 끝점으로 정렬
	- center: Flex Items를 가운데 정렬
	- space-between: 각 Flex Item 사이를 균등하게 정렬
	- space-around: 각 Flex Item의 외부 여백을 균등하게 정렬
- align-content: 교차 축의 여러 줄 정렬 방법(수직 정렬)
	- stretch: Flex Items를 시작점으로 정렬, 기본값
	- flex-start: Flex Items를 시작점으로 정렬
	- flex-end: Flex Items를 끝점으로 정렬
	- center: Flex Items를 가운데 정렬
	- space-between: 각 Flex Item 사이를 균등하게 정렬
	- space-around: 각 Flex Item의 외부 여백을 균등하게 정렬
- align-items: 교차 축의 한 줄 정렬 방법
	- stretch: Flex Items를 교차 축으로 늘림
	- flex-start: Flex Items를 각 줄의 시작점으로 정렬
	- flex-end: Flex Items를 각 줄의 끝점으로 정렬
	- center: Flex Items를 각 줄의 가운데 정렬
	- baseline: Flex Items를 각 줄의 문자 기준선에 정렬

## 플렉스(정렬) Items
- order: Flex Item의 순서
	- 0: 순서 없음, 기본값
	- 숫자: 숫자가 작을 수록 먼저
- flex-grow: Flex Item의 증가 너비 비율
	- 0: 증가 비율 없음, 기본값
	- 숫자: 증가 비율
- flex-shrink: Flex Item의 감소 너비 비율
	- 1: Flex Container 너비에 따라 감소 비율 적용
	- 숫자: 감소 비율
- flex-basis: Flex Item의 공간 배분 전 기본 너비
	- auto: 요소의 Content 너비, 기본값
	- 단위: px, em, rem 등 단위로 지정

## 전환
transition: 요소의 전환(시작과 끝) 효과를 지정하는 단축 속성
```
transition: 속성명  지속시간   타이밍함수  대기시간;
	  property duration timing-function delay
```
- transition-property: 전환 효과를 사용할 속성 이름을 지정
	- all: 모든 속성에 적용, 기본값
	- 속성이름: 전환 효과를 사용할 속성 이름 명시
- transition-duration: 전환 효과의 지속시간을 지정
	- 0s: 전환 효과 없음
	- 시간: 지속시간(s)을 지정
- transition-timing-function: 전환 효과의 타이밍함수를 지정
	- ease: 느리게-빠르게-느리게
	- linear: 일정하게
	- ease-in: 느리게-빠르게
	- ease-out: 빠르게-느리게
	- ease-in-out: 느리게-빠르게-느리게
- transition-delay: 전환 효과가 몇 초 뒤에 시작할지 대기시간을 지정
	- 0s: 대기시간 없음
	- 시간: 대기시간(s)을 지정

## 변환
transform: 요소의 변환 효과
```
transform: 변환함수1 변환함수2 변환함수3...;
transform: 원근법 이동 크기 회전 기울임;
```
- perspective: 하위 요소를 관찰하는 원근 거리를 지정
	- 단위: px 등 단위로 지정

perspective 속성과 함수 차이점
속성/함수| 적용 대상| 기준점 설정
:-:| :-: | :-:
perspective: 600px; | 관찰 대상의 부모 | perspective-origin
transform: perspective(600px) | 관찰 대상 | transform-origin

- backface-visibility: 3D 변환으로 회전된 요소의 뒷면 숨김 여부
	- visible: 뒷면 보임
	- hidden: 뒷면 숨김

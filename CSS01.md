# CSS 개요

## CSS 기본 문법
선택자(Selector) {속성: 값;}
주석: /* 설명 작성 */

## 선언 방식
내장 방식, 링크 방식, 인라인 방식, @import 방식

- 내장 방식: <style></style>의 내용으로 스타일을 작성하는 방식
```html
<style>
	div {
		color: red;
		margin: 20px;
	}
</style>
```
- 인라인 방식: 요소의 style 속성에 직접 스타일을 작성하는 방식 
```html
<div style="color: red; margin: 20px;"></div>
```
- 링크 방식: <link/>로 외부 css 문서를 가져와서 연결하는 방식
```html
<link rel="stylesheet" href="./css/main.css">
```
```css
/* main.css파일 */
div {
	color: red;
	margin: 20px;
}
```
- @import 방식: CSS의 @import 규칙으로 CSS 문서 안에서 또 다른 CSS 문서를  
가져와 연결하는 방식
```
@import url("./main.css");
```

## CSS 선택자
- 기본 선택자:
	- 전체 선택자: * 모든 요소를 선택.
	- 태그 선택자: 태그 이름으로 요소를 선택.
	- 클래스 선택자: class 속성의 값으로 요소 선택. 기호 .
	- 아이디 선택자: id 속성의 값으로 요소 선택. 기호 #
- 복합 선택자:
	- 일치 선택자: 선택자를 동시에 만족하는 요소 선택. span.orange
	- 자식 선택자: 선택자의 자식 요소 선택. ul > .orange
	- 하위 선택자: 선택자의 하위 요소 선택. 띄어스기가 선택자의 기호!
	- 인접 형제 선택자: 선택자의 다음 형제 요소 하나를 선택. .orange + li
	- 일반 형제 선택자: 선택자의 다음 형제 요소 모두를 선택. .orange ~ li
- 가상 클래스 선택자:
	- hover: 선택자 요소에 마우스 커서가 올라가 있는 동안 선택.
	- active; 선택자 요소에 마우스를 클릭하고 있는 동안 선택. 
	- focus: 선택자 요소가 포커스되면 선택. 
	- first-child: 선택자 형제 요소 중 첫째라면 선택.
	- last-child: 선택자 형제 요소 중 막내라면 선택.
	- nth-child(n): 선택자 형제 요소 중 (n)째라면 선택.
	- not: 선택자XYZ가 아닌 ABC 요소 선택. ABC:not(XYZ)
- 가상 요소 선택자:
	- before: 선택자 요소의 내부 앞에 내용을 삽입.
	- after; 선택자 요소의 내부 뒤에 내용을 삽입.
- 속성 선택자: 속성을 포함한 요소 선택. 
	- [속성이름]{}
	- [속성이름="값"]{}

## 선택자 우선순위
우선순위란 같은 요소가 여러 선언의 대상이 된 경우, 어떤 선언의 CSS 속성을  
우선 적용할지 결정하는 방법.  
1. 점수가 높은 선언이 우선함!
2. 점수가 같으면, 가장 마지막에 해석된 선언이 우선함!
```
!important - 9999999999점
ID 선택자 - 100점
Class 선택자 - 10점
태그 선택자 - 1점
전체 선택자 - 0점
인라인 선언 - 1000점
```
---
# CSS 속성

## 너비(width, height)
width, height: 요소의 가로/세로 너비.  
- auto: 브라우저가 너비를 계산, 기본값(요소에 이미 들어있는 속성의 값)
- 단위: px, em, vw등 단위로 지정
max-width, max-height: 요소가 커질 수 있는 최대 가로/세로 너비
- none: 최대 너비 제한 없음, 기본값
- 단위: px, em, vw등 단위로 지정
min-width, min-height: 요소가 작아질 수 있는 최소 가로/세로 너비
- 0: 최소 너비 제한 없음, 기본값
- 단위: px, em, vw등 단위로 지정

## CSS 단위
- px: 픽셀
- %: 상대적 백분율
- em: 요소의 글꼴 크기
- rem: 루트 요소의 글꼴 크기
- vw: 뷰포트 가로 너비의 백분율
- vh: 뷰포트 세로 너비의 백분율

## 외부 여백(margin)
요소의 외부 여백(공간)을 지정하는 단축 속성. 음수를 사용할 수 있다.
- 0: 외부 여백 없음. 기본값
- auto: 브라우저가 여백을 계산. 가로(세로)너비가 있는 요소의 가운데 정렬에 활용!
- 단위: px, em, vw등 단위로 지정
- %: 부모 요소의 가로 너비에 대한 비율로 지정

## 내부 여백(padding)
요소의 내부 여백(공간)을 지정하는 단축 속성. 요소의 크기가 커진다.
- 0: 내부 여백 없음. 기본값
- 단위: px, em, vw등 단위로 지정
- %: 부모 요소의 가로 너비에 대한 비율로 지정

## 테두리 선(border)
요소의 테두리 선을 지정하는 단축 속성. 요소의 크기가 늘어남.    
border: 선-두께(border-width) 선-종류(border-style) 선-색상(border-color);  
border-radius: 요소의 모서리를 둥글게 깎음.

## box-sizing
요소의 크기 계산 기준을 지정  
- content-box: 요소의 내용으로 크기 계산, 기본값
- border-box: 요소의 내용 + padding + border로 크기 계산

## overflow
요소의 크기 이상으로 내용이 넘쳤을 때, 보여짐을 제어하는 단축 속성  
- visible: 넘친 내용을 그대로 보여줌, 기본값
- hidden: 넘친 내용을 잘라냄
- scroll: 넘친 내용을 잘라냄, 스크롤바 생성
- auto: 넘친 내용이 있는 경우에만 잘라내고 스크롤바 생성

## display
요소의 화면 출력 특성  
- block: 상자 요소
- inline: 글자 요소
- inline-block: 글자 + 상자 요소
- flex: 플렉스 박스(1차원 레이아웃)
- grid: 그리드(2차원 레이아웃)
- none: 보여짐 특성 없음, 화면에서 사라짐
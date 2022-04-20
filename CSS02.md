# CSS 속성

## opacity
요소 투명도  
- 1: 불투명, 기본값
- 0~1: 0부터 1사이의 소수점 숫자

## 글꼴
- font-style: 글자의 기울기.
	- normal: 기울기 없음, 기본값
	- italic: 이텔릭체
	- oblique: 기울어진 글자
- font-weight: 글자의 두께(가중치)
	- normal, 400: 기본 두께, 기본값
	- bold, 700: 두껍게
	- bolder: 상위(부모) 요소보다 더 두껍게
	- lighter: 상위(부모) 요소보다 더 얇기
	- 100~900: 100단위의 숫자 9개, normal과 bold 이외 두께
- font-size: 글자의 크기
	- 16px: 기본 크기
	- 단위: px, em, rem등 단위로 지정
- line-height: 한 줄의 높이, 행간과 유사
	- normal: 브라우저의 기본 정의를 사용
	- 숫자: 요소의 글꼴 크기의 배수로 지정
	- 단위: px, em, rem 등의 단위로 지정
- font-family: 글꼴(서체) 지정
	- serif: 바탕체 계열
	- sans-serif: 고딕체 계열
	- cursive: 필기체 계열

## 문자
- text-align: 문자의 정렬 방식
	- left: 왼쪽 정렬
	- right: 오른쪽 정렬
	- center: 가운데 정렬
- text-decoration: 문자의 장식(선)
	- none: 장식 없음, 기본값
	- underline: 밑줄
	- line-through: 중앙 선
- text-indent: 문자 첫 줄의 들여쓰기
	- 0: 들여쓰기 없음
	- 단위: px, em, rem 등 단위로 지정
	- 음수를 사용할 수 있다. 반대는 내어쓰기(outdent)입니다.

## 배경
- background-color: 요소의 배경 색상
	- transparent: 투명함, 기본값
	- 색상: 지정 가능한 색상
- background-image: 요소의 배경 이미지 삽입
	- none: 이미지 없음, 기본값
	- url("경로"): 이미지 경로
- background-repeat: 요소의 배경 이미지 반복
	- repeat: 이미지를 수직, 수평 반복. 기본값
	- repeat-x: 이미지를 수평 반복
	- repeat-y: 이미지를 수직 반복
	- no-repeat: 반복 없음
- background-position: 요소의 배경 이미지 위치
	- 0% 0%: 0%~100% 사이 값
	- 방향: top, bottom, left, right, center 방향
	- 단위: px, em, rem 등 단위로 지정
- background-size: 요소의 배경 이미지 크기
	- auto: 이미지의 실제 크기, 기본값
	- 단위: px, em, rem 등 단위로 지정
	- cover: 비율을 유지, 요소의 더 넓은 너비에 맞춤
	- contain: 비율을 유지, 요소의 더 짧은 너비에 맞춤
- background-attachment: 요소의 배경 이미지 스크롤 특성
	- scroll: 이미지가 요소를 따라서 같이 스크롤
	- fixed: 이미지가 뷰포트에 고정, 스크롤X

## 배치
- position: 요소의 위치 지정 기준
	- static: 기준 없음, 기본값
	- relative: 요소 자신을 기준
	- absolute: 위치 상 부모 요소를 기준
	- fixed: 뷰포트(브라우저)를 기준
	- sticky: 스크롤 영역 기준
- 요소 쌓임 순서(Stack order): 어떤 요소가 사용자와 더 가깝게 있는지 결정
	1. 요소에 position 속성의 값이 있는 경우 위에 쌓임.(기본값 static 제외)
	2. 1번 조건이 같은 경우, z-index 속성의 숫자 값이 높을 수록 위에 쌓임.
	3. 1번과 2번 조건까지 같은 경우, HTML의 다음 구조일 수록 위에 쌓임.
- z-index: 요소의 쌓임 정도를 지정
	- auto: 부모 요소와 동일한 쌓임 정도, 기본값
	- 숫자: 숫자가 높을 수록 위에 쌓임

# HTML

## Doctype(DTD)
문서의 HTML **버전**을 지정.  
DOCTYPE(DTD, Document Type Definition)은 마크업 언어에서 문서 형식을 정의하며,  
웹 브라우저가 어떤 HTML 버전의 해석 방식으로 페이지를 이해하면 되는지를 알려주는 용도.

## HTML, HEAD, BODY
- html 태그  - 문서의 전체 범위. HTML 문서가 어디에서 시작하고, 끝나는지 알려주는 역할.  
- head 태그 - 문서의 정보를 나타내는 범위. 웹 페이지의 제목, 설명, 스타일 같은  
웹페이지의 보이지 않는 정보를 작성하는 범위.
- body 태그 - 문서의 구조를 나타내는 범위. 웹페이지의 보여지는 구조를 작성하는 범위.

## CSS, JS 연결하기
```html
<!-- CSS 파일 연결 -->
<link rel="stylesheet" href="./main.css">

<!-- JS 파일 연결 -->
<script src="./main.js"></script>
```

## 정보를 의미하는 태그
```html
<!-- HTML 문서의 제목(title)을 정의.-->
<title>Naver</title>
<!-- HTML 문서의 제작자, 내용, 키워드 같은 여러 정보를 검색엔진이나 브라우저에 제공-->
<meta charset="UTF-8" />
<meta name="author" content="HEROPY" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 이미지 출력하기
```html
<!-- alt는 이미지가 출력되지 못하는 경우 대신 출력할 텍스트 -->
<img src="./images/logo.png" alt="heropy">
```

# git
git은 컴퓨터 파일의 변경사항을 추적하고 여러 사용자들 간에 해당 파일 작업을
조율하기 위한 대표적인 버전 관리 시스템(VCS)이다.

## git 환경설정
```bash
$ git config --global user.name "당신의유저네임"
$ git config --global user.email "당신의메일주소"
$ git config --global core.editor "vim"
$ git config --global core.pager "cat"
```

## git create repo
```bash
# 현재 프로젝트에서 변경사항 추적.
$ git init
# origin이란 별칭의 원격 저장소를 연결.
$ git remote add origin https://github.com/{username}/{reponame}.git
# README 파일 생성.
$ touch README.md
# 변경사항을 추적할 특정 파일을 지정.
$ git add README.md
# 메세지와 함께 버전을 생성.
$ git commit -m "docs: Create README.md"
# origin이란 별칭의 원격 저장소의 main branch로 버전 내역 전송.
$ git push origin main
```

## git Conventional Commits
1. commit의 제목은 commit을 설명하는 하나의 구나 절로 완성
2. Importance of Capitalize
3. prefix 달기  
        - feat: 기능 개발 관련  
        - fix: 오류 개선 혹은 버그 패치  
        - docs: 문서화 작업  
        - test: test 관련  
        - conf: 환경설정 관련  
        - build: 빌드 관련  
        - ci: Continuous Integration 관련

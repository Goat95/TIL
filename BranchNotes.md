# Branch
분기점을 생성하여 독립적으로 코드를 변경할 수 있도록 도와주는 모델.

## Branch 명령어
```bash
# 사용 가능한 local branch 표시.
$ git branch
# 사용 가능한 remote branch 표시.
$ git branch -r
# branch 생성.
$ git branch branch명
# 내가 사용할 브랜치 지정.
$ git checkout branch명
$ git switch branch명
# branch 병합하기.
$ git merge branch명
# branch 삭제하기.
$ git branch -D branch명
```

## Branching models
- git flow
	- (hotfix)-main-(release)-develop-feature
	- pros: 가장 많이. 적용, 각 단계가 명확히 구분
	- cons: 복잡하다...
- github flow
	- main-feature
	- pros: 브랜치 모델 단순화, main의 모든 커밋은
	- cons: CI 의존성 높음
- gitlab flow
	- production-preProduction-main-feature.
	- pros: deploy, issue에 대한 대응이 가능하도록 보완.
	- cons: git flow와 반대

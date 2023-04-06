 ![[git-flow_overall_graph.png|300]]
 가장 유명한 브랜치 모델 : git flow 
 https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html

# git flow Cli

```js
brew install git-flow
git init
git flow init
```

모두 엔터 치면 
폴더(develop) 으로 이동 

## 우선 원칙
일상적인 개발은 develop 브랜치에서 이루어진다는게 원칙! 


1. 새로운 feature 브랜치 생성 
```bash
git flow feature start login
```

자동으로 develop 브랜치를 베이스로 두고 feature/login 브랜치를 생성하여 checkout 까지 해주는 cli... 이제 알게 됐다. 

2. 원격에 feature push 하는 CLI 
```bash
git flow feature publish login
```

3. feature이 develop으로 병합
```bash
 git flow feature finish login
```
병합 해주고 develop 브랜치로 이동 후 feature/login 삭제 

4. [릴리즈] develop에서 release 1.0 브랜치를 만들어준다. 
```bash
git flow release start 1.0
```

5. [릴리즈 끝난 후  마스터와 develop에 병합] 
	1. 릴리즈 브랜치를 마스터에 병합
	2. 릴리즈 이름으로 태그 작성 
	3. 릴리즈 브랜치 develop으로도 병합
	4. release 브랜치 삭제
```
git flow release finish 1.0
```


6. [핫픽스] 만들고 master, develop에 병합 
```bash
git flow hotfix start login
git flow hotfix finish login
```
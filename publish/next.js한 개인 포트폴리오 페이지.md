
# 이력서도 만들어야겠다. 
참고: https://resume.hyesungoh.xyz/
만들어진 것들을 참고해서 배우면서 해야겠다. 

타임 라인 만드려고 하는데 뭘로 만들면 좋을까>?
1. react-chrono : 454kb  4496 토탈 78
2. 그냥 html , css 및 기본 JS로? 
3. react-vertical-timeline-component 31.8 kB 이슈 10 이번주 28695 다운로드 Total Files 18
-> 3번으로 가자 

# idea
1. 노드 무한 이벤트 트리거 : stopPropagation()

# 그래프
그래프 로컬에서 보기
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install obsidian-export
obsidian-export ./test_md ./common_md
[[컨트리븃 해보기]]

# animation
- [x] 페이지 전환 에니메이션 
- [x] 로딩 기능 넣어서 UI/UX 기능 구현 
- [ ] 포인터 UI 그리고 애니메이션 주자 

# layout
- [x] 반응형 기본 footer, sidebar
 - [ ] 전역 공통 컴포넌트 project's detail layout
![[스크린샷 2023-04-10 오후 7.26.35.png|500]]


![[스크린샷 2023-04-10 오후 7.26.45.png|500]]
예배 아이디어
1. 나의 진로 설계도 맵을 구현해보자
2. 스크롤 이벤트로 목표를 위해 달려가는 이밎 표현


## 디자인
- [ ] 스펙을 첫 페이지에서 보여주면 좋을 것 같다.

## 상태관리 
/projects 라우트에서보이는 스텍은 현재 constant.ts라는 파일에서 데이터를 수정하면 반영이 되는데 여기 보여지는 데이터를 /projects/[...slug.tsx] 에 각각 데이터가 보여지게 하려면 어떻게 해야할까? 

![[스크린샷 2023-04-07 오후 7.33.26.png]]


-> 상태관리? 
-> 보이려고 하는 페이지에
```Js
import { PROJECT_LIST } from "../../lib/constants";
```

project_list 상수 객체를 불러와서 해당 key 값만 변형하여 쓸수 있으면 되지 않을까? 


d3 -> https://github.com/wchorski/nextjs-obsidian-publish



# CSS
- [ ] 글자가 짤리는데 css로 해결해보자! 
- [ ] 다크모드 색 전환  -> https://www.youtube.com/watch?v=YPkUczwF3mM

# SEO
- [ ] 페이지 마다 카카오톡 오픈 그래프로 이미지 설정하기 

# error
[[에러]]

# 중요한 보물들
## 1. url rfc 인코딩 디코딩 문제 
왜 스페이스 바가 안돼?
rfc 뭐야? 
일반 

## 2. SEO 
개인 웹페이지는 www. juyoungdev.com이라는 도메인 서버 이름을 소유하고 있다. juyoungdev.com을 검색할때가 아니라 프론트엔드 개발자 이주영이라고 검색했을때 결과물이 나오도록 할 수 없나? 
![[스크린샷 2023-05-24 오전 10.11.09.png]]
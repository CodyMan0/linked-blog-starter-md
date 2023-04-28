# 자동 MD 파일 업로드 레포

## 설계도 
1. 옵시디언 내부에서 obsidian-git이라는 플러그인을 활용하여 backup 명령어를 칩니다.
2. linked-blog-starter-md 레포에 푸쉬가 되고 github-action이 실행됩니다.
3. 그에 따라 linked-blog-starter 레포에 데이터가 지정한 폴더 위치에 삽입하여 자동적으로 vercel에 베포됩니다. 

![설계도](https://user-images.githubusercontent.com/93697790/228202361-5eef4db2-48e3-47e1-976d-244384ff4bbf.png)



## 계기
이전 jekyll로 만든 웹사이트에서 옵시디언 메모장의 변경사항이 있을 경우, 일일이 찾아 복사하여 붙여 넣었어야 했던 불편함이 있었습니다. 그래서 자동적으로 변경 사항을 저장하여 웹페이지에 반영되도록 시도하였습니다. 


## github-action code 

```yml
name: Publish Markdown Files
env:
  BLOG_REPO: CodyMan0/linked-blog-starter // 실제 웹페이지 레포지토리
  PUBLISH_DIR: publish
on:
  workflow_dispatch:
  push:
    branches: [main]
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          path: temp_md
      - name: Checkout linked blog starter repo
        uses: actions/checkout@v3
        with:
          path: temp_blog
          repository: ${{ env.BLOG_REPO }} // 실제 웹페이지 러포지토리와 연결 
      - name: Install Rust / cargo
        uses: actions-rs/toolchain@v1
        with:
          toolchain: stable
      - name: Install and run obsidian-export
        run: |
          cargo install obsidian-export
          rm -rf temp_blog/common_md && mkdir temp_blog/common_md
          ~/.cargo/bin/obsidian-export ./temp_md/${{ env.PUBLISH_DIR }} temp_blog/common_md
      - name: Move blog dir to currDir
        run: |
          cp -r temp_blog/. .
          rm -rf temp_blog
          rm -rf temp_md
      - name: Deploy Vercel
        uses: amondnet/vercel-action@v20
        with:
          # TODO: Update Github Secrets with values
          vercel-token: ${{ secrets.VERCEL_TOKEN }} # Required
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }} # Required
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }} # Required
          vercel-args: "--prod" #Optional
```

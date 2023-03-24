# 자동 MD 파일 업로드 레포


## 계기
이전 jekyll로 만든 웹사이트에서 옵시디언 메모장의 변경사항이 있을 경우, 일일이 찾아 복사하여 붙여 넣었어야했던 불편함이 있었습니다. 그래서 자동적으로 변경 사항을 반영하여 저절로 웹페이지에 반영되도록 시도하였습니다. 


## 문제 해결 과정

Obsidian git을 활용하여 한시간에 한번씩 혹은 원하는 시간에 백업을 합니다. 백업을 할 경우 github action을 활용하여 실제 메모가 보일 웹페이지를 가지고 와 백업된 데이터를 복사하여 붙혀넣어주는 .yml 코드를 작성하여 해결하였습니다. 

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

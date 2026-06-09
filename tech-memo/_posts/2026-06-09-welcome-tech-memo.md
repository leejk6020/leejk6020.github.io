---
layout: post
title: 기술메모를 시작하며
description: >
  설치 방법과 환경 설정을 기록해두는 기술메모 카테고리를 시작합니다. 글을 어떻게 쓰는지 간단한 사용법도 함께 정리합니다.
image:
  path: /assets/img/sidebar-bg.jpg
categories: [tech-memo]
tags: [meta, jekyll]
---

이것저것 설치하고 설정하다 보면 매번 같은 걸 다시 찾게 됩니다.
그래서 한 번 정리해둔 내용을 두고두고 꺼내 보려고 **기술메모** 카테고리를 만들었습니다.
{:.lead}

1. this list will be replaced by the toc
{:toc}

## 어떤 글을 적나요

- 각종 소프트웨어 **설치 방법**
- 개발 환경 **설정/세팅**
- 삽질하다 해결한 **트러블슈팅** 기록

## 새 글 추가하는 법

`tech-memo/_posts/` 폴더에 `YYYY-MM-DD-제목.md` 형식으로 파일을 만들면 됩니다.
맨 위 front matter에서 `categories: [tech-memo]` 만 지켜주면 이 카테고리에 자동으로 묶입니다.

```markdown
---
layout: post
title: 글 제목
description: >
  검색/미리보기에 쓰일 한 줄 설명.
categories: [tech-memo]
tags: [예시, 태그]
---

본문 시작...
```

> 파일 이름의 날짜가 미래면 발행되지 않습니다. 작성 시점 날짜로 맞춰주세요.
{:.note}

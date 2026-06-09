---
layout: post
title: nvm으로 Node.js 설치/버전 관리
description: >
  nvm을 설치해 여러 버전의 Node.js를 자유롭게 오가며 사용하는 방법. macOS / Linux 공통.
image:
  path: /assets/img/sidebar-bg.jpg
categories: [tech-memo]
tags: [nodejs, nvm, javascript]
---

프로젝트마다 요구하는 Node 버전이 달라서 골치 아플 때, **nvm**(Node Version Manager) 하나면 끝납니다.
{:.lead}

1. this list will be replaced by the toc
{:toc}

## 1. nvm 설치

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

설치 후 셸을 다시 열거나 아래를 실행합니다.

```bash
source ~/.nvm/nvm.sh
```

## 2. Node 설치

```bash
nvm install --lts      # 최신 LTS 설치
nvm install 20         # 특정 메이저 버전
```

## 3. 버전 전환

```bash
nvm use 20             # 현재 셸에서 20 사용
nvm alias default 20   # 기본 버전 고정
nvm ls                 # 설치된 버전 목록
```

## 4. 프로젝트별 자동 전환

프로젝트 루트에 `.nvmrc` 파일을 두면 됩니다.

```bash
echo "20" > .nvmrc
nvm use        # .nvmrc 버전으로 전환
```

> Windows에서는 nvm 대신 [nvm-windows](https://github.com/coreybutler/nvm-windows)를 사용하세요.
{:.note}

---
layout: post
title: 윈도우 서버에 Gitea 설치하기
description: >
  Windows Server에 경량 Git 호스팅 서비스 Gitea(1.26.2)를 설치하고, MySQL을 데이터베이스로 연결해 초기 설정까지 진행하는 방법.
image:
  path: /assets/img/tech-memo/gitea_thumb.webp
categories: [tech-memo]
tags: [gitea, git, windows-server, mysql]
---

사내에서 가볍게 Git 저장소를 호스팅하고 싶을 때 **Gitea** 만한 게 없습니다.
단일 실행 파일이라 Windows Server에도 부담 없이 올릴 수 있습니다.
{:.lead}

1. this list will be replaced by the toc
{:toc}

## 0. 준비물

- Windows Server (2016 이상 권장)
- 관리자 권한 PowerShell / 콘솔
- **MySQL** 인스턴스 (이 글은 `127.0.0.1:3306`, DB 이름 `gitea` 기준)

## 1. 실행 파일 내려받기

[Gitea 다운로드 페이지](https://dl.gitea.com/gitea/)에서 Windows용 실행 파일을 받습니다.
이 글에서는 `gitea-1.26.2-gogit-windows-4.0-amd64.exe` 를 `D:\installFiles` 에 두고 진행합니다.

## 2. MySQL에 데이터베이스 준비

Gitea가 사용할 빈 데이터베이스를 미리 만들어 둡니다.

```sql
CREATE DATABASE gitea CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

## 3. 실행

실행 파일이 있는 폴더에서 `web` 명령으로 띄웁니다.

```powershell
cd D:\installFiles
.\gitea-1.26.2-gogit-windows-4.0-amd64.exe web
```

콘솔에 `Listen: http://0.0.0.0:3000` 과 `Prepare to run install page` 가 보이면 준비 완료입니다.

![Gitea 실행 콘솔](/assets/img/tech-memo/01-gitea-console.png){:.lead loading="lazy"}

Gitea 실행 콘솔 — 3000번 포트로 리스닝 시작.
{:.figcaption}

> 상단의 `SCRIPT_TYPE "bash" is not on the current PATH` 경고는 Windows라 bash가 없어서 나는 것으로, 동작에는 지장이 없습니다.
{:.note}

## 4. 초기 설정 (localhost:3000)

브라우저에서 `http://localhost:3000/` 에 접속하면 **초기 설정** 화면이 뜹니다.

![Gitea 초기 설정 화면](/assets/img/tech-memo/02-gitea-install-mysql.png){:.lead loading="lazy"}

데이터베이스 설정 — MySQL, 호스트 `127.0.0.1:3306`, 이름 `gitea`.
{:.figcaption}

데이터베이스 설정을 실제 환경에 맞게 입력합니다.

- **데이터베이스 유형**: `MySQL`
- **호스트**: `127.0.0.1:3306`
- **이름(DB)**: `gitea`
- **사용자명 / 비밀번호**: MySQL 계정 정보

이어서 아래 항목도 확인합니다.

- **저장소 루트 경로** / **로그 경로**: 원하는 폴더로 지정
- **서버 도메인 / 베이스 URL**: 실제 접속 주소로 지정
- 마지막에 **관리자 계정**을 꼭 생성

> 설정값은 `D:\installFiles\custom\conf\app.ini` 에 저장됩니다. 이후 수정은 이 파일에서 합니다.
{:.note}

맨 아래 **"Gitea 설치"** 버튼을 누르면 설치가 진행됩니다.

![Gitea 설치 진행 중](/assets/img/tech-memo/03-gitea-installing.png){:.lead loading="lazy"}

"설치 중입니다, 잠시만 기다려 주세요..." — 설치가 끝나면 로그인/대시보드 화면으로 넘어갑니다.
{:.figcaption}

## 5. Windows 서비스로 등록

매번 콘솔로 띄울 순 없으니 서비스로 등록해 자동 실행되게 합니다.
`Ctrl+C` 로 3번의 실행을 멈춘 뒤:

```powershell
sc.exe create gitea start= auto `
  binPath= "\"D:\installFiles\gitea-1.26.2-gogit-windows-4.0-amd64.exe\" web --config \"D:\installFiles\custom\conf\app.ini\""
sc.exe description gitea "Gitea Git Service"
sc.exe start gitea
```

서비스 상태 확인:

```powershell
Get-Service gitea
```

## 6. 동작 확인

다시 `http://localhost:3000/` 에 접속해 로그인되면 완료입니다.
새 저장소를 만들고 클론 테스트까지 해보세요.

```bash
git clone http://<서버주소>:3000/<user>/<repo>.git
```

> 운영 환경이라면 3000 포트 직접 노출 대신 **IIS/Nginx 리버스 프록시 + HTTPS** 구성을 권장합니다.
{:.note}

---
layout: post
title: Gitea 설치 삽질기 — "설치 중" 화면에서 멈췄을 때
description: >
  Windows 서버에 Gitea를 설치하다 "설치 중입니다" 화면에서 30분간 멈춘 경험. 원인 진단 명령어와, 다시 겪지 않으려면 어떻게 해야 하는지 정리했습니다.
image:
  path: /assets/img/tech-memo/gitea_thumb.webp
categories: [tech-memo]
tags: [gitea, windows-server, troubleshooting, 삽질기]
---

[윈도우 서버에 Gitea 설치하기](/tech-memo/2026-06-05-gitea-install-windows-server/) 글대로 따라가다,
초기 설정에서 **"설치 중입니다, 잠시만 기다려 주세요..."** 화면이 30분째 그대로였습니다.
정상이 아니었고, 결국 처음부터 다시 깔았습니다. 같은 길로 빠지지 않도록 과정을 남깁니다.
{:.lead}

1. this list will be replaced by the toc
{:toc}

## 증상

초기 설정 폼을 채우고 **"Gitea 설치"** 를 눌렀는데, 컵 아이콘과 함께 "설치 중입니다..." 스피너만
계속 돌고 화면이 넘어가지 않았습니다. 30분을 기다려도 그대로였습니다.

![설치 중 화면](/assets/img/tech-memo/03-gitea-installing.png){:.lead loading="lazy"}

이 화면에서 몇 분 이상 멈춰 있으면 정상이 아닙니다. 십중팔구 **뒤에서 Gitea 서버 프로세스가 죽었고, 브라우저만 응답을 기다리는 상태**입니다.
{:.note}

## 진단 — 서버가 살아있나?

가장 먼저 Gitea가 정말 떠 있는지부터 확인합니다. PowerShell에서:

```powershell
netstat -ano | findstr :3000     # 3000 포트 LISTENING 여부
tasklist | findstr gitea         # gitea 프로세스 존재 여부
sc query gitea                   # 서비스로 등록했다면 상태
```

콘솔에 찍혀 있던 PID(제 경우 `2228`)를 직접 조회해 봤더니:

```powershell
PS C:\> tasklist /FI "PID eq 2228" /V
정보: 실행 중인 작업 중 지정된 조건에 일치하는 작업이 없습니다.
```

**프로세스가 이미 죽어 있었습니다.** 즉 설치 페이지가 멈춘 게 아니라, 응답해 줄 서버 자체가 사라진 상태였던 겁니다.

## 원인 — 콘솔 창을 닫으면 Gitea도 죽는다

`gitea.exe web` 을 콘솔에서 띄운 채로 설치를 진행하고 있었는데, 그 **콘솔 창이 닫히면(또는 종료되면) Gitea 프로세스도 같이 종료**됩니다.
서버가 죽으니 브라우저의 설치 요청은 영원히 응답을 못 받고 스피너만 돕니다.

실행 파일을 다시 찾으려다 한 번 더 헤맸습니다.

```powershell
PS C:\> Get-ChildItem C:\ -Filter "*gitea*.exe" -Recurse -ErrorAction SilentlyContinue
PS C:\>     # 결과 없음
```

C 드라이브만 뒤져서 "파일이 사라졌다"고 착각했는데, 실제 실행 파일은 **`D:\installFiles`** 에 있었습니다.
검색은 설치한 드라이브를 정확히 지정해야 합니다.

```powershell
Get-ChildItem D:\ -Filter "*gitea*.exe" -Recurse -ErrorAction SilentlyContinue
```

## 해결 — 이렇게 다시 했다

1. 남은 프로세스 정리 후 실행 파일 위치(`D:\installFiles`) 확인
2. **콘솔을 닫지 않고** 띄워둔 상태에서 설치 진행 — 또는 아예 처음부터 [Windows 서비스로 등록](/tech-memo/2026-06-05-gitea-install-windows-server/#5-windows-서비스로-등록)해서 콘솔 종속을 없앰
3. DB는 **우선 SQLite3로 한 번 정상 기동을 확인**한 뒤, 안정되면 MySQL로 전환
4. 접속은 `localhost` 대신 `http://127.0.0.1:3000` 으로도 시도 (가끔 localhost 이름 해석 때문에 대기하기도 함)

## 다음엔 이렇게 (체크리스트)

- [ ] 설치 중에는 **콘솔 창을 절대 닫지 않는다** (닫으면 프로세스 종료)
- [ ] 가능하면 처음부터 **Windows 서비스로 등록**해 콘솔 종속을 제거
- [ ] 실행 파일 검색은 **설치한 드라이브 전체**를 대상으로 (`D:\` 등)
- [ ] DB는 **SQLite로 먼저 검증** 후 MySQL/MSSQL 전환
- [ ] "설치 중" 화면이 몇 분 이상이면 기다리지 말고 `netstat :3000` 부터 확인

> 핵심 교훈: "설치 화면이 멈췄다"가 아니라 **"서버가 죽었다"** 를 의심하라. 멈춘 UI 뒤의 프로세스 생존 여부부터 확인하면 진단이 훨씬 빠릅니다.
{:.note}

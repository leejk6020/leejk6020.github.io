---
layout: post
title: "BatteryBar — 블루투스 기기 배터리를 메뉴바에서"
description: >
  연결된 블루투스 키보드·마우스·트랙패드·AirPods의 배터리 상태를 macOS 메뉴바에 표시하는 앱. 한국어·English·日本語 소개와 다운로드(DMG)를 제공합니다.
image:
  path: /assets/img/utils/batterybar-icon.png
categories: [utils]
tags: [macos, swift, menubar, bluetooth]
---

연결된 블루투스 기기들의 배터리 상태를 macOS **메뉴바**에서 한눈에 보는 앱입니다.
메뉴바 아이콘은 전체 기기 중 **가장 낮은 배터리 수준**을 반영합니다.
{:.lead}

🌐 **언어 / Language / 言語** — [한국어](#한국어) · [English](#english) · [日本語](#日本語)

## 다운로드 / Download

<a href="/assets/downloads/BatteryBar.dmg" class="btn" download>⬇️ BatteryBar.dmg (v1.0, ~420KB)</a>

- **Version**: 1.0  ·  **Requires**: macOS 13+  ·  **Format**: DMG
- DMG를 열면 3개국어 안내 파일(`먼저 읽어주세요 — READ ME.txt`)이 함께 들어 있습니다. / A trilingual guide (`READ ME.txt`) is included inside the DMG. / DMG 内に3か国語の案内ファイルが同梱されています。

---

## 한국어

연결된 블루투스 키보드·마우스·트랙패드·AirPods(좌/우/케이스) 등의 배터리를 macOS 메뉴바에 표시합니다.

### 주요 기능

- 🔋 메뉴바에 **최저 배터리 %** + 아이콘 표시, 클릭하면 기기별 목록이 펼쳐집니다.
- 🔄 **새로고침** 버튼으로 즉시 갱신 (자동으로 2분마다 갱신)
- 🚀 **로그인 시 자동 실행** 토글
- 🔔 **저배터리 알림** — 임계값(10/15/20/30/40%) 이하로 떨어지면 알림. 회복(임계값+5%) 후 다시 떨어지면 재알림.
- 🌐 **언어 전환** — English(기본) / 한국어 / 日本語 실시간 전환 (시스템 언어와 무관)

### 설치 방법

1. 위에서 **BatteryBar.dmg** 를 다운로드합니다.
2. DMG를 열고 **BatteryBar** 를 **응용 프로그램(Applications)** 폴더로 드래그합니다.
3. 처음 실행 시 **"확인되지 않은 개발자"** 경고가 나오면 → **시스템 설정 › 개인정보 보호 및 보안** 맨 아래의 **[확인 없이 열기]** 를 누르세요.
4. 실행하면 메뉴바 우측에 배터리 아이콘 + 최저 배터리 %가 나타납니다.

> 로그인 항목과 알림은 앱을 `/Applications` 로 옮긴 뒤 실행하는 것을 권장합니다.
{:.note}

**"확인되지 않은 개발자" 경고 해제** — 이 앱은 ad-hoc 서명만 되어 있고 Apple 공증이 없습니다. 아래 두 방법 중 하나로 해제하세요. (둘 다 macOS 26.5.2에서 검증 완료)

- **방법 A (클릭만, 권장)**: **시스템 설정 › 개인정보 보호 및 보안** 맨 아래 **[확인 없이 열기]** 버튼을 누릅니다.
- **방법 B (터미널)**: `xattr -dr com.apple.quarantine "/Applications/BatteryBar.app"`

---

## English

Shows the battery level of connected Bluetooth devices — keyboard, mouse, trackpad, AirPods (left/right/case) — right in the macOS menu bar. The menu-bar icon reflects the **lowest** battery among all devices.

### Features

- 🔋 Menu-bar icon shows the **lowest battery %**; click to expand the per-device list.
- 🔄 **Refresh** button for instant updates (auto-refreshes every 2 minutes).
- 🚀 **Launch at login** toggle.
- 🔔 **Low-battery alerts** — notifies when a device drops below the threshold (10/15/20/30/40%). Re-arms after recovery (threshold + 5%).
- 🌐 **Language switch** — English (default) / 한국어 / 日本語, switchable live (independent of system language).

### Installation

1. Download **BatteryBar.dmg** above.
2. Open the DMG and drag **BatteryBar** into your **Applications** folder.
3. On first launch, if you see an **"unidentified developer"** warning → go to **System Settings › Privacy & Security** and click **[Open Anyway]** at the bottom.
4. The battery icon and lowest battery % appear on the right side of the menu bar.

> Moving the app to `/Applications` before first launch is recommended so login-item and notification paths stay stable.
{:.note}

**Bypassing the "unidentified developer" warning** — the app is ad-hoc signed and not notarized by Apple. Use one of the two methods below (both verified on macOS 26.5.2):

- **Method A (clicks only, recommended)**: In **System Settings › Privacy & Security**, click **[Open Anyway]** at the bottom.
- **Method B (Terminal)**: `xattr -dr com.apple.quarantine "/Applications/BatteryBar.app"`

---

## 日本語

接続中の Bluetooth デバイス（キーボード・マウス・トラックパッド・AirPods（左/右/ケース）など）のバッテリー残量を macOS のメニューバーに表示します。メニューバーのアイコンは全デバイスのうち **最も低いバッテリー残量** を反映します。

### 主な機能

- 🔋 メニューバーに **最低バッテリー %** とアイコンを表示。クリックでデバイス一覧が開きます。
- 🔄 **更新** ボタンで即時更新（2分ごとに自動更新）。
- 🚀 **ログイン時に自動起動** トグル。
- 🔔 **低バッテリー通知** — しきい値（10/15/20/30/40%）を下回ると通知。回復（しきい値+5%）後に再度下がると再通知。
- 🌐 **言語切替** — English（既定）/ 한국어 / 日本語 をリアルタイムで切替（システム言語とは無関係）。

### インストール方法

1. 上の **BatteryBar.dmg** をダウンロードします。
2. DMG を開き、**BatteryBar** を **アプリケーション（Applications）** フォルダへドラッグします。
3. 初回起動時に **「未確認の開発元」** の警告が出たら → **システム設定 › プライバシーとセキュリティ** の一番下にある **[このまま開く]** をクリックします。
4. 起動するとメニューバー右側にバッテリーアイコンと最低バッテリー % が表示されます。

> ログイン項目と通知は、アプリを `/Applications` に移してから起動することを推奨します。
{:.note}

**「未確認の開発元」警告の解除** — このアプリは ad-hoc 署名のみで、Apple の公証（notarization）はありません。以下の2つの方法のいずれかで解除してください。（どちらも macOS 26.5.2 で検証済み）

- **方法A（クリックのみ、推奨）**: **システム設定 › プライバシーとセキュリティ** の一番下の **[このまま開く]** ボタンをクリック。
- **方法B（ターミナル）**: `xattr -dr com.apple.quarantine "/Applications/BatteryBar.app"`

---

## 동작 방식 / How it works / 仕組み

배터리 데이터는 macOS 내장 명령을 파싱해서 얻습니다. 별도 권한이나 백그라운드 데몬이 필요 없습니다. /
Battery data comes from a built-in macOS command — no special permissions or background daemon required. /
バッテリー情報は macOS 標準コマンドの解析で取得します。特別な権限やバックグラウンドデーモンは不要です。

```sh
system_profiler SPBluetoothDataType -json
```

**기술 스택 / Tech stack**: Swift + SwiftUI (`MenuBarExtra`, `LSUIElement=true`) · ServiceManagement (`SMAppService`, launch at login) · UserNotifications (`UNUserNotificationCenter`, 5% hysteresis).

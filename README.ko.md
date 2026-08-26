[English](README.md) · [繁體中文](README.zh-TW.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

# Open Agent Usage

Open Agent Usage는 AI 코딩 에이전트의 사용량 할당량을 메뉴 막대에 표시하는 macOS 상주 앱입니다. **Claude Code**, **Codex**, **Gemini**, **Antigravity** 네 가지 서비스의 사용량을 읽어옵니다.

모든 데이터는 Mac에 이미 존재하는 파일에서만 읽어오며, **어디에도 업로드하지 않습니다**. 이 앱이 외부와 연결하는 유일한 경우는 Gumroad와의 통신이며, 그마저도 Pro 라이선스 키를 활성화할 때만 발생합니다.

메뉴 막대에는 각 한도의 사용률과 초기화 시점이 표시되며, 색상으로 상태를 한눈에 알 수 있습니다: 30% 이하는 초록색, 60% 이하는 파란색, 80% 이하는 주황색, 80% 초과는 빨간색입니다. 메뉴 막대 아이콘을 클릭하면 패널이 열리고, 서비스별 계정, 요금제, 시간대별 사용량을 확인할 수 있습니다.

이 저장소에는 **소스 코드가 포함되어 있지 않습니다**. Open Agent Usage는 컴파일된 바이너리로 배포되는 상용 소프트웨어입니다. 자세한 내용은 〈[라이선스](#라이선스)〉를 참고하십시오.

## 기능

| | 무료 | Pro |
|---|:---:|:---:|
| 4개 에이전트 전체의 메뉴 막대 사용량 표시 | 지원 | 지원 |
| 라이트/다크 모드, 11가지 강조 색상 | 지원 | 지원 |
| 4개 언어 지원 (영어, 번체 중국어, 일본어, 한국어) | 지원 | 지원 |
| 계정, 요금제, 시간대별 사용량 패널 | 지원 | 지원 |
| 세션 목록 (각 Claude Code 세션이 무엇을 하고 있는지 확인하고 클릭 한 번으로 해당 창으로 이동) | 미지원 | 지원 |
| AI 에이전트가 호출할 수 있는 `open-agent-usage` 명령줄 인터페이스 | 미지원 | 지원 |
| 가격 | 무료 | US$4.99 (일회성 결제) |

새로 설치하면 계정 등록 없이 **모든 Pro 기능을 30일간 무료로 체험**할 수 있습니다. 체험 기간이 끝나도 Pro 라이선스를 구매하지 않는 한 무료 기능은 계속 사용할 수 있습니다.

## 설치 방법

1. [Releases](../../releases/latest)에서 최신 `.dmg`(또는 `.zip`)를 다운로드합니다.
2. 디스크 이미지를 열고 **Open Agent Usage**를 **Applications** 폴더로 드래그합니다.
3. 이 빌드는 아직 **Apple 공증(notarization)을 받지 않았기 때문에**, 처음 실행할 때 macOS Gatekeeper가 이를 차단합니다. 여는 방법은 아래를 참고하십시오.

이 버전은 프리뷰 빌드입니다. 공증된 빌드는 추후 릴리스로 제공될 예정이며, 그전까지는 아래 방법 중 하나로 열어야 합니다.

### 공증되지 않은 앱 열기 (권장 방법)

Finder의 Applications 폴더에서 앱을 **control 키를 누른 채 클릭**하고 **"열기"**를 선택한 다음, 나타나는 대화 상자에서 **"열기"**를 한 번 더 클릭합니다. 이 작업은 처음 한 번만 필요하며, 이후에는 평소처럼 열립니다.

### 대안: 터미널 사용

```bash
xattr -dr com.apple.quarantine /Applications/OpenAgentUsage.app
```

## 추가 설정

### Claude Code 사용량 확인에는 브리지 스크립트가 필요합니다

Claude Code는 사용량 데이터를 상태 표시줄의 표준 입력(stdin)에만 전달할 뿐, 파일로 저장하지 않습니다. Open Agent Usage가 이 데이터를 읽으려면 작은 브리지 스크립트를 설치해야 합니다.

```bash
/Applications/OpenAgentUsage.app/Contents/Resources/scripts/install-claude-bridge.sh
```

이 스크립트는 변경 전에 `~/.claude/settings.json`을 자동으로 백업합니다. 기존 상태 표시줄은 그대로 작동하며 겉모습도 바뀌지 않습니다.

- 설치 상태 확인: `--status` 옵션 사용
- 브리지 제거 및 원래 설정 복원: `--uninstall` 옵션 사용

### Gemini 사용량 확인에는 손쉬운 사용 권한이 필요합니다

**시스템 설정 → 개인정보 보호 및 보안 → 손쉬운 사용**을 열고 **Open Agent Usage**를 활성화합니다.

Gemini 앱이 실행 중이지 않으면 패널의 Gemini 항목은 자동으로 숨겨집니다.

## Pro 구매

Pro 라이선스는 여기에서 구매할 수 있습니다: **https://playmaker12.gumroad.com/l/openagentusage**

구매 후 Gumroad에서 라이선스 키를 이메일로 보내드립니다. 앱의 **설정 → Purchase**에서 키를 붙여넣고 활성화하십시오. 활성화 시 확인을 위해 인터넷 연결이 한 번 필요하며, 이후 Pro 기능은 오프라인에서도 정상적으로 작동합니다.

## 시스템 요구 사항

- macOS 15 이상
- Apple silicon 및 Intel 모두 지원 (universal binary)

## 문제 신고

- 이메일: aione314159@gmail.com
- 또는 이 저장소의 GitHub Issues에 등록

## 라이선스

Open Agent Usage는 상용 소프트웨어이며, 이 저장소에는 소스 코드가 포함되어 있지 않습니다.

Copyright (c) 2026 aione. All rights reserved.

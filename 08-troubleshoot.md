---
title: 문제 해결하기
layout: default
permalink: troubleshoot.html
---

## 문제 해결하기

---

### Cask 명령어에서 에러가 발생할 때

Cask 실행 중에 에러가 발생한다면 몇 가지 대처법이 있습니다.

먼저 Cask가 최신 버전인지 확인합니다.(`cask --version` 명령어로 현재 버전을 확인할 수 있습니다)Cask를 업그레이드하고 `cask upgrade-cask` 명령어로 의존 라이브러리를 업그레이드합니다.(`git pull` 명령어로 직접 디렉토리를 변경하는 방법은 추천하지 않습니다)

에러가 계속 발생한다면 Cask의 의존 라이브러리를 삭제합니다. 의존 라이브러리는 `~/.emacs.d/.cask/EMACS-VERSION/bootstrap`에 있습니다. 디렉토리를 삭제하고 명령어를 다시 실행해봅니다.

여전히 작동하지 않는다면 공식 저장소에 [이슈를 생성(Create an issue)](github.com/cask/cask/issues/new)하고 도움을 요청합니다. `--verbose`나 `--debug` 옵션을 사용해 나오는 출력 결과를 함께 알려주세요.

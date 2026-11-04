# 인튜브 업데이트 검증 앱

준비일: 2026-11-04

배포 주소: https://jongmissss.github.io/adhoc/intube/

| 앱 | Android | iOS |
| --- | --- | --- |
| KLMS | 1.1.8 (118), Google 내부 공유 서명 APK | 1.1.0 (114), Development 서명 Release IPA |
| tubeLearn | 1.1.13 (101121), Google 내부 공유 서명 APK | 1.0.5 (6), Development 서명 Release IPA |

Android 신규 단말은 페이지의 Google 공유 낮은 버전 설치 → 높은 버전 링크 열기(설치하지 않음) → 앱 새 실행 순서를 따른다. APK 단독 설치만으로 팝업이 표시된다고 보장하지 않는다. 내부 공유 링크는 2026-10-31 업로드 기준 2026-12-30 만료 예정이며 링크당 100명 제한이 있다. 2026-11-04 브라우저에서 네 링크 모두 해당 앱의 공유 안내로 열리는 것을 확인했다. 현재 상용 버전·잔여 다운로드 수를 확인했다고 해석하지 않는다.

iOS는 정식 Ad Hoc/Enterprise가 아닌 기존 Apple Development 프로파일로 서명했다. 등록된 기기만 설치할 수 있으며 iOS 26.0 이상과 개발자 모드가 필요하다. 등록 기기는 KLMS 62대, tubeLearn 5대다. UDID 목록·인증서·개인키·프로파일 원문은 별도 게시하지 않는다. IPA에는 정상 설치에 필요한 서명 및 embedded provisioning profile이 포함된다.

`klms-ios.plist`와 `tubelearn-ios.plist`는 Xcode가 생성한 설치 manifest를 배포 경로에 맞춰 게시한 파일이다. HTTPS IPA·아이콘 URL과 번들/버전 일치를 검증했다. 이번 URL을 통한 실제 iPhone OTA 설치는 미검증이며, 실패 시 Mac Xcode/Apple Configurator로 등록된 기기에 설치할 수 있다. 실제 기기 설치나 앱 데이터를 변경하는 검증은 이번 작업에서 수행하지 않았다.

각 바이너리의 버전·크기·SHA-256·프로파일 만료는 `artifacts.json`과 `SHA256SUMS.txt`에서 확인한다. 배포 검증은 공개 페이지와 모든 바이너리·manifest의 HTTPS 응답 및 재다운로드 해시 일치로 확인한다. 모바일 스토어에 제출하거나 상용 버전을 출시하는 작업은 포함하지 않는다.

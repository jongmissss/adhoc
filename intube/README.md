# 인튜브 업데이트 검증 앱

준비일: 2026-11-04

배포 주소: https://jongmissss.github.io/adhoc/intube/

| 앱 | Android | iOS |
| --- | --- | --- |
| KLMS | 1.1.8 (118), Google 내부 공유 서명 APK | 1.1.0 (116), Apple Distribution Ad Hoc 서명 IPA |
| tubeLearn | 1.1.13 (101121), Google 내부 공유 서명 APK | 1.0.5 (7), Development 서명 Release IPA |

Android 신규 단말은 페이지의 Google 공유 낮은 버전 설치 → 높은 버전 링크 열기(설치하지 않음) → 앱 새 실행 순서를 따른다. APK 단독 설치만으로 팝업이 표시된다고 보장하지 않는다. 내부 공유 링크는 2026-10-31 업로드 기준 2026-12-30 만료 예정이며 링크당 100명 제한이 있다. 2026-11-04 브라우저에서 네 링크 모두 해당 앱의 공유 안내로 열리는 것을 확인했다. 현재 상용 버전·잔여 다운로드 수를 확인했다고 해석하지 않는다.

iOS는 정식 Ad Hoc/Enterprise가 아닌 기존 Apple Development 프로파일로 서명했다. 등록된 기기만 설치할 수 있으며 iOS 26.0 이상과 개발자 모드가 필요하다. 등록 기기는 KLMS 63대, tubeLearn 6대다. UDID 목록·인증서·개인키·프로파일 원문은 별도 게시하지 않는다. IPA에는 정상 설치에 필요한 서명 및 embedded provisioning profile이 포함된다.

`klms-ios.plist`와 `tubelearn-ios.plist`는 Xcode가 생성한 설치 manifest를 배포 경로에 맞춰 게시한 파일이다. HTTPS IPA·아이콘 URL과 번들/버전 일치를 검증했다. 이번 URL을 통한 실제 iPhone OTA 설치는 미검증이며, 실패 시 Mac Xcode/Apple Configurator로 등록된 기기에 설치할 수 있다. 실제 기기 설치나 앱 데이터를 변경하는 검증은 이번 작업에서 수행하지 않았다.

각 바이너리의 버전·크기·SHA-256·프로파일 만료는 `artifacts.json`과 `SHA256SUMS.txt`에서 확인한다. 배포 검증은 공개 페이지와 모든 바이너리·manifest의 HTTPS 응답 및 재다운로드 해시 일치로 확인한다. 모바일 스토어에 제출하거나 상용 버전을 출시하는 작업은 포함하지 않는다.

2026-11-04 iOS 재생성: 지정 테스트 기기를 포함한 갱신 프로파일로 두 IPA를 다시 서명했다. KLMS 앱·알림 확장 2개 및 tubeLearn 앱의 기기 포함을 확인했고, 기존 서명 인증서를 유지했다. 이전 다운로드 캐시를 피하기 위해 IPA 파일명에 빌드 번호를 포함했다. 실제 요청 기기에서의 설치 시험은 수행하지 않았다.

2026-11-18 KLMS iOS 교체: 선택 업데이트 팝업 QA용 1.1.0 (116) Ad Hoc(release-testing) IPA로 교체했다(같은 날 게시한 1.1.4 빌드들을 대체). 11-04 QA 빌드(1.1.0 (115))와 같이 MARKETING_VERSION=1.1.0으로 덮어써 스토어 1.1.1보다 낮게 만들었다. 서명은 Apple Distribution, 프로파일은 iOS Team Ad Hoc(등록 기기 64대, 만료 2027-08-19)이며 앱과 알림 확장 2개 모두 1.1.0 (116)이고 지정 신규 기기 포함을 확인했다. 기존 `klms-ios.plist` URL을 유지하고 IPA 파일명을 `klms-ios-1.1.0-116.ipa`로, manifest bundle-version을 1.1.0으로 바꿨다. 실제 기기 OTA 설치와 팝업 표시는 미검증이다. 위 iOS 서명 설명 중 KLMS 부분은 이 항목이 대체한다.

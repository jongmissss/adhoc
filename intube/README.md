# 인튜브 업데이트 검증 앱

준비일: 2026-11-04

배포 주소: https://jongmissss.github.io/adhoc/intube/

| 앱 | Android | iOS |
| --- | --- | --- |
| KLMS | 1.1.12 (10112), 생체 로그인 수정 APK | 1.1.0 (119), Apple Distribution Ad Hoc 서명 IPA |
| tubeLearn | 1.1.13 (101121), Google 내부 공유 서명 APK | 1.0.5 (7), Development 서명 Release IPA |

Android 신규 단말은 페이지의 Google 공유 낮은 버전 설치 → 높은 버전 링크 열기(설치하지 않음) → 앱 새 실행 순서를 따른다. APK 단독 설치만으로 팝업이 표시된다고 보장하지 않는다. 내부 공유 링크는 2026-10-31 업로드 기준 2026-12-30 만료 예정이며 링크당 100명 제한이 있다. 2026-11-04 브라우저에서 네 링크 모두 해당 앱의 공유 안내로 열리는 것을 확인했다. 현재 상용 버전·잔여 다운로드 수를 확인했다고 해석하지 않는다.

iOS는 정식 Ad Hoc/Enterprise가 아닌 기존 Apple Development 프로파일로 서명했다. 등록된 기기만 설치할 수 있으며 iOS 26.0 이상과 개발자 모드가 필요하다. 등록 기기는 KLMS 63대, tubeLearn 6대다. UDID 목록·인증서·개인키·프로파일 원문은 별도 게시하지 않는다. IPA에는 정상 설치에 필요한 서명 및 embedded provisioning profile이 포함된다.

`klms-ios.plist`와 `tubelearn-ios.plist`는 Xcode가 생성한 설치 manifest를 배포 경로에 맞춰 게시한 파일이다. HTTPS IPA·아이콘 URL과 번들/버전 일치를 검증했다. 이번 URL을 통한 실제 iPhone OTA 설치는 미검증이며, 실패 시 Mac Xcode/Apple Configurator로 등록된 기기에 설치할 수 있다. 실제 기기 설치나 앱 데이터를 변경하는 검증은 이번 작업에서 수행하지 않았다.

각 바이너리의 버전·크기·SHA-256·프로파일 만료는 `artifacts.json`과 `SHA256SUMS.txt`에서 확인한다. 배포 검증은 공개 페이지와 모든 바이너리·manifest의 HTTPS 응답 및 재다운로드 해시 일치로 확인한다. 모바일 스토어에 제출하거나 상용 버전을 출시하는 작업은 포함하지 않는다.

2026-11-04 iOS 재생성: 지정 테스트 기기를 포함한 갱신 프로파일로 두 IPA를 다시 서명했다. KLMS 앱·알림 확장 2개 및 tubeLearn 앱의 기기 포함을 확인했고, 기존 서명 인증서를 유지했다. 이전 다운로드 캐시를 피하기 위해 IPA 파일명에 빌드 번호를 포함했다. 실제 요청 기기에서의 설치 시험은 수행하지 않았다.

2026-11-19 KLMS iOS 교체: 로그인 화면 상용 동일화 1.1.0 (119) Ad Hoc(release-testing) IPA로 교체했다(같은 날 게시한 바이오 인증 무한 대기 수정 1.1.0 (118)을 대체). 누적 변경 내용은 상단 safe area 겹침 수정(kaist_ios eeeccf4), 바이오 인증 후 빈 화면 무한 대기 수정(kaist_ios 84f3668: 간편 로그인 빈 응답/20초 무응답 시 안내 후 일반 로그인 이동, 네트워크 오류 화면, 로딩 표시, 취소/실패 안내), 로그인 화면을 상용 버전과 같은 배치로 복원(kaist_ios b6de4da)이다. 업데이트 팝업 테스트 조건은 유지된다: MARKETING_VERSION=1.1.0으로 덮어써 스토어 1.1.1보다 낮다. 서명은 Apple Distribution, 프로파일은 기존 iOS Team Ad Hoc 재사용(등록 기기 64대, 만료 2027-08-19)이며 앱과 알림 확장 2개 모두 1.1.0 (119)이고 지정 신규 기기 포함과 codesign --verify --deep --strict 통과를 확인했다. 빌드 측에서 실기기(iPhone 12 Pro, iOS 26.6.2) 직접 설치로 로그인 화면을 확인했다. 기존 `klms-ios.plist` URL과 bundle-version 1.1.0을 유지하고 IPA 파일명을 `klms-ios-1.1.0-119.ipa`로 바꿨다. 이 페이지를 통한 OTA 설치는 미검증이다. 위 iOS 서명 설명 중 KLMS 부분은 이 항목이 대체한다.

2026-11-19 KLMS Android 재업로드: 바이오 인증 및 웹 로그인 응답 제한, 작은 화면 여백·상태바 수정이 포함된 1.1.12 (10112) APK를 Google 내부 앱 공유에서 재서명해 게시했다(`klms-android-1.1.12-9f6ca334.apk`). 인증서 SHA-256은 기존 1.1.8과 같은 97ce3481590eb86700cba9263e5b54adabe4ef630dc15a0cdf89ea0627adf2a4다. 내부 앱 공유 링크로 연결된 기기에 업데이트해 앱 데이터 유지, 단일 base APK, 버전·서명·DEX 일치를 확인했다. 게시 APK의 실제 기기 설치와 페이지 다운로드 검증은 별도로 기록한다.

# Windows에서 moru를 iPhone에 설치하기

이 경로는 GitHub의 Mac 빌드 머신에서 만든 **네이티브 iPhone 앱**을 Windows의 AltStore Classic으로 개인 서명해 설치합니다. Mac 소유나 유료 Apple 개발자 가입은 필요하지 않습니다. 본인의 Apple Account와 iPhone은 필요하며, 실제 설치는 기기에서 확인해야 완료됩니다.

## 1. Mac 클라우드에서 IPA 만들기

공개 소스 업로드가 승인된 저장소에서 **Actions → iPhone native app - UNSIGNED → Run workflow**를 실행합니다. 자동 실행·앱스토어 업로드는 없습니다. 비공개 저장소에서는 이 작업이 실행되지 않도록 설정했습니다.

작업이 성공하면 `moru-ios-UNSIGNED-실행번호` 아티팩트를 내려받아 압축을 풉니다. 안의 `moru-ios-unsigned.ipa`가 설치에 사용할 파일입니다. GitHub에서 받은 바깥 ZIP을 IPA로 이름만 바꾸면 안 됩니다. 아티팩트 보관 기간은 1일입니다.

함께 받은 `BUILD-REPORT.md`, `bundle-metadata.json`, `SHA256SUMS.txt`에서 빌드 결과와 파일 해시를 확인할 수 있습니다. 실패한 작업의 진단 아티팩트에는 IPA가 없을 수 있습니다. 이 경우 실패한 단계를 먼저 해결해야 합니다.

빌드는 Flutter 3.44.8과 Xcode 26.2를 사용하고, 공식 모델을 정해진 SHA-256으로 검증합니다. 서명 인증서·프로비저닝·Apple 비밀번호를 GitHub에 올리지 않습니다. `UNSIGNED` 파일은 개인 서명을 거친 뒤 iPhone에서 실행할 수 있습니다.

## 2. Windows와 iPhone 준비

1. [AltStore 공식 Windows 설치 안내](https://faq.altstore.io/altstore-classic/how-to-install-altstore-windows)의 링크로 iTunes·iCloud와 AltServer를 설치합니다. 해당 안내는 Apple에서 직접 받는 버전을 사용하며, Microsoft Store iCloud를 유지해야 한다면 안내의 대체 절차를 따릅니다.
2. 공식 안내대로 AltServer를 관리자 권한으로 실행하고 iPhone을 USB로 연결합니다. iPhone 잠금을 풀고 컴퓨터 신뢰 요청을 승인합니다.
3. 공식 안내대로 iTunes 로그인과 Wi-Fi 동기화를 설정합니다.
4. Windows 알림 영역의 AltServer에서 **Install AltStore → 내 iPhone**을 선택합니다. 본인 Apple Account 인증과 필요한 확인 코드는 본인이 AltServer·Apple의 화면에서 직접 입력합니다.
5. iPhone의 **설정 → 일반 → VPN 및 기기 관리**에서 본인 개발자 계정을 신뢰합니다. 메뉴 이름은 iOS 버전에 따라 조금 다를 수 있습니다.
6. iOS 16 이상에서는 **설정 → 개인정보 보호 및 보안 → 개발자 모드**를 켜고 재시작·확인을 마칩니다. moru 자체의 최소 지원 버전은 iOS 15입니다.

## 3. moru 설치

Windows에서 **Shift 키를 누른 채 AltServer 아이콘을 클릭**하고 **Sideload .ipa…**를 선택합니다. 내려받은 `moru-ios-unsigned.ipa`와 본인 iPhone을 선택하고, 요청되는 개인 서명을 본인 계정으로 진행합니다. 이 메뉴는 [AltServer 공식 릴리스 안내](https://faq.altstore.io/release-notes/altserver)에 설명되어 있습니다.

설치가 끝나면 iPhone에서 moru를 열고 사진 선택·샘플 불러오기·얼굴 보정·사진 저장을 확인합니다. 카메라와 사진 보관함 권한은 실제로 사용할 때 허용하면 됩니다. 이 앱은 release/AOT 빌드이므로 별도의 JIT 활성화 절차가 필요하지 않습니다.

## 4. 7일마다 서명 갱신

무료 계정으로 설치한 앱은 7일 후 만료됩니다. 위의 **Sideload .ipa…** 방식으로 직접 설치한 moru는 만료 전에 같은 IPA를 다시 설치해 갱신합니다. AltStore 자체가 관리하는 앱은 **My Apps → Refresh All**로 갱신할 수 있습니다. 갱신할 때 AltServer가 실행 중이어야 하고 iPhone은 USB 또는 같은 Wi-Fi로 연결되어 있어야 합니다. [AltStore 갱신 안내](https://faq.altstore.io/altstore-classic/your-altstore), [AltServer 연결 안내](https://faq.altstore.io/altstore-classic/altserver)

Apple 무료 계정에는 동시 설치 앱 수와 App ID 수 제한도 있습니다. 유료 가입이나 제한 우회 없이 사용 가능한 범위에서 설치합니다. [Apple Personal Team 제한](https://developer.apple.com/help/account/basics/about-your-developer-account/)

설치 오류가 나면 화면에 나온 오류 번호를 확인하고 [AltStore 공식 오류 안내](https://faq.altstore.io/altstore-classic/error-codes)를 참고합니다. 비밀번호나 인증 코드를 채팅·저장소에 공유할 필요는 없습니다. 빌드 성공과 실제 iPhone 설치 성공은 각각 확인합니다.

이 프로젝트는 macOS 텍스트 편집기 [CotEditor](https://github.com/coteditor/CotEditor)를 변형한 것입니다.

# Gray Editor 빌드 가이드

## 준비 사항

- macOS Tahoe 26 이상이 설치된 Mac
- Xcode 26.5
- Git과 인터넷 연결 (소스 코드 및 Swift 패키지 다운로드용)

Xcode를 설치한 뒤 한 번 실행하여 초기 설정을 마칩니다.

## 소스 코드 다운로드

터미널에서 원하는 위치로 이동한 후 저장소를 복제합니다.

```bash
git clone https://github.com/answndud/gray-editor.git
cd gray-editor
open CotEditor.xcodeproj
```

GitHub 저장소 접근 권한이 필요한 경우 해당 계정으로 인증해야 합니다.

## Xcode에서 빌드 및 실행

1. Xcode에서 `Configurations/CodeSigning.xcconfig`를 엽니다.
2. 기본 서명 설정을 주석 처리하고 Ad Hoc 서명 설정을 활성화합니다.

   ```xcconfig
   //#include "CodeSigning-Default.xcconfig"
   #include "CodeSigning-AdHoc.xcconfig"
   ```

3. Xcode 상단에서 `CotEditor` 스킴과 `My Mac` 실행 대상을 선택합니다.
4. Swift 패키지 다운로드가 완료될 때까지 기다립니다. 플러그인 실행을 신뢰할지 묻는 창이 나타나면 내용을 확인하고 허용합니다.
5. **Product > Run**을 선택하거나 `⌘R`을 눌러 빌드하고 실행합니다. 빌드만 하려면 **Product > Build** 또는 `⌘B`를 사용합니다.

빌드된 `GrayEditor.app`은 Xcode의 프로젝트 탐색기에서 **Products > GrayEditor.app**을 우클릭하고 **Show in Finder**를 선택해 찾을 수 있습니다. 필요하면 앱을 응용 프로그램 폴더로 복사할 수 있습니다.

## 빌드 후 용량 정리

1. 먼저 `GrayEditor.app`을 **응용 프로그램** 폴더 등 아래에서 삭제할 폴더 밖으로 복사하고, 복사한 앱이 실행되는지 확인합니다. 빌드 결과물 안의 앱을 그대로 두면 정리할 때 함께 삭제됩니다.
2. Xcode를 종료합니다.
3. 저장소 폴더에 `build` 또는 `SourcePackages` 폴더가 있다면 Finder에서 휴지통으로 옮기거나, 터미널에서 저장소 폴더로 이동한 뒤 다음 명령으로 삭제합니다.

   ```bash
   cd /경로/gray-editor
   rm -rf build SourcePackages
   ```

4. Xcode가 별도로 만든 빌드 파일도 삭제하려면 Xcode의 **Window > Projects**에서 이 프로젝트의 Derived Data 옆 삭제 버튼을 사용합니다. 해당 메뉴가 보이지 않으면 Finder의 **이동 > 폴더로 이동**에서 `~/Library/Developer/Xcode/DerivedData`를 열고, 이 프로젝트에 해당하는 폴더만 휴지통으로 옮깁니다. 휴지통을 비우면 공간이 반환됩니다.

빌드를 다시 할 때 삭제한 빌드 파일은 다시 생성되고 Swift 패키지는 필요에 따라 다시 다운로드됩니다. 앞으로 소스 수정이나 재빌드가 필요 없다면 복사한 앱을 확인한 후 저장소 폴더 `gray-editor` 자체도 삭제할 수 있습니다. 이 경우 소스 코드와 저장소 안에서 변경한 내용도 함께 삭제됩니다.

## 라이선스

소스 코드와 이미지 리소스의 라이선스 조건은 [LICENSE](LICENSE)를 확인하세요.

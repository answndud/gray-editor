macOS 텍스트 편집기 [CotEditor](https://github.com/coteditor/CotEditor)를 변형한 프로젝트임.

# Gray Editor 빌드 가이드

## 준비 사항

- macOS Tahoe 26 이상이 설치된 Mac
- Xcode 26.5
- Git과 인터넷 연결 (소스 코드 및 Swift 패키지 다운로드용)

Xcode 설치 후 최초 실행 및 초기 설정 완료 필요.

## 소스 코드 다운로드

터미널에서 원하는 위치로 이동 후 저장소 복제:

```bash
git clone https://github.com/answndud/gray-editor.git
cd gray-editor
open CotEditor.xcodeproj
```

저장소 접근 권한이 필요한 경우 해당 GitHub 계정 인증 필요.

## Xcode에서 빌드 및 실행

1. Xcode에서 `Configurations/CodeSigning.xcconfig` 열기.
2. 기본 서명 설정 주석 처리 및 Ad Hoc 서명 설정 활성화:

   ```xcconfig
   //#include "CodeSigning-Default.xcconfig"
   #include "CodeSigning-AdHoc.xcconfig"
   ```

3. Xcode 상단에서 `CotEditor` 스킴 및 `My Mac` 실행 대상 선택.
4. Swift 패키지 다운로드 완료 대기. 플러그인 실행 신뢰 확인 창이 나타나면 내용 확인 후 허용.
5. **Product > Run** 또는 `⌘R`로 빌드 및 실행. 빌드만 필요한 경우 **Product > Build** 또는 `⌘B` 사용.

빌드된 앱 위치: Xcode 프로젝트 탐색기에서 **Products > GrayEditor.app** 우클릭 후 **Show in Finder** 선택. 필요에 따라 앱을 응용 프로그램 폴더로 복사 가능.

## Finder 문서 아이콘 갱신

GrayEditor는 TXT, Markdown, JSON에 회색 문서 아이콘을 포함한다. 새 앱을 응용 프로그램 폴더에 복사하거나 기존 앱을 교체한 후에는 Finder가 이전 아이콘을 계속 표시할 수 있다. GrayEditor 창에서는 회색인데 Finder에서 초록색이 보이면 Finder를 한 번 재실행한다.

```bash
killall Finder
```

Finder가 잠시 종료된 뒤 다시 실행된다. 처음 설치하는 Mac이나 이미 아이콘이 갱신된 경우에는 실행할 필요가 없다. 재실행 후에도 초록색이면 해당 파일의 **정보 가져오기 > 다음으로 열기**에서 GrayEditor가 선택돼 있는지 확인한다.

기존 CotEditor를 휴지통으로 옮긴 Mac에서는 macOS가 휴지통 안의 앱을 문서 타입 제공자로 계속 등록할 수 있다. 이 경우 특히 JSON의 초록색 아이콘 선언이 남을 수 있다. 휴지통에 `CotEditor.app`이 있을 때 다음 명령으로 오래된 등록을 해제하고 Finder를 갱신한다.

```bash
/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -u ~/.Trash/CotEditor.app
killall Finder
```

이 Mac에서는 이 작업 직후 JSON 아이콘도 회색으로 보이기 시작했다. 앱 파일은 삭제하지 않았다. 휴지통의 앱이 나중에 다시 등록되어 초록색이 재발하면 해당 `CotEditor.app`을 휴지통에서 완전히 삭제한 뒤 다시 갱신한다.

다른 앱이 기본 앱인 파일이나 파일에 직접 지정한 사용자 아이콘은 별도로 표시될 수 있다.

## 빌드 후 용량 정리

1. `GrayEditor.app`을 **응용 프로그램** 폴더 등 삭제 대상 밖으로 복사한 후 실행 확인. 빌드 결과물 안에 남은 앱은 정리 시 함께 삭제됨.
2. Xcode 종료.
3. 저장소 폴더에 `build` 또는 `SourcePackages`가 있으면 Finder에서 휴지통으로 이동하거나 터미널에서 다음 명령으로 삭제:

   ```bash
   cd /경로/gray-editor
   rm -rf build SourcePackages
   ```

4. Xcode의 별도 빌드 파일 정리: **Window > Projects**에서 이 프로젝트의 Derived Data 옆 삭제 버튼 사용. 해당 메뉴가 없으면 Finder의 **이동 > 폴더로 이동**에서 `~/Library/Developer/Xcode/DerivedData`를 열고 이 프로젝트에 해당하는 폴더만 휴지통으로 이동. 공간 확보를 위해 휴지통 비우기 필요.

재빌드 시 빌드 파일은 다시 생성되며 Swift 패키지는 필요에 따라 다시 다운로드됨. 소스 수정이나 재빌드가 불필요한 경우 복사한 앱 확인 후 저장소 폴더 `gray-editor`도 삭제 가능. 저장소 삭제 시 소스 코드와 내부 변경 사항도 함께 삭제됨.

## 라이선스

소스 코드 및 이미지 리소스의 라이선스 조건: [LICENSE](LICENSE) 참고.


<br/><br/>
# IOS Bootstrap
<br/><br/>

- Architecture: MVVM, VIPER
- Network: RxMoya
- Rx: RxSwift
- TDD/BDD: Quick, Nimble
- CI/CD: Gitlab CI, fastlane
- DB: Realm

<br/><br/>

### .gitignore
```
.DS_Store
build/
*.pbxuser
!default.pbxuser
*.mode1v3
!default.mode1v3
*.mode2v3
!default.mode2v3
*.perspectivev3
!default.perspectivev3
*.xcworkspace
!default.xcworkspace
xcuserdata
*.moved-aside
DerivedData
.idea/
AdHoc/
Mix/
Pods/
Podfile.lock
screenshots/
fastlane/report.xml
fastlane/Preview.html
fastlane/screenshots/**/*.png
fastlane/test_output
```

or 

```
Swift:
curl -o .gitignore https://www.gitignore.io/api/swift

Objective-C:
curl -o .gitignore https://www.gitignore.io/api/objective-c
```
<br/><br/>

### pods
```
# Fabric
pod 'Fabric', '1.7.3'
pod 'Crashlytics', '3.10.0'

# Keyboard
pod 'IQKeyboardManagerSwift', '5.0.7'

# UI
pod 'PureLayout'
pod 'Kingfisher', '4.8.0'
pod 'lottie-ios', '2.5.0'
pod 'Hue', '3.0.1'

#Network
pod 'Moya/RxSwift'

# Cache
pod 'KeychainSwift', '11.0.0'

# Rx
pod 'RxSwift'
pod 'RxCocoa'
```

<br/><br/>

### Lint

#### Build Phases
```
if which swiftlint >/dev/null; then
swiftlint
else
echo "error: SwiftLint does not exist, download it from https://github.com/realm/SwiftLint"
exit 1
fi
```
#### .swiftlint.yml
```
disabled_rules:
- function_parameter_count
- nesting
- variable_name
- weak_delegate
- trailing_comma
opt_in_rules:
- empty_count
- force_unwrapping
- private_outlet
warning_threshold: 15
line_length: 150
file_length:
warning: 500
type_body_length:
warning: 400
error: 450
excluded:
- Carthage/
- Frameworks/
- Pods
reporter: "xcode"
```

<br/><br/>

## CI - Gitlab CI

### Installation
```
gitlab-ci-multi-runner register
gitlab-ci-multi-runner verify
gitlab-ci-multi-runner stop
gitlab-ci-multi-runner status
```
### .gitlab-ci.yml
```
stages:
- build

build_code:
stage: build
script:
- xcodebuild clean -workspace ProjectSwift.xcworkspace -scheme ProjectSwift | xcpretty
- xcodebuild test -workspace ProjectSwift.xcworkspace -scheme ProjectSwift -enableCodeCoverage YES -destination 'platform=iOS Simulator,name=iPhone 8,OS=12.2' | xcpretty -s
tags:
- ios
```



---
title: "Framework Not Found with xcode 12 openssl etc"
date: 2021-04-29
categories:
  - blog
tags:
  - ios
  - react-native
---


```
To do that, navigate to Build Settings of your project and add Any iOS Simulator SDK with value arm64 inside Excluded Architecture.

```
일반적으로 user-define 설정을 따르지 않는경우 arm64를 excluded architecture.에 any ios simulator에 넣는다 넣고 cleanbuild 후 에뮬레이터를 돌린다.

XCConfig 파일을 사용할 경우에는 
```
EXCLUDED_ARCHS[sdk=iphonesimulator*] = arm64
```

Pod project에

```
s.pod_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64' }
s.user_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64' }

```

한후 pod install

```
post_install do |installer|
  installer.pods_project.build_configurations.each do |config|
    config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
  end
end



```

참고 https://stackoverflow.com/questions/63607158/xcode-12-building-for-ios-simulator-but-linking-in-object-file-built-for-ios?page=1&tab=votes#tab-top



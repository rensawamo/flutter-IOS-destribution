# iOS destribution(2024/2)

##  fvmを使う場合
``` sh
fvm list
fvm use (上記ver)
or
fvm use stable
```


## gitigonreに先に以下を追加しておく

```sh
ExportOptions.plist
ExportOptions.pem
*.pem
**/.fvm/flutter_sdk
**/lib/firebase_options.dart
```


## 使用する　エンコードコマンド
```sh
$ base64 -i input.xxx  -o output.pem 
```


##  必要な環境変数
- APPLE_APP_PASSWORD :  　アプリ用パスワード

- APPLE_ID : 　 Apple Developerの　Apple ID


- CERTIFICATES_P12_BASE64 : 　 Certificates と p12 のエンコード


- CERTIFICATE_PASSWORD :　 パスワード


- PROVISIONING_PROFILE_BASE64 :　  Provisioning profile　のエンコード

  

- EXPORTOPTIONS_BASE64 :  　 ExportOptions.plistのエンコード


- IOS_APP_ID : firebase のiOS アプリ名


- CREDENTIAL_FILE_CONTENT : GCP トークン



## APPLE_APP_PASSWORD  
https://appleid.apple.com/ に移動　→ サインイン　→ 下記よりアプリ用パスワードを作成

  ![image](https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/238b6e41-1c27-49cb-ab5a-5ba53e069f2d)



## APPLE_ID 
Apple Developerの　Apple ID


## CERTIFICATES_P12_BASE64
キーチェーンより証明書の要求を作成　→   https://developer.apple.com/ に移動　　→  Certificates, IDs, & Profiles　→  Certificates　→ より　以下を選択し　.cerファイルをダウンロード　　

<img width="557" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/e299fffe-f2dc-4024-9304-161c769d2afa">
<img width="190" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/e5187f07-e9b1-4125-8ca1-1cf3c6bbd0f4">


→  ダブルクリック　　→  キーチェーンの鍵に登録されている　→ 右クリックで　書き出す　を選択　
　

![image](https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/33768b2f-cd35-4249-a2e4-1a2b6764c317)

→  .p12 ファイルが作成される　→　エンコード

<img width="250" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/3eb3a920-f862-4ad9-befe-a59f3e27e846">


## CERTIFICATE_PASSWORD
上記の書き出しの時に　パスワードを設定するため、メモしておく



## PROVISIONING_PROFILE_BASE64
https://developer.apple.com/ に移動　　→  Certificates, IDs, & Profiles　→ 
Profiles　→ より　以下を選択し　.mobileprovisio ファイルをダウンロード　→ 　エンコード

<img width="597" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/018c37c4-edae-4be4-8292-53b3fa2103a9">

<img width="323" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/a78b09c3-d0fc-47fd-afdb-e98bf08549d5">



## EXPORTOPTIONS_BASE64
xcodeに移動　→ 以下を設定

![image](https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/de4b0efa-7426-46b5-afac-8b46be3a6dc5)



→ Product → Archeve → Destribute App   →   　Custom 　

<img width="500" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/fb5b594d-28fd-432e-8dd9-12d7e3fe687a">


<img width="716" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/48128a11-6daf-40b9-85bc-82a86f90ac23">


→ 　App Store Connect 　


<img width="356" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/838e4e05-5340-4654-b0ce-7b7f70ca06c9">


→　 Export 

<img width="330" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/56b25e0e-7e0a-4cb1-a91d-d4e6580a76a1">


→　 ExportOptions.plistをふくむフォルダをダウンロード　　


<img width="564" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/322a6796-4b2d-405d-831f-317f3284a4e3">


→  ExportOptions.plistをプロジェクトのルートディレクトに入れる　→  エンコード


<img width="323" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/5b0f5259-f488-44a9-9768-32d3a166e4bf">




## firebase 導入
上記で作成した Bundel Identifer と同じ バンドル IDで　firebaseのiosプロジェクトを作成。

以下に　GoogleService-Info.plist ファイルを追加する。
<img width="606" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/0bc1c3b1-2aea-456a-8b42-5b618a7336c1">


上記の後、firebaseの画面に移動 → アプリの追加 → flutter で
firebase login コマンドなどを順番に実行し、プロジェクトに firebase_option.dartが追加されていることを確認する

![image](https://github.com/rensawamo/firebase_destribution/assets/106803080/3ed7ca87-d419-4bb5-9bc8-2b831be7b779)


### firebase core の導入
[pubget](https://pub.dev/)
から firebase_core のバージョンを指定して

```sh
flutter pub get
```

firebase_core がないと xcodeでエラーが出る場合は
ios/Flutter/Release.configを以下のように修正

```sh
#include? 'Pods/Target Support Files/Pods-Runner/Pods-Runner.release.xcconfig'
#include 'Generated.xcconfig'
#include 'Target Support Files/Pods-Runner/Pods-Runner.profile.xcconfig'
```


###  GCP トークン の発行

https://github.com/wzieba/Firebase-Distribution-Github-Action/wiki/FIREBASE_TOKEN-migration#guide-2---the-same-but-with-screenshots

以下のコマンドは、現在では非推奨。
```sh
firebase login:ci
```






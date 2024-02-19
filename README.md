# flutter_ios_destribution

## .gitigonreに先に以下を追加しておく

```sh
ExportOptions.plist
ExportOptions.pem
```


## 使用する　エンコードコマンド
```sh
$ base64 -i input.xxx  -o output.pem 
```



## 環境変数と準備

### ・　APPLE_APP_PASSWORD  
https://appleid.apple.com/ に移動　→ サインイン　→ 下記よりアプリ用パスワードを作成

→  ![image](https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/238b6e41-1c27-49cb-ab5a-5ba53e069f2d)



### ・　APPLE_ID 
Apple Developerの　Apple ID


### ・　CERTIFICATES_P12_BASE64
キーチェーンより証明書の要求を作成　→   https://developer.apple.com/ に移動　　→  Certificates, IDs, & Profiles　→  Certificates　→ より　以下を選択し　.cerファイルをダウンロード　　

<img width="557" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/e299fffe-f2dc-4024-9304-161c769d2afa">

→  ダブルクリック　　→  キーチェーンの鍵に登録されている　→ 右クリックで　書き出す　を選択　→ エンコード
　
<br>

![image](https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/33768b2f-cd35-4249-a2e4-1a2b6764c317)



### ・　CERTIFICATE_PASSWORD
上記の書き出しの時に　パスワードを設定するため、メモしておく



### ・　PROVISIONING_PROFILE_BASE64
https://developer.apple.com/ に移動　　→  Certificates, IDs, & Profiles　→  Profiles　→ より　以下を選択し　.mobileprovisio ファイルをダウンロード　→ エンコード

<img width="597" alt="image" src="https://github.com/rensawamo/flutter-IOS-destribution/assets/106803080/018c37c4-edae-4be4-8292-53b3fa2103a9">



### ・　EXPORTOPTIONS_BASE64
xcodeに　移動　→ 以下を設定


→ Product → Archeve で　Custom 　→ 　App Store Connect 　→　 Export 　→　 ExportOptions.plistをふくむフォルダをダウンロード　　→　　ExportOptions.plistをプロジェクトのルートディレクトに入れる　→  エンコード








# 【iOS】プッシュ通知の受信に必要な証明書の作り方(開発用)
アプリにプッシュ通知を組み込む際、ビルド時に必要な証明書の作り方を解説します　*2016/09/28作成*

![画像1](/readme-img/001.png)

## はじめる前の確認と注意
* [Apple Developer Program](https://developer.apple.com/account/)の登録（有料）が必要です
* 上記アカウントを既に別のMacで既に開発用証明書を利用している場合は少し複雑で、そのMacをから開発証明書に紐付く「秘密鍵.p12」をエクスポートし、これから使用するMacに渡す必要があります（同じものを使う必要があるため）
 * Apple Developer Programからダウンロードした「開発用証明書」と受け取った「秘密鍵.p12」をキーチェーンアクセスで紐付けた後、③AppIDの作成から作業を行ってください。
* 作業は少し複雑です。作り方を誤るとプッシュ通知が動作しない可能性がありますので、丁寧に作業していきましょう！

## 作業手順

* 下図の内容と順番で作成していきます

![画像i2](/readme-img/i002.png)

* 作成したファイルはダウンロードし、同じフォルダにまとめておきましょう

* ①CSRファイルを作成します　※初回利用時のみ
 * __注意__：CSRファイルは既に作成したものがあれば、新しく作成してください！必ず既存のものを使用します。複数作成してしまうとファイル名が同じであるため区別できなくなり失敗につながる恐れがあります。
* 「キーチェーンアクセス」を開いて、メニューバーの「キーチェーンアクセス」＞「証明書アシスタント」＞をクリックします

![画像i3](/readme-img/i003.png)

* 「鍵ペア情報」を確認して「続ける」をクリックし、「設定結果」が出るので「完了」をクリックします
* 保存場所を選択して「保存」をクリックします

![画像i4](/readme-img/i004.png)

* ここから[Apple Developer Programのメンバーセンター](https://developer.apple.com/account/)にログインして作業を行います

![画像i5](/readme-img/i005.png)

* ②開発用証明書(.cer)を作成します　※初回利用時のみ
 * __注意__：開発用証明書(.cer)ファイルは既に作成したものがあれば、新しく作成しないでください！必ず既存のものを使用します。複数作成してしまうとファイル名が同じであるため区別できなくなり失敗につながる恐れがあります。
* 「Certificates」＞「All」＞右上の「＋」をクリックして、「iOS App Development」にチェックをいれます

![画像i6](/readme-img/i006.png)
![画像i7](/readme-img/i007.png)
![画像i8](/readme-img/i008.png)

* ③AppIDを作成します
* 「Identifiers」＞「App IDs」＞右上の「＋」をクリックします

![画像i9](/readme-img/i009.png)
![画像i10](/readme-img/i010.png)
![画像i11](/readme-img/i011.png)
![画像i12](/readme-img/i012.png)

* ④動作確認で使用する端末の登録をします
 * 既に登録済みの場合、この作業は不要です
* 「Devices」＞「All」＞右上の「＋」をクリックします

![画像i13](/readme-img/i013.png)

* UDIDは下記のいずれかの方法で調べることができます

![画像i14](/readme-img/i014.png)
![画像i15](/readme-img/i015.png)

* 先ほどの入力欄に調べたUDIDをコピーして貼り付け、「Continue」をクリックします

![画像i16](/readme-img/i016.png)

* ⑤プロビジョニングプロファイルを作成します
* 「Provisioning Profiles」＞「All」＞右上の「＋」をクリックします

![画像i17](/readme-img/i017.png)
![画像i18](/readme-img/i018.png)
![画像i19](/readme-img/i019.png)
![画像i20](/readme-img/i020.png)

* ⑥APNs用証明書(.cer)の作成をします
 * 既に作成済みの「②開発用証明書(.cer)」を使用する場合は「①CSRファイル」がありません。ここで、必要となりますので、「①CSRファイル」の作成後作業を行ってください。
* 「Certificates」＞「All」＞右上の「＋」をクリックします

![画像i21](/readme-img/i021.png)
![画像i22](/readme-img/i022.png)

* CSRファイルは①開発用証明書(.cer)作成時と同じものを使用します

![画像i23](/readme-img/i023.png)
![画像i24](/readme-img/i024.png)

* ⑦APNs用証明書(.p12)を書き出します
* キーチェーンアクセスを開きます
* ⑥で作成した「APNs用証明書(.cer)」をダブルクリックしてキーチェーンアクセスを開きます
* 三角のアイコンをクリックして、開きます
 * 重要：証明書と秘密鍵を別々にする必要があります！

![画像i27](/readme-img/i027.png)
![画像i28](/readme-img/i028.png)

* これで準備完了です！！

## この後使用する証明書やファイルの確認
* 作成したものの中で、以下の３点を使用します
 * ②開発用証明書(.cer)
 * ⑤プロビジョニングプロファイル
 * ⑦APNs用証明書(.p12)

## 参考
* [Swift3(iOS10以上)用プッシュ通知サンプル](https://github.com/natsumo/Swift3PushApp)
* [Swift2(iOS8,9)用プッシュ通知サンプル](https://github.com/natsumo/SwiftPushApp)
* [ObjectiveC(iOS10以上)用プッシュ通知サンプル](https://github.com/natsumo/ObjcPushApp_ios10)
* [ObjectiveC(iOS8,9)用プッシュ通知サンプル](https://github.com/natsumo/ObjcPushApp)

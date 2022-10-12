CoeFont API の[Text2speech](https://docs.coefont.cloud/#tag/Text2speech)を使って日本語文字列を音声Buffer(wav/mp3)に変換します。

# 概要
CoeFont API の[Text2speech](https://docs.coefont.cloud/#tag/Text2speech)を使って日本語文字列を音声Buffer(wav/mp3)に変換します。

[2022年7月より、LiteプランでのAPI利用ができなくなり](https://prtimes.jp/main/html/rd/p/000000024.000078329.html) 、作者はこのノードをメンテナンスできないので、一定期間後にアーカイブにします。大変残念です。

このノードを利用するには、CoeFontの法人アカウントが必要です。また無料のCoeFontを使う場合にも、API経由の利用となりますのでアカウントのポイント残高を消費(1文字5pt～)します。ポイント残高にはご注意ください。

# インストール
```
npm i node-red-contrib-coefont-text2speech
```

もしくは、「パレットの管理」から導入してください。（導入後、パレットに反映されない場合は一度ブラウザのリロードをお願いします）
※なお、Node-RED 2.0.0以降でないと動作しないようです。

# 利用方法
プロパティウインドウでCoeFontのアクセスキー/シークレットキーと音声を生成したい文字列を指定することで、Buffer形式のWAVで音声が出力されます。
[node-red-contib-play-audio](https://flows.nodered.org/node/node-red-contrib-play-audio)を使うことで、エディタ内で音声を再生することができます。
Injectノードなどでmsg.payloadで文字列を入力することで、音声を生成することができます。

![image](https://user-images.githubusercontent.com/17796/160324383-4716e6b0-3c6f-4752-bfeb-fc717f038642.png)


## 入力パラメータ
入力パラメータはノードプロパティで設定しますが、msgオブジェクトでも指定することができ、両方で指定された場合はmsgオブジェクトが優先されます。

### 必須パラメータ
 - CoeFont AccessKey (msg.akey) : CoeFont のAccess Keyを指定。
 - CoeFont SecretKey (msg.skey) : CoeFont のClient Secretを指定。

Access KeyとClient Secretは、[CoeFont API情報](https://coefont.cloud/account/api) で生成してください。

### オプションパラメータ
 - CoeFont ID (msg.cfid) : 音声変換を行うcoefontのID。coefont詳細画面のurlに表示される個別のuuidを参照。デフォルトは「[ミリアル(喜)](https://coefont.cloud/coefonts/9e0c2783-804c-4f77-81ab-1fbc70d15ffc)」。(無料音声ですが、1文字あたり5pt消費されます。
 - テキスト (msg.payload) : 生成する文章を指定。最大で1000文字指定できます。デフォルトは"こんにちは"。
 - スピード (msg.speed) : 音声の速度。1.0で通常速度。0.5で半速。2.0で2倍速。デフォルトは1.0。
 - ピッチ (msg.pitch) : 音声のピッチ。±1200で1オクターブ変化。デフォルトは0。
 - 句点 (msg.kuten) : 句点の間隔(秒)。デフォルトは0.7。
 - 読点 (msg.toten) : 読点の間隔(秒)。デフォルトは0.4。
 - 音量 (msg.volume) : 音量(倍)。デフォルトは1。
 - 抑揚 (msg.intonation) : 抑揚。デフォルトは1。
 - 音声フォーマット (msg.format) : 出力音声のフォーマット。"wav"か"mp3"を指定。 デフォルトは"wav"。

## 出力
 - 音声Buffer出力 : node-red-contib-play-audio で再生できます。
 - 音声ファイルURL : このURLに対してhttp-requestノードを使ってHTTP GETすることで音声ファイルを取得できます。

# その他
生成された音声データは、 CoeFontの[サービス利用規約](https://coefont.cloud/termsOfUse)に従って利用してください。

このノードは、[node-red-nodegen](https://github.com/node-red/node-red-nodegen)で生成されました。
また、作成にあたっては、Qiitaの記事 [Node-REDでCoeFont CLOUD APIを使い高品質のTTSを試す](https://qiita.com/Y-Shikase/items/2d773dc4d970228437d5)を参考にさせていただきました。

# 既知の不具合
 - ノードパレットに導入した際、リロードしないと反映しない
 - 導入時、ノードの名前が正しく反映されない。(「sf.4008898c5f8d8781」となる。node-red-nodegenの仕様かもしれません。）

# LICENCE
Apache 2.0


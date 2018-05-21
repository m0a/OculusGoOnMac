# OculusGoOnMac


前回は玉転がしゲームをOculusGoに対応しました。
https://qiita.com/m0a/items/98cdc1e03cf067769578

その後、もくもく会でUnityアプリを作りました。

作ったゲームの動画は[こちら](https://youtu.be/rGerw-k5Vd8
)

上記を作ってみてわかったことがあります。
**デバックが辛い**。
Editor上でPlayしようとしても視点操作等が効ききません。
実機で動作確認すると変更するたびに数分待たされます。


そこでゲームパッドでOculsuGoのコントローラとヘッドトラッキングの代替を行うことにします。
アナログパッドに二軸コントローラが2つあればそれぞれをヘッドトラッキング、コントローラーのモーショントラッキングに代替できそうです。

# 準備
macだと使えるゲームパッドに限りがあるようです。PCだと問題ないと思いますが。
先ずは``LOGICOOL ゲームパッド F310``を入手します。秋葉原のヨドバシ2Fで、山ほど置いてあったので
入手性は容易なようです。

下記手順に従います。これでこのコントローラーがUnityで使えるようになります。
http://heyassy.hateblo.jp/entry/2017/10/08/113757

<img width="481" alt="Xbox_360_Controllers.png" src="https://qiita-image-store.s3.amazonaws.com/0/3844/2ed2bba2-54a3-71aa-a42f-27fc47e9e6c9.png">

目標は上記のような感じにヘッドトラッキングとコントローラーのトラッキングに対応させます。


# Unity上での作業

## TLDR
以下にサンプルを含めたコードが置いてあります。そのまま動くと思います。
https://github.com/m0a/OculusGoOnMac

## 内容

変更したコードは
[``OVRCameraRig.cs``](https://raw.githubusercontent.com/m0a/OculusGoOnMac/master/Assets/Oculus/VR/Scripts/OVRCameraRig.cs)と[``OVRTrackedRemote.cs``](https://raw.githubusercontent.com/m0a/OculusGoOnMac/e9854803523d55cfb780ddd8d0a0833a0b3e93d6/Assets/Oculus/VR/Scripts/Util/OVRTrackedRemote.cs) のみです。
もし既存の環境に入れるのであれば上記2ファイルを置き換える感じで行けると思います。

### ``OVRCameraRig.cs``
ヘッドトラッキングとコントローラーのトラッキングをEditor利用時はダミーコードが動くように調整しています。
[``プラットフォーム依存コンパイル``](https://docs.unity3d.com/jp/current/Manual/PlatformDependentCompilation.html)の機能を使い、実機には影響しないようにしています。

### ``OVRTrackedRemote.cs``
本来は実機コントローラーの接続状態を見て配下のコントローラーメッシュの有効化無効化を行う機能ですが、
Editor利用時は強制的にOculusGoコントローラー(右手)が有効化するように修正しています。
[``プラットフォーム依存コンパイル``](https://docs.unity3d.com/jp/current/Manual/PlatformDependentCompilation.html)の機能を使い、実機には影響しないようにしています。


# まとめ

こんなかんじで動けば成功です。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">macでのOculusGo開発環境できました。頭の動きに追従してコントローラも回転させてもいいかもしれませんけど、そこは好みかなと。<a href="https://twitter.com/hashtag/OculusGoDev?src=hash&amp;ref_src=twsrc%5Etfw">#OculusGoDev</a> <a href="https://t.co/dHRD3XHPN1">pic.twitter.com/dHRD3XHPN1</a></p>&mdash; m0a (@abe00makoto) <a href="https://twitter.com/abe00makoto/status/998414649212092420?ref_src=twsrc%5Etfw">2018年5月21日</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

問題点としてはUnityの作法がわからないのでコード共有方法がこれでいいのかってことです。
もっといい方法があればご教授下さい。








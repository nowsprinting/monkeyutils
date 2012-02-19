#monkeyutils.py

monkeyutils.pyは、Android DSKに同梱の[monkeyrunner](http://developer.android.com/guide/developing/tools/monkeyrunner_concepts.html)によるテストをサポートするモジュールです。

[Androidテスト部](https://sites.google.com/site/androidtestclub/)において、Testterのシステムテスト用に書いたモジュールです。

現在のところ、

- 複数デバイス向けのテストスクリプトを一本化
- 複数デバイスのテストを自動化
- スクリーンショットの格納先統一、画像比較の自動化

を実現しています。


使用例は、

Testter wiki: [Testterのシステムテスト実行方法](https://atec.backlog.jp/wiki/TESTTER/Testter%E3%81%AE%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%83%86%E3%82%B9%E3%83%88%E5%AE%9F%E8%A1%8C%E6%96%B9%E6%B3%95)

を参照してください。

- user: guest
- pass: guest

でログインできます。


##関数一覧

###get_adb_devices()
$ adb devices コマンドで得られる、接続されているデバイスの（シリアル番号の）リストを返します。

Testterでは、alltest.pyからのみ使用しています。

Windowsでは動作しません。


###get_dpi_ratio(device, width, height)
引数は、MonkeyDeviceオブジェクト, テストケース上の想定width, 同じくheight。

テスト対象の画面サイズを取得し、想定width/heightとの比率を求めてタプルで返します。
例えば、480x800のデバイス、width=320、height=480が指定された場合、
( 1.5, 1.67)
が返ります。

各テストケースの先頭で呼び出し、テストケース内で座標指定の補正に使用しています。


###get_device_name(device)
引数は、MonkeyDeviceオブジェクト。

渡されたMonkeyDeviceオブジェクトからモデル名とAndroidバージョンを取得し、アンダースコアで結合してデバイス名として返します。

このデバイス名は、スクリーンショット格納ディレクトリ名として使用しています。


###take_and_compare_snapshot(device, testcase, filename)
引数は、MonkeyDeviceオブジェクト, テストケース名, snapshotのファイル名。

以下を実行します。

+ スクリーンショットを撮影、所定のディレクトリ（デバイス名/テストケース名）に格納する。
+ snapshot_expected下に同パスのファイルが存在するとき、ImageMagickのcompareコマンドで比較を行ない結果をsnapshot_compare/下に格納する。



#Auther
[@nowsprinting](https://twitter.com/#!/nowsprinting)



#License

Copyright 2011, Android Test and Evaluation Club

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

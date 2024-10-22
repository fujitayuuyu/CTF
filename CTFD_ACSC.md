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

##

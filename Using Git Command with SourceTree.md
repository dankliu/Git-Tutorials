
##一、Git 環境建立與指令說明##
----------

 - 可申請如下遠端環境帳號如GitLab, Bitbucket進行
	- Git Remote: https://gitlab.com/ ,  https://bitbucket.org/
 - 安裝本機用戶端環境Git指令版 
	- Git Client Command: https://git-scm.com/
 - 安裝圖形介面環境Sourcetree
	- Git Client GUI: https://www.sourcetreeapp.com/
 - 修改程式後操作流程為
	- commit本地端，push遠端

**1. Git global setup (設定Git全域參數設定)**  
git config --global user.name "xxxxxx輸入使用者名稱"  
git config --global user.email "xxxxxx輸入使用者信箱"  

查看已設定全域參數  
git config --list  
	
**2. Create a new repository (於遠端複製新的儲存庫)**  
git clone git@gitlab.com:xxxxxx/xxxxxx.git  
cd ITRI-Logistics-Streaming  
touch README.md  
git add README.md  
git commit -m "add README"  
git push -u origin master  
附註：push後的orign表示該遠端remote的名稱，可自行定義  
也可擁有多組遠端儲存庫，可參閱5. Change Remote Path 新增後再push  

**3. Existing folder or Git repository (於本地已有的儲存庫上傳遠端)**  
cd existing_folder  
git init  
git remote add origin git@gitlab.com:xxxxxx/xxxxxx.git  
git add .  
git commit  
git push -u origin master​  

**4. Show Remote Path**  
git remote -v  
rigin	https://gitlab.com/xxxxxx/xxxxxx.git (fetch)  
origin	https://gitlab.com/xxxxxx/xxxxxx.git (push)  

**5. Change Remote Path**  
git remote add gitlab git@gitlab.com:xxxxxx/xxxxxx.git (remote add後名稱為給予加入的遠端代號)  
SourceTree設定方式：\Repository\Repository Setting\Remotes Add  
  
**6. 新增Add File or Folder**  
Git使用add指令加入檔案時會進行暫存，表示進入下次Commit狀態  
可使用git status觀看變化情形  

git add file  
git add folder/  

**7. 取消Add File or Folder**  
git rm --cached file  
git rm --cached -r folder/  

**8. 新增一個Commit**  
若尚未加入git add暫存清單的檔案則不會加入此次Commit  
git commit  

**9. Show Commint Log**  
git log  
65-0A40291-92:GitTest TonyLiu$ git log  
commit 1d27da9d55259247d0c5d33345fc2f28f40c43f5  
Author: TonyLiu <dankliu@gmail.com>  
Date:   Wed Dec 16 14:29:16 2015 +0800  

    Commint v1.00  

**10. Show File Change Status**  
git status  
65-0A40291-92:bFlier-Price-Compare TonyLiu$ git status  
On branch master  
Your branch is up-to-date with 'origin/master'.  
nothing to commit, working directory clean  

嘗試新增一檔案version2.txt，再進行查看狀態即可看到顯示Untracked files:  
若要加入Commit清單暫存可再次進行git add指令加入  

65-0A40291-92:GitTest TonyLiu$ git status  
On branch master  
Untracked files:  
  (use "git add <file>..." to include in what will be committed)  

	version2.txt  

**11. Revert, Rebase取消這次或某次Commit**  
兩者不同點在於Revert可以寫入紀錄，Rebase為直接取消  
git revert  
git rebase -i  

**12. Reset回到某一版本的狀態**  
git log --oneline顯示Commit紀錄  
git log --oneline  
5-0A40291-92:GitTest TonyLiu$ **git log --oneline**  
180e624 Commit v2.00  
1d27da9 Commint v1.00  
65-0A40291-92:GitTest TonyLiu$ **git reset 1d27da9**  
Unstaged changes after reset:  
D	version.txt  

**13. Checkout取得某次Commit版本**  
git log --oneline顯示Commit紀錄  
git log --oneline  
5-0A40291-92:GitTest TonyLiu$ **git log --oneline**  
180e624 Commit v2.00  
1d27da9 Commint v1.00  

65-0A40291-92:GitTest TonyLiu$ **git checkout 1d27da9**  
Previous HEAD position was 180e624... Commit v2.00  
HEAD is now at 1d27da9... Commint v1.00  
65-0A40291-92:GitTest TonyLiu$ ls -l  
total 8  
drwxr-xr-x  2 TonyLiu  staff  68 12 16 14:21 folder  
-rw-r--r--  1 TonyLiu  staff  10 12 16 15:06 **version.txt**  

5-0A40291-92:GitTest TonyLiu$ **git checkout 180e624**  
Previous HEAD position was 1d27da9... Commint v1.00  
HEAD is now at 180e624... Commit v2.00  
65-0A40291-92:GitTest TonyLiu$ ls -l  
total 8  
drwxr-xr-x  2 TonyLiu  staff  68 12 16 14:21 folder  
-rw-r--r--  1 TonyLiu  staff   9 12 16 15:07 **version2.txt**  


##二、建立新分支branch與合併##
----------

**1. 可使用git branch -v如下方是查看目前分支**
65-0A40291-92:GitTest TonyLiu$ git branch -v
* Slaver aa531ca last
  master aa68f17 Revert "Commit v2.00"

**2. 如何修改/取消上一次的 commit**
git commit --amend 修改上一次的 commit 訊息
git commit --amend 檔案1 檔案2... 將檔案1、檔案2加入上一次的 commit
git reset HEAD^ --soft 取消剛剛的 commit，但保留修改過的檔案
git reset HEAD^ --hard 取消剛剛的 commit，回到再上一次 commit的 乾淨狀態

**3. 分支基本操作(branch)**
git branch 列出所有本地端的 branch
git branch -r 列出所有遠端的 branch
git branch -a 列出所有本地及遠端的 branch
git branch "branch名稱" 建立一個新的 branch
git checkout -b "branch名稱" 建立一個新的 branch 並切換到該 branch
git branch branch名稱 起始點 以起始點作為基準建立一個新的 branch，起始點可以是一個 tag，branch 或是 commit
git branch --track branch名稱 遠端branch 建立一個 tracking 遠端 branch 的 branch，這樣以後 push/pull都會直接對應到該遠端的branch
git branch --set-upstream branch 遠端branch 將一個已存在的 branch 設定成 tracking 遠端的branch
git branch -d "branch 名稱" 刪除 branch
git -r -d 遠端branch 刪除一個 tracking 的遠端 branch，例如git branch -r -d wycats/master
git push repository名稱 :遠端branch 刪除一個 repository 的 branch，通常用在刪除遠端的 branch，例如git push origin :old_branch_to_be_deleted
git checkout branch名稱 切換到另一個 branch(所有修改過程會被保留)

**4. 遠端操作(remote)**
git remote add remote名稱 remote網址加入一個remote repository，例如 git remote add github git://github.com/gogojimmy/test.git
git push remote名稱 :branch名稱 刪除遠端 branch，例如 git push origin :somebranch
git pull remote名稱 branch名稱 下載一個遠端的 branch 並合併(注意是下載遠端的 branch 合併到目前本地端所在的 branch)
git push 類似於 pull 操作，將本地端的 branch 上傳到遠端

**5. 合併操作(merge)**
git merge branch名稱 合併指定的 branch 到目前的 branch
git merge branch名稱 --no-commit 合併指定的 branch 到目前的 branch 但是不會產生合併的 commit
git cherry-pick SHA 將某一個 commit 的內容合併到目前 branch，指定 commit 是使用該 commit 的 SHA 值，例如 git cherry-pick 7300a6130d9447e18a931e898b64eefedea19544

**6. 暫存操作(stash)**
git stash 將目前所做的修改都暫存起來
git stash apply 取出最新一次的暫存
git stash pop 取出最新一次的暫存並將他從暫存清單中移除
git stash list 顯示出所有的暫存清單
git stash clear 清除所有暫存


三、SourceTree 使用方式與案例介紹
------------------
兩次Commit分別上傳 version_1.txt, version_2.txt
Edward Liu@EdwardLiu-NB MINGW32 ~/Desktop/GitTEST (master)
$ ls -l
total 2
-rw-r--r-- 1 Edward Liu 197121 13 十二 16 20:34 version_1.txt
-rw-r--r-- 1 Edward Liu 197121 13 十二 16 20:37 version_2.txt

- Checkout 取得某個版本程式，於Commit列表右鍵選擇Checkout

![enter image description here](https://lh3.googleusercontent.com/-Fjj-TVZNyZo/VnFhXWy0lkI/AAAAAAAACR0/WFQU7NLt76M/s0/2015-12-16_205019.jpg "2015-12-16_205019.jpg")

改變狀態如下，HEAD更改到Commit Version 1.0.0
檔案狀態也從兩個檔案恢復到一個 version_1.txt，同理若想回到Commit Version 2.0.0
則可以在Version 2.0.0進行Checkout

Edward Liu@EdwardLiu-NB MINGW32 ~/Desktop/GitTEST (master)
$ ls
version_1.txt

![enter image description here](https://lh3.googleusercontent.com/-kKjlGh2ANl8/VnFjAO4OQYI/AAAAAAAACSM/tIHLG9Mrad0/s0/2015-12-16_211003.jpg "2015-12-16_211003.jpg")

- Reset 將目前版本指向其他Commit

![enter image description here](https://lh3.googleusercontent.com/-ZKJYwrtyt7M/VnFhNxJN6LI/AAAAAAAACRo/ebntW-BS1Tw/s0/2015-12-16_205051.jpg "2015-12-16_205051.jpg")

使用Reset current branch to this commit後會把Commit Version 2.0.0給還原到尚未Commit狀態
也就是保留檔案狀態維持在Untracked files的version_2.txt

Edward Liu@EdwardLiu-NB MINGW32 ~/Desktop/GitTEST (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        version_2.txt

nothing added to commit but untracked files present (use "git add" to track)
![enter image description here](https://lh3.googleusercontent.com/-SNsictbAKIY/VnFlbMBEuVI/AAAAAAAACSc/TX1c-6NYPb4/s0/2015-12-16_212053.jpg "2015-12-16_212053.jpg")

- Reverse 取消某次Commit並建立紀錄

同樣在Commit列表對Commit Version 1.0.0右鍵點選Reverse commit
![enter image description here](https://lh3.googleusercontent.com/-hLjILPgKhkg/VnFg5gVmG-I/AAAAAAAACRc/Np-LOKI910k/s0/2015-12-16_205118.jpg "2015-12-16_205118.jpg")

完成後發現檔案狀態只剩下version_2.txt，第一次Commit的檔案已經不在

Edward Liu@EdwardLiu-NB MINGW32 ~/Desktop/GitTEST (master)
$ ls
version_2.txt

檢查檔案狀態也沒有在Commit暫存檔案內
Edward Liu@EdwardLiu-NB MINGW32 ~/Desktop/GitTEST (master)
$ git status
On branch master
nothing to commit, working directory clean

但這樣的用途如下圖在於可使得Commit持續的保持前進且保留這次更動記錄
![enter image description here](https://lh3.googleusercontent.com/-MZTgWpAekSs/VnFomAupB3I/AAAAAAAACS8/gf3Z15P2LBo/s0/2015-12-16_213502.jpg "2015-12-16_213502.jpg")

---
title: "來做一個自己的網站吧 - Hugo 快速架站一次就上手"
date: 2020-04-10T09:35:29+08:00
draft: false
---

<!--category = [“machine learning”]-->
<!--**Note:** 強烈建議掃描以下 QR code 或鍵入網址([shorturl.at/cfhkL](shorturl.at/cfhkL))至網頁閱讀，獲得更佳閱讀體驗-->

<!--![QR code](http://s04.calm9.com/qrcode/2020-04/8C0UINZ6M7.png "QR code")-->

## 在我們開始之前...
### 為什麼我需要學習做網站呢？

隨著網路普及程度的倍倍增長，當我們聽到一個新的品牌、新的人事、新的產品，總會反射性地先拿起手機 google，想在網路的大海中，找尋關於這個新名詞的蛛絲馬跡。這時如果有個好的門面，往往能先留下好的第一印象。學會這項技能，求職者可以拿來做個人履歷、攝影師可以拿來當 portfolio，PM 可以拿來讓最新研發的產品被更多人看見...而許多熱心開發者的貢獻，更讓一般靜態網站開發的門檻降至 10 分鐘可上手的程度 (如同這篇文章的標題)，如此快速上手又益處無窮的技能，怎麼不學呢？😃

![Hugo-intro](https://upload.cc/i1/2020/04/10/T6mpMI.png "Hugo 介紹")

### 為什麼我需要用 Hugo 來做網站呢？
一個網站的構成，分為 html, css, javascript 三部份，其中 html 負責網站的架構編排，css 負責網站的風格(如顏色，大標字體應該多大...)，javascript 則負責管理網站的內容，以及使用者的操作行為。學習這三項東西往往讓不少人打退堂鼓；而坊間大家常用的 wordpress, Blogger, Medium 雖然不需要碰觸這些底層知識，卻犧牲了客製化
的方便(舉例來說，想在 Medium 貼上數學式是不可能的)。

而今天要介紹的 Hugo ，定位是靜態網頁生成器 (*static site generator*)，所謂靜態指的是使用者不會傳資料到開發者這邊 (像是提供帳密登入功能)，單純為了呈現某樣東西而生的網站，稱為靜態網站。我們可以透由簡單易讀的語法 (如 Markdown) 來讓這個工具幫我們自動生成上一段提到的 html ，並且保有客製化的自由，而前人也寫好了許多功能 (像是標籤管理、字數統計...等)，算是集一般部落格的方便上手，與自幹的彈性於一身，並且可以託管在如 github page 等免費的網頁平台上，維護起來可說是十分方便！

現在就讓我們開始吧！

---


## 前置 - 要先準備好的工具

* 終端機: 用來對電腦下指令的程式，每個作業系統都有內建 <br />
  (Windows -> PowerShell, MacOS -> iTerm)
* 文字編輯器 (像是 vim, sublime, 一般的文字記事本也是可以的)
* hugo: 本篇教學使用的靜態網頁生成工具，[一鍵安裝](https://gohugo.io/getting-started/installing/)
* git: 分佈式版本控制系統，用來追蹤網站的版本紀錄及部署，[安裝教學](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* 註冊一個 [GitHub](https://github.com/) 帳號， GitHub 為我們要託管網站的平台，也是 git 的雲端

---


## 架站 - 先在自己的電腦把網站架起來吧


完成這個段落後，我們可以在自己的電腦上運行網站，並做一些基本的客製化

1. 首先，先在終端機輸入以下指令建立網站的骨幹，並切換工作目錄至創好的資料夾

  ```bash
  hugo new site [資料夾名稱]
  cd [資料夾名稱] # 進到該資料夾
  ```

2. 為網站選一個漂亮的門面， Hugo 官網提供了許多熱心開發者提供的[免費主題](https://themes.gohugo.io/)

  <!--![Hugo-theme](https://upload.cc/i1/2020/04/10/0Evuac.png "Hugo 主題")-->

3. 選擇喜歡的主題後 (我選了 [Even](https://themes.gohugo.io/hugo-theme-even/))
   ，參照主題下方的 Installation 指示將主題給抓下來

  ![Even-installation](https://upload.cc/i1/2020/04/10/YN5VTb.png "Even Installation")

   ```
   git clone https://github.com/olOwOlo/hugo-theme-even themes/even
   ```

4. 安裝指示下的**Note**欄位，會告訴我們一些使用該主題的注意事項。以 Even 這個主題為例，我們要將 `config.toml` 這個檔案複製到存放網站骨幹的資料夾下(也就是我們剛剛創的資料夾)

```bash
cp themes/even/config.toml . # copy config.toml to current directory
```

5. `config.toml` 是一個特殊的檔案，他定義了網站的各個參數 (如網站的標題，作者的favicon, 社交連結, 是否要 enable 某些特殊功能...等)，通常各個欄位後頭也都會解釋該參數的用途，我們可以視需求更改

  ![Customize-config](https://upload.cc/i1/2020/04/10/SeXAFd.png "Simple Customization")

完成了以上步驟後，我們已經有了一個網站雛型，可以用以下指令在 `http://localhost:1313/` 查看網站

```bash
hugo server -D
```

**注意**: `http://localhost:1313/` 這個網址其實是我們在 `config.toml` 的`baseURL` 欄位所定義的 (上圖中的第一行)，`localhost`是一個特殊的網址，只能在自己的電腦上查看

---

## 寫文 - 用 markdown 輕鬆寫文章
接著，我們要在網站上添加一些內容，並利用容易上手的 **markdown** 語法來生成 html。 \
本段落以建構分享科普文章的網站做為例子，可以簡便地放上數學方程式及有 highlighting 的程式碼。

首先，利用以下指令創建一篇新的文章

```bash
hugo new post/[文章名稱].md
```

下一步則是編輯文章，打開`content/post/[文章名稱].md` 做編輯 (這裡我取名叫Hello-world)

  ![Post-init](https://upload.cc/i1/2020/04/10/l4hwLi.png "一開始空空如也")

而 md 這個副檔名表示為 markdown ，可以用它的語法來寫文章 ([markdown語法教學](https://markdown.tw/))
這裡簡略地提幾個較為常用的

* \# : 標題相關
* \* : 粗體、斜體、列表
* \> : 引用
* \$ : 數學式
* \` : 程式碼 highlightling

舉[這篇文章](http://localhost:1313/hugo-kopo/post/hello-world/)為例，下圖展示了 markdown (下)與其生成的 html (上) 的差別，有沒有覺得markdown 簡單好讀非常多呢？😆

  ![Comarison-md-html](https://upload.cc/i1/2020/04/10/uckIaF.png "markdown vs html 大比較！")

完成編輯，並確認文章顯示符合我們心中所想後，把 `draft` 設成 `false`，如下圖

  ![Undraft](https://upload.cc/i1/2020/04/10/t4ecVR.png "Undraft")

---

## 部署 - 放到網路上，分享給全世界吧

到目前為止，我們已經有了網站的雛型，也知道了怎麼新增內容，最後一步便是將自己的作品放到網路上供大家瀏覽啦！這裡我們選用 GitHub 作為託管的平台 ~

1. 在 GitHub 上創建新的 Repository ，如下圖

  ![Create-repo](https://upload.cc/i1/2020/04/10/mCWRXH.png "創建新的 Repository")

2. 再來會看到 GitHub 請我們輸入的一串指令，這個指令是用來建立我們的電腦和這個平台的接口，用終端機輸入這串指令

  ![GitHub-init](https://upload.cc/i1/2020/04/10/YmGQOX.png "建立與 GitHub 間的接口")

3. 接下來的步驟為利用 git 開分支 (*branch*) 的功能，幫助我們分開管理 markdown 及 config 和生成的 html。
   如下圖，我們將 markdown 及 config 交由 `master` 分支管理，生成的 html 與網頁呈現相關的檔案則由 `gh-pages` 管理

  ![Git-branch](https://upload.cc/i1/2020/04/10/VkFxbJ.png "開不同分支管理網站")

   **注意**: 放在 `gh-pages` 上的檔案會被 GitHub 默認為要託管至其上的網站相關檔案

   因為利用到 git 較為複雜的功能，這個步驟為整篇教學中最困難的部份，但只要照著以下指令輸入便可以輕鬆完成

   ```bash
    # gh-pages 和 master 是完全獨立的兩分支
    git checkout --orphan gh-pages
    git reset --hard
    git commit --allow-empty -m "Initializing gh-pages branch"
    git push origin gh-pages
    git checkout master

    # publishdir 為用來存放 html 的資料夾 (名稱可以自訂，以下我用 public)，由 gh-pages 分支管理
    git worktree add -B gh-pages [publishdir] origin/gh-pages 
   ```

4. 在[建構網站](https://sunprinces.github.io/hugo-kopo/post/hugo-diy/#%E5%BB%BA%E6%A7%8B%E7%B6%B2%E7%AB%99)的段落曾提到，`baseURL` 為網站的網址，之前因為我們只在自己的電腦上查看，所以用 `localhost`，但現在我們要將網站託管至 GitHub，因此需要改成 GitHub 提供給我們的網址 (`https://[GitHub用戶名字].github.io/[Repository名字]`)

5. 最後一步則是利用 hugo 幫我們把 markdown 生成 html，並上傳到 GitHub

```bash
hugo # 生成 html
cd public # 進到放 html 的資料夾
git add --all # 把所有檔案加進 git 的版本控制
git commit -m "My first website 🙌"
git push origin gh-pages # 將更新推至 GitHub
```

大功告成！我們可以到 `https://[GitHub用戶名字].github.io/[Repository名字]` 查看我們的心血結晶了！😄

## 結語

在這篇文章中，我們利用 Hugo 幫我們快速建立了靜態網站，有興趣的讀者，可以到每個主題的官網，去看如何做更細部的客製化。雖然無可避免地要開始跟 html, css, javascript 這網頁三大元素打交道，但只要會 google ，幾乎都可以找到解答，又因為我們已經有了一個雛型供我們做修改，學習到的新技巧可以很快地呈現出來，學習回饋來的即時，也比較不會澆熄學習熱忱！

值得一提的是，這篇教學文就是用一樣的方法做出來的喔！

## 附錄

### 手把手影片教學
{{< youtube GrL5-vOGLX0 >}}

### 參考資料

* [Hugo 官網安裝教學](https://gohugo.io/getting-started/quick-start/), https://gohugo.io/getting-started/quick-start/
* [Markdown 官網語法教學](https://markdown.tw/)， https://markdown.tw/


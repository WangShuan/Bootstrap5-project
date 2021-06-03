# Bootstrap5 最終設計稿筆記

## 安裝 bootstrap 以修改特定樣式

要安裝有兩種方式 一個是使用 npm 另一個是進入官網點擊它的 Download 原始碼

npm 方式：

1. 創建你的項目資料夾 假設叫 bs5
2. 打開你的終端機 cd 到 bs5 資料夾
3. 輸入指令 `npm i bootstrap`

進官網下載方式：

1. 點擊進入[下載網址](https://bootstrap5.hexschool.com/docs/5.0/getting-started/download/)
2. 往下找到下載原始碼
3. 點擊後下載解壓縮
4. 找到裡面的 SCSS 資料夾把他拉到你的資料夾中使用

注意：
這裡要下載的不是 css 檔案而是 scss 檔案(要使用 scss 才能客製化編輯修改 bootstrap 的樣式)
所以這邊不能直接點擊首頁的下載 首頁的下載是編譯完成的 css 檔與 JS 檔

## 修改樣式

首先找到 scss/\_variable.scss 檔案 這支是修改變數的
在裡面會看到有一段代碼為：

```sass=
$theme-colors: (
"primary": $primary,
"secondary": $secondary,
"success": $success,
"info": $info,
"warning": $warning,
"danger": $danger,
"light": $light,
"dark": $dark,
) !default;
```

修改/添加 bootstrap 色系就在這邊

這裡依照設計稿 把 $secondary $dark $warning $danger 改成設計稿的顏色
如下：

```sass=
$theme-colors: (
"primary": $primary,
"secondary": #858377,
"success": $success,
"info": $info,
"warning": #FFDF65,
"danger": #FF785E,
"light": $light,
"dark": #636057,
) !default;
```

然後再設定 $body-color 為 #494846
(用 VS Code 在變數檔案中按 control + F 可以開啟搜尋，在搜尋框輸入 $body-color 就可以找到它)

另外 tooltips 的樣式也是從這裡直接修改 如下：

```sass=
$tooltip-color: $warning !default;
$tooltip-bg: $body-color !default;
```

## 字形

設計稿用 Noto Sans TC 做中文字， Baloo Tamma 2 做數字與一些英文字符號等。
我這邊載入 Google 字型的樣式 兩個字型放一起用｜符號隔開，空格改成加號即可。

這邊附上 [Google 下載字體的網址](https://fonts.google.com/)
在搜索框輸入你要找的字 然後點擊進入該字體會看到一排各種粗細的字 右邊有 + 號可以選擇 選完之後點擊畫面右上角三個正方行一個加號的 icon 按鈕就可以複製引入的代碼了～

貼到你的 head 中後就可以直接寫 font-family: "Noto Sans TC" 或 font-family: "Baloo Tamma 2" 了

這邊我直接單獨把 "Baloo Tamma 2" 做一個 class 來用

另外順便附上校長提供的 [Google Font 教學筆記](https://hackmd.io/@YmcMgo-NSKOqgTGAjl_5tg/ryar-vGOd/%2FbvLKze7nRU6kOa2jZxXDIg)

## 開始做

### header

首先因為這個頭部非滿版 但是他的背景跟下面邊框都是滿版的 所以先寫一個 div 設置背景跟邊框 然後裡面再寫一個 div 給他 container 的樣式 等等的 navbar 就放在 container 裡面～

設計稿的頭部 navbar 直接拿 bootstrap5 的元件複製貼上改一下就好 (還有手機版服務 超棒 XD)

所以我們來到[這裡](https://bootstrap5.hexschool.com/docs/5.0/components/navbar/) 複製貼上 再改一下字，完成 XD

LOGO 的部分就用 navbar-brand 這個 class 來套 裡面放 LOGO 圖片 設計稿有給 LOGO 寬高 可以直接寫在 img 標籤上

再來右邊有兩顆按鈕登入、註冊 這個就貼兩個 button 元件 然後改一下樣式即可 按鈕貼右邊可以使用 flex end 實現

然後整個 navbar 的下面是不是有一條 warning 色的邊框 那個請參考通用類別的邊框(按鈕的圓弧效果也可以在那邊找到使用方式)

這裡我就不詳細寫了 怕你們給我複製貼上 我會被校長飛踢 XD

### 最上面主要區塊

接著往下是一個標籤、一個標題，然後左邊圖片、右邊雜七雜八東西

這裡用格線系統，首先上面標題跟標籤的部分，我自己是直接設十二欄～
然後左邊圖片佔七欄 右邊鬼東西佔五欄～可以參考[這個](https://drive.google.com/file/d/1mFN6FTRijd2tT2gfFqK4Yxw9LRKWOl86/view)
這邊圖片是圓弧狀的 所以需要加上圓弧邊框不然四個角落會出現白色區塊

再來講一下雜七雜八那塊有一個<span
    class="main">『專案募資中！...後一百字省略』的區塊，這邊可以[參考這個](https://bootstrap5.hexschool.com/docs/5.0/customize/components/#creating-your-own)
我自己是直接設 border bg-white 等等實現啦 但在嗑 bootstrap5 客製化教學影片的時候剛好看到這個(後悔莫及) 給各位拿去配～

其他要注意的是 hover 效果，在雜七雜八那邊有四個小 icon 分別是 認證、品質、原生、人氣 這裏的 hover 效果請使用 [tooltips 元件](https://bootstrap5.hexschool.com/docs/5.0/components/tooltips/) 要記得加入 JS 代碼把它初始化才有正確效果～

### nav&tab 的 nav

再來繼續往下是 nav&tab 頁籤功能～
這裡因應設計稿我是把它做成同一頁，如果同學堅持想做四頁用 href 連結也可以哩！但我不負責教學 XD

首先用一個 div 把 nav 包起來 給 div 加上 position-sticky 讓 nav 往下滾動後可以黏在頭部～～ 順便也給 div 上下加邊框～～ <span
    class="main">這邊要請同學加一段手寫的樣式 z-index 999

然後請自己手寫 active 的那個下底線樣式 我是寫這樣 給你們參考：

```sass=
.nav .active {
  font-weight: bold;
  border-bottom: 2px solid #ffc107;
}
```

### nav&tab 的 tab - 專案內容

nav 先這樣 往下來說 tab 的部分 這裏我目前只做 tab 第一個專案介紹
這邊我設專案介紹那區塊佔 8 欄 另外一堆逼人贊助的卡片佔 4 欄
然後這裡我在 row 身上有設大 gutter (g-5) 因為我看設計稿兩個區塊的鴻溝 48px ～

再來講裡面內容的部分 那一堆像佛經的文字部分在設計稿用 justify 對齊 但 bootstrap 只有對齊左右跟置中 沒有 justify 所以這裡要去 `_utilities.scss` 改一下 如下：

```sass=
"text-align": (
  responsive: true,
  property: text-align,
  class: text,
  values: (
  start: left,
    end: right,
    center: center,
    justify: justify // 加這行
  )
),
```

剩下應該沒啥好說的圖片記得加 img-fluid ～

### 最下方表單 form

下一個部分是表單～因為他也佔 8 欄 我是直接寫在 tab 的那個 8 欄裡面

表單一開始的 icon 手手愛心那個，用 flex 加上水平置中就可以做了～這應該沒問題吧！

再來標題那個 贊助專案 左右加水平線那個，你們給我自己搞，我每日任務出過了！不會的我一個人圍毆你！

上面兩個東西弄完開始正式做表單 首先要用 form 標籤～ 在 form 標籤裡面就可以開始放 label + input 了～
我們可以直接到[表單概觀](https://bootstrap5.hexschool.com/docs/5.0/forms/overview/)這邊複製範例過來～

第一個贊助方案是 select 標籤！這邊我隨便做三個 option 分別叫 方案一二三～ 代碼大概長這樣：

```htmlembedded=
<label for="project" class="form-label">贊助方案</label>
<select class="form-select" id="project">
    <option selected="">請選擇一個方案</option>
    <option value="1">方案1</option>
    <option value="2">方案2</option>
    <option value="3">方案3</option>
</select>
```

form-\* 的 class 請不要忘記加 不然會導致無法對齊 畫面變得很醜～！

說明一下：label 的 for 屬性是用來綁定跟對齊的～ 一個 label 通常對應一個 input 或 select 並且這邊是使用 id ～ 這部分跟 bootstrap 無關
單純是 label 標籤的特性。

這邊記得加表單驗證！！！
主要是在 form 標籤身上加 class `.needs-validation` 然後加一個屬性 `novalidate`(取消預設的 HTML5 驗證)
再來是裡面的 input 跟 select 加上 required 屬性 表示這些欄位必填 沒填驗證會失敗出現警告這樣
最後就在表單的按鈕加上 type="submit" 然後貼上 form 表單驗證的 js 即可～

```javascript=
(function () {
  "use strict";
  var forms = document.querySelectorAll(".needs-validation");
  Array.prototype.slice.call(forms).forEach(function (form) {
  form.addEventListener(
    "submit",
    function (event) {
      if (!form.checkValidity()) {
        event.preventDefault();
        event.stopPropagation();
      }
      form.classList.add("was-validated");
    },
    false
    );
  });
})();
```

然後其他沒要注意的了 下一題～

### 下方右邊逼人贊助專案的卡片區

下一題是那個一直逼人贊助的卡片區塊～～

說明一下因為這個區塊他到時候是黏在右上角 可以滾動 且跟左邊 tab 區塊的滾動是分開的 所以要另外設置高度 overflow 跟 position

首先這邊是一個 col-5 然後裡面先給一個 div 這個 div 給他設高度 讓他高度為螢幕高減去 nav 的高度 這邊可以使用 `calc(100vh - xxx)`
calc() 方法是 CSS3 出的 它可以用來加減乘除各種不同單位的數字 要記得在運算符號左右留空白 如果你沒留空白就無法計算會報錯～然後 100vh 是指螢幕高度 100% ～設完高度後給他加上 overflow-auto
讓他超過高度的地方可以滾動～

然後再給他加上 position-sticky 把它黏在 nav 的下面～這裡可能也是需要手寫計算 top 設多少～～
再來就可以直接在 div 裡面加入卡片元件了～基本上也沒啥大問題好說，圖片圓形的部分也是參考通用類別的邊框即可找到～

然後第一個卡片缺錢事務所裡面的 icon 是用 font-awesome ～ 這邊需要自己手寫樣式設定一個圓形的背景 gray 的區塊放 icon 才有辦法達到設計稿的效果～
sabisu 給你們看我的代碼：

```htmlembedded=
<div class="bg-secondary rounded-circle text-center me-2" style="width: 30px;height: 30px;">
    <i class="fab fa-facebook-f text-white lh-lg"></i>
</div>
```

### footer

ok 最後就我們的 footer 了背景色跟 $body-color 是同色的～啊這邊要注意一下，我不知道你們有沒有遇到這個問題，就是<span
    class="main">在設計稿點擊文字可以複製內容，但我點擊 footer 的那行字 複製後都長這樣：
Copyright � 拼拼 All rights reserved.
所以貼心的 me 手動幫你們補一下：

```
Copyright © 拼拼 All rights reserved.
```

## JS 代碼部分

### 點擊 nav 切換頁籤時滾到 tab 區塊效果

請在每個 nav 的 li 的 a 連結身上加這個 `onclick="goToTab()"`

然後在 body 標籤最下面加上新的 `script` 標籤
並將下面代碼加入到 `script` 標籤中：

```javascript=
function heightToTop(ele) {
  let bridge = ele;
  let root = document.body;
  let height = 0;
  do {
    height += bridge.offsetTop;
    bridge = bridge.offsetParent;
  } while (bridge !== root);

  return height;
}
function goToTab() {
  window.scrollTo({
    top: heightToTop(document.getElementsByClassName("tab-content")[0]) - 70,
    behavior: "smooth",
  });
}
```

### 手機版點擊按鈕滾到表單區塊效果

請先在手機版新增一個贊助專案按鈕 寬度 100% 並取消圓角 然後給該按鈕加上 `id="bottomBtn" onclick="goForm()"`
再給表單加上 `id="form"`

然後在剛才的 script 標籤加入以下代碼：

```javascript=
function goForm() {
  window.scrollTo({
    top: heightToTop(form) - 170,
    behavior: "smooth",
  });
}

var bottomBtn = document.getElementById("bottomBtn");
bottomBtn.style.display = "none";
window.onscroll = function () {
  const t = document.documentElement.scrollTop || document.body.scrollTop;
  if (bottomBtn !== null) {
    if (
      t >
        heightToTop(document.getElementsByClassName("tab-content")[0]) - 100 &&
      t < heightToTop(form)
    ) {
      bottomBtn.style.display = "block";
    } else {
      bottomBtn.style.display = "none";
    }
  }
};

```

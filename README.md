Node.js Learn<br>
自主學習Node.js的觀念和指令後做的統整&學習筆記
===

## 目錄
- [自主學習Node.js的觀念和指令後做的統整&學習筆記](#自主學習nodejs的觀念和指令後做的統整學習筆記)
  - [目錄](#目錄)
    - [安裝方式](#安裝方式)
      - [Windows 系統](#windows-系統)
      - [MacOS 系統](#macos-系統)
      - [Linux 系統 (以 Ubuntu 為例)](#linux-系統-以-ubuntu-為例)
    - [Node.js 核心觀念](#nodejs-核心觀念)
      - [Introduction to Node.js](#introduction-to-nodejs)
      - [A brief history of Node.js](#a-brief-history-of-nodejs)
      - [How to install Node.js?](#how-to-install-nodejs)
      - [How much JavaScript do you need to know to use Node.js?](#how-much-javascript-do-you-need-to-know-to-use-nodejs)
      - [Differences between Node.js and the Browser](#differences-between-nodejs-and-the-browser)
      - [The V8 JavaScript Engine](#the-v8-javascript-engine)
      - [Run Node.js scripts from the command line](#run-nodejs-scripts-from-the-command-line)
      - [How to exit from a Node.js program?](#how-to-exit-from-a-nodejs-program)
    - [Node.js 核心模組](#nodejs-核心模組)
      - [HTTP](#http)
    - [參考資料來源](#參考資料來源)
      - [官方文件](#官方文件)
      - [網路文章](#網路文章)
      - [網路影片](#網路影片)




---
### 安裝方式
- 官方網站會先分成LTS.Current兩個版本
  + `LTS`(Long-term support): Recommended for most users
  + `Current`: Latest features
- 安裝Node.js之後,也會自動安裝NPM
- 若想要安裝指定版本的Node.js,可以輸入以下指令
  + $ `brew install node@<specific version>`
    * 例: `brew install node@10`
  + 可參考[How to install specific NodeJS version](https://medium.com/@katopz/how-to-install-specific-nodejs-version-c6e1cec8aa11)
- 若想要安裝指定版本的NPM(Node Package Manager),可以輸入以下指令
  + 升級到Latest version: `npm install -g npm@latest`
  + 升級到Most recent release version: `npm install -g npm@next`
  + 可參考[Try the latest stable version of npm](https://docs.npmjs.com/try-the-latest-stable-version-of-npm)
- 如果想要在同一台電腦上面,切換Node的版本,可以安裝NVM(Node Version Manager)
  + **MacOS**
    * $ `brew install nvm`
  + **Linux**
    * $ `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash`
  + 接下來要到(~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc)的其中一個檔案,新增以下3行指令**到該檔案的最下面**
    * `export NVM_DIR="$HOME/.nvm"`<br
      `[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"`  # This loads nvm<br>
      `[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"`  # This loads nvm bash_completion<br>
  + 檢查是否正常安裝NVM
    * $ `command -v nvm`: 如果有成功安裝NVM的話,應該要回傳`nvm`
  + 檢查安裝的NVM版本
    * $ `nvm --version` 
  + 可參考[Node Version Manager](https://github.com/nvm-sh/nvm#troubleshooting-on-macos)


#### Windows 系統
  + 連結: https://nodejs.org/en/download/
  + 安裝完成後,可以用CLI指令檢查 **Node** & **NPM**的版本
    * $ `node --version` 
    * $ `npm --version`
#### MacOS 系統
  + 連結: https://nodejs.org/en/download/package-manager/#macos
    * 指令: `brew install node`
  + 安裝完成後,可以用CLI指令檢查 **Node** & **NPM**的版本
    * $ `node --version` 
    * $ `npm --version`
#### Linux 系統 (以 Ubuntu 為例)
  + 連結: https://github.com/nodesource/distributions/blob/master/README.md
  + 指令: 
    * $ `sudo apt-get install -y nodejs`

---
### Node.js 核心觀念
#### Introduction to Node.js
`先備知識`
> `One process`: 一個全域的Object,可以在任何地方被執行,並保有執行時的資料<br>
> `One thread`: single-thread,在一個`process`中只能執行一件事<br>
> `One event loop`: 一個事件迴圈,因為它使Node可以是非同步(asynchronous) & 非阻塞I/O(non-blocking I/O); 因為Node是single-thread的,透過callback.Promise.async/await能將工作分散給system kernel<br>
> `One JS Engine Instance`: 一個Javascript實例,用來執行Javascript的程式碼<br>
> `One Node.js Instance`: 一個Node實例,用來執行Node的程式碼<br>

- Node是一個免費.開源.跨平台的Javascript執行環境,讓開發者可以在瀏覽器以外也能使用Javascript
  + 也因此讓廣大的前端開發者們,可以加入後端開發的行列,並且不用因此需要多學一門程式語言 
- Node是基於Chrome瀏覽器的V8引擎來建立出的執行環境,因此能有非常好的效能
- Node是由開源社群來共同維護,並且能使用最新的ECMAScript標準
  + 因此不必等待所有用戶更新他們的瀏覽器,就可以選擇要使用的Node版本來達到來決定要使用哪個ECMAScript版本
  + 可參考官方文件[ECMAScript 2015 (ES6) and beyond](https://nodejs.org/en/docs/es6/) 
- Node應用程式在單個進程(single process)中運行,無需為每個請求建立新線程(thread),能處理數千個併發連接(concurrent connections),也不會因此而增加管理線程(thread)上的負擔
  + 同時Node也在其標準函式庫中提供了一組非同步I/O原語(asynchronous I/O primitives)來防止Javascript的程式碼被阻塞住,因此在Node中使用非阻塞式語法(non-blocking paradigms)來開發是正常且普遍的
  + 當Node執行會有I/O的操作(e.g. 從網路上讀取資料.存取資料庫or檔案系統)時,Node會自動在response回傳時才恢復操作,而不是無效地阻擋住線程和浪費CPU週期等待時間
- 受惠於npm的簡單結構,其促使Node生態系可以蓬勃地發展,目前在npm上已經有超過1,000,000個開源軟體&工具可供使用
- Node.js算是一個低階的平台,然而在社群(community)上有數千個函式庫與好用的框架建構於Node.js之上
- 範例程式碼
  + ```javascript
    const http = require('http');

    const hostname = '127.0.0.1';
    const port = process.env.PORT;

    const server = http.createServer((req, res) => {
        res.statusCode = 200
        res.setHeader('Content-Type', 'text/plain')
        res.end('Hello World!\n')
    });

    server.listen(port, hostname, () => {
      console.log(`Server running at http://${hostname}:${port}/`)
    });
    ```
  + 以上程式碼會建立一個新的http server並回傳,同時這個server也會監聽指定的port & host name
  + 當server準備就緒時,將執行callback function,在這時也會通知我們server正在運行中
  + 每當收到一個新的request時,都會呼叫該request event,並提供兩個物件(objects)
    * 請求物件(request): `http.IncomingMessage`
      * 它會提供request details 
    * 回應物件(response): `http.ServerResponse`
      * 它會用來將data回傳給呼叫request event的那方
  + 在這種狀況下, 我們會將狀態碼設定為200,以表示該request成功<br>
    => `res.statusCode = 200`
  + 並設定Content-Type標頭<br>
    => `res.setHeader('Content-Type', 'text/plain')`
  + 最後,會關閉response,並將內容作為參數添加到res.end()中<br>
    => `res.end('Hello World\n')`

#### A brief history of Node.js
- Node.js最初是由Ryan Lienhart Dahl,於2010/05月初次發表,相比於Javascript(1995/12月)與網際網路的誕生(1989年)來說,在技術領域中,並不算是很長的時間,但目前看來Node會持續存在下去
  + <img src="./pic/NodeJS%20logo.png" width="500px" /><br>
  + <img src="./pic/NodeJS作者%20Ryan%20Lienhart%20Dahl.jpg" width="500px" /><br>
- 受惠於[瀏覽器的效能競爭戰](https://zh.wikipedia.org/wiki/%E6%B5%8F%E8%A7%88%E5%99%A8%E5%A4%A7%E6%88%98#Google_Chrome%E7%9A%84%E5%B4%9B%E8%B5%B7%E8%88%87Internet_Explorer%E7%9A%84%E8%A1%B0%E8%90%BD)(2003~2008年)後的結果,各家瀏覽器供應商爭相為用戶提供最佳性能,Javscript engine的運行效能也越來越好,而Node使用的Chrome瀏覽器的Javascript engine---V8,在性能上也有卓越的提升
- 另一個使Node快速崛起的關鍵因素是[Web2.0](https://zh.wikipedia.org/wiki/Web_2.0)的誕生,例如Flickr.Gmail等,讓Javascript開始被視為一個更為重要的程式語言
- Node恰巧是在正確的時間和正確的時間構建的,它為JavaScript服務器端開發引入了許多創新思維和方法,這些方法和方法已經為許多開發人員提供了幫助,這就是為什麼它開始流行的原因
- Node.js 簡史(Change log)
  + 西元2009年
    * [Node.js](https://nodejs.org/en/)誕生
    * 最初版[npm](https://www.npmjs.com/)問世
  + 西元2010年
    * [Express.js](https://expressjs.com/)框架 誕生
    * [socket.io](https://socket.io/) 誕生
  + 西元2011年
    * npm 發布1.0版本
    * 許多大型公司開始採用Node.js,例:LinkedIn.Uber等
  + 西元2012年
    * 越來越多人開始採用Node.js
  + 西元2013年
    * 第一個使用Node.js的大型部落格平台: [Ghost](https://ghost.org/)
    * [koa](https://koajs.com/)框架 誕生
  + 西元2014年
    * 重大事件: [io.js](https://socket.io/)誕生,是Node.js的主要Fork出來的專案,目的是為了加入Javascript的ES6語法支援並提升了效能 
  + 西元2015年
    * [Node.js基金會](https://openjsf.org/)誕生 (目前隸屬於OpenJS Foundation旗下的其中一個專案)
    * io.js合併回Node.js專案中
    * npm開始推出私有模組(private modules)
    * Node.js 4發布(直接跳過Node.js 1,2,3)
      * 可參考[Node_changelog](https://github.com/nodejs/node/blob/master/CHANGELOG.md)
  + 西元2016年
    * kik模組的left-pad事件爆發,引起開源社群的一陣騷動
    * [Yarn](https://classic.yarnpkg.com/en/)套件管理包工具 誕生
    * Node.js 6發布
  + 西元2017年
    * npm開始更加注重安全性
    * Node.js 8發布
    * [HTTP/2 核心模組](https://nodejs.org/api/http2.html) 發布
    * V8將Node加入它的測試套件中,使Node成為繼Chrome之後的Javascript engine正式目標
    * 達成30億次/週的下載流量紀錄
  + 西元2018年
    * Node.js 10發布
    * [ES modules.mjs](https://nodejs.org/api/esm.html)開始加入實驗性支援(experimental support)
    * Node.js 11發布
  + 西元2019年
    * Node.js 12發布  
    * Node.js 13發布
  + 西元2020年
    * Node.js 14發布
    * Node.js 15發布

#### How to install Node.js?
- Node有很多種安裝方式,最常見的方式是透過套件管理包(package manager)下載,在這種情況下,每個作業系統有自己的安裝方式
  + 可參考[安裝方式](#安裝方式)的章節
- NVM(Node Version Manager)是一種執行Node.js的流行方法
  + nvm讓我們可以輕鬆切換Node版本
  + 假如碰到錯誤時,可以安裝新版本以嘗試輕鬆地回滾(rollback)
  + nvm也是個有效的工具讓我們可以輕鬆地使用Node的舊版本來測試我們的程式碼
  + 可參考[Node Version Manager(nvm)](https://github.com/nvm-sh/nvm)
- 如果使用macOS,推薦使用[Homebrew](https://brew.sh/)來安裝Node
- 當安裝完Node之後,就可以使用`$ node xxx.js`在CLI中執行Node程式

#### How much JavaScript do you need to know to use Node.js?
- 身為一個初學者,我們常常難以判斷要到什麼樣的程度才是對程式設計的能力足夠有自信的
- 當我們剛開始學習Javascript,我們可能會對Javascript的結束位置,以及Node的起始位置與結束位置感到很困惑
- 建議先理解Javascript的主要觀念後,在開始投入於Node的研究中
- 以下是Javascript目前的主要觀念
  + 詞彙結構(Lexcial Structure)
  + 運算式(Expressions)
  + 型別(Types)
  + 變數(Variables)
  + 函式(Functions)
  + `this` 關鍵字
  + 箭頭函式(Arrow Functions)
  + 迴圈(Loops)
  + 範圍(Scopes)
  + 陣列(Arrays)
  + 模板文字(Template Literals)
  + 分號(Semicolons)
  + 嚴謹模式(Strict Mode)
  + ECMAScript 6,7,8 (手稿語言規範)
- 如果能將以上的Javascript主要觀念都掌握到的話,無論是在瀏覽器還是在Node中,您都將成為一名熟練的JavaScript開發人員
- 以下是理解**非同步程式設計**的(asynchronous programming),這也是Node.js的基本觀念之一
  + [非同步程式設計](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)與[回呼](https://developer.mozilla.org/zh-TW/docs/Glossary/Callback_function) (Asynchronous programming and callbacks)
  + [計時器](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Timeouts_and_intervals) (Timers)
  + [Promise物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise) (ES6以後開始加入的語法)
  + [Async & Await](https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/Asynchronous/Async_await)
  + [閉包](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Closures)(Closures)
  + [事件迴圈](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/EventLoop) (The Event Loop)

#### Differences between Node.js and the Browser
- 瀏覽器與Node.js都是使用Javascript程式語言來開發的
- 建構出一個運行在瀏覽器的應用程式與建構出一個運行在Node的應用程式完全不同; 儘管都是使用Javascript程式語言來開發,卻仍存在一些關鍵差異,使體驗完全不同
- Node改變的是整個生態系統(ecosystem),因為它讓我們可以使用一種程式語言-Javascript,就可以完成我們所有的網頁開發工作(包含前端 & 後端),這是一個獨特的優勢地位
- 在瀏覽器中,我們花費大多數的時間在與[DOM](https://developer.mozilla.org/zh-TW/docs/Glossary/DOM)或是其他網頁平台的APIs(例: Cookies)。 當然,這些東西並不存在於Node之中。Node也不會有[Document物件](https://developer.mozilla.org/zh-TW/docs/Web/API/document)與[Window物件](https://developer.mozilla.org/zh-TW/docs/Web/API/Window)以及其他所有透過瀏覽器提供的物件們
- 在瀏覽器中,我們沒有那些Node透過其內建模組所提供的實用APIs(例: [文件系統訪問功能](https://nodejs.org/api/fs.html) (filesystem access functionality))
- 另一個比較大的差異是在Node中,我們控制的是**環境**,除非您構建一個任何人都可以在任何地方部署的開源應用程式,否則我們通常會知道應該在哪個版本的Node上運行該應用程式; 但是在瀏覽器的環境中,我們無法選擇使用者會使用的瀏覽器,這點非常不方便
  + 這也意味著我們可以使用該Node版本可支援的所有ECMAScript 6-7-8-9的現代化Javascript語法
- 由於Javascript的變化如此之快,但是瀏覽器與使用者所使用的瀏覽器並沒有這麼迅速的升級,因此我們不得不使用較舊的JavaScript/ECMAScript版本
  + 這時我們可以使用[Babel](https://babeljs.io/)來將程式碼轉換成可與ES5可相容的語法,然後再交給瀏覽器
  + 然而在Node中,我們並不需要這樣做
- 還有一個重大的差異是在Node中,我們使用的是CommonJS模組系統; 但是在瀏覽器中,我們會依照ECMAScript的模組標準來實作Javascipt語法
  + 實際上,這代表我們會分別使用
    * require() => 在Node.js中
    * import => 在瀏覽器中  


#### The V8 JavaScript Engine
- [V8](https://v8.dev/)是用來支持Google Chrome瀏覽器的Javascript engine。當我們使用Chrome瀏覽器時,它需要我們的Javascript程式碼並執行它們 
- V8負責提供Javascript執行時所需要的執行環境(runtime)。`DOM`和其他的Web APIs則由瀏覽器負責提供
- Javascript engine是能獨立運作的,並不一定需要跟隨著託管(hosted)它的瀏覽器,這也促使Node的興起
- 西元2009年時,V8被選為用來作為Node.js的Javascript engine,並且隨者Node的爆炸性成長,V8成為了現在為大量使用Javascript編寫伺服器端程式碼(server-side code)的engine
- Node生態系非常龐大,受惠於此,V8也支援桌面應用程式(例: [Electron](https://www.electronjs.org/))
- 其他瀏覽器使用的Javascript engine
  + Firefox: [SpiderMonkey](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey)
  + Safari: [JavaScriptCore(也被稱為Nitro)](https://developer.apple.com/documentation/javascriptcore)
  + Microsoft Edge: 最初是基於[ChakraCore](https://github.com/Microsoft/ChakraCore)開發的,後來轉由基於[Chromium](https://www.chromium.org/) & V8 engine來重構
    * 可參考[Download the new Microsoft Edge based on Chromium](https://support.microsoft.com/en-us/microsoft-edge/download-the-new-microsoft-edge-based-on-chromium-0f4a3dd7-55df-60f5-739f-00010dba52cf)  
- V8引擎是由C++程式語言所編寫。它是可攜帶式的(portable),可提供跨平台支援(on macOS &Windows & Linux ...等等)
  + V8也與其他的Javascript engine一樣,V8也在持續改進中,也加速了Web和Node生態系的快速發展; 多年來,在網路上有很多關於性能調校的競賽,身為開發者和使用者的我們也受惠於此,讓我們能擁有更快.效能更好的機器(machines)可以使用
- Javascript通常被認為是一種直譯式語言(interpreted language),但是在現代化的Javascript engine中,已不再只是直譯Javascript,它們也編譯Javascript
  + 從西元2009年開始,當SpiderMonkey JavaScript compiler被加入到Firefox瀏覽器 v3.5之中以後,每個人都開始追隨這種做法
  + Javascript會被V8 engine進行內部即時編譯(just-in-time compilation, JIT)以加快執行速度; 這可能是一種違反直覺的方式,但是從2004年引入Google Maps以來,Javascript已經從一種通常用來執行幾十行程式碼的小型應用程式的程式語言,逐漸發展成可以在瀏覽器中執行成千上萬行的大型.完整的應用程式的程式語言
  + 演變至今,我們的應用程式已經可以在瀏覽器持續執行數小時,而這也不僅限於單純的表單驗證規則(a few form validation rules)或是簡單的程式碼(simple scripts)
  + 在現代的新世界中,"編譯"Javascript是非常有意義的,因為雖然編寫Javascript仍然需要花費很多時間,但是一旦開發完成後,它將比起純直譯程式碼來的擁有更好的效能

#### Run Node.js scripts from the command line
- 當我們安裝好Node.js後,通常我們會用可在全域執行的`node`指令,接著傳遞要執行的檔名作為參數到CLI上
  + 假設我們的主要Node應用程式的檔名叫做`app.js` 
  + 例: $ `node app.js`
  + 提醒: 要在包含`app.js`的檔案路徑下執行該指令才行

#### How to exit from a Node.js program?
- 有多種方法可以終止Node應用程式
  + CLI: $ `ctrl-C`
  + 程式碼: `process.exit()`
  + 程式碼: `process.on('SIGTERM', callback function)`
- Node的核心模組-[Process](https://nodejs.org/api/process.html)提供了一個簡便的方法,讓我們可以從一個Node應用程式退出,可執行以下的command
  + $ `process.exit()`
  + 當Node執行到這邊時,該進程(process)就會被立即強致終止。這代表任何處於`pending狀態`的`callback function`與任何網路請求(network request)仍然會被傳送出去; 然而任何訪問文件系統(`filesystem`)或是進程(`process`),例如: [process.stdout()](https://nodejs.org/api/process.html#process_process_stdout) 或是 [process.stderr](https://nodejs.org/api/process.html#process_process_stderr)都將立刻被不正常地終止(ungracefully terminated right away.)
  + 如果這樣是我們想要的結果,那我們可以傳遞一個整數,以此作為像作業系統發出的退出碼(exit code)
    * 例: $ `process.exit(1)`
    * 補充: 退出碼(exit code)
      * 預設值: 0 (代表成功) 
      * 當`exit code` <= 0 時,表示指令執行成功
      * 當`exit code` > 0 時,表示指令執行失敗
    * 不同的退出碼具有不同的意義,我們可以利用這些退出碼來讓我們系統中的"程式與程式"之間能互相溝通
    * 可參考[Node核心模組-Process的 Exit codes 章節](https://nodejs.org/api/process.html#process_exit_codes)
  + 我們也可以設定process.exitCode屬性來指定當Node應用程式退出時,要回傳什麼退出碼
    * 使用process.exitCode的情境,需滿足以下條件
      * 當使用process.exit([code]) -> 且未指定退出碼時
      * 進程(process)正常地終止(exits gracefully)時
    * 例: $ `process.exitCode = 1`
    * 當Node應用程式終止時,將會return該退出碼,在完成處理所有進程(process)後,Node應用程式將會正常地退出
    * 可以利用`process.exit([code])`來推翻掉(override)先前的`process.exitCode`的設定值
  + 另一種常見的情況是當我們啟動一個伺服器,例如: HTTP server
    * ```javascript
        const express = require('express')
        const app = express()

        app.get('/', (req, res) => {
          res.send('Hi!')
        })

        app.listen(3000, () => console.log('Server ready'))
      ```
    * 以上的程式永遠不會終止! 如果我們呼叫`process.exit()`,這時正在處理的pending與running request都將被終止,而這不是一個好的做法
    * 這時候比較好的解決方法是對該command發出`SIGTERM`信號(signal),並使用process模組的signal handler來進行處理
      * 可參考[Signal events](https://nodejs.org/api/process.html#process_signal_events)
    * ```javascript
        const express = require('express')
        const app = express()
        app.get('/', (req, res) => {
          res.send('Hi!')
        })

        const server = app.listen(3000, () => console.log('Server ready'))

        process.on('SIGTERM', () => {
          server.close(() => {
            console.log('Process terminated')
          })
        })
      ``` 
    > Q: 什麼是信號(signals)?<br>
      A: 信號是[POSIX](https://zh.wikipedia.org/wiki/%E5%8F%AF%E7%A7%BB%E6%A4%8D%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F%E6%8E%A5%E5%8F%A3)的相互通訊系統: 當通知(notification)被發送到一個進程(process),以便將發生的事件(event)通知給進程(process)
    * `SIGKILL`是告訴進程(process)立即中止的信號
    * `SIGTERM`是告訴進程(process)正常終止的信號。這是從例如[upstart](http://upstart.ubuntu.com/) & [supervisored](http://supervisord.org/)等其他流程管理工具發出的信號
    * 我們也可以在應用程式中的另一個函式中,發出這個信號
      * $ `process.kill(process.pid, 'SIGTERM')`
      * 也可以從其他執行中的Node應用程式or其他在我們的作業系統中正在執行的應用程式,來得知我們想要終止的應用程式的ID(process ID, pid)


---
### Node.js 核心模組
#### [HTTP](https://nodejs.org/api/http.html)
> method
  + [http.createServer([options][, requestListener])](https://nodejs.org/api/http.html#http_http_createserver_options_requestlistener)<br>
    * 會回傳一個 http.Server 實例
    * options
      * http.IncomingMessage
      * ServerResponse
      * insecureHTTPParser (Default: false)
      * maxHeaderSize (Default: 16384 (16KB)
    * requestListener (Function)
> Class
  + [Class: http.IncomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage)
    * 這個Class物件會由http.server與http.ClientRequest所建
    * 它是用來作為被傳給request event & response event的第1個參數
    * 它會被用來存取回應物件的狀態(response status),標頭(response headers),資料(response data)
  + [Class: http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse)
    * 這個Class物件會由HTTP server內部自動建立,而不是透過user來建立的
    * 它是用來作為被傳給request event的第2個參數
    > property
      * [response.statusCode](https://nodejs.org/api/http.html#http_response_statuscode)
        * 當使用隱式標頭(implicit headers)時,也就是當沒有明確地使用[response.writeHead()](https://nodejs.org/api/http.html#http_response_writehead_statuscode_statusmessage_headers)時,這個屬性會在headers被更新時決定要傳給client端什麼狀態碼(status code)
        * 當回應標頭(response header)已經傳到client端之後,這個屬性會指出已經發送出去的狀態碼
        * 預設是200 (number型別)
        * 例: `response.statusCode = 404;`
    > method
      * [response.setHeader(name, value)](https://nodejs.org/api/http.html#http_response_setheader_name_value)
        * args
          * name: (string)
          * value: (any)
          * Returns: [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse)  
        * 回傳一個回應物件(response object)
        * 為隱式標頭(implicit header)設定一筆單一的值,若此標頭已經存在於待發送的header中,那麼待發送header的值就會被取代掉
        * 若要發送為同一個名稱的多個header時,可以用一個Array['xxx', 'yyy']來包住所有的header值
          * 如果輸入非字串型別的值,將自動被儲存下來,而無須多做修改
          * 當header的name或是value包含無效的字元時,就會引發TypeError錯誤
        * 例: `response.setHeader('Content-Type', 'text/html');`
        * 例: `response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);`
        * 當headers被設定為使用response.setHeader(),它們將會被合併到其他所有要傳給
        [response.writeHead()](https://nodejs.org/api/http.html#http_response_writehead_statuscode_statusmessage_headers)的headers,並且會自動將要傳給response.writeHead()的headers列為優先
          * 若需要逐步新增headers,讓未來有需要的話可以檢索和修改,請使用response.setHeader(),而不要使用response.writeHead()
        * ```javascript
          // Returns content-type = text/plain
          const server = http.createServer((req, res) => {
            res.setHeader('Content-Type', 'text/html');
            res.setHeader('X-Foo', 'bar');
            res.writeHead(200, { 'Content-Type': 'text/plain' });
            res.end('ok');
          });
          ```
      * [response.end([data[, encoding]][, callback])](https://nodejs.org/api/http.html#http_response_end_data_encoding_callback
        * args
          * data: (string || Buffer)
          * encoding: (string)
          * callback: (Function)
          * Returns: (this)
        * 這個方法會向server發送信號,表示所有的回應標頭(response header)和內文(body)皆已發送出去,這時server應認定該請求消息已完成
        * response.end()需要在每個回應的**結尾**都使用它
        * 如果data參數有給定的話,它實際上是去呼叫[response.write(data, encoding)](https://nodejs.org/dist/latest-v15.x/docs/api/http.html#http_response_write_chunk_encoding_callback),並接著執行res.end(callback)
        * 如果callback函式有給定的話,該callback函式會在回應串流(response stream)結束之後才會被呼叫並執行


---
### 參考資料來源
#### 官方文件
- [Node.js](https://nodejs.org/en/)
- [Node Package Manager(NPM)](https://www.npmjs.com/)
- [Node Version Manager(NVM)](https://github.com/nvm-sh/nvm)
- [Express.js](https://expressjs.com/)

#### 網路文章
- [Understanding Worker Threads in Node.js](https://vagrantpi.github.io/2019/11/01/understanding-worker-threads-in-Node.js)
- [深入理解 Node.js 的設計錯誤 — 從 Ryan Dahl 的演講中反思](https://medium.com/rytass/%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3-node-js-%E7%9A%84%E8%A8%AD%E8%A8%88%E9%8C%AF%E8%AA%A4-%E5%BE%9E-ryan-dahl-%E7%9A%84%E6%BC%94%E8%AC%9B%E4%B8%AD%E5%8F%8D%E6%80%9D-cedbf32cb188)

#### 網路影片
- [10 Things I Regret About Node.js - Ryan Dahl - JSConf EU](https://www.youtube.com/watch?v=M3BM9TB-8yA&feature=emb_logo)

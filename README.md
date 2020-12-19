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
      - [How to read environment variables from Node.js?](#how-to-read-environment-variables-from-nodejs)
      - [How to use the Node.js REPL?](#how-to-use-the-nodejs-repl)
      - [Node.js, accept arguments from the command line](#nodejs-accept-arguments-from-the-command-line)
      - [Output to the command line using Node.js](#output-to-the-command-line-using-nodejs)
    - [Node.js 核心模組](#nodejs-核心模組)
      - [HTTP](#http)
      - [Process](#process)
      - [Console](#console)
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

#### How to read environment variables from Node.js?
- `process`核心模組提供了`env`屬性,`process.env`屬性會託管當啟動Node進程(process)的時候的所有Node環境變數
- 以下是一個預設在`development`環境下,存取`NODE_ENV`這個環境變數的範例
  + 提醒: 因為它是Node的核心模組,所以`process`模組不需要事先匯入(`require()`),可以直接開始使用
  + ```javascript
      process.env.NODE_ENV // "development"
    ```
- 當在腳本(script)執行之前,可以先將該屬性設定為`production`,來告訴Node這是一個`production`的生產環境
  + ```javascript
      process.env.NODE_ENV // "production"
    ```
- 當然我們也可以利用上述的方式再設定我們需要的自定義環境變數

#### How to use the Node.js REPL?
- 我們可以利用$ `node`指令來執行我們寫好的Node腳本(script)
  + 例: $ `node script.js`
- 如果我們省略要執行的腳本名稱這個參數的話,就會進入`REPL模式`
  > 補充: `REPL`又被稱為Read Evaluate Print Loop(讀取-求值-輸出循環的互動式介面, REPL),是一種程式語言的環境(主要是在CLI console畫面中)。他會使用單個表達式作為使用者輸入,並在執行後將結果回傳到CLI console畫面上<br>
  > 補充: `REPL模式`因為是互動式介面,所以支援可利用`Tab`鍵做自動補全(autocomplete)的功能,它會嘗試自動完成所寫的內容,以匹配已定義的變量或預定義的變量
  + node `REPL模式`範例情境
    * ```console
        ❯ node
        >
      ```
    * 該指令會停留在閒置模式(idle mode),並等待我們輸入些什麼東西。更精確地說是`REPL模式`正在等待我們輸入一些Javascript的程式碼
  + 我們從簡單的範例開始看看
    * ```console
        > console.log('test')
        test
        undefined
        >
      ```
    * 第一個值`test`是要告訴CLI console要打印(print)出什麼值,接著我們收到`undefined`,它是執行中(running)的`console.log()`
    * 接著我們可以開始輸入一行新的Javascript的程式碼
- 探索Javascript物件(Objects)
  + 我們可以試著輸入Javascript的類別(Class),像是`Number`,並在後面加上一個`.` ,再接著按下`Tab`按鈕來自動補全
  + ![node REPL模式-探索Number類別](/pic/node%20REPL模式-探索Number類別.png)
- 探索Javascript的全域物件(global)
  + 我們可以試著輸入Javascript的類別(Class),像是`global`,並在後面加上一個`.` ,再接著按下`Tab`按鈕來自動補全
  + ![node REPL模式-探索全域物件(global)](/pic/node%20REPL模式-探索全域物件(global).png)
- 探索特殊變數(`_`)
  + 如果在某些程式碼後面輸入`_`,則將回傳上一個操作的結果
- 探索點命令(Dot commands)
  + REPL模式有一些特別的指令,這些指令都是由`.`為開頭的
  + 舉例來說
    * `.help`: 顯示所有的點命令(dot commands)的幫助(help)
    * `.editor`: 啟用編輯模式,可以輕鬆地開始寫多行Javascript程式碼。一旦進入這個模式,我們將要使用`ctrl-D`的組合鍵來執行我們寫的Javascript多行程式碼
    * `.break`: 當輸入多行表達式(multi-line expression)時,輸入`.break`指令將終止進一步的輸入(abort further input)。與`ctrl-C`組合鍵的功能是一樣的
    * `.clear`: 將`REPL`模式的內文重新設定(reset)為一個空物件,並清除當前正在輸入的任何多行表達式
    * `.load`: 讀取當前工作目錄路徑下的Javascript檔案
    * `.save`: 將我們在`REPL連線`(session)中的所有對指定檔案的輸入儲存起來
    * `.exit`: 退出`REPL模式`。與連續按下`ctrl-C`組合鍵**兩次**的功能是一樣的
  + 其實`REPL模式`會知道什麼時候要輸入多行表達式,而不需要呼叫`.editor`
    * 以下是範例程式碼 
      * ```javascript
          [1, 2, 3].forEach(num => {
        ```
    * 這時候當我們按下`enter`鍵時,`REPL模式`會到新的下一行,並以`...`作為開頭,表示我們現在可以繼續在該區塊(block)工作
      * 情境說明
      * ```javacript
          ... console.log(num)
          ... })
        ``` 
    * 如果我們這時候在一行的句尾加上`.break`時,該多行表達式的模式將會停止並不會被執行

#### Node.js, accept arguments from the command line
- 我們可以將不限制數量的參數(arguments)傳遞給Node應用程式,參數的形式可以使用以下2種形式
  + 獨立的參數值(standalone)
    * $ `node app.js joe`
  + 鍵->值形式的參數值(key and value)
    * $ `node app.js name=joe`
- 這也將改變我們在Node應用程式的程式碼中,如何得到此值的方式,我們可以透過Node內建的核心模組`process`來得到此值,該模組的[process.argv](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_argv)屬性會揭露(exposes)出一個陣列(array),其中包含當啟動Node應用程式的進程的時候,整個命令列(command-line)要傳遞的所有參數
  + 第1個元素是node指令的完整路徑(= [process.execPath](https://nodejs.org/api/process.html#process_process_execpath))
  + 第2個元素會是正在被執行的Javascript檔案的路徑位置
  + 剩下的元素就是任何其他的命令列參數(command-line arguments)
- 範例程式碼
  + 以下的範例程式碼會利用一個迴圈來遍歷(iterate over)所有的參數們(也包括node指令的完整路徑與正在被執行的Javascript檔案的路徑位置)
  + ```javascript
      process.argv.forEach((val, index) => {
        console.log(`${index}: ${val}`)
      })
      ```
- 我們可以透過建立一個新的陣列並切片(`array.slice()`方法)來獲得額外的參數(不包含前兩個參數)
  + ```javascript
      const args = process.argv.slice(2)
    ```
- 如果我們的參數沒有索引名稱的話(without index name)
  + 例: $ `node app.js joe`
    * ```javascript
        const args = process.argv.slice(2)
        console.log(args[0])
      ```
    * 我們可以透過以上的範例程式碼來存取命令列參數(command-line arguments)
- 另一種情況是,我們會以鍵值(key-value)形式來傳遞命令列參數
  + 例: $ `node app.js name=joe`
  + ```javascript
      const args = require('minimist')(process.argv.slice(2))
      args['name'] //joe
      ```
    * 以上述範例程式碼為例,`args[0]`是`name=joe`,這種情況我們就會需要來解析(parse)它,最佳的做法是,我們可以利用npm上面的[minimist](https://www.npmjs.com/package/minimist)套件來處理這些**鍵值形式的參數**
  + 這次我們就要在每個參數的鍵(key)之前使用雙破折號(double dashes)
    * 例: $ `node app.js --name=joe`
  

#### Output to the command line using Node.js
> npm的[chalk](https://github.com/chalk/chalk)套件--- 可設定終端機輸出文字的樣式與顏色<br>
> npm的[progress](https://www.npmjs.com/package/progress)套件---可以在`CLI console`畫面上創造進度條的套件<br>
- 利用[console](https://nodejs.org/api/console.html#console_console)核心模組的基本輸出(basic output)
  + Node有一個`console`核心模組,該模組提供了許多與`CLI`有用的互動方法
  + 它基本上跟我們在瀏覽器上看到的`console`物件是一樣的
  + 最基本與最有用的方法是[console.log([data][, ...args])](https://nodejs.org/api/console.html#console_console_log_data_args),這個方法會打印出(print)我們傳遞給console的字串
    * 如果我們傳遞物件,該方法會自動幫我們轉換成字串
    * 我們也可以傳遞多個變數給`console.log()`
    * 範例程式碼
    * ```javascript
        const x = 'x'
        const y = 'y'
        console.log(x, y)
      ```
      * 以上的程式碼,Node會將兩個變數都打印出來(print)
    * 我們也可以傳遞變數給模板字串
    * 範例程式碼
    * ```javascript
        console.log('My %s has %d years', 'cat', 2)
      ```
      * `%s`: 將變數格式化為字串
      * `%d`: 將變數格式化為數字
      * `%i`: 將變數格式化為其整數部分
      * `%o`: 將變數格式化為物件
    * 範例程式碼
    * ```javascript
        console.log('%o', Number)
      ```
- 清除後台(console)-[console.clear()](https://nodejs.org/api/console.html#console_console_clear)
  + 範例程式碼
  + ```javascript
      console.clear()
      ```
    * 該方法會將後台清空(註: 該方法的行為也會取決於我們是使用哪種後台)
- 計算元素數量-[console.count([label])](https://nodejs.org/api/console.html#console_console_count_label)
  + `console.count()`是一個方便的方法
  + 範例程式碼
  + ```javascript
      const x = 1
      const y = 2
      const z = 3
      console.count(
        'The value of x is ' + x + 
        ' and has been checked .. how many times?'
      )
      console.count(
        'The value of x is ' + x + 
        ' and has been checked .. how many times?'
      )
      console.count(
        'The value of y is ' + y + 
        ' and has been checked .. how many times?'
      )
      ```
    * 以上的程式碼會計算該字串被打印出(print)幾次了,並將其次打印在旁邊
  + 範例程式碼
    * 我們也可以只計算蘋果和橘子的數量
    * ```javascript
        const oranges = ['orange', 'orange']
        const apples = ['just one apple']
        oranges.forEach(fruit => {
          console.count(fruit)
        })
        apples.forEach(fruit => {
          console.count(fruit)
        })
      ```
- 打印出堆棧追蹤(print stack trace)-[console.trace([message][, ...args])](https://nodejs.org/dist/latest-v15.x/docs/api/console.html#console_console_trace_message_args)
  + 在某些情況下,打印出函數的堆棧調用情況是很有用的,這也許就能回答我們的一個問題---我們該如何到達程式碼的其中一個部分?
  + 我們可以利用`console.trace()`方法來完成
  + 範例程式碼
    * ```javascript
        const function2 = () => console.trace()
        const function1 = () => function2()
        function1()
      ```
      * 以上的範例程式碼會打印出堆棧追蹤(stack trace)
      * 如果我們在Node的`REPL模式`中嘗試以上的範例程式碼,會得到以下的回傳資訊
      * ```javascript
          Trace
            at function2 (repl:1:33)
            at function1 (repl:1:25)
            at repl:1:1
            at ContextifyScript.Script.runInThisContext (vm.js:44:33)
            at REPLServer.defaultEval (repl.js:239:29)
            at bound (domain.js:301:14)
            at REPLServer.runBound [as eval] (domain.js:314:12)
            at REPLServer.onLine (repl.js:440:10)
            at emitOne (events.js:120:20)
            at REPLServer.emit (events.js:210:7)
        ```
- 計算執行Node程式碼所花費的時間-[console.time([label])](https://nodejs.org/dist/latest-v15.x/docs/api/console.html#console_console_time_label) & [console.timeEnd([label])](https://nodejs.org/dist/latest-v15.x/docs/api/console.html#console_console_timeend_label)
  + 我們可以使用`console.time()` & `console.timeEnd()`
  + 範例程式碼
  + ```javascript
      const doSomething = () => console.log('test')
      const measureDoingSomething = () => {
        console.time('doSomething()')
        //do something, and measure the time it takes
        doSomething()
        console.timeEnd('doSomething()')
      }
      measureDoingSomething()
    ```
- 標準輸出 & 標準錯誤-[console.log([data][, ...args])](https://nodejs.org/dist/latest-v15.x/docs/api/console.html#console_console_log_data_args) & [console.error([data][, ...args])](https://nodejs.org/dist/latest-v15.x/docs/api/console.html#console_console_error_data_args)
  + 如我們所見,`console.log()`非常適合在後台(Console)打印出訊息,這也就是所謂的標準輸出(standard output, `stdout`)
  + 反之,`console.error()`則會將訊息打印到標準錯誤(standard error, `stderr`)流(stream)上面
    + `stderr`流不會出現在後台(Console)上,但是它會出現在錯誤日誌上(error log)
- 為文字輸出上色-[跳脫序列(escape sequences)](https://gist.github.com/iamnewton/8754917) & npm的[chalk](https://github.com/chalk/chalk) package
  + 我們可以利用跳脫序列(escape sequence)將文字輸出上色
  + 跳脫序列是一組字符代表一種顏色
  + 範例程式碼
    * ```javascript
        console.log('\x1b[33m%s\x1b[0m', 'hi!')
      ```
    * 在`CLI`上進入Node的`REPL模式`中,執行以上的程式碼會看到`hi`變成黃色的字體
    * ![利用Node REPL模式下的跳脫序列來為文字輸出上色](/pic/利用Node%20REPL模式下的跳脫序列來為文字輸出上色.png)
    * 然而這樣做其實是一種低階(low-level)方法,最簡單的做法是利用套件(library)來將文字輸出上色
  + 我們可以利用npm上面的`chalk`套件,該套件不僅可以為文字輸出上色,也可以將文字輸出的字體變成**粗體**or*斜體*or帶有下劃線
    * 我們可以透過`CLI`指令來安裝`chalk`這個套件,安裝完後就可以立即使用它
      * $ `npm install chalk`
    * 範例程式碼
    * ```javascript
        const chalk = require('chalk')
        console.log(chalk.yellow('hi!'))
      ```
      * 從上面的範例程式碼可以看出我們可以使用`chalk.yellow()`這個方法會比起跳脫序列(escape sequences)來得更好記與更好閱讀
    * 更多相關功能可以參考[chalk]((https://github.com/chalk/chalk))
- 建立進度條-npm的[progress](https://www.npmjs.com/package/progress) package
  + `progress`是一個非常棒的套件在CLI console畫面上創造**進度條**的套件
  + 可以先利用npm來安裝`progress`這個套件
    * $ `npm install progress`
  + 範例程式碼
  + ```javascript
      const ProgressBar = require('progress')

      const bar = new ProgressBar(':bar', { total: 10 })
      const timer = setInterval(() => {
        bar.tick()
        if (bar.complete) {
          clearInterval(timer)
        }
      }, 100)
      ```
    * 以上的範例程式碼會建立一個含有10個步驟(steps)的進度條(progress bar),每100毫秒就會執行一次
    * 當進度條完成時,就會清除這個間隔(clear the interval)




---
### Node.js 核心模組
#### [HTTP](https://nodejs.org/api/http.html)
- 要使用HTTP server & client,必須要先`require('http')`
- Node的HTTP介面(interfaces)旨在支援HTTP協定的許多功能
,因為這些功能傳統上較難使用,尤其是在大量.大塊(chunk-encoded)的訊息
  + 該介面非常地小心,永遠不會緩衝(buffer)整個請求(requests)和回應(responses),所以使用者可以傳送實時資料流(stream data)
- HTTP訊息標頭(message headers)通常用物件(object)來表示
  + 範例`HTTP message header`
  + ```javascript
      { 'content-length': '123',
        'content-type': 'text/plain',
        'connection': 'keep-alive',
        'host': 'mysite.com',
        'accept': '*/*' 
      }
  + 鍵(keys)要用小寫表示,值(values)是按照原本的不變
- 為了能支援所有可能的HTTP應用程式,Node的HTTP API是屬於非常底層的,它只處理資料流(stream handling),但是不解析實際的標頭(headers)或是正文(context)
  + 可參考[message.headers](https://nodejs.org/api/http.html#http_message_headers)以了解該如何處理重複標頭(duplicate headers)的細節
- 收到的原始標頭會保留在[message.rawHeaders](https://nodejs.org/api/http.html#http_message_rawheaders)屬性值中,並以陣列(array)的形式來儲存該資訊,像是`[key, value, key2, value2, ...]`
  + 以上述的`HTTP message header`為例,它的`message.rawHeaders`的值會像是以下的陣列(array)形式
  + ```javascript
      [ 'ConTent-Length', '123456',
        'content-LENGTH', '123',
        'content-type', 'text/plain',
        'CONNECTION', 'keep-alive',
        'Host', 'mysite.com',
        'accepT', '*/*'
      ]
    ```
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
      * [response.end()](https://nodejs.org/api/http.html#http_response_end_data_encoding_callback)
        * 完整版: response.end([data[, encoding]][, callback]) 
        * args
          * data: (string || Buffer)
          * encoding: (string)
          * callback: (Function)
          * Returns: (this)
        * 這個方法會向server發送信號,表示所有的回應標頭(response header)和內文(body)皆已發送出去,這時server應認定該請求消息已完成
        * response.end()需要在每個回應的**結尾**都使用它
        * 如果data參數有給定的話,它實際上是去呼叫[response.write(data, encoding)](https://nodejs.org/dist/latest-v15.x/docs/api/http.html#http_response_write_chunk_encoding_callback),並接著執行res.end(callback)
        * 如果callback函式有給定的話,該callback函式會在回應串流(response stream)結束之後才會被呼叫並執行

#### [Process](https://nodejs.org/dist/latest-v15.x/docs/api/process.html)
- `process`是一個全域的物件,針對當前的Node應用程序的進程(process),提供資訊與控制
  + 讀: 獲取process資訊(資源使用、執行環境、執行狀態)
  + 寫: 執行process操作(監聽事件、排程任務、發出警吿)
- 因為`process`身為global物件,所以可以在Node應用程式中直接使用,而無需事先require()。
  + 但它也還是能透過require()來匯入並使用這個模組
  + 例: $ `const process = require('process');`
> Process events
  + [Event: **exit**](https://nodejs.org/api/process.html#process_event_exit)
    * args
      * code: (integer)
    * 由於以下的任一個原因而導致Node應用程式即將退出時,將發出(emitted)該事件
      * 明確地呼叫`process.exit()`方法時
      * Node的事件循環(event loop)不再需要執行其他額外的工作時
    * 目前沒有方法可以防止在這個時間點要退出事件循環(event loop),一旦所有的**exit**監聽器(listener)執行結束後,就會終止Node的進程
    * 只要有給定退出碼(不管是透過`process.exitCode`屬性或是現在這個**exit事件**的`exitCode`參數)並傳遞給`process.exit()`方法時,該事件監聽回呼函式(listener callback function)就會被呼叫
      * 範例程式碼 
      * ```javascript
          process.on('exit', (code) => {
            console.log(`About to exit with code: ${code}`);
          });
        ```
    * 監聽功能**必須只**執行**同步化的操作**,以下的範例程式碼,該Node進程會在呼叫`exit`事件監聽器(event listeners)後**就立即退出**,因而導致任何仍在事件迴圈(event loop)中的佇列(queued)中的額外的工作都會被拋棄(abandoned)
      * 以下的程式碼為例,`setTimeout()`這個函式**永遠不會**被執行到
      * 情境說明(**錯誤示範**)
        * ```javascript
            process.on('exit', (code) => {
              setTimeout(() => {
                console.log('This will not run');
              }, 0);
            });
          ```
  + [Event: **Signal events**](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_signal_events)
    * 信號事件(Signal events)會在Node進程(process)收到信號時發出(emitted)
    * 信號(Signals)不能用在[Worker threads](https://nodejs.org/dist/latest-v15.x/docs/api/worker_threads.html#worker_threads_worker_threads)
    * 信號處理器(signal handler)會將收到的信號名稱(signal's name)做為第一個參數
      * 例: `SIGINT`, `SIGTERM`
    * 每個事件(event)的名稱將會是大寫的常用信號名稱
      * 例: `SIGINT` => SIGINT 信號們
    * ```javascript
        // Begin reading from stdin so the process does not exit.
        process.stdin.resume();

        process.on('SIGINT', () => {
          console.log('Received SIGINT. Press Control-D to exit.');
        });

        // Using a single function to handle multiple signals
        function handle(signal) {
          console.log(`Received ${signal}`);
        }

        process.on('SIGINT', handle);
        process.on('SIGTERM', handle);
      ```
    * `SIGTERM`與`SIGINT`在非Windows作業系統的環境中,擁有預設處理器可以在退出程式碼之前,重置終端機模式為**128 + signal number**。如果這些信號之一已安裝了監聽器(listener),則將刪除其默認行為(Node應用程式也不再退出)
    * `SIGTERM`: 在Windows作業系統的環境中不支援,但可以監聽它(listened on)
    * `SIGINT`: 在終端機中是可被所有作業系統所支援的,它通常可以用`ctrl-C`來產生
    * `SIGKILL`: 不能安裝監聽器(listener),它將無條件終止Node應用程式,無論我們在哪個作業系統的環境中
    * 補充: 因為Windows作業系統並不支援信號(signals),所以不能說是等同於信號終止,但是Node有提供了一些仿效的做法,例如: [process.kill()](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_kill_pid_signal)與[subprocess.kill()](https://nodejs.org/dist/latest-v15.x/docs/api/child_process.html#child_process_subprocess_kill_signal)
      * 發送`SIGINT`,`SIGTERM`,`SIGKILL`將導致目標進程(target process)無條件被終止。此後,子進程(subprocess)將回報該進程(process)已被信號(signal)終止了
      * 發送信號(signal) `0` 可以用來做為一種獨立的平台以測試進程(process)的存在  
> method
- [process.cpuUsage([previousValue])](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_cpuusage_previousvalue)
  * args
    * previousValue: (Object)
      * 上一次呼叫process.cpuUsage()的回傳值
  * Returns: (Object)
    * user: (integer)
    * system: (integer)
  * 該方法會回傳一個具有`user`, `system`的物件(`Object`),來表示當前的進程(current process)的`user`和`system`的時間使用率
    * 這些值都是以百萬分之一秒為單位(微秒)--->時間單位
    * 這些值分別用來測量花在使用者端的程式碼＆系統端的程式碼的時間
    * 當有多個CPU內核在為這個進程(process)執行工作時,則這些值最終可能會大於實際經過的時間
  * 上一次呼叫`process.cpuUsage()`的結果可以作為參數傳遞給函式,以得知差異讀數(diff reading)
  * ```javascript
      const startUsage = process.cpuUsage();
      // { user: 38579, system: 6986 }

      // spin the CPU for 500 milliseconds
      const now = Date.now();
      while (Date.now() - now < 500);

      console.log(process.cpuUsage(startUsage));
      // { user: 514883, system: 11226 }
    ``` 
- [process.memoryUsage()](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_memoryusage)
  + Returns: (Object)
    * rss: (integer)
      * rss => (常駐集的大小,Resident Set Size),代表該進程(process)在主記憶體裝置中已被使用掉的內存記憶體空間(即總分配內存的子集); 包括所有的`C++`與`Javascript`的物件和程式碼
    * heapTotal: (integer)
      * 參考V8 engine的內存記憶體使用情況 
    * heapUsed: (integer)
      * 參考V8 engine的內存記憶體使用情況 
    * external: (integer)
      * 參考由V8 engine管理的`C++物件`綁定到`Javascript物件`的內存記憶體使用量 
    * arrayBuffers: (integer)
      * 參考分配到`ArrayBuffers` & `SharedArrayBuffers`,也包含所有Node應用程式的[Buffer](https://nodejs.org/dist/latest-v15.x/docs/api/buffer.html)物件
      * `arrayBuffers`也包含在`external`的值中
      * 當Node應用程式被用作嵌入式函式庫時,該值可能為0,是因為在這種情況下`arrayBuffers`可能不會被追蹤到
  + 該方法會回傳一個物件(`Object`)來描述Node應用程式的內存記憶體(memory)用量
    * 這個值會以`bytes`為單位來表示
  + 範例程式碼
    * 以下面的程式碼為例
      * ```javascript
          console.log(process.memoryUsage());
        ```
    * 會產生一個物件
      * `{
            rss: 4935680,
            heapTotal: 1826816,
            heapUsed: 650472,
            external: 49879,
            arrayBuffers: 9386
          }`
  + 當使用[Worker threads](https://nodejs.org/dist/latest-v15.x/docs/api/worker_threads.html#worker_threads_class_worker)時,`rss`將會是一個對於整個進程(entire process)有效的值(valid),而其他參數僅會參考到當前的進程
- process.resourceUsage()
  + Returns: (Object)
    * userCPUTime: (integer)
      * 對應到`ru_utime`的值,並以微秒為單位表示
      * 與process.cpuUsage().user的值相同
    * systemCPUTime: (integer)
      * 對應到`ru_stime`的值,並以微秒為單位表示
      * 與process.cpuUsage().system的值相同
  + 該方法會回傳一個物件(`Object`)來表示當前進程(current process)的資源使用率(resource usage); 以上所有該方法的回傳值都是來自於呼叫[uv_rusage_t struct](https://docs.libuv.org/en/v1.x/misc.html#uv_getrusage)的uv_getrusage()方法的回傳值
    > uv_getrusage(): Gets the resource usage measures for the current process.
- process.cwd()
  + Returns: (string)
    * 該方法會回傳當前進程(current process)所在的工作目錄的路徑(working directory)
  + 範例程式碼
    * ```javascript
        console.log(Current directory:  {process.cwd()});
      ```
- process.exit([code])
  + args
    * code: (integer)
      * 表示要指定的退出碼
      * 預設值: 0 (代表成功)
  + 該方法指示Node應用程式以同步地方式(synchronously)來終止進程(terminate the process)並顯示退出碼
    * 若[code]參數被省略,則會以`0`為退出碼或是`process.exitCode`的值為準(當該屬性在之前有被設定過的話)
    * Node應用程式不會在所有的[Event: 'exit'](https://nodejs.org/api/process.html#process_event_exit)事件監聽器(event listeners)被呼叫之前就終止掉
  + 範例程式碼
    * 以失敗(failure)的狀態碼來退出Node應用程式 
    * $ `process.exit(1);`
    * 在執行該Node應用程式的shell上,我們會看到退出碼(exit code)為`1`
  + 當我們呼叫`process.exit()`方法時,會強迫Node應用程式盡快地終止該進程,即便是還有pending狀態中的非同步操作尚未完全完成的情況,包括I/O操作,像是`process.stdout` & `process.stderr`
    * 在大多數的情況下,其實我們並不需要明確地呼叫`process.exit()`方法。因為在事件循環(event loop)當中沒有額外pending狀態中的工作的話,Node應用程式就會自行退出
    * 我們也可以透過設定好`process.exitCode`屬性的值,來告知進程在正常退出時,要使用哪個退出碼
  + 情境說明(**錯誤示範**)
    * ```javascript
        // This is an example of what *not* to do:
        if (someConditionNotMet()) {
          printUsageToStdout();
          process.exit(1);
        }
      ```
    * 以上的程式碼是一個使用`process.exit()`的**錯誤示範**,可能會因此導致要print到stdout的資料被截斷或遺失
    * 這樣做之所以有問題的原因是因為在Node的世界中要寫入到`process.stdout`有時候是非同步的(asynchronous),也可能會在Node的事件迴圈(event loop)中多次發生
    * 所以我們需要在額外寫入到stdout之後,才能呼叫process.exit()來強制將該進程退出
  + 範例程式碼(**正確做法**)
    * ```javascript
        // How to properly set the exit code while letting
        // the process exit gracefully.
        if (someConditionNotMet()) {
          printUsageToStdout();
          process.exitCode = 1;
        }
      ```
    * 以上的程式碼是正確的解決方法,我們應該要先設定好`process.exitCode`屬性的值,而不是直接呼叫`process.exit()`方法,並避免為事件迴圈(event loop)安排額外的工作來允許該進程能自然地退出
    * 如果是因為遇到錯誤情況而有必要強制終止該進程的話,可以拋出一個`uncaught error`,並根據這個錯誤來終止該進程,也會比直接呼叫`process.exit()`來得更安全
  + 在[Worker threads](https://nodejs.org/dist/latest-v15.x/docs/api/worker_threads.html#worker_threads_worker_threads)中,`process.exit()`會停止當前的線程(current thread),而不是當前的進程(current process)
- [process.kill(pid[ ,signal])](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_kill_pid_signal)
  + args
    * pid: (number)
      * 給定一個進程(process) ID
    * signal: (string || number)
      * 以字串或是數值的形式來發送信號
      * 預設值: `SIGTERM`
  + 該方法會將信號(signal)發送給指定`pid`的進程(process)
  + 信號的名稱為字串型別,常見的像是`SIGINT`, `SIGHUP`
  + 當給定的目標`pid`不存在時,該方法會拋出錯誤。作為特殊情況時,可以利用`0`作為信號來測試某個`pid`的進程是否存在
    * 當在Windows作業系統時,想砍掉一個進程群組(kill a process group)會拋出一個錯誤
  + 其實`process.kill()`這個方法只是一個信號發送器(signal sender),就如同 $`kill` 的系統指令一樣
    * 比起單純的系統指令 $`kill`,發送信號的這個方法可能會額外做一些其他的事,而不單純只是砍掉目標進程(kill the target process)
  + 範例程式碼
    * ```javascript
        process.on('SIGHUP', () => {
          console.log('Got SIGHUP signal.');
        });

        setTimeout(() => {
          console.log('Exiting.');
          process.exit(0);
        }, 100);

        process.kill(process.pid, 'SIGHUP');
      ```
    * 當Node應用程式的進程收到`SIGUSR1`的信號時,Node會啟動一個偵錯器(debugger)
      * 可參考[Signal events](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_signal_events)
- [process.nextTick(callback[ ,...args])](https://nodejs.org/dist/latest-v15.x/docs/api/process.html#process_process_nexttick_callback_args)
  + args
    * callback: (Function)
      * 回呼函式 
    * ...args: (any)
      * 當有呼叫callback function時,要附加給該回呼函式的參數們
    * 該方法會新增一個`callback function`到"next tick queue"。當Javascript堆疊(stack)當前的操作執行完成並允許事件迴圈(event loop)繼續之前,該佇列(queue)會完全耗盡(fully drained)
      * 如果要循環地重複呼叫`process.nextTick()`,可能會建立一個無限循環的迴圈(infinite loop)
      * 相關背景知識可參考[Event Loop](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#process-nexttick)章節的介紹
  + 範例程式碼
    * ```javascript
        console.log('start');
        process.nextTick(() => {
          console.log('nextTick callback');
        });
        console.log('scheduled');
        // Output:
        // start
        // scheduled
        // nextTick callback
      ```
  + process.nextTick()方法在開發API時很重要,以便給用戶在物件被構建(constructed)**之後**,但是在任何I/O相關操作發生**之前**,來指派事件處理器(assign event handlers)
    * ```javascript
        function MyThing(options) {
          this.setupOptions(options);

          process.nextTick(() => {
            this.startDoingStuff();
          });
        }

        const thing = new MyThing();
        thing.getReadyForStuff();

        // thing.startDoingStuff() gets called now, not before.
  + 對於API來說,要馬 100%同步 or 100%非同步,是很重要的事情
    * 情境說明(**錯誤示範**)
      * ```javascript
          // WARNING!  DO NOT USE!  BAD UNSAFE HAZARD!
          function maybeSync(arg, cb) {
            if (arg) {
              cb();
              return;
            }

            fs.stat('file', cb);
          }
        ```
    * 以上的範例是冒險的(hazardous),因為假設我們遇到以下的情況
      * 接下來的情況會造成不清楚到底是foo() 或是 bar()先被呼叫
      * 情境說明(**錯誤示範**)
      * ```javascript
          const maybeTrue = Math.random() > 0.5;

          maybeSync(maybeTrue, () => {
            foo();
          });

          bar();
        ```
    * 範例程式碼(**正確做法**)
      * 以下的做法會比較好 
      * ```javascript
          function definitelyAsync(arg, cb) {
            if (arg) {
              process.nextTick(cb);
              return;
            }

            fs.stat('file', cb);
          }
        ```
- [process.send(message[, sendHandle[, options]][, callback])](https://nodejs.org/api/process.html#process_process_send_message_sendhandle_options_callback)
  + args
    * message: (Object)
    * sendHandle ([net.Server])(https://nodejs.org/api/net.html#net_class_net_server) || [net.Socket](https://nodejs.org/api/net.html#net_class_net_socket))
    * options: (Object)
      * 被用作將特定操作類型的發送參數化
      * `options`也支援以下的屬性
        * `keepOpen`: (boolean)
          * 當在傳遞`net.Socket`的實例們(instances)時,可以用來傳遞的值
          * 預設值: false
          * 當`keepOpen`=true時, `socket`會在發送過程(sending process)中保持開放
  + Returns: (boolean)
    * 如果是利用`IPC channel`來產生Node應用程式的話,`process.send()`方法可以用來傳遞訊息給父進程(parent process)
      * 消息(message)會被parent's [ChildProcess](https://nodejs.org/api/child_process.html#child_process_class_childprocess)物件作為[message event](https://nodejs.org/api/child_process.html#child_process_event_message)來接收
    * 如果未使用`IPC channel`來產生Node應用程式的話,則`process.send()`回傳的結果將會是`undefined`
    * 該訊息(message)已經歷過序列化(serialization)與解析(parsing)
      * 結果消息(resulting message)可能會跟最初發送的消息不太一樣
- [process.uptime()](https://nodejs.org/api/process.html#process_process_uptime)
  + Returns: (number)
  + 該方法會回傳當前Node應用程式已經運行多久的秒數
    * 回傳值會包括含有小數點的秒數,可以利用Math.floor()來算出小於等於所給數字的最大整數
      * 例: $ `Math.floor(5.95)` => `5`  
> property
- [process.argv](https://nodejs.org/api/process.html#process_process_argv)
  + Type: (string) 
  + 該屬性會回傳一個陣列(array),該陣列會包含當啟動Node應用程式的進程的時候,整個命令列(command-line)要傳遞的所有參數
    * 其中的第一個元素會是[process.execPath](https://nodejs.org/api/process.html#process_process_execpath)
    * 第二個元素會是正在被執行的Javascript檔案的路徑位置
    * 剩下的元素就是任何其他的命令列參數(command-line arguments)
  + 範例程式碼
    * 假設以下範例程式的檔案名稱是`process-args.js`
    * ```javascript
        // print process.argv
        process.argv.forEach((val, index) => {
          console.log(`${index}: ${val}`);
        });
      ```
    * 可以利用以下的方式來啟動Node應用程式的進程(process)
      * $ `node process-args.js one two=three four`
    * 將會回傳以下的值
      * ```javascript
          0: /usr/local/bin/node
          1: /Users/mjr/work/node/process-args.js
          2: one
          3: two=three
          4: four
        ```
- [process.debugPort](https://nodejs.org/api/process.html#process_process_debugport)
  + Type: (number)
  + 該屬性值代表當啟用(enabled)Node應用程式的除錯器時(dubugger),所使用的埠號(port)
- [process.env](https://nodejs.org/api/process.html#process_process_env)
  + Type: (Object) 
  + 該屬性會回傳一個物件,包含使用者的環境變數
    * 像是以下的`Object`
    * ```javascript
        {
          TERM: 'xterm-256color',
          SHELL: '/usr/local/bin/bash',
          USER: 'maciej',
          PATH: '~/.bin/:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin',
          PWD: '/Users/maciej',
          EDITOR: 'vim',
          SHLVL: '1',
          HOME: '/Users/maciej',
          LOGNAME: 'maciej',
          _: '/usr/local/bin/node'
        } 
      ```
    * 可以修改這個環境變數的物件,但僅限於該Node應用程式進程(process),或者除非明確地要求不會反應到其他[Worker threads](https://nodejs.org/api/worker_threads.html#worker_threads_class_worker)上
      * 換句話說,以下的範例並不會如預期地運作
      * $ `node -e 'process.env.foo = "bar"' && echo $foo`
      * 雖然將執行以下操作
      * ```javascript
          process.env.foo = 'bar';
          console.log(process.env.foo);
        ```
  + 從Node v10.0.0的版本以後開始,指派給`process.env`的環境變數的值**不會**再做隱性轉換型別
    * 所以以下的方式**不建議**再使用
    * 情境說明(**錯誤示範**)
    * ```javascript
        process.env.test = null;
        console.log(process.env.test);
        // => 'null'
        process.env.test = undefined;
        console.log(process.env.test);
        // => 'undefined'
      ```
  + 如果要從`process.env`的屬性值中,刪除Node應用程式的環境變數的話,可以利用Javascript的`delete`指令來完成
    * 範例程式碼
      * ```javascript
          process.env.TEST = 1;
          delete process.env.TEST;
          console.log(process.env.TEST);
          // => undefined
        ```
  + 在Windows作業系統中,環境變數沒有區分大小寫(case-insensitive)
    * 以下範例程式碼**僅限於Windows作業系統中**可以這樣使用
    * ```javascript
        process.env.TEST = 1;
        console.log(process.env.test);
        // => 1
      ```
  + 除非在建立[Worker](https://nodejs.org/api/worker_threads.html#worker_threads_class_worker)實例時有明確指定環境變數,不然每個`Worker thread`都有自己的一份`process.env`副本(copy),是基於它們各自的父線程(parent thread)的環境變數(`process.env`),或是任何被作為`env`選項並給定到`Worker constructor`
    * `Worker threads`之間並無法看到`process.env`的修改,只有主線程(main thread)才能進行對作業系統或是本機加載項(native add-ons)做看得見的修改
- [process.execArgv](https://nodejs.org/api/process.html#process_process_execargv)
  + Type: (string [set])
  + 該屬性會回傳當Node應用程式的進程被啟動時,在Node.js命令列上面的特定選項的集合(the set of Node.js-specific command-line options)
    * 這邊所指的特定選項(options)並不會出現在`process.argv`的屬性值之中,而且也不包括可執行的(executable),該準備要執行的檔案名稱,以及該準備要執行的檔案名稱**後面**的任何選項(options)
    * 這些選項對於以與父級相同執行環境的子進程(child process)是很有用的
    * 在終端機(CLI)執行該以下的指令後
      * 例: $ `node --harmony script.js --version`
      * 檢視`process.execArgv`的屬性值會得到
        * => `['--harmony']`
      * 對照檢視`process.argv`的屬性值會得到
        * => `['/usr/local/bin/node', 'script.js', '--version']`
    * 可參考有關[Worker constructor](https://nodejs.org/api/worker_threads.html#worker_threads_new_worker_filename_options)中的`execArgv`屬性以了解更多的訊息
- [process.execPath](https://nodejs.org/api/process.html#process_process_execpath)
  + Type: (string)
  + 該屬性值會回傳Node應用程式的進程中的可執行文件(executable)的絕對路徑
    * 例: `'/usr/local/bin/node'`  
    * 如果遇到可執行文件的路徑是`symbolic link`,會自動解決掉該問題 
- [process.exitCode](https://nodejs.org/api/process.html#process_process_exitcode)
  + 型別: (integer)
  + 當進程被正常地退出時,或是透過`process.exit()`方法退出時但沒有給定退出碼時,`process.exitCode`的屬性值代表該進程的退出碼
  + 當我們給定process.exit([code])方法的退出碼參數值時,會推翻(override)之前的`process.exitCode`的屬性值設定
- [process.pid](https://nodejs.org/api/process.html#process_process_pid)
  + Type: (integer)
  + 該屬性會回傳該進程的ID(process ID, pid)
    * $ `console.log(`This process is pid ${process.pid}`);` 
- [A note on process I/O](https://nodejs.org/api/process.html#process_a_note_on_process_i_o)
  + [process.stdin](https://nodejs.org/api/process.html#process_process_stdin)
  + [process.stdout](https://nodejs.org/api/process.html#process_process_stdout)
  + [process.stderr](https://nodejs.org/api/process.html#process_process_stderr)
- [process.title](https://nodejs.org/api/process.html#process_process_title)
  + Type: (string)
  + 該屬性會回傳當前的進程標題(current process title) => 也就是會回傳當前`ps`的值
  + 當指派新的值給`process.title`屬性時,會修改掉當前`ps`的值
- [process.version](https://nodejs.org/api/process.html#process_process_version)
  + Type: (string)
  + 該屬性值代表Node.js的版本號(version)
    * ```javascript
        console.log(`Version: ${process.version}`);
        // Version: v14.8.0
      ```
    * 如果想要取得不帶有前綴v開頭的版本號字串的話,可以利用以下的屬性值
      * $ `process.versions.node`       

> Exit codes(退出碼)
- 在沒有其他額外的**非同步操作**處於`pending狀態`後,Node應用程式通常會以`0`的退出碼來正常退出
- 以下是常見的退出碼
  + `0`: 正常退出 (預設值)
  + `1`: 未捕獲的致命錯誤(Uncaught Fatal Exception),並且沒有受到`domain`或是[uncaughtException](https://nodejs.org/api/process.html#process_event_uncaughtexception)事件處理器來處理
  + 以下略...

#### [Console](https://nodejs.org/api/console.html#console_console)
  + `console`模組提供了一組簡單的除錯控制台(debugging console),類似於網頁瀏覽器所提供的Javascript控制台機制
  + `console`模組會匯出(export)兩個特定的元件(specific components)
    * 第一個特定的元件是: [Console類別(class)](https://nodejs.org/api/console.html#console_class_console)的方法,像是`console.log()`&`console.error()`&`console.warn()`,它們可以被用來寫入到Node流(stream)中
    * 第二個特定的原件是: 一個全域(global)的`console`實例(instance)會寫入到[process.stdout](https://nodejs.org/api/process.html#process_process_stdout)與[process.stderr](https://nodejs.org/api/process.html#process_process_stderr)。全域的`console`物件可以直接被使用,而**不用**事先匯入(**require('console')**)
  + **注意**: 全域的`console`物件方法既不能像類似它們的瀏覽器API一樣始終同步(consistently synchronous),也不能像Node流(streams)一樣始終非同步(consistently asynchronous)
    * 可參考`process`模組的 [A note on process I/O](https://nodejs.org/api/process.html#process_a_note_on_process_i_o) 章節
  + 使用全域的`console物件`的範例程式碼
    * ```javascript
        console.log('hello world');
        // Prints: hello world, to stdout
        console.log('hello %s', 'world');
        // Prints: hello world, to stdout
        console.error(new Error('Whoops, something bad happened'));
        // Prints error message and stack trace to stderr:
        //   Error: Whoops, something bad happened
        //     at [eval]:5:15
        //     at Script.runInThisContext (node:vm:132:18)
        //     at Object.runInThisContext (node:vm:309:38)
        //     at node:internal/process/execution:77:19
        //     at [eval]-wrapper:6:22
        //     at evalScript (node:internal/process/execution:76:60)
        //     at node:internal/main/eval_string:23:3

        const name = 'Will Robinson';
        console.warn(`Danger ${name}! Danger!`);
        // Prints: Danger Will Robinson! Danger!, to stderr
      ```
  + 使用`Console類別`的範例程式碼
    * ```javascript
        const out = getStreamSomehow();
        const err = getStreamSomehow();
        const myConsole = new console.Console(out, err);

        myConsole.log('hello world');
        // Prints: hello world, to out
        myConsole.log('hello %s', 'world');
        // Prints: hello world, to out
        myConsole.error(new Error('Whoops, something bad happened'));
        // Prints: [Error: Whoops, something bad happened], to err

        const name = 'Will Robinson';
        myConsole.warn(`Danger ${name}! Danger!`);
        // Prints: Danger Will Robinson! Danger!, to err
      ```
> Class
- [Class: Console](https://nodejs.org/api/console.html#console_class_console)
  + `Console`類別可以用來建立簡單且可配置(configurable)的輸出流(output streams)紀錄器(logger),並且可以利用以下兩種方式來存取,或是用它們相仿的解構對應物件(destructured counterparts)來存取
    * 存取方式一: `require('console').Console`
      * 例: `const { Console } = require('console');`
    * 存取方式二: `console.Console`
      * 例: `const { Console } = console;`
  > method
    * [console.clear()](https://nodejs.org/api/console.html#console_console_clear)
      * 當標準輸出(`stdout`)是`TTY`時,呼叫`console.clear()`的時候,會嘗試清除`TTY`; 當標準輸出(`stdout`)不是`TTY`時,則該方法不會做任何事情
      * 使用特定的`console.clear()`操作時,會因為使用的作業系統不同or終端機類型不同,而有所差異。在大部分的Linux作業系統中,`console.clear()`方法會執行與`clear`指令差不多的操作; 在Windows作業系統中,`console.clear()`將僅會清除掉在當前(current)的終端機視口(terminal viewport)中的Node應用程式的二進制(binary)文件的輸出(output)
    * [console.count([label])](https://nodejs.org/api/console.html#console_console_count_label)
      * args
        * label: (string)
          * 可以給定要顯示的計數器的標籤值
          * 預設值: `default`
      * 該方法會回傳一個內部計數器(internal counter)維持顯示一組`標籤`(label) & `次數`(times)
        * `標籤`(label): 可以透過呼叫`console.count()`方法時,由開發者給定標籤值
        * `次數`(times): 指定給標籤,呼叫`console.count()`方法並輸出給`stdout`的次數
        * 範例程式碼
        * ```console
            > console.count()
            default: 1
            undefined
            > console.count('default')
            default: 2
            undefined
            > console.count('abc')
            abc: 1
            undefined
            > console.count('xyz')
            xyz: 1
            undefined
            > console.count('abc')
            abc: 2
            undefined
            > console.count()
            default: 3
            undefined
            >
          ```
    * [console.error([data][, ...args])](https://nodejs.org/api/console.html#console_console_error_data_args)
      * args
        * data: (any)
        * ...args: (any)
      * 該方法會用新的一行(newline)打印(print)出標準錯誤(`stderr`)
      * 該方法可以傳遞多個參數
        * 第一個參數會被用來當作主要訊息(primary message)
        * 其他額外的參數(additional arguments)會被用作替換值(substitution),類似於[printf(3)](https://man7.org/linux/man-pages/man3/printf.3.html)
          * 其他額外的參數都會被傳遞給`util.format()`方法
          * 相關資訊可參考[util.format()](https://nodejs.org/api/util.html#util_util_format_format_args)方法
      * 範例程式碼
      * ```javascript
          const code = 5;
          console.error('error #%d', code);
          // Prints: error #5, to stderr
          console.error('error', code);
          // Prints: error 5, to stderr
          ```
        * 若格式化元素(formatted elements),例如: `%d`沒有在新的一行中被發現,則[util.inspect()](https://nodejs.org/api/util.html#util_util_inspect_object_options)方法會被呼叫,並在每個參數上呼叫該元素(`%d`),並將結果的字串值連接起來
    * [console.log([data][, ...args])](https://nodejs.org/api/console.html#console_console_log_data_args)
      * args
        * data: (any)
        * ...args: (any)
      * 該方法會用新的一行(newline)打印(print)出標準輸出(`stdout`)
      * 該方法可以傳遞多個參數
        * 第一個參數會被用來當作主要訊息(primary message)
        * 其他額外的參數(additional arguments)會被用作替換值(substitution),類似於[printf(3)](https://man7.org/linux/man-pages/man3/printf.3.html)
          * 其他額外的參數都會被傳遞給`util.format()`方法
          * 相關資訊可參考[util.format()](https://nodejs.org/api/util.html#util_util_format_format_args)方法
      * 範例程式碼
      * ```javascript
          const count = 5;
          console.log('count: %d', count);
          // Prints: count: 5, to stdout
          console.log('count:', count);
          // Prints: count: 5, to stdout
        ``` 
    * [console.time([label])](https://nodejs.org/api/console.html#console_console_time_label)
      * args
        * label: (string)
        * 可以給定該計時器的標籤值,以作為計時器識別用
        * 預設值: `default`
      * 該方法會啟動一個計時器(timer)被用來計算該操作(operation)的持續時間
      * 計時器會用獨一無二(unique)的標籤(label)來識別
      * 計時器會呼叫同標籤(same label)的`console.timeEnd()`方法來停止計時器,並將經過的時間以合適的時間單位輸出到標準輸出(`stdout`)中
        * 舉例來說,如果經過的時間是3869毫秒(ms),那麼`console.timeEnd()`方法會顯示"3.869"秒
    * [console.timeEnd([label])](https://nodejs.org/api/console.html#console_console_timeend_label)
      * args
        * label: (string)
        * 可以給定該計時器的標籤值,以作為計時器識別用
        * 預設值: `default`
      * 該方法會停止之前透過呼叫`console.time()`方法設定好的計時器,並將結果打印(print)到標準輸出(`stdout`)中
      * 範例程式碼
      * ```javascript
          console.time('100-elements');
          for (let i = 0; i < 100; i++) {}
          console.timeEnd('100-elements');
          // prints 100-elements: 225.438ms
        ```
    * [console.trace([message][, ...args])](https://nodejs.org/api/console.html#console_console_trace_message_args)
      * args
        * message: (any)
        * ...args: (any)
      * 該方法會將`Trace:`這段字串打印(print)到標準錯誤(`stderr`)中,接著透過[util.format()](https://nodejs.org/api/util.html#util_util_format_format_args)方法打印出格式化過的字串(formatted message),並堆棧追蹤(stack trace)到程式碼中的當前位置
      * 範例程式碼
      * ```javascript
          console.trace('Show me');
          // Prints: (stack trace will vary based on where trace is called)
          //  Trace: Show me
          //    at repl:2:9
          //    at REPLServer.defaultEval (repl.js:248:27)
          //    at bound (domain.js:287:14)
          //    at REPLServer.runBound [as eval] (domain.js:300:12)
          //    at REPLServer.<anonymous> (repl.js:412:12)
          //    at emitOne (events.js:82:20)
          //    at REPLServer.emit (events.js:169:7)
          //    at REPLServer.Interface._onLine (readline.js:210:10)
          //    at REPLServer.Interface._line (readline.js:549:8)
          //    at REPLServer.Interface._ttyWrite (readline.js:826:14)
        ```







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

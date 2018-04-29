# solidity-sample

# Solidity & web3.js

## 連結參考

* [區塊鏈模擬](https://anders.com/blockchain/tokens.html)
* [獎賞減半機制](http://www.bitcoinblockhalf.com/)
* [待處理的比特交易](https://blockchain.info/unconfirmed-transactions)
* [比特區塊鏈資訊](https://blockchain.info/)
* [以太幣值轉換](https://etherconverter.online/)

## 環境建立與範例程式碼

* [web3.js 官網](http://web3js.readthedocs.io/en/1.0/index.html)
* [範例程式碼](https://github.com/gonsakon/solidity-sample)
    * [metamask](https://metamask.io/)(請先安裝)
* [remix](https://remix.ethereum.org/)
* [rinkeby 測試主機取得以太幣](https://faucet.rinkeby.io/)、[Google Plus](https://plus.google.com/)
    * [請大家將地址貼上去](https://docs.google.com/document/d/172qjSFhgraGBbAWbNAgeaNeotoWCz5oFu_nCE4Y13qg/edit)
* [測試官方網站區塊鏈查詢](https://rinkeby.etherscan.io/)
* [prepos](https://prepros.io/) (本次 workshop 需要使用 localhost 環境，若你本身會架設，則無須安裝)

## 比特跟以太的差異

* 比特是記錄 交易記錄
* 以太多一個智能合約，讓我們可以透過合約來記錄任何內容

## 以太智能合約 (smart ConTract)

* 先試試看轉一筆錢到對方的 address 帳號
* 以太除了跟比特幣一樣除了可以儲存交易記錄外，還可以自己寫一個智能合約
* 將執行的程式公開在區塊鏈上，所有資訊公開透明，以達到去中心化。
* 一個合約會有
    * balance：合約裡面有多少以太幣
    * sotrage：可以存值進合約裡
    * code：Raw 機械語言程式碼

## 環境安裝

## Solidity 程式教學

* 副檔名為 .sol 檔案，.sol 會編譯出 bytecode、ABI(Application Binary interface)
* 網頁端這裡要讀取區塊鏈的話，是使用 JS 執行 ABI，再去區塊鏈尋找編譯出來的 bytecode
* 寫法很像 JavaScript

```
pragma solidity ^0.4.23;

contract messageBoard {
    string public message;
    int public num = 129;
    function messageBoard(string initMessage) public {
        message = initMessage;
    }
    function editMessage(string _editMessage) public{
        message = _editMessage;
    }
}
```

### 變數

* string -  字串
* int - 允許負數
    * int8：-128~127
    * int16：-32768~32767
    * int32： -2147483648~[2147483647](tel:2147483647)
    * 都不寫的話，預設就是 int256
* uint - 0 或 正數
* fixed/unfixed - 小數點
* bool 步林
* address 地址

### 函式

```

`          函式名稱    函式種類       回傳內容 
function message() public view returns(string){
    return message
}`
```



```
pragma solidity ^0.4.23;
contract messageBoard {
    string public message;
    // 函式傳參數
    function messageBoard(string initMessage) public {
        message = initMessage;
    }
    // 函式不傳參數
    function editMessage() public {
        message = 'hello';
    }
    // 函式 return 傳值
    `function callMessage() public view returns(string){
        return message
    }`
}
```

### 函式種類

* public：所有人都可使用該函式
* private：只限合約內部使用
* view、constant：只能讀取變數，不能修改變數
* pure：不可讀、也不可改
* payable：要傳送錢的時候使用

### solidity 跟一般程式的差異

* 寫得每一行程式碼需要考慮 gas，任何運算都會有 gas 手續費
* 需要寫很多非同步程式碼，或寫排程去戳交易狀態，一個交易動輒 10分鐘~3 hr
* 去中心化，智能合約可對外公佈與查詢

```
pragma solidity ^0.4.23;

contract messageBoard {
    string public message;
    int public num = 129;
    int public people = 0;
    function messageBoard(string initMessage) public {
        message = initMessage;
    }
    function editMessage(string _editMessage) public{
        message = _editMessage;
    }
    function showMessage() public view{
        message = 'abcd';
        
    }
    function pay() public payable{
        people++;
    }
    
}
```

## 設計一個留言版

* [範例合約](https://rinkeby.etherscan.io/address/0xefd35a0c1b6b7dc083c290123f132c4a1477ebaa)

```
pragma solidity ^0.4.23;
contract messageBoard {
    string public message;
    function messageBoard(string initMessage) public {
        message = initMessage;
    }
    function editMessage(string editMessage) public {
        message = editMessage;
    }
}
```

## web3.js 介接合約內容

* [web3.js 官網](https://web3js.readthedocs.io/en/1.0/getting-started.html)

## [借據系統 (event log)](https://rinkeby.etherscan.io/address/0xb1656f2dae22d4aed53f4766f75a06b9596f6e8e)

* 條件 0.15
* 誰可以領錢
* Storage中大致的价格是：每32字节（256位）存储需要消耗20,000气（Gas）。而日志大致是每字节8气（Gas）

## [報名名單寫 LOG 記錄資料](https://rinkeby.etherscan.io/address/0x58fd12f3040e020d98374cf07fb8009656c8d276)，設計自己的合約平台

mapping

```
pragma solidity ^0.4.23;
contract messageBoard {
    mapping (uint128 => bool) public list;
    string public message;
    function messageBoard(string initMessage) public {
        message = initMessage;
    }
    function addMapping(uint128 _add) public {
       list[_add] = true;
    }
}
```


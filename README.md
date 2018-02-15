https://github.com/miguelmota/ethereum-input-data-decoder
でもよう  
http://vinceg.github.io/Bootstrap-Admin-Theme/index.html  
https://github.com/VinceG/Bootstrap-Admin-Them

 コントラクト取得用関数(javascriptの先頭に記載)  
 
        web3.setProvider(new web3.providers.HttpProvider('http://localhost:8545'));
        web3.eth.defaultAccount=web3.eth.accounts[0]
        
        var url = "http://127.0.0.1:8545";
        var contAddr = "●●●";
        var ABI = ●●●;
        
        var Web3 = require('web3');
        var web3 = new Web3();
        var provider = new web3.providers.HttpProvider(url);
        web3.setProvider(provider);
        web3.eth.defaultAccount = web3.eth.accounts[0];
        var master = web3.eth.contract(ABI).at(contAddr);
 
ログイン関数  

    //ログイン(アンロック)
    function login() {
        user_name = $("#userName").val();
        var password = $("#password").val();
        var JSONdata = createJSONdata("personal_unlockAccount", [ user_name, password, 30 ]);

        executeJsonRpc(url, JSONdata, function success(data) {
            //ログイン成功
            if (data.error == null) {
                console.log("login success!");
            } else {
                //ログインエラー
                console.log("login error");
            }
            init();
        }, function error(data) {
            //ログインエラー
            console.log("login error");
        });
    }
    
    function isAccountLocked(account) {
          try {
              web3.eth.sendTransaction({
                  from: account,
                  to: account,
                  value: 0
              });
              return false;
          } catch (err) {
              return (err.message == "authentication needed: password or unlock");
          }
      }

    function unlockAccountsIfNeeded(accounts, passwords, unlock_duration_sec = 300) {
        for (var i = 0; i < accounts.length; i++) {
            if (isAccountLocked(accounts[i])) {
                console.log("Account " + accounts[i] + " is locked. Unlocking")
                web3.personal.unlockAccount(accounts[i], passwords[i], unlock_duration_sec);
            }
        }
    }
    
inputタグのidにuserNameとpasswordを記載。
ボタンタグにonclick="login();を記載

任意の関数の作り方
https://qiita.com/kanehara/items/5f09401813b52a326ac5  
https://qiita.com/kenmazsyma/items/e5aa007374ce753ebfd5  
https://ethereum.stackexchange.com/questions/8362/passing-an-array-as-a-parameter-from-javascrpt-web3-to-a-solidity-function
https://ethereum.stackexchange.com/questions/11550/correct-syntax-using-web3-for-contracts-with-multiple-parameter-methods


htmlで文字の書き換え  
http://www.pori2.net/js/DOM/2.html

JSeclpseデバッグ  
http://dotnsf.blog.jp/archives/1064464085.html

導入  
http://blog.potix.jp/2017/07/13/ethreum-contract-develop.html

leaflet plugin
https://qiita.com/pokohide/items/6329f1f92253ced23599

    <html>
    <head>
     <title>Hello world!</title>
    </head>
    <!-- <link rel="stylesheet" href="css/iziModal.min.css">
    <script src="https://code.jquery.com/jquery-2.2.4.min.js" type="text/javascript"></script>
    <script src="js/iziModal.min.js" type="text/javascript"></script> -->
    <link rel="stylesheet" href="css/iziModal.min.css">

    <body>


    <button data-iziModal-open=".iziModal">クリックするとウィンドウが表示されます</button>
    <div class="iziModal" data-izimodal-title="Create New Contract" data-izimodal-subtitle="Please input the detail you create">
    <p>
    name<input type="text" name="名前" value="太郎"><br>
    address<input type="text" name="名前" value="太郎"><br>
    detail<input type="text" name="名前" value="太郎"><br>
    contribute<input type="text" name="名前" value="太郎"><br>
    <button onclick="ubo()" data-izimodal-close="">create!</button>


    <!-- <a href="javascript:void(0)" data-izimodal-close=""></a>
     -->

    <!-- https://qiita.com/mikuhonda/items/9de7c5ef625d7704da2a 揃え方 -->

    </p>
    <!-- / .iziModal --></div>

     <div id="iine" onclick="addElementIine()">
      <img src="iine.png" width="5%" height="10%">
      <!-- <img src="AlwaysIine.png" width="5%" height="10%"> コントラクトからすでにGetしてるか確認して、してたらイベント無 -->
     </div>
     <div id="iineCount">0</div> <!-- コントラクトからGetしてくる -->
     <div id="dame" onclick="addElementDame()">
      <img src="dame.png" width="5%" height="10%">
      <!-- <img src="AlwaysIine.png" width="5%" height="10%"> コントラクトからすでにGetしてるか確認して、してたらイベント無 -->
     </div>
     <div id="dameCount">0</div> <!-- コントラクトからGetしてくる -->
     <input type="text" id="iine2Count" />
     <button type="button" onclick="addElementIine2()">SEND</button>
     <!-- <script src="//ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script> -->
     <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js"></script>

    <script src="js/iziModal.min.js" type="text/javascript"></script>
    <script>

    $(function(){
     $(".iziModal").iziModal();
    })

    function ubo(){
     console.log("a");
      }

      function addElementIine(){
       var s = document.getElementById('iineCount');
       s.innerHTML = parseInt(s.textContent)+1;
       /*
       カウントアップメソッドを実行する、対価のトークンを受け取る
       */
      }
      function addElementDame(){
       var s = document.getElementById('dameCount');
       s.innerHTML = parseInt(s.textContent)+1;
       /*
       カウントアップメソッドを実行する、対価のトークンを受け取る
       */
      }
      function addElementIine2(){
       var s2 = document.getElementById('iine2Count');
       console.log(s2.value);
       /*
       s2の分だけETH送金メソッドを実行する、対価のトークンを受け取る
       */
      }
     </script>
    </body>

    </html>

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

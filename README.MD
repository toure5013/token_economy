HOW TO USE : 

 - git clone https://github.com/toure5013/token_economy.git
 - npm i web3 (install web3)




------------------------------------------------------------------------------------------------------------------------


1 - INCLURE WEB 3 
<!-- INCLURE WEB3 DANS TON CODE : PAR LE CDN METHONE 1-->
<script src="./node_modules/web3/dist/web3.min.js"></script>

<!-- INCLURE WEB3 DANS TON CODE : PAR LE local METHONE 2-->
<script src="./assets/js/web3.js"></script>

<!-- INCLURE WEB3 DANS TON CODE : PAR LE CDN METHONE 3-->
<script src="https://cdnjs.cloudflare.com/ajax/libs/web3/1.6.1-rc.0/web3.min.js"></script>


2 - VERIFY METAMASK AVAILABILITY
<script >
  async function CheckMetamaskConnection() {
    // Modern dapp browsers...
    if (window.ethereum) {
      window.web3 = new Web3(window.ethereum)
      try {
        // Request account access if needed
        // await ethereum.enable(); //depreciated
        // Acccounts now exposed
        // getAccounts()
        return true
      } catch (error) {
        // User denied account access...
        return false
      }
    }
    // Legacy dapp browsers...
    else if (window.web3) {
      window.web3 = new Web3(web3.currentProvider)
      // Acccounts always exposed
      return true
    }
    // Non-dapp browsers...
    else {
      // console.log('not found CheckMetamaskConnection')
      console.log(
        'Non-Ethereum browser detected. You should consider trying MetaMask!',
      )
      return false
    }
  }
</script>

3 - INTERCONNECTION DU SMART CONTRAT

<script >
$(document).ready(async function () {});

if (IsMetamask) {
      //mettre ajour stepper
      console.log(")))))");
      $('.ismetamask-installed').removeClass("bg-danger").addClass('bg-success');
      $('.ismetamask-installed').attr("disabled", true);

      // console.log(web3.eth);
      try {
        myContract = await new web3.eth.Contract(
          SmartContractABI,
          SmartContractAddress,
          {
            data: SmartContractByteCode,
          },
        )
      } catch (error) {
        // console.log(error);
        console.log("Une erreur est advenue");
        return;
      }
}

</script>



/*****************************************************
  * METHODS FOR WALLET AND USER ACCOUNTS
*****************************************************/
/**
* Gets account details
*/

<script>
   async function getAccounts() {
    try {
      const _accounts = await web3.eth.getAccounts()

      for (const account of _accounts) {
        const balanceWei = await web3.eth.getBalance(account)
        const balance = web3.utils.fromWei(balanceWei)
        accounts.push({
          account,
          balance,
        })
      }
      return { error: false, account: accounts[0].account, balance: accounts[0].balance }
    } catch (error) {
      // User denied account access...
      console.log('error getAccounts')
      console.log(error)
      return { error: true, error: error }
    }
  }
</script>


NB : 
L'application ne marche lorsque nous cliquons directement sur le index. Il faut créer un sreveur local

-  php -S localhost:8000   
-  node js (lite server)


4 - interract with your smart contract 
await myContract.methods.mint(1000).send({from: '0x40b43d492bed2Fa90B30CA1618530c1a6b7601C7'})
- cas pratique de la foonction transfert 
    function transfer(address receiver, uint tokens) public override returns (bool success) {
        balances[msg.sender] = safeSub(balances[msg.sender], tokens);
        balances[receiver] = safeAdd(balances[receiver], tokens);
        emit Transfer(msg.sender, receiver, tokens);
        return true;
    }

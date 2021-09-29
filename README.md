<h1 align="center">Criação de Criptomoeda</h1>

<img src="coin-build.jpg" alt="coin-build" width="900" height="500">

## Objetivo

Vamos criar uma criptomoeda do zero, tudo feito no browser através do REMIX IDE, Metamask e por fim vamos lançar nossa criptomoeda na exchange Uniswap.

### Compilar Smart Contract

- Acesse o REMIX IDE através desse <a href="https://remix.ethereum.org/">link</a>.
- Crie um Smart Contract com o nome de _Token.sol_ dentro da pasta **contracts**:

![image](https://user-images.githubusercontent.com/84604722/135319543-f77f85a2-db5f-4f99-95da-d96b965066df.png)

- Cole o código abaixo no Smart Contract que acabamos de criar:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract Token {

    string public name;
    string public symbol;
    uint256 public decimals;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);

    constructor(string memory _name, string memory _symbol, uint _decimals, uint _totalSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        totalSupply = _totalSupply; 
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address _to, uint256 _value) external returns (bool success) {
        require(balanceOf[msg.sender] >= _value);
        _transfer(msg.sender, _to, _value);
        return true;
    }

    function _transfer(address _from, address _to, uint256 _value) internal {
        require(_to != address(0));
        balanceOf[_from] = balanceOf[_from] - (_value);
        balanceOf[_to] = balanceOf[_to] + (_value);
        emit Transfer(_from, _to, _value);
    }

    function approve(address _spender, uint256 _value) external returns (bool) {
        require(_spender != address(0));
        allowance[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    function transferFrom(address _from, address _to, uint256 _value) external returns (bool) {
        require(_value <= balanceOf[_from]);
        require(_value <= allowance[_from][msg.sender]);
        allowance[_from][msg.sender] = allowance[_from][msg.sender] - (_value);
        _transfer(_from, _to, _value);
        return true;
    }

}
```

- Clique em "Compile Token.sol" o contrato:

![image](https://user-images.githubusercontent.com/84604722/135319861-f3b17a3f-d9bc-42d9-9200-1356b82b179e.png)

### Metamask

- Precisamos entrar na nossa wallet da Metamask, instale a extensão do metamask através desse <a href="https://metamask.io/download.html">link</a>.

- Caso não tenha nenhuma wallet, crie uma nova:


- Vamos colocar eth da testnet 



### Deploy do Smart Contract

- Voltando ao IDE REMIX, selecione a opção Deploy and run Transactions:

- Mude o campo **JavascriptVM(London)** para **injected Web3**






Deploy Simple ERC20 Token on Remix
Deploy Token on Remix
Compile and deploy contracts on JVM to check all is working well
Copy Token.sol Solidity Code into a file in Remix rename Token.sol
Select Solidity Compiler Page
On Compiler Options dropdown select 0.8.6 version
Click "Compile Token.sol" button
Select Deploy and Run Transactions Page
Environment dropdown select JavaScript VM
Accounts dropdwon -> pick any of the accounts in dropdown
Deploy Button
Enter the parameters for deployment for (name, symbol, decimals,totalSupply)
Example paramters "TokenName", "TKT", 18, 7000
Click deploy button
Deployed Contracts
Scroll down to deployed contracts section and click on deployed contract
View buttons for all the functions you can carry out on contract e.g approve, transfer etc
Deploy Token to Kovan Testnet
Select Deploy and Run Transactions Page
Environment dropdown select Injected Web3 (to allow use of Metamask)
Accounts dropdwon will have first currently selected Metamask account
Get some testnet ETH, Kovan ETH into the deploying account
Copy the address from accounts
Go to https://linkfaucet.protofire.io/kovan paste account and request some Kovan ETH
Deploy Button
Enter the parameters for deployment for (name, symbol, decimals,totalSupply)
Example paramters "TokenName", "TKT", 18, 7000000000000000000000
Click deploy button and confirm transaction on MetaMask
Deployed Contracts
Scroll down to deployed contracts section and click on deployed contract
View buttons for all the functions you can carry out on contract e.g approve, transfer etc (Deployer will have all the initial tokens)
Copy the Deployed Token address on Deployed Contracts e.g 0x5b01c8aE3185774068AF96978e1461c2A31e8A9e
List ERC20 Token on Uniswap
Go to Uniswap
Click on Pool Tab
Click on More Tab and Select Create Pool
Add Liquidity
Under Select Pair leave ETH selected
Click on Select Token dropdown
Paste your deployed Token address into Search
Your deployed Token will show => Click Import
On same add Liquidity Page, select a fee e.g 0.3% fee ideal for stable pairs
Initialize Pool
On same Liquidity Page => Set the starting price for Token e.g 0.001
Set the price range 0.001 to 0.002
Deposit Amounts
Ensure you have sufficient balances for the amounts you will choose to deposit
Select amount of ETH to deposit e.g 0.001 ETH corresponding equal amount of your Token will be displayed
Click Approve Button and confirm transaction on Metamask
Once transaction finished you can click on Preview to view the added Token vs ETH liquidity pool
Click Add to finalize the adding of assets and liquidity pool creation
New Pool will display once success on your positions on page

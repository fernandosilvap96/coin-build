<h1 align="center">Criação de Criptomoeda</h1>

<img src="coin-build.jpg" alt="coin-build" width="900" height="500">

## Objetivo

Vamos criar uma criptomoeda do zero, tudo feito no browser através do REMIX IDE, Metamask e por fim vamos lançar nossa criptomoeda na exchange Uniswap.

O tutorial será dividido em 4 partes

> Compilar o Smart Contract

> Configurar o Metamask

> Deploy do Smart Contract

> Listar a criptomoeda em uma exchange

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

- Clique em "Compile Token.sol":

![image](https://user-images.githubusercontent.com/84604722/135319861-f3b17a3f-d9bc-42d9-9200-1356b82b179e.png)

### Configurar o Metamask

- Precisamos entrar na nossa wallet do Metamask, instale a extensão do Metamask através desse <a href="https://metamask.io/download.html">link</a>.

- Caso não tenha nenhuma wallet, crie uma nova.

- Agora vamos colocar eth da testnet na nossa wallet, para isso siga os passos abaixo: 

1º Passo: Conecte sua wallet na testnet Kovan:

![image](https://user-images.githubusercontent.com/84604722/135322313-b275e28d-38c6-43c6-a2e4-a8e9aea4176a.png)

2º Passo: Copie o seu endereço:

![image](https://user-images.githubusercontent.com/84604722/135322523-9e97fc33-3b92-446d-b29f-f0b0d14a4489.png)

3º Passo: Acesse o site <a href="https://linkfaucet.protofire.io/kovan">Kovan Faucet</a>, coloque seu endereço e clique em "Send request":

![image](https://user-images.githubusercontent.com/84604722/135322909-0711e1e1-3c21-411c-b6cb-e2ca7fcc2e50.png)

### Deploy do Smart Contract

- Voltando ao IDE REMIX, selecione a opção Deploy and run Transactions:

- Mude o campo "Environment" para **injected Web3**, caso dê erro tente atualizar a página, compilar novamente e então você deve chegar a essa configuração:

![image](https://user-images.githubusercontent.com/84604722/135323933-9e0ff73c-79da-45cf-95d7-043865b08a40.png)

- Coloque os dados para Deploy, ex = Name: _FernandoCoin_ / Symbol: _FC_:

![image](https://user-images.githubusercontent.com/84604722/135324420-a1b6b568-24e5-44b4-8a84-7f55d0c9a071.png)

- Clique em "transact", e então confirme a transação no Metamask.

- Para consultar o endereço do contrato e todas as transações que fizemos, entre no site <a href="https://kovan.etherscan.io/">TESTNET Kovan</a> e coloque o endereço da sua wallet:

![image](https://user-images.githubusercontent.com/84604722/135326533-ebbb6ebd-c993-4322-ae9d-d70416c04d50.png)

- Copie o endereço do contrato que geramos na hora do Deploy, basta clicar em "Contract Creation":

![image](https://user-images.githubusercontent.com/84604722/135326927-f45cf4d2-ceae-4b85-ba8a-ef1574777f18.png)

![image](https://user-images.githubusercontent.com/84604722/135327087-7e93330a-5c90-4ada-81c5-b00731d8aaf6.png)

### Listar a criptomoeda em uma exchange (DEX)

- Com o endereço do nosso contrato copiado, vamos acessar o site da <a href="https://app.uniswap.org/#/swap">Uniswap</a> e então conectar nossa Metamask wallet:

![image](https://user-images.githubusercontent.com/84604722/135327866-8528eec9-d09b-4694-84fe-e27b415be601.png)

- Selecione a opção Metamask e conclua a conexão:

![image](https://user-images.githubusercontent.com/84604722/135328034-dba65e89-bebb-4f8e-8e17-3cbf0270ff5c.png)

- Clique no campo "Selecione um token" e cole o endereço do nosso contrato:

![image](https://user-images.githubusercontent.com/84604722/135331195-6ca230f8-245e-48a8-888f-21c74c5c1020.png)

![image](https://user-images.githubusercontent.com/84604722/135329264-1d83ee14-395a-471b-b774-10d8f9820771.png)

-  Clique em importar, após finalizar a importação nós concluimos esse tutorial.

##### Obrigado pela sua atenção, sinta-se a vontade para entrar em contato caso esteja com alguma dúvida ou para dar feedback.

Linkedin: <a href="https://www.linkedin.com/in/fernando-pinto-405011176/">Fernando Pinto</a> 

Email: fernando-p_@outlook.com



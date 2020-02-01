---
layout: post
title: "Ethereum DAPP"
---
## Understand the flow before Ethereum development ##

---

### Table of Contents 
- geth
- ganache
- node.js
- truffle
- metamask

ethereum dapp 개발하고 싶어서 강의를 들었는데 흐름 파악을 이해하는 것부터 막혔다.. 이제 조금씩 이해하기 시작해서 잊어버리지 않도록 작성해야지!!!! <br>
Mac 을 사용하기 때문에 Mac 환경으로 설명할 것임! <br><br>

---

솔리디티 이론에 대해서 배우고, 실전을 통해 테스팅과 디버깅, 배포를 진행할 것이다. 이때, DAPP 개발에 가장 많이 쓰이는 <mark>트러플 프레임워크랑 가나슈를 사용하여</mark> DAPP을 같이 만들어 볼 것이다. 
<br>

매물은 매입할 수 있고 매입자 정보를 입력한 다음에 제출하게 되면 메타마스크를 통해 운영자 계좌로 송금하게 될 것이고 매입자 정보를 블록체인에 저장한다. 
매입 완료 후에 UI가 업로드되고 블록체인에 저장된 매입자 정보를 볼 수 있다.

이더리움 블록체인이 어떻게 돌아가는지 먼저 geth를 통해서 처음부터 살펴볼 것이다.

---

### <용어정리>

### geth 

Go Ethereum의 약자로, go 언어로 만들어졌고 풀 이더리움 노드를 내 로컬 환경에서 command line interface를 통해 실행시키는 프로그램

```
Version: 1.9.6-stable
Architecture: amd64
Protocol Versions: [63]
Network Id: 1
Go Version: go1.13.1
Operating System: darwin
GOPATH=
GOROOT=/usr/local/Cellar/go/1.13.1/libexec
```
<br>

### ganache

스마트 컨트랙을 개발하는 단계에서 여러 편리한 인터페이스를 제공한다. 보기 좋은 UI로 제공하는 이더리움 블록체인 툴, 계정 미리 생성되어 있고 스마트 컨트랙을 데스트하기엔 최적의 툴이다. <br>
트랜잭션과 블록 등 다양하게 볼 수 있고 사용할 수 있다. <br><br>
NETWORK ID : 가나슈 서버의 내부 블록체인 식별ID가 현재 5777로 초기 설정돼서 이더리움 노드를 실행하는 것이다. <br>

RPC SERVER : geth나 metamask에서 이 주소로 연결하면 가나슈 환경을 그대로 사용할 수 있도록 하는 것이다. <br>

> shaft clap gun expire course crouch magnet furnace grant shop used vacant

<br>

### node.js

server side javascript 플랫폼이고 npm도 같이 설치된다. 트러플 프레임워크도 npm을 통해서 다운 받아야 한다.

```
node -v : v10.16.3
npm -v : 6.9.0
```
<br>

### truffle

스마트 컨트랙을 컴파일하고 테스트하며 배포도 할 수 있게 해주는 프레임워크 <br>
10개의 계정과 개인키 생성, MNEMONIC 등 알아서 생성해줌 

```
Truffle v4.1.15 (core: 4.1.15)
Solidity v0.4.25 (solc-js)
```

<br>

### metamask

<mark>이더리움 개인지갑</mark> <br>
이더리움을 보유하고 송금 및 관리할 수 있는 암호화폐 지갑이다. 메타마스크는 구글 크롬 웹브라우저에서 플러그인 방식으로 사용하는 크롬 확장 프로그램이다. 

<br>

### web3

<mark>Web3는 우리가 이더리움 블록체인과 통신할 수 있도록 해주는 API의 집합체라고 보면 된다.</mark> 즉, 우리의 컨트랙트와 데이터를 주고 받을 수 있도록 정해진 규약대로 메시지를 만들어주는 역할을 한다. 우리는 자바스크립트로 만들어진 Web3를 사용해야 하니, 정확히는 Web3.js를 사용하는 것이다. 

<br><br><br><br>

*참고*

- geth로 다 개발(geth로 직접 private network랑 계정 생성)
- truffle 이미 만들어짐
- ganache 이미 만들어짐
- metamask에 연결 가능

<br>

=> 이렇게 정리를 해보았고 하나씩 적용해보고 서로 연결시켜서 확인도 해봐야겠다.

---
 
 
### geth 이용해보기

geth를 사용해서 로컬 환경에 이더리움 노드를 구축할 것이다. 먼저 순서대로 정리하자면, <br>

- genesis block을 생성하여 private network를 구축(노드 초기화) 
- 4개의 새로운 계정 생성 
- 노드 실행
- 계정 확인 등 가능

---

#### <mark>genesis block 생성</mark>

**- 폴더를 만들어 그 폴더 안으로 들어간다.**

```
> cd Blockchain
```

**- 프라이빗 노드를 만들기 이전에 블록체인 맨 처음 블록인 제네시스 블록을 생성해야함. 노드를 초기화 시키는데 꼭 필요하다.**

```
> puppeth  //genesis block 생성, geth 설치할때 같이 install되는 Tool
```

**- network 이름을 지정한다.**

```
> Please specify a network name to administer (no spaces, hyphens or capital letters please)
> songnetwork
```

**- 2번 제네시스 생성을 누름**

```
What would you like to do? (default = stats)
 1. Show network stats
 2. Configure new genesis
 3. Track new remote server
 4. Deploy network components
 >2
```

**- 1번을 선택**

```
What would you like to do? (default = create)
 1. Create new genesis from scratch
 2. Import already existing genesis
> 1
```
...이어서 해주다가 networkId는 5027 <br>
그리고 제네시스 블록을 json 파일로 추출해야하므로 2번 Manage existing genesis를 누름 <br>
이렇게 마무리가 되면 제네시스 파일이 잘 생성된 것이다! <br><br>

**- json 파일을 열어주면**

```
code songnetwork.json 
```
코드가 열리고, 블록체인의 블록이 어떤 내용을 담고 있나 보여주는 부분이다.
첫 번째 블록의 정보를 나타낸다. 제네시스 내용을 읽고 체인의 첫 시작을 어떻게 해야하는지 초기화 하는 것이다.


<br><br>

#### <mark>private node 초기화</mark>

이제 제네시스 블록을 만들었으니까 이걸 가지고 프라이빗 노드를 초기화를 할 것이다.

```
> geth --datadir . init songnetwork.json
```
geth 명령어를 사용해서 현재 디렉토리 이 블록체인 폴더 안에다가 프라이빗 노드 데이터를 저장하겠다. init은 프라이빗 노드를 초기화하기 위한 제네시스 블록의 파일 이름을 명시하는데 사용된다.

geth가 실행되고 제네시스 블록을 사용해서 노드 초기화를 완성시킨 것이다. 한마디로 이더리움 프라이빗 네트워크가 구축이 된 것이다. 

폴더를 들어가면 geth(모든 chain에 관한 데이터 저장)와 keystore(앞으로 만들 계정들이 들어있는 공간) 폴더가 새로 만들어진 것을 확인할 수 있다.

<br><br>

#### <mark>4개의 새로운 계정 생성</mark>

```
> geth --datadir . account new
```

비밀번호 : 유진

폴더 안에 keystore를 보면 이더리움 계정 4개가 생성된 것을 확인할 수 있다. 

```
> geth --datadir . account list
```

참고로 첫 번째 계정은 모든 채굴 보상이 다 이 계정으로 들어간다.

<br><br>

#### <mark>노드 실행</mark>

노드 초기화를 했으니 노드 실행을 해야하는데 어떤 스크립트를 만들어서 파라미터를 지정해줘야한다. 폴더 안에 nodestart.sh 라는 파일을 만들 것이다. 

```
> vi nodestart.sh
```

```
> geth –-networkid 5027 –-mine –-minerthreads 2 –-datadir “./” –-nodiscover –-rpc –-rpcport “8545” –-rpccorsdomain “*” –-nat “any” –-rpcapi eth,web3,personal,net –-allow-insecure-unlock –-password ./password.sec –-ipcpath “~/Library/Ethereum/geth.ipc”
```

```
> atom password.sec
```

노드 실행

```
> sh nodestart.sh
```
정기적으로 노드가 새로운 블록을 채굴하는 모습을 볼 수 있다. 

<br><br>

#### <mark>계정 확인 등 가능</mark>

노드가 계속 채굴하고 있는 동안 새로운 terminal을 열어서 

```
> geth attach
```

```
Welcome to the Geth JavaScript console!

instance: Geth/v1.9.6-stable/darwin-amd64/go1.13.1
coinbase: 0xcc8826e573d12ed9e827e0223c6cf4913639601d
at block: 66 (Tue, 24 Dec 2019 13:48:03 KST)
 datadir: /Users/song-yujin/Blockchain
 modules: admin:1.0 debug:1.0 eth:1.0 ethash:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0

```

=> coinbase는 우리가 만든 첫 번째 계정을 뜻한다.

<br>


백그라운드로 계속 돌고 있는 노드에 연결시켜서 자바스크립트 콘솔을 여는 것이다. 

```
> eth.coinbase
"0x8d8b684bfbcdaa9cb8fe4733def63faa82cf96ec"
> eth.accounts
["0x8d8b684bfbcdaa9cb8fe4733def63faa82cf96ec", "0x656b2d6c75ac56cb92d6c951f3babfcc84df5b47", "0x82ed21034f88a1a87a4dc61bf4e6f1fb0b5c5dd5", "0xc94afe3e3381524c126c8c420e6bafb1b2dbebf8"]
> eth.getBalance(eth.accounts[1])
0
> eth.getBalance(eth.coinbase)
136000000000000000000
> web3.fromWei(eth.getBalance(eth.coinbase),"ether")
146
> miner.stop()
null
> miner.start()
null
> personal.unlockAccount(eth.coinbase,"dbwls",300)
true
> personal.unlockAccount(eth.accounts[1],"dbwls",300)
true
> eth.sendTransaction({from:eth.coinbase,to:eth.accounts[1],value:web3.toWei(20,"ether")})
"0xd4b4fcba9e6ba0db6fccebac92ac6edd6b8b77c295b2a256c3b6e42f89cee537"
> eth.getBalance(eth.accounts[1])
20000000000000000000
> miner.stop()
null
> 
```

<br><br>

이상 내 로컬 환경에서 돌아가고 있는 이더리움 노드에 geth 콘솔에 연결해서 계정 리스트와 잔액 보는 것과 채굴 멈추기, 재시작, 계정 사이에 송금하기를 배웠습니다. 

<br>

---

### truffle & contract (구조 설명,배포)

지금부터 이더리움 스마트 컨트랙트를 사용한 분산 어플리케이션 개발에 아주 많이 사용하는 트러플 프레임워크를 사용할 것이다.

<br>

**- 블록체인 폴더 안에 트러플 이라는 폴더를 만든다.**

```
Yujins-MacBookPro:~ song-yujin$ cd Blockchain/
Yujins-MacBookPro:Blockchain song-yujin$ mkdir -p truffle
Yujins-MacBookPro:Blockchain song-yujin$ cd truffle
Yujins-MacBookPro:truffle song-yujin$ pwd
/Users/song-yujin/Blockchain/truffle
Yujins-MacBookPro:truffle song-yujin$ truffle init
Downloading...
Unpacking...
Setting up...
Unbox successful. Sweet!

Commands:

  Compile:        truffle compile
  Migrate:        truffle migrate
  Test contracts: truffle test
Yujins-MacBookPro:truffle song-yujin$ code .
```
> truffle init // 이 루트 안에다가 프로젝트를 초기화할 것이다.

폴더 안을 보면 contracts, migrations 등 볼 수 있다. 
contracts : 솔리디티 컨트랙을 보관하는 곳, 컨트랙을 배포할때 스크립트 파일을 실행하게 한다.(밑에 migrations에 있는)


migrations : 스크립트 파일은, 배포하는 과정에 쓰이는 로직이 담겨있다. 이 스크립트 파일은, 위에 파일을 노드에 배포하는 역할을 한다.


**- MyContract.sol , 2_deploy_contracts.js를 만든다.**

```
pragma solidity ^0.4.24;

contract MyContract {
    struct Student {
        string studentName;
        string gender;
        uint age;
    }
   
    mapping(uint256 => Student) studentInfo;
   
    function setStudentInfo(uint _studentId, string _name, string _gender, uint _age) public {
        Student storage student = studentInfo[_studentId];
       
        student.studentName = _name;
        student.gender = _gender;
        student.age = _age;
    }
   
    function getStudentInfo(uint256 _studentId) public view returns (string, string, uint) {
        return (studentInfo[_studentId].studentName, studentInfo[_studentId].gender, studentInfo[_studentId].age);
    }
}
```

```
var MyContract = artifacts.require("./MyContract.sol");

module.exports = function(deployer) {
  deployer.deploy(MyContract);
};
```

이 파일에다가 마이컨트랙 파일을 불러오고 노드에 배포한다.

**- 배포!**

마이컨트랙을 배포할 것이다. 파일 안에 프로젝트 초기화한 곳으로 이동한다. 새로운 터미널로 

```
> truffle develop
```

그러면 트러플 내부에서 이더리움 노드를 실행시키고 테스트 계정 10개를 생성한다. <br>
다른 터미널을 열어서 현재 트러플에서 돌고 있는 노드의 로그 상태를 보는 것을 실행할 것이다.

```
> truffle develop --log //현재 실행중인 트러플 내부의 노드에 연결한다.
```

다른 원래 창으로 다시 돌아와서

```
>migrate //트러플 이더리움 노드에 2개 컨트랙을 배포했다. 트랜잭션 해시와 어느 주소로 배포가 되었는지 알려준다.
```

*우리가 나중에 컨트랙을 수정했으면 또 배포를 해야하는데, 기존에 배포된 주소로는 다시 배포가 되지 않는다. 아예 새로운 주소로 배포해야 한다. 수정할 때마다 사용하는 커맨드가 있다.*

```
>migrate --compile-all --reset
```

##### <mark>-> 이렇게 트러플로 스마트 컨트랙을 배포해보고 트러플 기본 구조를 설명함</mark>

<br>

---

### truffle & contract (트러플 콘솔 사용)

트러플도 web3 API를 지원한다.

```
truffle(develop)> web3.eth.accounts
[ '0x627306090abab3a6e1400e9345bc60c78a8bef57',
  '0xf17f52151ebef6c7334fad080c5704d77216b732',
  '0xc5fdf4076b8f3a5357c5e395ab970b5b54098fef',
  '0x821aea9a577a9b44299b9c15c88cf3087f3b5544',
  '0x0d1d4e623d10f9fba5db95830f7d3839406c6af2',
  '0x2932b7a2355d6fecc4b5c0b6bd44cc31df247a2e',
  '0x2191ef87e392377ec08e7c08eb105ef5448eced5',
  '0x0f4f2ac550a1b4e2280d04c21cea7ebd822934b5',
  '0x6330a553fc93768f612722bb8c2ec78ac90b3bbc',
  '0x5aeda56215b167893e80b4fe645ba6d5bab767de' ]
truffle(develop)> web3.fromWei(web3.eth.getBalance(web3.eth.accounts[0]),"ether")
BigNumber { s: 1, e: 1, c: [ 99, 92686510000000 ] }
truffle(develop)> web3.fromWei(web3.eth.getBalance(web3.eth.accounts[0]),"ether").toNumber()
99.9268651
truffle(develop)> web3.fromWei(web3.eth.getBalance(web3.eth.accounts[1]),"ether").toNumber()
100
truffle(develop)> 

```

이제 우리가 트러플 노드에 배포했던 우리의 마이컨트랙을 가져오고 그 안에 있는 함수를 사용할 것이다. 그것을 사용하기 위해서는 전역 변수에다가 마이컨트랙에 instance를 저장해야한다.

```
>MyContract.deployed().then(function(instance) { app = instance; }) 
```

=> 자바스크립트 문법이고, 마이컨트랙이 배포가 되었으면 ~을 하라. then안에다가 function을 넣어줬고 Instance 가 있음. 콜백으로 받음. 이것을 app에다가 대입을 한다.

app변수를 통해서 노드에 배포된 우리의 마이컨트랙과 소통을 할 수 있다.

app을 누르면 많은 정보를 볼 수 있다. 맨 밑에 우리가 만든 함수를 확인할 수 있다. 


```
truffle(develop)> app.setStudentInfo(1111,"yujin","female",23, {from: web3.eth.accounts[1]})
{ tx:
   '0xe08a3a54445584e46a327d4148e3dd8df6b5fd417b627db79d4ef270d9cc579a',
  receipt:
   { transactionHash:
      '0xe08a3a54445584e46a327d4148e3dd8df6b5fd417b627db79d4ef270d9cc579a',
     transactionIndex: 0,
     blockHash:
      '0xccedb93d1ff388ad4aba8d1676e0b89be06ac13290b7c9919613c0ffc06d6c4f',
     blockNumber: 5,
     gasUsed: 85300,
     cumulativeGasUsed: 85300,
     contractAddress: null,
     logs: [],
     status: '0x1',
     logsBloom:
      '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000' },
  logs: [] }

```

마지막 파리미터는 트러플 내부에서 인식하는 것인데, 함수를 쓸 때 어느 계정으로 불러와서 사용하는 것인지 명시해주는 것이다.

트랜잭션이 성공하면서 receipt 영수증을 받았다. log 보는 terminal을 보면 또 트랜잭션이 생성된 것을 확인할 수 있다.
그리고 이제 2번째 계정 확인하면 100이 이제 아니다. 

확인도 할 수 있다. 

```
truffle(develop)> app.getStudentInfo(1111)
[ 'yujin', 'female', BigNumber { s: 1, e: 1, c: [ 23 ] } ]
```

이 함수는 View 타입을 써서 트랜잭션을 생성하지도 않고 가스가 발생 안된다.


##### <mark>-> 여기까지 트러플만 사용해서 테스팅하는 방법을 알아봤고 굉장히 좋은 환경을 제공해줬다.</mark>

<br>

---

### truffle & contract (가나슈 사용)

<mark>다음으로 트러플과 가나슈 콤보로 테스트할 수 있는 환경을 소개하겠다.</mark> <br>
가나슈를 사용하면 비주얼적으로 쉽게쉽게 진행 상황을 빨리 알아차릴 수 있는 장점이 있다. 그만큼 스마트 컨트랙을 테스트하기에 적당하다.
트러플에서 가나슈 네트워크에 연결을 하겠다.

<br><br>

**- 비주얼코드에서 truffle.js 파일에서**

```
module.exports = {
  networks: {
    ganache: {
      host: "localhost",
      port: 8545,
      network_id: "*"
    }
  }
};   //그리고 가나슈을 확인해본다.
```

이제 환경설정을 했으니까 이제 컨트랙을 가나슈 노드에 배포해보겠다.
<br>
이번에는 트러플 콘솔에 접속하지 않은 상태에서 바로 배포해보겠다.

```
Yujins-MacBookPro:~ song-yujin$ cd Blockchain/
Yujins-MacBookPro:Blockchain song-yujin$ cd truffle/
Yujins-MacBookPro:truffle song-yujin$ truffle migrate --compile-all --reset --network ganache
Compiling ./contracts/Migrations.sol...
Compiling ./contracts/MyContract.sol...
Writing artifacts to ./build/contracts

Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x3ebd94612fa4fc30abc4bba0f05ef8e6f77b2f51de966e428dc39ae26ee6e248
  Migrations: 0x27b61efb1824da5611941285c320386da052efec
Saving successful migration to network...
  ... 0x508077dd93cdf7bbcd0250e942a0063b641fd380933ddee801e53fb27c4f1e09
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying MyContract...
  ... 0x5c87254f580dbcd9d7575f95d7de435a63a269798004ee6491c718ef2e08e7a6
  MyContract: 0x0b4b148c6ab76335899a1294c22f48964cb04869
Saving successful migration to network...
  ... 0x29201dc86b136269a8bb2283b0a883dd53b3486a62bb01e4bb0ce8685e6e5abc
Saving artifacts...
```
컨트랙을 다시 재컴파일하면서 새로운 주소로 컨트랙을 배포한다.
json 파일을 열어보면 networks 쪽에 5027이 생긴 것을 확인할 수 있음. 적혀있는 주소에 컨트랙이 존재한다는 것을 알 수 있다.

<br>

이제 트러플 콘솔에 접속해서 가나슈에 배포된 컨트랙과 소통하겠다.

*트러플 콘솔 들어가기*
```
Yujins-MacBookPro:truffle song-yujin$ truffle console --network ganache
```

```
truffle(ganache)> MyContract.deployed().then(function(instance) { app = instance; })
undefined
truffle(ganache)> app.setStudentInfo(1111,"yujin","female",23, {from:web3.eth.accounts[1]})
{ tx:
   '0x0d5910d94d49ef54fb0e04d5e3021b744070bbeb14445c49e57422e24f3f4e49',
  receipt:
   { transactionHash:
      '0x0d5910d94d49ef54fb0e04d5e3021b744070bbeb14445c49e57422e24f3f4e49',
     transactionIndex: 0,
     blockHash:
      '0x200f52a1efed7cfbe6c3c81d3ac577e407806ea2d931d8e2b8afaf1bc8baab38',
     blockNumber: 5,
     from: '0x2dcca9b61e50d79a90a813fcd6a42c3a3ac52e6f',
     to: '0x0b4b148c6ab76335899a1294c22f48964cb04869',
     gasUsed: 85300,
     cumulativeGasUsed: 85300,
     contractAddress: null,
     logs: [],
     status: '0x1',
     logsBloom:
      '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
     v: '0x1b',
     r:
      '0x80d64d623c02e61903b503856f8ce9d1df3f0845ec71a153981bdf3f59789502',
     s:
      '0x72887662665acfe104e77143084189286c21635951dcb89899e8d5136ed5e613' },
  logs: [] }
truffle(ganache)> 
```
2번째 계정을 사용하면서 가나슈를 확인하면 balance가 감소한 것을 확인할 수 있다. 

##### <mark>-> 방식은 같지만 가나슈 인터페이스를 쓰면서 전보다 더 편하게 직관적으로 테스트 할 수 있다.</mark>


**<mark>이렇게 트러플 시리즈를 통해 트러플은 스마트컨트랙의 빌드와 배포를 간편화시키는 것을 알았고 배포하는 사이클을 관리하고 트러플 콘솔을 통해 스마트컨트랙과 소통할 수 있다는 것을 알게 되었다.</mark>**

---

## 이더리움 부동산 스마트 계약 개발

*부동산 댑에 쓰일 스마트 컨트랙을 만들어볼 것이다. 
단순이 A라는 사람이 전체 매물을 올리면 B라는 사람이 매입가를 지불하고 매입 완료할 수 있는 사이클 예제를 만들 것이다.*

*<이 예제의 시나리오> <br>
매물을 아주 많이 소유한 부자가 사이트에 올린다.
사이트에 접속한 유저들이 자신이 매입하고 싶은 물건을 골라서 자신의 정보(이름,나이)를 입력하고, 매입가를 트랜잭션을 통해서 부자한테 송금하면 매물을 소유하게 된다.*

*매물의 ID와 매물의 정보만 블록체인에서 가져오는 식으로 할 것이다.*


**- 스타터 템플렛 받기**

블록체인 폴더에 들어가서 real-estate 파일을 만들어준다. <br>
truffle init 통해서 빈 프로젝트를 생성했었다. 댑개발에 가장 기본적인 기초환경만 주어졌다. 우리가 웹 개발하면서 많이 쓰이는 부트스트랩, 제이쿼리 파일이 트러플 init과 함께 미리 추가되어져 있으면 더 편리할 것이다. <br>

*댑 개발에 필요한 정형화된 표준 탬플렛을 다운받는 곳 => <mark>https://truffleframework.com</mark> 들어가면 됨*

우리는 프론트앤드 기본중에 기본인 자바스크립트와 제이쿼리를 사용한 표준 탬플릿을 이용할 것임. 

### 코드를 확인해보면 

- <mark>contracts</mark> : 솔리디티 컨트랙을 보관하는 곳, 컨트랙을 배포할때 스크립트 파일을 실행하게 한다.(밑에 migrations에 있는)


- <mark>migrations</mark> : 스크립트 파일은, 배포하는 과정에 쓰이는 로직이 담겨있다. 이 스크립트 파일은, 위에 파일을 노드에 배포하는 역할을 한다.


- <mark>src 폴더</mark>가 추가되어있는데 이 안에다가 댑의 프론트앤드를 담당하는 구조를 설정했다. css 폴더에 부트스트랩 css를 넣어주었다.


- 이미지나 js폴더도 있다. <mark>js폴더</mark>는 프론트앤드 로직을 담당할app.js 파일과 기타 스크립트 파일을 넣어주었다.
truffle과 web.js는 노드와 소통하기 위한 필수적인 파일이다.

- <mark>Real-setatate.json</mark>은 10개의 메몰 데이터를 추가했다, 각각 5개 필드가 있음 아이디 필드 면적 가격 등등 이 데이터를 통해 유저들에게 리스트로 보여주는 역할을 할 것이다.
- <mark>bs-config.json</mark> 은 이 댑을 돌릴때 앞으로 라이트 서버를 통해서 돌릴건데 그때 필요하다.

- <mark>Pack파일</mark>은 라이트 서버를 설치하고 기타 노드 모듈을 npm을 통해 설치할때 필요한 파일 

- <mark>truffle.js</mark>는 환경설정 담당

---

### 컨트랙 소유자 설정 

생성자의 역할이 class의 맴버필드를 초기화하는 사용된다. 솔리디티 생성자도 같다. 다른 언어와 다르게 배포할 때 단 1번만 실행하고 끝이나고 그 이후로는 호출할 수 가 없다. 이 이점을 이용하여 컨트랙의 소유자를 설정할 수 있다. 
즉, 배포할 때 사용된 계정이 이 컨트랙의 소유자가 될 수 있도록 하는 것이다.

```
pragma solidity ^0.4.23;

contract RealEstate {
    address public owner; //자동으로 getter함수가 만들어지게된다.public 

    constructor() public{
        owner = msg.sender;  //우리가 컨트랙을 배포할 때 어떤 계정을 통해서 배포해야됨. 배포하는 단계에서 생성ㅈㅏ가 호출되는데 생성자 안에 있는 이 라인을 읽는다. 주소값을 상태변수 owner에 대입하는 과정. msg.sender는 현재 사용하는 계정으로 이 컨트랙 안에 있는 생성자나 함수를  
    }
}
```


이렇게 기본 탬플랫을 만들고 제이슨 데이터를 불러와서 템플렛을 완성시키고 UI에다가 10개의 매물 리스트를 보이게 해주었다.

---

<sub>참고사이트 : https://hackernoon.com/hands-on-creating-your-own-local-private-geth-node-beginner-friendly-3d45902cc612</sub>



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

마이컨트랙을 배포할 것이다. 파일 안에 프로젝트 초기화한 곳으로 이동한다. 새로운 터미널로 blockchain/truffle 폴더로 들어가서 입력해준다.

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

생성자의 역할이 class의 맴버필드를 초기화하는 사용된다. 솔리디티 생성자도 같다. 다른 언어의 생성자와 다르게 배포할 때 단 1번만 실행하고 끝이나고 그 이후로는 호출할 수가 없다. 이 이점을 이용하여 컨트랙의 소유자를 설정할 수 있다. 
즉, 배포할 때 사용된 계정이 이 컨트랙의 소유자가 될 수 있도록 하는 것이다.

```
pragma solidity ^0.4.23;

contract RealEstate {
    address public owner; //상태변수에 public 을 붙이면 자동으로 getter함수가 만들어지게된다.

    constructor() public{
        owner = msg.sender;  //우리가 컨트랙을 배포할 때 어떤 계정을 통해서 배포해야됨. 배포하는 단계에서 생성자가 호출되는데 생성자 안에 있는 이 라인을 읽는다. 주소값을 상태변수 owner에 대입하는 과정. msg.sender는 현재 사용하는 계정으로 이 컨트랙 안에 있는 생성자나 함수를 불러오는 것, 값은 주소형이다.
    }
}
```

이제 가나슈를 실행해서 가나슈 노드에 우리가 만든 컨트랙을 배포한다. 그리고 owner 변수에 계정주소가 잘 저장이 되었나 확인해 볼 것이다.

 ```
 Yujins-MacBookPro:real-estate song-yujin$ truffle migrate --network ganache
Compiling ./contracts/Migrations.sol...
Compiling ./contracts/RealEstate.sol...
Writing artifacts to ./build/contracts

Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x80351c199218cf85bd21f25ab79cc64354407020362b688e6121bdfb957e8e63
  Migrations: 0x527b5e352f7c3cd9cc6216decc8e0a9ee1714874
Saving successful migration to network...
  ... 0x999c47e43e0df4955878d39fdf55e7f8c9eb1d380f3b723a83f9eb8a1360793f
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Deploying RealEstate...
  ... 0x8856e57f82851f4fd0f570f7e93174234cbcfd060d4ca5365729feca109f67d1
  RealEstate: 0xd8efcddd4ec55b13ca75cca6fd6352c48ca2a5ea
Saving successful migration to network...
  ... 0xbfec8a505d3369db7e1d6e0c85d00cd51f8256a0b39541f06441f489fcd57c7e
Saving artifacts...
 ```
 
 첫번째 계정이 default로 배포하는데 사용되면서 Balance가 줄어들었다.
 
 이제 truffle console 로 들어가서..
 
 ```
 Yujins-MacBookPro:real-estate song-yujin$ truffle console --network ganache
 truffle(ganache)> RealEstate.deployed().then(function(instance) {app=instance;})
undefined
truffle(ganache)> app.owner.call() 
'0x20bb5789f444e47a88c366f0bfe41ecb3c75bd4c'. //이렇게 하면 배포된 소유자가 누구인지 확인할 수 있음.
 ```
앞으로 이 owner의 변수는 어떤 사람이 매물을 매입했을 때 그 매입가를 이 owner 계정으로 송금할 것이다. <br>
정리하면, 가나슈의 첫번째 계정으로 배포하게 됐고 그 계정으로 real-estate 컨트랙의 생성자를 호출해서 이 컨트랙의 onwer 즉, 소유자를 가나슈의 첫번째 계정으로 설정했다. 이 뜻은 내가 사용하고 싶은 계정으로 언제든지 컨트랙의 소유자를 설정할 수 있다는 것인데, 이것은 나중에 볼 것이다. 


---

### 첫 테스팅 

이어서, 우리의 첫 테스트 스크립트를 작성할 것이다. 블록체인의 스마트 컨트랙을 한번 배포하면, 배포된 주소에서는 수정이 불가능하기 때문에 최대한 많은 테스팅을 하고 메인넷에 배포해야된다.<br>
테스트 폴더에 스크립트 파일을 하나 만들 것이다.

> TrestRealEstate.js

처음 필요한게 real-estate 컨트랙을 가져와서. 변수로 접근할 수 있도록 하는 것이다.

 ```
var RealEstate = artifacts.require("./RealEstate.sol"); //솔리디티 파일을 가져옴

contract('RealEstate',function(accounts){
var realEstateInstance; //전역변수를 하나 선언.

    it("컨트랙의 소유자 초기화 테스팅",function(){
        return RealEstate.deployed().then(function(instance) {
            realEstateInstance = instance;
            return realEstateInstance.owner.call();
        }).then(function(owner){
            assert.equal(onwer.toUpperCase(), accounts[0].toUpperCase(),"owner가 가나슈 첫번째 계정과 동일하지 않습니다.");
        });
    });
});  //컨트랙을 테스트할 것인데, 2개의 인자를 받는다. 첫번째는 테스팅할 컨트랙의 이름, 2번째는 function을 받는데 계정이라는 인자를 콜백으로 받는다. accounts는 현재 연결된 노드에서 쓸 수 있는 계정들. 현재 가나슈 10개의 계정들을 말한다.
 ```
이제 터미널 열어서 트러플 테스트 커맨드를 통해서 통과하는지 볼 것이다.

```
Yujins-MacBookPro:real-estate song-yujin$ truffle test --network ganache
Using network 'ganache'.



  Contract: RealEstate
    ✓ 컨트랙의 소유자 초기화 테스팅


  1 passing (70ms)

```
여기까지 컨트랙 테스트를 실행해봤다.


---

### 매물 구입

매물 구입 함수를 만들어볼 것이다.

```
pragma solidity ^0.4.23;

contract RealEstate {
    struct Buyer{
        address buyerAddress; //매입자 계정주소
        bytes32 name;
        uint age;
    }
    mapping (uint => Buyer) public buyerInfo; //상태변수로 매핑
    address public owner;
    address[10] public buyers; //상태변수로 address타입의 고정된 배열을 선언
    constructor() public {
        owner = msg.sender;
    }

    function buyRealEstate(uint _id, bytes32 _name, uint _age) public payable{
        require(_id >= 0 && _id <= 9); //매물의 아이디가 0~9사이인지 체크함.
        buyers[_id] = msg.sender;
        buyerInfo[_id] = Buyer(msg.sender, _name, _age);

        owner.transfer(msg.value); //owner로 ether를 송금함

    }   //ether를 이 함수로 보내는 것이다.
}
```

이제 console에서 함수를 실행할 것이다.

```
Yujins-MacBookPro:real-estate song-yujin$ truffle migrate --compile-all --reset --network ganache
Compiling ./contracts/Migrations.sol...
Compiling ./contracts/RealEstate.sol...
Writing artifacts to ./build/contracts

Using network 'ganache'.

Running migration: 1_initial_migration.js
  Replacing Migrations...
  ... 0x5f25402b78d79d8f57a39b688a2474ebc85f1784fcca522d196cdf1e80571c25
  Migrations: 0xf9d00357bc93ece708686cff2b1f16d10783f2e0
Saving successful migration to network...
  ... 0x722ba993520212e220e518a7dcb065bba74e0f25e8cb91e2e2300b9bbbdca88b
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Replacing RealEstate...
  ... 0x3bb3ed3f2eb85b763695b38a436ae28f0e37e9ef2b8bd57718c220a1ab8fb593
  RealEstate: 0x955cb5c19a59d2fbee8dfac4dcee0e9e45b0775b
Saving successful migration to network...
  ... 0x512e40f5167705c1e908602c49a7a14bc3a9d4a81f0a1cd176197597586d9181
Saving artifacts...
(base) Yujins-MacBookPro:real-estate song-yujin$ truffle console --network ganache
truffle(ganache)> RealEstate.deployed().then(function(instance) { app = instance; })
undefined
truffle(ganache)> app.buyRealEstate(0,"yujin",24,{from: web3.eth.accounts[1], value: web3.toWei(1.50, "ether")})
{ tx:
   '0x6acb704adadc0b117a6fc27830b08b673619ba2319edab4ffcf217f1e469b46a',
  receipt:
   { transactionHash:
      '0x6acb704adadc0b117a6fc27830b08b673619ba2319edab4ffcf217f1e469b46a',
     transactionIndex: 0,
     blockHash:
      '0xaa3925e4d1a65e2cff08d384ba194a087ce3ac8cc06cc4b038e08dc3d640710c',
     blockNumber: 72,
     from: '0x2dcca9b61e50d79a90a813fcd6a42c3a3ac52e6f',
     to: '0x955cb5c19a59d2fbee8dfac4dcee0e9e45b0775b',
     gasUsed: 110901,
     cumulativeGasUsed: 110901,
     contractAddress: null,
     logs: [],
     status: '0x1',
     logsBloom:
      '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
     v: '0x1b',
     r:
      '0xf667ca2e6ce37d172d993dbdf3f8ae26629c051ce270a57de070381b0f92925d',
     s:
      '0x57774900756b0f065e4e88fec775c723a84d840c144fed32611c32534ad3ad3a' },
  logs: [] }
truffle(ganache)> 
```


---

### 이벤트(Event)

매물을 어떤 유저가 매입하면 매입이 완료되었다는 메시지를 생성할 것이다. 이벤트를 통해서 할 것이다. 생성자 위에다가 이벤트 구조를 만들어줄 것이다.

참고로, 어떤 이벤트가 발생되었을 때 이벤트 내용도 블록 안에 저장된다. 그래서 log 기록한다는 이름을 붙인 것. 

```
pragma solidity ^0.4.23;

contract RealEstate {
    struct Buyer{
        address buyerAddress; //매입자 계정주소
        bytes32 name;
        uint age;
    }
    mapping (uint => Buyer) public buyerInfo; //상태변수로 매핑
    address public owner;
    address[10] public buyers; //상태변수로 address타입의 고정된 배열을 선언

    //완료메시지로 어떤 계정에서 몇번 매물을 매입했습니다. 가 나올 것
    event LogBuyRealEstate( 
        address _buyer,
        uint _id
    );

    constructor() public {
        owner = msg.sender;
    }

    function buyRealEstate(uint _id, bytes32 _name, uint _age) public payable{
        require(_id >= 0 && _id <= 9); //매물의 아이디가 0~9사이인지 체크함.
        buyers[_id] = msg.sender;
        buyerInfo[_id] = Buyer(msg.sender, _name, _age);

        owner.transfer(msg.value); //owner로 ether를 송금함
        emit LogBuyRealEstate(msg.sender, _id);
    }   //ether를 이 함수로 보내는 것이다.
}
```

이제 console에서 이 이벤트를 어떻게 발생시키는지 확인할 것이다.

```
truffle(ganache)> migrate --compile-all --reset
Compiling ./contracts/Migrations.sol...
Compiling ./contracts/RealEstate.sol...
Writing artifacts to ./build/contracts

Using network 'ganache'.

Running migration: 1_initial_migration.js
  Replacing Migrations...
  ... 0xd4ed279f4a332e5709b9062c80726ff43374771f10ac629cd4ccc95001759f08
  Migrations: 0xe8222a494e47e919fc6bac97fc8df2ea647e31ae
Saving successful migration to network...
  ... 0x9620d881710316e84198df5f76aeb527729cc29f1caf588514a18cffc119b0ae
Saving artifacts...
Running migration: 2_deploy_contracts.js
  Replacing RealEstate...
  ... 0x188b5bc96c6b4c35641d4e877d69205a7a1b863094ec4b0c5868753f93c1d0f2
  RealEstate: 0xc357bcf3242b8c42d2a560b6762484b716685e5b
Saving successful migration to network...
  ... 0xc7b97d6b1608813d559ad430d19009c648e232dbb6c644e0d6d37b5626b5f060
Saving artifacts...
truffle(ganache)> RealEstate.deployed().then(function(instance) { app = instance; })
undefined
truffle(ganache)> app.LogBuyRealEstate({}, {fromBlock: 0, toBlock: 'latest'}).watch(function(error, event) { console.log(event); })
Filter {
  requestManager:
   RequestManager {
     provider: Provider { provider: [HttpProvider] },
     polls: {},
     timeout: null },
  options:
   { topics:
      [ '0x0868a2b77ef5243ab424f87952a349bc823a92fd01d9b45d2fec78b8eafb586b' ],
     from: undefined,
     to: undefined,
     address: '0xc357bcf3242b8c42d2a560b6762484b716685e5b',
     fromBlock: '0x0',
     toBlock: 'latest' },
  implementation:
   { newFilter:
      { [Function: send] request: [Function: bound ], call: [Function: newFilterCall] },
     uninstallFilter:
      { [Function: send] request: [Function: bound ], call: 'eth_uninstallFilter' },
     getLogs:
      { [Function: send] request: [Function: bound ], call: 'eth_getFilterLogs' },
     poll:
      { [Function: send] request: [Function: bound ], call: 'eth_getFilterChanges' } },
  filterId: null,
  callbacks: [ [Function] ],
  getLogsCallbacks: [],
  pollFilters: [],
  formatter: [Function: bound ] }
truffle(ganache)> app.buyRealEstate(0,"yujin",24,{from:web3.eth.accounts[1], value: web3.toWei(1.50, "ether")})
{ tx:
   '0x35b42c2785cd7c8112f107fb00a49aca7d7b23662ff28c39b3e45c75aa1d0ce1',
  receipt:
   { transactionHash:
      '0x35b42c2785cd7c8112f107fb00a49aca7d7b23662ff28c39b3e45c75aa1d0ce1',
     transactionIndex: 0,
     blockHash:
      '0x89079d8277dd5690aea093ef4a99beb2a50ce452e98d8184a35b3270bc80ccfa',
     blockNumber: 77,
     from: '0x2dcca9b61e50d79a90a813fcd6a42c3a3ac52e6f',
     to: '0xc357bcf3242b8c42d2a560b6762484b716685e5b',
     gasUsed: 112255,
     cumulativeGasUsed: 112255,
     contractAddress: null,
     logs: [ [Object] ],
     status: '0x1',
     logsBloom:
      '0x00000000000000000000080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000',
     v: '0x1c',
     r:
      '0x5aca08e765d32125004e892522f035e65b9b3fc144b02feb08576b0e83ca2796',
     s:
      '0x2cb76a4e90c6517028a970117d4263c50122a5b97d2253bf7fc9a9b49c20fe68' },
  logs: 		//이벤트의 모든 정보들이 나와있음, 블록에 저장함.
   [ { logIndex: 0,
       transactionIndex: 0,
       transactionHash:
        '0x35b42c2785cd7c8112f107fb00a49aca7d7b23662ff28c39b3e45c75aa1d0ce1',
       blockHash:
        '0x89079d8277dd5690aea093ef4a99beb2a50ce452e98d8184a35b3270bc80ccfa',
       blockNumber: 77,
       address: '0xc357bcf3242b8c42d2a560b6762484b716685e5b',
       type: 'mined',
       event: 'LogBuyRealEstate',
       args: [Object] } ] }
truffle(ganache)> { logIndex: 0,	//이벤트 초기화했을 때 나온 정보..
  transactionIndex: 0,
  transactionHash:
   '0x35b42c2785cd7c8112f107fb00a49aca7d7b23662ff28c39b3e45c75aa1d0ce1',
  blockHash:
   '0x89079d8277dd5690aea093ef4a99beb2a50ce452e98d8184a35b3270bc80ccfa',
  blockNumber: 77,
  address: '0xc357bcf3242b8c42d2a560b6762484b716685e5b',
  type: 'mined',
  event: 'LogBuyRealEstate',
  args:	//두 필드가 잘 작동되는 것을 확인할 수 있음.
   { _buyer: '0x2dcca9b61e50d79a90a813fcd6a42c3a3ac52e6f',
     _id: BigNumber { s: 1, e: 0, c: [Array] } } }
```

---

### 읽기전용 함수들

컨트랙의 마지막 함수들을 만들 것이다.  <br>
첫번째는 매입자의 정보를 불러오는 함수-> 어떻게 가져오나? buyerInfo를 이용한다.

```
pragma solidity ^0.4.23;

contract RealEstate {
    struct Buyer{
        address buyerAddress; //매입자 계정주소
        bytes32 name;
        uint age;
    }
    mapping (uint => Buyer) public buyerInfo; //상태변수로 매핑
    address public owner;
    address[10] public buyers; //상태변수로 address타입의 고정된 배열을 선언

    //완료메시지로 어떤 계정에서 몇번 매물을 매입했습니다. 가 나올 것
    event LogBuyRealEstate( 
        address _buyer,
        uint _id
    );

    constructor() public {
        owner = msg.sender;
    }

    function buyRealEstate(uint _id, bytes32 _name, uint _age) public payable{
        require(_id >= 0 && _id <= 9); //매물의 아이디가 0~9사이인지 체크함.
        buyers[_id] = msg.sender;
        buyerInfo[_id] = Buyer(msg.sender, _name, _age);

        owner.transfer(msg.value); //owner로 ether를 송금함
        emit LogBuyRealEstate(msg.sender, _id);
    }   //ether를 이 함수로 보내는 것이다.

    function getBuyerInfo(uint _id) public view returns (address, bytes32, uint){
        //매개변수로 받은 매물 아이디를 사용해서 키값으로 쓰고 해당 value값을 가져온다.
        Buyer memory buyer = buyerInfo[_id]; //id를 넘겨서 키값으로 쓰고 매입자를 불러와서 저장..

        return (buyer.buyerAddress, buyer.name, buyer.age); 
    }

//매입자들의 계정을 저장하는 배열
    function getAllBuyers() public view returns (address[10]){
        return buyers;
    }
}
```

이제 console에서 함수들을 실행할 것.


---

### 마무리 테스팅

```
var RealEstate = artifacts.require("./RealEstate.sol");

contract('RealEstate', function(accounts) { 
    var realEstateInstance;

    it("컨트랙의 소유자 초기화 테스팅", function() {
        return RealEstate.deployed().then(function(instance) {     
            realEstateInstance = instance;
            return realEstateInstance.owner.call();
        }).then(function(owner) {
            assert.equal(owner.toUpperCase(), accounts[0].toUpperCase(), "owner가 가나슈 첫번째 계정과 동일하지 않습니다.");       
        });
    });   

    it("가나슈 두번째 계정으로 매물 아이디 0번 매입 후 이벤트 생성 및 매입자 정보와 buyers 배열 테스팅", function() {
        return RealEstate.deployed().then(function(instance) {
            realEstateInstance = instnace;
            return realEstateInstance.buyRealEstate(0, "yujin", 24, {from: accounts[1], value: web3.toWei(1.50, "ether")});
        }).then(function(receipt){
            assert.equal(receipt.logs.length, 1, "이벤트 하나가 생성되지 않았습니다.");
            assert.equal(receipt.logs[0].event, "LogBuyRealEstate", "이벤트가 LogBuyRealEstate가 아닙니다.");
            assert.equal(receipt.logs[0].args._buyer, accounts[1], "매입자가 가나슈 두번째 계정이 아닙니다.");
            assert.equal(receipt.logs[0].args._id, 0, "매물 아이디가 0이 아닙니다.");
            return realEstateInstance.getBuyerInfo(0);
        }).then(function(buyerInfo){
            assert.equal(buyerInfo[0].toUpperCase(), accounts[1].toUpperCase(), "매입자의 계정이 가나슈 두번째 계정과 일치하지 않습니다.");
            assert.equal(web3.toAscii(buyerInfo[1]).replace(/\0/g, ''), "yujin", "매입자의 이름이 yujin이 아닙니다.");
            assert.equal(buyerInfo[2], 24, "매입자의 나이가 24살이 아닙니다.");
            return realEstateInstance.getAllBuyers();
        }).then(function(buyers){
            assert.equal(buyers[0].toUpperCase(), accounts[1].toUpperCase(), " Buyers 배열 첫번째 인덱스의 계정이 가나슈 듀번째 계정과 일치하지 않습니다. ")
        });
    })
}); 
```


---

## 이더리움 부동산 프론트앤드 개발

노드 모듈을 install 해야된다.  packeage.json 안에 있는 lite-server를 다운 받아야한다. terminal에서

```
Yujins-MacBookPro:real-estate song-yujin$ npm install
npm WARN deprecated fsevents@1.2.12: fsevents 1 will break on node v14+. Upgrade to fsevents 2 with massive improvements.

> fsevents@1.2.12 install /Users/song-yujin/Documents/Blockchain/real-estate/node_modules/fsevents
> node-gyp rebuild

gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_ORG_MIRROR
gyp WARN download NVM_NODEJS_ORG_MIRROR is deprecated and will be removed in node-gyp v4, please use NODEJS_ORG_MIRROR
No receipt for 'com.apple.pkg.CLTools_Executables' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLILeo' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLI' found at '/'.

gyp: No Xcode or CLT version detected!
gyp ERR! configure error 
gyp ERR! stack Error: `gyp` failed with exit code: 1
gyp ERR! stack     at ChildProcess.onCpExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/configure.js:345:16)
gyp ERR! stack     at ChildProcess.emit (events.js:198:13)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:248:12)
gyp ERR! System Darwin 19.4.0
gyp ERR! command "/usr/local/bin/node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Users/song-yujin/Documents/Blockchain/real-estate/node_modules/fsevents
gyp ERR! node -v v10.16.3
gyp ERR! node-gyp -v v3.8.0
gyp ERR! not ok 
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN realestate@1.0.0 No description
npm WARN realestate@1.0.0 No repository field.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 (node_modules/fsevents):
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.12 install: `node-gyp rebuild`
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: Exit status 1

added 335 packages from 271 contributors and audited 3508 packages in 12.056s
found 1 low severity vulnerability
  run `npm audit fix` to fix them, or `npm audit` for details
```

노드 모듈 폴더가 생성되면서 안에 라이트 서버를 포함한 기타 댑 실행에 필요한 모듈들이 설치된다. <br>
폴더가 생성되면서 안에 여러가지 모듈들이 설치되었다.

<mark>app.js 파일</mark>이 앞으로 댑을 움직일 엔진 같은 존재이다.

real-estate.json 각각의 데이터를 가져와서 우리가 만든 필드에 넣어서 매물 리스트에 넣을 것이다.

```
<div id="template" style="display: none;">
      <div class="col-sm-6 col-md-4 col-lg-3">
        <div class="panel panel-success panel-realEstate">
          <div class="panel-heading">
            <h3 class="panel-title">매물</h3>
          </div>
          <div class="panel-body">
            <img style="width: 100%;" src="">
            <br/><br/>
            <strong>아이디</strong>: <span class="id"></span><br/>
            <strong>종류</strong>: <span class="type"></span><br/>
            <strong>면적(m2)</strong>: <span class="area"></span><br/>
            <strong>가격(ETH)</strong>: <span class="price"></span><br/>
            <button class="btn btn-info btn-buy"
                    type="button"
                    data-toggle="modal"
                    data-target="#buyModal">
                    매입
            </button>
            <button class="btn btn-info btn-buyerInfo"
                    type="button"
                    data-toggle="modal"
                    data-target="#buyerInfoModal"
                    style="display: none;">
                    매입자 정보
            </button>
          </div>
        </div>
      </div>
    </div>
    
    
    init: function() {
    $.getJSON('../real-estate.json', function(data){
      var list = $('#list');
      var template = $('#template');

      for (i = 0; i < data.length; i++){
        template.find('img').attr('src',data[i].picutre);
        template.find('.id').text(data[i].id);
        template.find('.type').text(data[i].type);
        template.find('.area').text(data[i].area);
        template.find('.price').text(data[i].price);
        
        list.append(template.html());
      }
    })
  },
```

터미널로 실행한다.

```
 Yujins-MacBookPro:real-estate song-yujin$ npm run dev
```

10개의 리스트가 잘 나온다. 기본 탬플릿을 만들고 Json 데이터를 가져와서 탬플릿을 완성시키고 UI에다가 10개의 리스트가 잘 나오도록 해주었다.


---

## Web3 & 컨트랙 인스턴스화

web3.min.js 파일이 이더리움 블록체인과 소통할 수 있게 해주는 라이브러리이다. 스마트컨트랙과 연결해주는 중요한 파일이다. 우리 댑에서 쓸 수 있도록 먼저 인스턴스화 시킨다. 


```
App = {
  web3Provider: null,
  contracts: {},
	
  init: function() {
    $.getJSON('../real-estate.json', function(data){
      var list = $('#list');
      var template = $('#template');

      for (i = 0; i < data.length; i++){
        template.find('img').attr('src',data[i].picture);
        template.find('.id').text(data[i].id);
        template.find('.type').text(data[i].type);
        template.find('.area').text(data[i].area);
        template.find('.price').text(data[i].price);
        
        list.append(template.html());
      }
    })

    return App.initWeb3();
  },

  initWeb3: function() {
    if (typeof web3 != 'undefined' ){
      App.web3Provider = web3.currentProvider;
      web3 = new Web3(web3.currentProvider);
    } else{
      App.web3Provider = new web3.providers.HttpProvider('http://localhost:8545');
      web3 = new Web3(App.web3Provider);
    }

    return App.initContract;
  },
  //이것을 통해 댑에서 이더리움 블록체인과 소통할 수 있게 되었다.

  //우리가 만든 스마트컨트랙을 인스턴스화할 함수. 그래야 web3가 컨트랙을 어디에서 찾아야하고 어떻게 작동하는지 알 수 있다.
  initContract: function() {
		$.getJSON('RealEstate.json', function(data){
      App.contracts.RealEstate = TruffleContract(data);
      App.contracts.RealEstate.setProvider(App.web3Provider);
    })
  },

  buyRealEstate: function() {	

  },

  loadRealEstates: function() {
	
  },
	
  listenToEvents: function() {
	
  }
};

$(function() {
  $(window).load(function() {
    App.init();
  });
});

```


---

## 매입자 정보 모달 및 데이터 전달

프론트앤드에서 매물 구입 함수에 데이터를 어떻게 보낼 수 있는지 만들어볼 것이다. 블록체인에 정보들을 저장시키는 중요한 것이다.

> http://bootstrapdocs.com/v3.3.6/docs/javascript/#modals

사이트에 들어가서 예제를 복사한다. 수정한 것으로!

```
<div class="modal fade" tabindex="-1" role="dialog" id="buyModal">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title">Modal title</h4>
      </div>
      <div class="modal-body">
        <p>One fine body&hellip;</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```

우리가 만든 index.html의 template 밑에다가 수정해서 넣어준다.

```
    <div class="modal fade" tabindex="-1" role="dialog" id="buyModal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title">매입자 정보</h4>
          </div>
          <div class="modal-body">
            <input type="hidden" id="id" />
            <input type="hidden" id="price" />
            <input type="text" class="form-control" id="name" placeholder="이름" /><br/>
            <input type="number" class="form-control" id="age" placeholder="나이" />
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-default" data-dismiss="modal">닫기</button>
            <button type="button" class="btn btn-primary" onclick="App.buyRealEstate(); return false;">제출</button>
          </div>
        </div><!-- /.modal-content -->
      </div><!-- /.modal-dialog -->
    </div><!-- /.modal -->
```

```
App = {
  web3Provider: null,
  contracts: {},
	
  init: function() {
    $.getJSON('../real-estate.json', function(data){
      var list = $('#list');
      var template = $('#template');

      for (i = 0; i < data.length; i++){
        template.find('img').attr('src',data[i].picture);
        template.find('.id').text(data[i].id);
        template.find('.type').text(data[i].type);
        template.find('.area').text(data[i].area);
        template.find('.price').text(data[i].price);
        
        list.append(template.html());
      }
    })

    return App.initWeb3();
  },

  initWeb3: function() {
    if (typeof web3 != 'undefined' ){
      App.web3Provider = web3.currentProvider;
      web3 = new Web3(web3.currentProvider);
    } else{
      App.web3Provider = new web3.providers.HttpProvider('http://localhost:8545');
      web3 = new Web3(App.web3Provider);
    }

    return App.initContract;
  },
  //이것을 통해 댑에서 이더리움 블록체인과 소통할 수 있게 되었다.

  //우리가 만든 스마트컨트랙을 인스턴스화할 함수. 그래야 web3가 컨트랙을 어디에서 찾아야하고 어떻게 작동하는지 알 수 있다.
  initContract: function() {
		$.getJSON('RealEstate.json', function(data){
      App.contracts.RealEstate = TruffleContract(data);
      App.contracts.RealEstate.setProvider(App.web3Provider);
    });
  },

  buyRealEstate: function() {	
    var id = $('#id').val();
    var name = $('#name').val();
    var price = $('#price').val();
    var age = $('#age').val();

    console.log(id);
    console.log(price);
    console.log(name);
    console.log(age);

    $('#name').val('');
    $('#age').val('');

  },

  loadRealEstates: function() {
	
  },
	
  listenToEvents: function() {
	
  }
};

$(function() {
  $(window).load(function() {
    App.init();
  });

  $('#buyModal').on('show.bs.modal', function(e) {
    var id = $(e.relatedTarget).parent().find('.id').text();
    var price = web3.toWei(parseFloat($(e.relatedTarget).parent().find('.price').text() || 0), "ether");

    $(e.currentTarget).find('#id').val(id);
    $(e.currentTarget).find('#price').val(price);
  });
});
```

매입자 이름, 나이를 모달에서 입력하고 제출 버튼 입력하면 총 4개의 데이터를 매물 구입 함수에서 받을 수 있도록 했다.<br>
 그 다음에는 받은 값들을 컨트랙 매물 구입 함수에 매개변수로 넘기겠다.
 
 ---

## 컨트랙 매물구입함수 연결
 
 ```
App = {
  web3Provider: null,
  contracts: {},
	
  init: function() {
    $.getJSON('../real-estate.json', function(data) {
      var list = $('#list');
      var template = $('#template');

      for (i = 0; i < data.length; i++) {
        template.find('img').attr('src', data[i].picture);
        template.find('.id').text(data[i].id);
        template.find('.type').text(data[i].type);
        template.find('.area').text(data[i].area);
        template.find('.price').text(data[i].price);

        list.append(template.html());
      }
    })

    return App.initWeb3();
  },

  initWeb3: function() {
    if (typeof web3 !== 'undefined') {
      App.web3Provider = web3.currentProvider;
      web3 = new Web3(web3.currentProvider);
    } else {
      App.web3Provider = new web3.providers.HttpProvider('http://localhost:8545');
      web3 = new Web3(App.web3Provider);
    }

    return App.initContract();
  },

  initContract: function() {
	$.getJSON('RealEstate.json', function(data) {
      App.contracts.RealEstate = TruffleContract(data);
      App.contracts.RealEstate.setProvider(App.web3Provider);
    });
  },

  buyRealEstate: function() {	
    var id = $('#id').val();
    var name = $('#name').val();
    var price = $('#price').val();
    var age = $('#age').val();

    web3.eth.getAccounts(function(error, accounts) {
      if (error) {
        console.log(error);
      }

      var account = accounts[0];
      App.contracts.RealEstate.deployed().then(function(instance) {
        var nameUtf8Encoded = utf8.encode(name);
        return instance.buyRealEstate(id, web3.toHex(nameUtf8Encoded), age, { from: account, value: price });
      }).then(function() {
        $('#name').val('');
        $('#age').val('');
        $('#buyModal').modal('hide');       
      }).catch(function(err) {
        console.log(err.message);
      });
    });
  },

  loadRealEstates: function() {
	
  },
	
  listenToEvents: function() {
	
  }
};

$(function() {
  $(window).load(function() {
    App.init();
  });

  $('#buyModal').on('show.bs.modal', function(e) {
    var id = $(e.relatedTarget).parent().find('.id').text();
    var price = web3.toWei(parseFloat($(e.relatedTarget).parent().find('.price').text() || 0), "ether");

    $(e.currentTarget).find('#id').val(id);
    $(e.currentTarget).find('#price').val(price);
  });
});
```

이제 터미널로..

```
truffle migrate --compile-all --reset --network ganache
npm run dev
```


<메타마스크 에러 해결> 
settings 들어가서 connections 들어가서 Add site 탭에서 loaclhost입력하고 connect 버튼 누르니 해결되었다.


**정리**
어카운트 4에서 매물을 매입하면서 컨트랙의 buyrealEstate에 데이터를 넘겼고 함수 내에서 owner 계정으로 송금했다. 



 
 
 
---

<sub>참고사이트 : https://hackernoon.com/hands-on-creating-your-own-local-private-geth-node-beginner-friendly-3d45902cc612</sub>



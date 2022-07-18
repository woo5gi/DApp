# Dapp (NFT 생성, NFT 구매 및 판매)
**스마트 컨트랙트 (솔리디티)**

- NFT 민팅 (생성)
- NFT 판매 (구매 및 판매)
- 리믹스 (스마트 컨트랙트 IDE) 사용법

**프론트엔드 (React, Web3.js)**

- 프론트엔드 셋팅
- 메타마스크 (블록체인 지갑) 사용법
- 스마트 컨트랙트 연동 (Web3.js)
- 차크라UI (간단한 UI 디자인)

**스마트 컨트랙트 (솔리디티)**

- NFT 민팅 (생성)
- NFT 판매 (구매 및 판매)


# 솔리드 깨부시기 기본

### **1강 Hello Solidity**

**정의**

Solidity는 스마트 계약을 구현하기 위한 객체 지향 고급 언어입니다. 스마트 계약은 이더리움 상태 내에서 계정의 동작을 제어하는 프로그램입니다.

**문법**

solidity 파일 생성시 라이센스 명시를 맨 윗줄에 해줘야 한다.

print function 이 없어서 log를 사용한다.

문장이 끝날때마다 세미콜론을 붙여줘야한다

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract lec1{
     string public hi = "Hello Solidity";
}
```

### **2강 data type**

**1. boolean : true 와 false** 

! (Not) ex) !true => false

&& (AND) ex) true && false => false

|| (OR) ex) true && false => true

== (equality) ex) true == true => true

!= (inequality) ex) true != true => false

**2. string : string 형을 쓰실때는 " " 를 붙여서 쓰시면 됩니다.**

그러나, 솔리디티에서는 string 쓰는 것을 지양 ⇒  가스를 더 소비하기 때문

가스 = 스마트컨트랙을 운영시키는 연료

솔리디티 입장에서 string을 받아서 다시 byte화 시켜서 이해

반대로 byte를 string화 하여 꺼낸다

string과 byte를 왔다갔다 변경하여 가스를 소비하는것보단, 솔리디티입장에서 편하게 byte를 받는것을 더 좋아함

**3. bytes : 솔리디티는 byte1 ~ byte32 까지 존재**

뒤에 숫자에따라 byte의 크기 가 정해진다

byte32 로 쓴다면 길이가 32 개

byte의 크기를 안다면 크기에 맞게 지정해주시는 편이 낫다

**4. Integer : Integer 는 두가지 타입으로 나뉘어요**

int : 기호있는 integer

uint: 기호없는 integer

순전히 기호 있고 없는 차이는 음수의 값을 쓰냐 안쓰냐에 따라서 인티져의 범위가 달라진다

int : 기호있는 integer

- int8 : -2^7 ~ 2^7-1
- int16: -2^15~2^15-1
- int32: -2^31~2^31-1
- int64: -2^63~2^63-1
- int128 : -2^127~2^127-1
- int256 (=int): -2^255~2^255-1

uint: 기호없는 integer

- uint8 : 0~2^8-1
- uint16: -0~2^16-1
- uint32: -0~2^32-1
- uint64: -0~2^64-1
- uint128 : -0~2^128-1
- uint256 (=uint): 0~2^256-1

Integer는 밑에 연산자와 함께 쓰기도 함

+ 더하기 2+2 => 4

빼기 2-2 => 0

곱하기 2*2 =>4

/ 나누기 몫 2/2 => 1

% 나누기 나머지 2/2= 0

* 지수 2**2(=2^2) =4

**address : address는 20 bytes 의 길이**

address 는 문자 그대로 주소를 나타낸다

예를들어 스마트컨트랙을 배포한다 할 때, 배포된 스마트 컨트랙은 주소를 얻는다

이와 마찬가지로, 디지털 지갑의 계정마다 각자의 주소를 할당 받는다

이 주소를 통해서, 디지털 코인을 보내기도하고, 스마트 컨트랙을 불러오기도 한다

그러면, 쉽게 생각하면, 주소란 이더 같은 디지털 코인을 주고 받는 은행 계좌번호정도 라고 생각

이더리움을 보내기 위해서는 주소 payable을 붙여야 한다

주소 = 계좌번호

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 < 0.9.0;
/*
  data type
  boolean, bytes, address, uint
  
  reference type
  string, Arrays, struct
  
  mapping type
*/
contract lec2{
    // bolean : true/false
    bool public b = false;
    
    // ! || == != &&
    bool public b1 = !false; //true
    bool public b2 = false || true; // true
    bool public b3 = false == true; //false
    bool public b4 = false != false; // false
    bool public b5 = false && true; // false
    
    //bytes 1~32
    bytes4 public bt = 0x12345678;
    bytes public bt2 = "STRING";
    
    //address 
    address public addr = 0xd9145CCE52D386f254917e481eB44e9943F39138;
    
    // int(음수 포함) Vs uint (음수 안 포함)
    
    //int8 : -2^7 ~ (2^7)-1
    int8 public it = -4;
    //uint8 : 0 ~ 2^8-1
    uint8 public it2 = 123;
    
    //uint256 : 0 ~ 2^256-1
    uint256 public it3 = 123;
}
```

### 3강 ether/GWei/wei 그리고 gas

이더리움의 코인은 ETH 이더 이다

1 ether = 10^9 Gwei = 10^18 wei

다시 말하자면 1^18 wei 는 1 이더를 나타낸다 = 한국돈 100원은 1원이 100 개있다

0.00000000000000001 ehter = 1 wei 

비슷한 예로, 코인 마켓에서 0.01 ether 를 샀다고 가정하였을때, 저희는 1^16wei를 산거라고 할 수 있다

1ether = 10^9 Gwei 라는 도대체 Gwei는 무엇??

Gwei = 주로 가스를 소비했을때, 사용되는 단위이다

스마트 컨트랙을 사용하기위해서 또는, 이더리움 블록체인과 상호작용하기 위해서는 가스가 필요하다

가스비용을 Gwei 단위로 낸답니다.

**그렇다면 가스비용은 어떻게 책정될까요?**

- 사용하고자 하는 스마트 컨트랙 안에 정의된 코드의길이에 따라 가스 비용이 책정된다
    - 길이가 짧을수록 소비되는 가스가 적어짐
- 스마트 컨트랙 안에 무엇으로 정의 되냐에 따라 가스 소비하는 비용이 달라진다
    - 예를들어, string 이나 modifer를 사용하는경우 가스가 더 많이 들어간다
- 이더리움에서 제공하는 [옐로우 페이퍼](https://ethereum.github.io/yellowpaper/paper.pdf)를 보면, 어떤 내장기능을 사용하냐에 따라 가스 소비량을 계산할 수 있다

**그렇다면 가스는 왜 만든걸까요?**

이더리움에 의하면, 가스를 만든이유는 DDoS(Distributed Denial of Service) 공격에서 좀 더 자유로워 지기 위해서 만들었다고 한다

예를 들어, 해커가 고의적으로 블록체인 네트워크를 다운 시킬려고, 스마트 컨트랙을 지속적으로 작동하게 반복 시켜 과부화를 준다고 가정 했을때, 해커는 작동을 반복시킬때마다 Gas 비용을 지불해야함

그렇기 때문에 해커입장에서는 이더를 지불하고 공격을 해야하는데 쉽지가 않다

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 < 0.9.0;
/*
    1 ether = 10^9 gwei = 10^18wei
    0.000000000000000001 = 1^-18 =1wei
    0.01 ether = 10^16 gwei
*/
contract lec2{
    uint256 public value = 1 ether;
    uint256 public value2 = 1 wei;
    uint256 public value3 = 1 gwei;
}
```

## Function

## ****Function 1 - 정의****

**1. Parameter 와 Retrun 값이 없는 function 정의**

function 이름 () public { // (public, private, internal, external) 변경가능.  // 내용 }

여기서 주의해야 할 점은, public 과 같은 **접근제어자를 함수명 뒤에 써줘야 함**

접근제어자는 public, private, internal, external 이 있다

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract Lec4 {
    uint256 public a = 3;
    function changeA() public{
        a =5;
    }
}
```

위에 예시가 있듯이, a 라는 변수는 3을 갖고 있습니다.

그러나 changeA()라는 함수를 실행시키시면 a는 5가 됩니다.

**2. Parameter는 있고, Retrun 값이 없는 function 정의**

function 이름 (받고싶은 타입 변수명 ) public {  // 내용 }

ex) function 이름 (uint 256 _value) public {  // 내용 }

1 번과 달라진점은 uint256 _value 라는 부분

이뜻은 uin256 타입으 파라미터를 받겠다

더 나아가서, type 은 여러가지를 쓸수가 있다 예를들어, byte, string, address 등등

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract Lec4 {
    uint256 public a = 3;
    function changeA(uint256 _value) public{
        a =_value;
    }
}
```

인제 changeA를 실행할때마다, _value의 파라미터 값을 넣어 주어야함

이 파라미터는 a에 대입이 되어 값이 변경 된답니다.

**만약에 2 개 이상의 파라미터가 필요하시다면,**

    function changeA(uint256 _value1, uint256 _value2) public{
        a =_value;
    }

**3. Parameter는 있고, Retrun 값이 있는 function 정의**

function 이름 (받고싶은 타입 변수명 ) public returns(반환하고자 하는 type) { // 내용 }

ex)function 이름 (uint 256 _value) public returns(uint256) {  // 내용 }

returns에 (uint256)이 있으니, uint256만 반환한다라는 뜻입니다.

여기서 주의해야 할 점은, **변수명이 없고 타입만 써주시면 됩니다.**

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract Lec4 {
    uint256 public a = 3;
    function changeA(uint256 _value) public returns(uint256){
        a =_value;
        return a;
    }
}
```

위와 같이 써주신다면, changeA 함수가 실행될때, _value의 파라미터 값을 받고

a 변수에 _value 파라미터가 대입된후 a 값이 리턴됩니다. 물론 a의 값은 uint256 타입입니다.

### ****5강 function 2 - public,private,internal, external****

function의 접근제어자는 public, private, internal, external 이 있다

**사실 접근제어자는 변수 앞에도 쓰이기도 한다**

**1. public : 어디서든 접근이 가능하다.**

```jsx
contract Lec5 {
    uint256 public a = 3;
}
```

**아주 간단하게, 변수에 public을 넣었다**

Lec5라는 스마트 컨트랙을 배포하니, a 라는 변수가 생기며, 클릭하니 값이 나오는걸 확인 할 수 있다

반면에, public 과 반대되는 private을 한번 넣으면

**private이니 외부에서 접근이 힘들다**

```jsx
contract Lec5 {
    uint256 private a = 3;
}
```

public 과는 다르게 a 라는 변수조차 접근 하기 힘들다.

즉 public을 정의 해줌으로써, 어디서든 접근이 가능한 getter 함수를 자동으로 만들어 주었다

```jsx
// 두개의 스마트 컨트랙을 사용해서 public 예제
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract Public_example {
    uint256 public a = 3;

    function changeA(uint256 _value) public {
        a =_value;
    }
    function get_a() view public returns (uint256)  {
        return a;
    }
}

contract Public_example_2 {

    Public_example instance = new Public_example();

    function changeA_2(uint256 _value) public{
      instance.changeA(_value);
    }
    function use_public_example_a() view public returns (uint256)  {
        return instance.get_a();
    }
}
```

Public_example 과 Public_example_2 라는 두개의 스마트 컨트랙이 있다

Public_example_2 를 사용하여 Public_example 에 접근 할 것

Public_example_2 에  **Public_example instance = new Public_example();**  이 인스턴스를 통해서 Public_example 컨트랙에 접근이 가능하다

즉, 인스턴스는 Public_example 의 분신이라고 간단하게 일단 생각하면 된다

**Public_example 컨트랙은 당연히 모든 부분이 public 이니 쉽게 접근이 가능하다**

**2. private: 오직 private이 정의된 스마트 컨트랙에서만 접근가능**

```jsx
contract Lec5 {
    uint256 private a = 3;
}
```

**이 스마트 컨트랙을 배포를 하면 a 라는 변수가 리믹스 상에서 보여지지가 않음 접근을 하려면 오직 Lec5안에서만 가능하기 때문**

**Lec5_2처럼 instance 를 만들어서도 접근이 불가능하답니다.**

```jsx
contract private_example {
    uint256 private a = 3;

    function get_a() view public returns (uint256)  {
        return a;
    }

}
```

위에 private_example을 배포를 하면, a 변수는 보이지 않고 get_a의 function 만 보인다

물론 get_a는 public이니 보이는거고 a는 private이니 보이지 않는다

그러나, private 특성으로 private_example라는 같은 스마트 컨트랙에 있는 get_a function 을 통해서

private a 변수를 접근 해서 값을 불러 왔다

**이런식으로 private을 사용하면, 본 변수 값은 은닉화 시킬 수 있다**

**3. external : 오직 밖에서만 접근 가능.**

external이기에, external이 정의된 스마트 컨트랙 내에서는 사용이 불가능 하다(private과 반대)

```jsx
contract external_example {
    uint256 private a = 3;

    function get_a() view external returns (uint256)  {
        return a;
    }

}

contract external_example_2 {

    external_example instance = new external_example();

    function external_example_get_a() view public returns (uint256)  {
        return instance.get_a();
    }
}
```

**external_examle 의 get_a 는 external 로 정의 되어 있기에, external_examle 내에서는 접근이 불가능하다**

그러나, external_examle _2는 전혀 별개의 스마트 컨트랙이기에 가능하다

**4. internal : 오직 internal이 정의된 스마트 컨트랙 내에서, 상속받은 자식 스마트 컨트랙에서 접근 가능.**

**internal 은 private 과 비슷, private에서 한가지 기능(상속받은 자식 접근 가능)이 더 추가**

> public: 모든곳에서 접근 가능
> 

> external: public 처럼 모든곳에서 접근 가능하나, external이 정의된 자기자신 컨트랙 내에서 접근 불가
> 

> private: 오직 private이 정의된 자기 컨트랙에서만 가능( private이 정의된 컨트랙을 상속 받은 자식도 불가능)
> 

> internal: private 처럼 오직 internal 이 정의된 자기 컨트랙에서만 가능하고, internal이 정의된 컨트랙을 상속받은 자식들도 접근이 가능
> 

### ****6강 function 3 - View 와 Pure****

**function use_public_example_a() view public returns (uint256) {**

**//...**

**}**

저 키워드의 자리는 pulbc 과 같은 접근 제한자 앞 이나 뒤 어디든 붙이면 된다

**function use_public_example_a() view public returns (uint256)**

**function use_public_example_a() public view returns (uint256)**

**1.view : storage state 를 읽을 수 있지만, 그 state 값을 변경할 수 없다.**

```jsx
pragma solidity >=0.7.0 <0.9.0;

contract View_example{
     uint256 public a = 1;

    function read_a() public view returns(uint256){
        return a+2;
    }
}
```

function 의 밖에 있는 것들은 storate에 저장이 된다

a 가 storage state

read_a() 라는 간단히 a 값을 리턴하는 함수 만들었다

그러나, a 를 리턴하니, 당연히 storage state를 읽었다고 할수 있으니 view 를 넣어야 한다

**read_a()에서 storage state의 값을 바꾼다면**

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;

contract View_example{
     uint256 public a = 1;

    function read_a() public returns(uint256){
        a = 3;
        return a+2;
    }
}
```

**이런식으로 아무것도 안써주면 된다**

**2.pure : storage state 를 읽으면 안되고, 그 state값을 변경할 수 도 없다.**

```jsx
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.7.0 <0.9.0;
contract Pure_example{

    function read_a() pure public returns(uint256){
        uint256 a2 = 3;
        return a+2;
    }
}
```

**pure는 storage state를 읽지 못하고, 변경도 불가하니 당연히, 함수 밖의 외부의 값을 가져올 수 없어서 함수 내에 정의된 로컬변수들과 사용**

위에서 로컬변수 a 는 3 을 대입받고, 2를 더해서 마지막에는 5로 리턴한다

> **view : function 밖의 변수들을 읽을수 있으나 변경 불가능**
> 

> **pure : function 밖의 변수들을 읽지 못하고, 변경도 불가능**
> 

> **viwe 와 pure 둘다 명시 안할때: function 밖의 변수들을 읽어서, 변경을 해야함.**
> 

### ****7강 function 4 - String****

function 에 string 파라미터를 넣고, 그 받은 파라미터를 다시 리턴

string 을 function 내에서 쓰려면, memory 라는 키워드가 필요

solidity 는 storage, memory, calldata ,stack 이렇게 4개의 저장 영역으로 나뉘어 있다

**storage** : 대부분의 변수, 함수들이 저장되며, 영속적으로 저장이되어 가스 비용이 비싸다

**memory**: 함수의 파라미터, 리턴값, 레퍼런스 타입이 주로 저장이 된다 storage 처럼 영속적이지 않고, 함수내에서만 유효하기에 storage보다 가스 비용이 싸다

**Colldata** : 주로 external function 의 파라메터에서 사용된다

**stack**: EVM (Ethereum Virtual Machine) 에서 stack data를 관리할때 쓰는 영역인데 1024Mb 제한적

string을 쓰기위해서는 memory 일식적으로 저장하는 키워드를 써야한다

string은 레퍼런스 타입이라고 볼 수 있다 ⇒ 그렇기 때문에, memory키워드를 넣어줘야한다

```jsx
// SPDX-License-Identifier  GPL-30
pragma solidity >= 0.7.0 < 0.9.0;

contract lec7 {

    function get_string(string memory _str) public pure returns( string memory){
        return _str;
    }
}
// string을 받아서 그대로 리턴함
```

memory는 늘 string 다음에 붙여준다

pure를 쓰는이유는, 파라미터 받은걸 바로 리턴하기해서, storage 에 저장된 변수들을 읽지 않았기때문 pure을 쓴다

## **Instance**

### ****8강 instance 1 - 정의****

**인스턴스는 주로 하나의 컨트랙에서 다른 컨트랙을 접근할 때 쓰임**

```jsx
// SPDX-License-Identifier:GPL-30
pragma solidity >= 0.7.0 < 0.9.0;

contract A{

    uint256 public a = 5;

    function change(uint256 _value) public {
        a = _value;
    }

}

contract B{

}
```

현재 B 컨트랙에서 A 컨트랙에 접근하여, 변수 a 와 change 함수 사용 하려면 A를 B컨트랙에서 인스턴스화 해야 접근이 가능

```jsx
contract B{

    A instance = new A();

  }
```

**컨트랙이름 인스터스의 이름 = new 컨트랙이름();**

인스터스를 이용해 접근해야하는데 접근할때는 . 을 붙여서 이동

예를들어서, instance.change(_value) 할 수 있습니다.

```jsx
// SPDX-License-Identifier:GPL-30
pragma solidity >= 0.7.0 < 0.9.0;

contract A{

    uint256 public a = 5;

    function change(uint256 _value) public {
        a = _value;
    }

}

contract B{

    A instance = new A();

    function get_A() public view returns(uint256) {
        return instance.a();
    }
    function change_A(uint256 _value) public  {
        instance.change(_value);
    }

}
```

현재 스마트컨트랙 B 에서, A 의 instance 는 . 붙여 접근함을 볼 수가 있다

**get_A 에서는 컨트랙 A의 변수를 접근해야하니 instance.a()를 써준걸 알 수가 있다**

**변수를 접근할때는 () 를 붙여야 리턴이 된다**

change_A에서는 instance.change(_value) 로 해줌으로써, 컨트랙 A의 함수 change를 접근할걸 알 수있다

instance 는 A 스마트 컨트랙의 분신과 같은 존재

스마트컨트랙 A를 따로 배포하고, 인스턴스 A를 스마트컨트랙 B를 통해서 배포한다고 가정하였을때,이 두개의 컨트랙은 완전히 다르다 **때문에, instance를 만들어서 변수 a의 값을 변경한다해도, 스마트컨트랙 A 자체만 따로 배포한곳에는 값에 영향을 주지가 않는다.**


# 관련 
## WEB3.0

[https://www.youtube.com/watch?v=EmVgMPjYgG4](https://www.youtube.com/watch?v=EmVgMPjYgG4)

### WEB3.0 이란?

- 컴퓨터가 시맨틱 웹 기술을 이용하여 웹페이지에 담긴 내용을 이해하고 개인 맞춤형 정보를 제공할 수 있는 지능형 웹기술을 말함
- WEB1.0 - E 커머스, 브라우저 엑세스등 일방적인 웹환경
- WEB2.0 - SNS,모바일,클라우드 컴퓨팅 등의 특징
- WEB3.0 - ai 기반, 탈중앙데이터 구조, **엣지컴퓨팅**등의 탈중화라는 특징

### 엣지컴퓨팅이란?

- 클라우드 컴퓨팅의 분산을 의미한다
- 컴퓨팅을 분산시켜 이용자 주변의 디바이스나 단말기 자체에서 이 작업을 처리하는 기술
- 자율주행, 스마트팩토리, 가상현실 VR
- 5G - 더빠르고 많은 정보를 나눠서 처리 할 수있게 한것이 핵심
- 5G기술을 통해 IOT 기기에서 AI 를 활용한 서비시를 제공할 수 있게 되면서 ‘초연결’ 사회가 가능해짐
- 엣지 컴퓨팅 단점
    - 분산된 스팟에서 클라우드 컴퓨팅이 하던 일을 대신하다보니 그와 동등한 수준의 보안 시스템을 갖춰야하는데 많은 비용이 소모 됨
    - 중간에서 데이터 경중에 따라서 클라우드로 갈 것인가 OR 엣지에서 자체적으로 처리 할 것인가
    - 이 과정에서 데이터의 중요성에 대한 판단미스 또는 데이터 유실에 대한 리스크가 있다고함
- **#엣지컴퓨팅 #보안 # 판단 # 데이터**

WEB3.0은 현재 진행형이고 그안에 메타버스가 주목 받는게 코인에도 영향을 끼침

**블록체인의 탈중앙화**

노드들은 각자의 해시파워를 사용해 블록을 생성하고 생태계를 유지해 나가는 모델과 크게 다르지 않음

**골램, 앵커**

- 알트코인 중에서 엣지 컴퓨팅 개념을 꼭 집어 메인 비즈니스 모델로 내세운 프로젝트
- 기술 초기라 보안이나 각종 기술적 문제로 실용화의 한계
- 프로젝트가 아직 유지되고 있고 기술적 한계가 앞으로 극복된다고하면 주목 받을 수 있는 프로젝트

**보안이슈**

- 엣지 컴퓨팅 역할을 하는 개별 디바이스에도 중앙화 시설에 준하는 보안 수준을 갖춰야 함
- 이더리움 생태계 확장과 각종 메인넷의 DAPP 서비스의 발달로 오라클, layer2, 멀티체인과 같은 offchain 환경이 필요해 짐에 따라서 보안 솔류션은 점점 주목 받을 수 밖에 없음
- nu사이퍼, 마스크네트워크, 파일코인

**판단능력**

- 디바이스에서 입력된 데이터들을 분류하고 처리해주는 능력을 말함
- web3.0의 키포인트인 AI
- AI 를 만들기 위해선 ‘머신러닝’(기계학습)이 필요 → 기계학습을 위해서는 ‘빅데이터’ 가 필요 함

**레이블링**

- 빅데이터가 머신러닝에 쓰이려면 광대한 양과 범위 그리고 정돈되지 않은 데이터를 어느정도 정리 해야 함
- 기계학습에 쓰일 수 있게 광범위한 빅데이터를 정리해 주는 작업 (=노가다)
- 로봇이 아님을 증명하기 위해 reCAPCHA 한것이 구글의 고서변역이나 자율주행 데이터에 사용되었다고 함
- 레이블링에 블록체인 인센티브 구조가 활용되는 사례가 늘고 있다고 함
- 마로의 바이트브릿지(워크박스), 코인리스트에서 세일을 진행 했엇던 휴먼프로토콜, 브레인트러스트 등이 해당 됨
- 엑시인피니티의 사례처럼 부업으로 벌 수 있는 수입이 본 수입을 능가한다면 트래픽이 몰리게 되어 관련 프로젝트 또한 주목 할만 함

**데이터분야**

- 분산 컴퓨팅과 마찬가지로 분산데이터 스토리지는 코인시장에 등장한지 꽤 오래된 모델임
- 스토리지 시아코인 등이 대표적인 프로젝트

## WEB3.0 코인 BEST8

[https://www.youtube.com/watch?v=x6bVRvn_K9I](https://www.youtube.com/watch?v=x6bVRvn_K9I)

### 엣지컴퓨팅

**이더리움 ( 메인스트림 )**

- 노드들에 의해서 이더리움 생태계의 모든 서비스가 운영
- 광범위한 엣지 컴퓨팅 모델
- 하나의 소우주

**icp** 

- 원래 이름은 디피니티
- 골램이나 앵커는 예전에 만들어지고 디피니티는 비교적 최근에 만들어짐
- 웹/앱서비스 체계 구조의 효율성을 높혀 개발이 쉽고 효율적으로 하게 해주는 네트워크
- 운영체제 최적화, 데이터 관리, 방화벽 등 의 문제를 해결하기 위해
- 소프트웨어 앱, 데이터관리, 웹/앱서비스, 인프라 기능이 추가된 다기능 블록체인 네트워크를 구현해 개발자들이 서비스 개발에만 전념할 수 있는 환경을 만들었음 (잡무 -icp, 개발자 - 개발)

### Ai

**휴먼프로토콜**

- 데이터레이블링 작업에 대한 인센티브 구조가 메인 모델
- 머신러닝을 위한 빅데이터 가공에 필요한 잔업들을 블록체인 인센티브를 통해 아웃소싱하는것
- 이를 통해 가공된 데이터를 활용해 자율주행이나 사물인식 인공지능시스템 개발을 하게 됨
- 업비트에 상장되어 있는 김치코인 마로가 워크박스를 통해 선보임
- 코인리스트에서 세일이 진행된 프로젝트

**브레인트러스트**

- 코인리스트에서 세일이 진행된 프로젝트
- 탈중앙 일자리 연결 네트워크를 모델로 세움
- 구인구직 플랫폼 역할을 탈중앙화된 커뮤니티에 맡기고 그에 따른 인센티브를 제공하는 구조
- A 라는 회사에 채용 공고가 나게되면 그자리에 맞는 인재를 추천하게 됨 → 자신이 추천한 인재가 고용되면 그에 따른 보상으로 BTRST 라는 코인을 받게 되는 것 ⇒ 데이터 레이블링
- 브레인트러스트는 사람들이 구직자와 구직자 간의 조건을 직접 검토하고 그에 맞는 추천을 하게 됨에 따라서 데이터의 신뢰성이 높음 ⇒ 데이터를 바탕으로 AI기반의 잡매칭 시스템을 구축할수있음
- 코인베이스에 상장 되어 있음

### 스토리지

**파일코인**

- 너무유명 역대최고액의 ICO 금액을 모집한 기록도 있음
- IPFS라는 분산형 파일 시스템이 핵심 모델임
- 중앙화된 웹서버 환경인 HTTP와 다르게 분산된 개별 사용자 컴퓨터가 웹 서버 역할을 하며 파일 저장소 역할도 함
- 비트토렌트나 기존 분산 스토리지/컴퓨팅 모델의 혼합형이 모델임
- 강력한 보안성이 기존 모델들과의 차별점으로 작용
- 업비트 비트마켓 기준 저점대비 7배가 오른뒤 다시 거의 제자리로 백 함

**SWARM(BZZ) 토큰**

- 분산형 저장 플랫폼이자 콘텐츠 배포 서비스이며 또한 이더리움 web 3 스택의 계층 서비스
- 코인리스트 세일 이후 계속 하락 상장이후 고점대비 -70%를 기록중임
- 상장된 거래소는 코인리스트나 오케이 엑스 외의 대부분 잡다한 거래소여서 메이저 상당에 대한 여지는 남아있음

### 보안 (WEB3.0 환경에서 제일 주목)

**누사이퍼**

- 분산애브 분산프로토콜 내에서 데이터의 암호화를 컨트롤 할 수 있는 프로젝트
- A라는 기밀 데이터가 있는데 온전히 나만 컨트롤 할 수 있음 A데이터를 알고 싶은 사람이 있으면 권한을 위임받아서 데이터를 열람 할 수 있음
- 이 암호화과정과 데이터 거래 과정에서 누싸이퍼 코인이 사용 됨
- 분산된 개별 포인트 에서도 중앙화된 포인트 외 동일한 수준의 보안 시스템을 구축해야 함
- 웬만한 메이저 거래소에 모두 상장 되어 있음
- 업비트 상장으로 인해 이미지가 안좋아짐 그래도 차트적으로 안정 됨

**마스크네트워크**

- SNS 에서 암호화된 포스팅이나 메세지 사용가능
- 트위터 중점적 활용
- 웹 2.0 환경인 SNS 유저들에게 웹3.0 환경을 자연스럽게 연결시켜가는 전략
- 마스트네트워크를 통해서 유저들은 트위터에서 NFT를 구매하거나 암호화폐를 전송하거나 선물할 수 있음
- ITO를 통해서 트위터에서 토큰 세일에 참여할 수도 있음
- 누싸이퍼처럼 전천후 보안 솔루션 같은 느낌은 아님
- 웹 3.0 에대한 모토를 확실히 하고있음
- 트위터유저 → 마스크네트워크 유저로 전환
- 코베 상장 종목

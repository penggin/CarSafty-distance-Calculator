# CarSafty-distance-Calculator

이 프로젝트는 학교 수학2 과목의 세특을 위해 제작되었습니다. (20916 이동훈)

## 소개

+ 이 프로젝트는 **Python 3.8.10** 을 이용해 제작되었습니다.
+ 이 프로젝트는 세특 제출용이며, 정보시간에 배운 문제해결 단원의 내용과, 수2의 정적분 단원의 내용을 활용하여 자세히 서술하였습니다.
+ 순차적으로 코드를 실행할수있으며, 수학, 과학적 탐구와 시각화에 유리한 구글코랩(쥬피터노트북) 을 이용하여 제작되었습니다.
+ 기호계산을 위해 sympy모듈을, 시각화를 위해 matplotlib, numpy 모듈을 사용하였습니다.

## 사용방법

+ 이 프로젝트는 구글의 코랩(주피터노트북) 으로 만들어졌으며, 온라인에서 실행하실수 있습니다.
+ ~~링크 : <https://colab.research.google.com/drive/1gEBomDgeINv7NEKotYWrEMnq-ecuz_on?usp=sharing>~~
+ 오류로 인해 위의 링크가 작동하지 않아, 아래의 방법을 사용해주세요.
1. https://colab.research.google.com/ 에 접속합니다.
2. 구글계정으로 로그인합니다.

3. 
![image](https://user-images.githubusercontent.com/77449586/125331532-135cc580-e383-11eb-907e-1256dd428e41.png)

위의 창이 보인다면 계속 진행하시고, 안보이신다면 1번의 링크로 다시 들어가시면 됩니다.

4. GitHub를 선택하신후, 링크를 붙여넣어주세요. 링크 : https://github.com/penggin/CarSafty-distance-Calculator

5.
![image](https://user-images.githubusercontent.com/77449586/125331753-5a4abb00-e383-11eb-9c9f-1c1a3f2cc8b1.png)

파란색으로 강조된것을 눌러주시면 실행이 가능합니다.
파일 안에서의 사용법은 아래의 첨부된 gif를 참고하시거나, 구글에 "구글 코랩 사용법" 이라 검색해주세요.


### 문제분석

문제 : 수학 교과서에 기재되어 있는 "안전을 위한 앞차와의 거리" 라는 수학 역량 플러스의 내용을 이용하여, 자동차의 속도, 브레이크를 밟을때까지의 시간, 도로의 마찰계수 를 입력받아 자동차의 정지거리, 시간에 따른 요소들의 그래프를 얻고싶다.

**문제의 이해와 분석**

현재상태 : 수동으로 계산해서 값을 구할수도 있지만, 이 경우엔 정확한 값을 얻을수 없고, 정확하게 시각화를 할수도 없다.

목표상태 : 현재상태의 문제를 해결한 상태

필요한 정보 : 브레이크를 밟고 난 후 t초뒤의 속도를 구하는 공식, 자동차의 초기속도, 브레이크를 밟을때까지의 시간, 도로의 마찰계수

**문제의 분해**

+ 어떤 방식을 사용해서 시각화를 할수 있을까?
+ 어떤 공식을 이용하여 제동거리를 계산할수 있을까?
+ 어떤 방법으로 시간에따른 자동차의 속도를 구할수 있을까?
+ 어떤 방법으로 시간에따른 자동차의 거리를 구할수 있을까?
+ 어떤 방법으로 시간에따른 자동차의 가속도를 구할수있을까?

-----
### 문제의 구조화

해당 문제를 그림으로 구조화하면 다음과 같다.

![image](https://user-images.githubusercontent.com/77449586/125203548-c0680d00-e2b3-11eb-9c71-fe1003c6e7fe.png)


-----
### 알고리즘

알고리즘의 다섯가지 조건들은 다음과 같다.
1. 0개 이상의 입력
2. 1개 이상의 출력
3. 수행가능성
4. 명확성
5. 유한성

다음의 조건에 맞추어 알고리즘을 설계해보자!

**알고리즘 설계**

이 프로젝트에선 **의사코드**를 이용해 먼저 간략히 구성하고, **순서도** 를 이용하여 정밀하게 설계해볼것이다. 

우선은 의사코드를 이용하여 구성해보자.

이 프로그램은 다음과 같은 방식으로 작동해야한다.
1. 변수들을 입력받는다. (마찰계수, 브레이크 밟을때까지의 시간, 자동차의 초기속도)
2. 공주거리, 제동거리, 정지거리를 계산한다.
3. 공식을 이용해 시각화한다.
4. 계산한 내용들을 출력한다.

그리고 우리는 이것들을 만들기 위해, 수학적으로 접근할 필요가 있다.
우선 주어진 공식은 a = (마찰계수) * (중력가속도)라고 할때 브레이크를 밟고 난 후 t초 후의 속도인
```v(t) = v0 - at```

가 된다.
수업시간에 배웠듯이 속도를 미분하면 가속도의 함수가 되고, 속도를 적분하면 거리함수가 된다.
위에서의 거리함수, 속도함수, 가속도함수를 이용하여 그래프를 그릴수 있다.

그 다음은 공주거리, 제동거리, 정지거리를 구하는 과정이다.

**공주거리**는 운전자가 위험을 인지하고, 브레이크를 밟기 전까지의 거리이다. (그래프는 공주거리를 제외하고 그린다.)
즉, 공주거리는 {브레이크를 밟기까지의 시간} * {자동차의 속도} 로 구할수 있다.

**제동거리**는 운전자가 브레이크를 밟은후 멈출때까지의 거리이다.
제동거리는 제동까지 걸린시간을 t초, a = (마찰계수) * (중력가속도), v0이 초기속도 라고할때 다음과 같은방식으로 구할수 있다.

![image](https://user-images.githubusercontent.com/77449586/125204441-59008c00-e2b8-11eb-82ae-c95a6a6bfce3.png)
 
**정지거리** 는 간단히 {공주거리} + {제동거리} 로 구할수 있다.

**순서도로 구성하기**
순서도에서 쓰이는 기호들은 다음과 같은 의미를 가진다.

![image](https://user-images.githubusercontent.com/77449586/125204509-b0066100-e2b8-11eb-8789-42b4378bbbf2.png)

이제 위에서 의사코드로 짠 알고리즘을 순서도로 구성해보자.

![수학 (1)](https://user-images.githubusercontent.com/77449586/125289696-7ede6d00-e35a-11eb-9188-5ba065eecb94.png)

순서도로는 다음과 같이 나타낼수있다. 그렇다면 이제 코드를 짜는 순서로 넘어가보자.

### 코드짜기

**변수 네이밍 정리**
코드를 짜다보니 겹치는 변수들이 있어서 여기서 한번 정리를 하고 가려고 한다.

v0 = 자동차의 초기속도

t0 = 인지후, 브레이크를 밟기까지의 거리

g = 중력가속도의 크기

u = 도로의 마찰계수

a = 마찰계수 * 중력가속도

t = 미지수

gongju_distance = 공주거리

ft = f(t) = 속도함수

ft0 = ft를 풀기위한 임시값

T = 자동차가 멈추기까지의 시간 (dict)

t1 = 자동차가 멈추기까지의 시간을 T에서 추출한것

Ft = F(t) = 거리함수 = f(t)를 적분한것

vt = v(t) = 가속도함수 = f(t)를 미분한것



나는 이전의 수학과제 제출(구간함수의 실생활 적용) 에선, vscode(편집기 이름)라는 IDE(편집기)를 사용하였다.
하지만 이번의 활동에서는 다른것을 사용해볼것이다.

이번 활동에서는 vscode같은 IDE 대신, 구글의 colab(코랩)을 사용해 볼것이다.
구글 코랩은 주피터 노트북을 기반으로 작동하며, 주피터 노트북은 과학 수학 등 하나하나 과정을 지켜보며 변화나, 결과 등을 관찰하는 연구 목적에 더 적합하다.
한번 예시를 살펴보자.

하나의 작업을 하는데에 2초가 소요되고, 총 3회의 작업을 하는 프로그램이 있다고 가정해보자.
아래의 사진은 일반적인 IDE(vscode)를 사용한 모습이다.
![vsexample](https://user-images.githubusercontent.com/77449586/125286639-02965a80-e357-11eb-94b0-e074cbc42176.gif)

vscode를 사용하였을때는 작업이 멈추지않고 한번에 진행되며, 현재 어떤 작업이 진행되고있는지 정확히 알기 어렵다.
이제 같은 프로그램을 주피터노트북에서 구성하여 실행해보자.

![image](https://user-images.githubusercontent.com/77449586/125286966-57d26c00-e357-11eb-9fa4-9b66bede8b87.png)

위의 사진으로 볼수있듯이, 주피터 노트북은 구간별로 코드들을 분리하여 실행할수있다.
이제 실행모습을 살펴보자!
![colabexample](https://user-images.githubusercontent.com/77449586/125287475-ea730b00-e357-11eb-9707-98d8688bba51.gif)

이처럼 주피터노트북에선 코드들을 분리하여 실행시킬수있다.
이제 진짜로 코드를 짜러 가보자!!

우선 대부분의 코드들은 코드의 제일 처음에 필요한 모듈을을 import(불러오기)한다.
그러므로 먼저 필요한 모듈들을 import해보자!
![image](https://user-images.githubusercontent.com/77449586/125290221-0b892b00-e35b-11eb-9ea1-c77f62d897bf.png)

필요한 모듈들을 import하고, 완료되었을때 알려주는 코드를 짜보았다.

그 다음으로는 아래의 순서도 부분인, 정보들을 입력받는 코드를 짜볼것이다.

![image](https://user-images.githubusercontent.com/77449586/125288460-23f84600-e359-11eb-83d7-9dfd93bf59ac.png)

![image](https://user-images.githubusercontent.com/77449586/125289864-aaf9ee00-e35a-11eb-959d-d16de0cf6959.png)

위의 순서도에서는 값들을 입력받은후 각각의 변수에 집어넣는다. 아래는 위의 순서도를 코드로 짠것이다.
![image](https://user-images.githubusercontent.com/77449586/125311392-56f90480-e36e-11eb-94aa-baec67f87f71.png)

위의 코드에서는 각각의 값들을 python의 내장함수인 input() 을 이용하여 값을 입력받았다.
여기서 input은 값을 str(문자열)으로 돌려주기때문에 실수형(float)로 바꿔주어야 한다. (보통이라면 정수형(int)로 바꾸었겠지만, 이 계산을 할때 소수도 계산할수있기때문에 실수형을 사용함.)

다음은 이 부분을 짜볼것이다.

![image](https://user-images.githubusercontent.com/77449586/125306271-05e71180-e36a-11eb-9c56-5b8aa74a735b.png)

아래의 코드는 위의 순서도를 바탕으로 코드를 짠것이다.
![image](https://user-images.githubusercontent.com/77449586/125308959-50698d80-e36c-11eb-8419-1cb1a57b7812.png)

(절대 공주거리를 영어로 번역한것을 찾지못해 gongju_distance 라고 한것이 아니다... ㅋㅋ)

다음은 이쪽부분을 짜보자!

![image](https://user-images.githubusercontent.com/77449586/125316519-25366c80-e373-11eb-9d3e-915746cf5a5f.png)

위의 순서도를 코드로 구성하면 아래와 같아진다.

![image](https://user-images.githubusercontent.com/77449586/125317652-21efb080-e374-11eb-83d1-673e3e148d84.png)

이제 거의 마지막이다!! 식을 그래프로 나타내기만 하면 거의 끝이다!!!
순서도는 다음과 같다.

![image](https://user-images.githubusercontent.com/77449586/125317940-5c594d80-e374-11eb-807a-30572892aacd.png)

(뭐... 하나뿐이여서 순서라는게 없긴 하지만 ㅎ...)

먼저 거리그래프를 그리는 코드를 짜보자.

![image](https://user-images.githubusercontent.com/77449586/125325391-d6410500-e37b-11eb-98fb-1e73600aaf9d.png)

그 다음으로는 속도의 그래프이다. (사실 구조는 같기때문에 주석으로 설명은 넣지 않았다.)

![image](https://user-images.githubusercontent.com/77449586/125325457-ea850200-e37b-11eb-802a-f0d2562fd95a.png)

그 다음은 가속도의 그래프이다.

![image](https://user-images.githubusercontent.com/77449586/125325491-f40e6a00-e37b-11eb-893b-1abfdd7fd22b.png)

이제 진짜 마지막 과정이다.

![image](https://user-images.githubusercontent.com/77449586/125325533-ff619580-e37b-11eb-9740-300fffddd11e.png)

사실 주피터 노트북에서는 구역들이 분리되어있고, 사용자가 직접 눌러가며 실행하는것이기 때문에 자동으로 처음으로 가게 할수는 없다.
그러므로 간단한 안내를 해주는 코드를 짜보자.

![image](https://user-images.githubusercontent.com/77449586/125326506-1654b780-e37d-11eb-9914-b1c113a7d8e5.png)

이제 진짜로 끝이다.

### 테스트 해보기!
테스트 값으로는 교과서 144p의 활동 1번의 값들을 사용하였다!

![usingexample](https://user-images.githubusercontent.com/77449586/125327185-cfb38d00-e37d-11eb-8712-d4cb5ac0ec27.gif)

(만약 위의 gif가 흐리게 보이신다면, gif를 클릭해서 봐주세요.)

(이 코드를 테스트 하시려면, 상단의 사용방법 부분을 참고해주세요.)

### 느낀점들
이전에는 python을 이용하여 수학관련된 연산을 사칙연산에서 벗어나지 안는 수준까지만 했었는데, 이 활동을 하며 python에서 수학, 과학 계산과 관련된 numpy, sympy 같은 모듈과, 시각화 모듈인 matplotlib 를 처음 사용해보게 되어서, 무척 흥미로웠다. 또한 이 활동을 통해 어떤 방식으로 이 문제를 해결할수 있는가? 라는 고민을 하며 하나하나씩 해결해 나가는게 재미있었다.

조금 힘들었던 점은 앞에서 언급했다시피 전에는 사칙연산을 벗어나지 않는 범위 내에서 까지만 사용했었지만, 이 활동에는 수2에서 배운 미분, 적분, 정적분 등이 활용되는 활동이여서 관련 자료를 찾아보며 배우면서 만드는 점이 조금 힘들었다. (이걸 만드려고 오류를 엄청 냈었다 ㅎ..)

흥미로웠던 점은, 이전엔 프로그래밍 언어에서는 미분, 적분 같은 사칙연산을 벗어난 연산들은 조금 힘들거라고 생각했었는데 막상 시도해보니 실행속도도 빠르며, 사용방법도 그렇게까진 더럽지 않아서 놀랐다. 그리고 시각화 모듈인 matplotlib 는 처음써봤는데 생각보다 매우 깔끔한 그래프를 그려주어서 놀랐고, 추가적으로 찾아보니 다른 그래프들도 그릴수 있어서 한번더 놀랐다. 나중에 이 활동에서 배운 내용들을 개인프로젝트에서도 활용해봐야겠다는 생각이 들었다.

타교과와 연계되는 부분은 정보 교과이다. 위에서 프로그램을 구성하기위해 사용했던 문제분리, 의사코드, 순서도 들은 모두 정보시간에 배운 내용들이고, 그 배운 내용들을 바탕으로 활용하여 이 프로젝트를 진행하게 되었다.

이 쓴 내용들을 바탕으로, 코딩에 관심있는 친구에게 이것에 대한 내용을 가르쳐주고, 실습시켜줄 예정이다. (현재 진행중)

**선생님 긴글 읽느라 수고하셨습니다!!**

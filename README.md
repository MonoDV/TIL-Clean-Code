# TIL-Clean-Code

> 클린 코드 내용 정리

---

## 1장 깨끗한 코드

깨끗한 코드란 무엇인가?

### 핵심

**나쁜 코드** 가 쌓이면 쌓일수록, **생산성** 은 떨어진다.

### 나쁜 코드로 치르는 대가

-   코드를 고칠 때마다 문제가 발생함
-   스파게티 코드를 **해독** 하느라 오랜 시간이 걸린다
-   얽히고 설킨 코드를 더욱 쌓게된다

#### 결국 시스템을 다시 설계하려면 막대한 비용이 든다

> 빨리 가려면 깨끗한 코드를 유지해야 한다.
> `그렇다면 깨끗한 코드를 작성하는 방법은 무엇일까?`

### 많은 프로그래머들이 생각하는 깨끗한 코드의 요소

-   논리가 간단해야 버그가 숨어들지 못한다
-   오류는 명백한 전략에 의거해 철저히 처리
-   깨끗한 코드는 잘 쓴 문장처럼 읽힌다
-   설계자의 의도를 숨기지 않는다
-   모든 테스트를 통과한다
-   중복이 없다
-   클래스, 메서드, 함수 등을 최대한 줄인다.

### 이 후의 내용은, 이 책의 저자가 생각하는 '깨끗한 코드'에 대한 내용이다.

---

## 2장 의미있는 이름

클린한 코드를 작성하기 위한 이름을 정하는 기본적인 가이드라인.

### 핵심

### 단락

-   의도를 분명히 밝혀라
    -   int d; // 경과 시간(댠위:날짜) :x:
    -   int elapsedTimeInDays; :white_check_mark:
-   그릇된 정보를 피하라
    -   List 자료형이 아닌데 accountList라고 명명 :x: -> 사실 이름에 List도 쓰지 않는데 이는 뒤에서 다룬다
    -   흡사한 이름을 사용하지 말라
        -   XYZControllerForEfficientStorageOfStrings
        -   XYZControllerForEfficientHandlingOfStrings
-   의미있게 구분하라
    -   컴파일을 통과하기 위해 명명하는 경우 ex) klass...
    -   불용어를 붙이는 경우
        -   a1, a2, a3, ... :x:
        -   Product클래스 작성 후 ProductInfo, ProductData :x: -> Info, Data는 아무 의미도 제공하지 못함
        -   getAccount(), getAccounts(), getAccountList() :x: -> 어떤 메서드를 호출해야 할 지 모름
-   발음하기 쉬운 이름을 사용하라
    -   genymdhms(generate date, year, monthj, day, hour, minute, second) :x:
    -   generationTimestamp :white_check_mark:
-   검색하기 쉬운 이름을 사용하라
    -   grep으로 찾기 쉽도록 숫자 등을 상수로 명명
    -   5 -> const int WORK_DAYS_PER_WEEK = 5 :white_check_mark:
-   인코딩을 피하라
    -   접두어를 사용하는 것
        -   멤버 변수 앞에 "m\_"으로 시작하는 접두어 사용 :x:
        -   인터페이스 이름 앞에 "I"로 시작하는 접두어 사용 -> 필자는 추천하지 않음
            -   인코딩이 필요하다고 생각되는 경우 차라리 구현체에 "Imp" 접미사를 붙이는 선호
-   자신의 기억력을 시험하지 마라
    -   r이라는 이름이 URL의 소문자라는 사실을 알고 있다고해서 사용하지 마라
    -   모두가 이해할 수 있도록 명료하게
-   클래스 이름
    -   명사나 명사구가 적합
    -   Customer, WikiPage, Account, AddressParser :white_check_mark:
    -   Manager, Processor, Data, Info :x:
-   메서드 이름
    -   동사나 동사구가 적합
    -   postPayment, deletePage, save :white_check_mark:
    -   생성자 중복정의시, 정적 팩토리 메서드 사용
        -   Complex fulcrumPoint = Complex.FromRealNumber(23.0); :thumbsup:
        -   Complex fulcrumPoint = new Complex(23.0); -> 나쁘진 않지만 위의 방법을 추천
-   기발한 이름은 피하라
    -   웃기자고 특정 문화에서 사용하는 농담을 사용하는것은 지양하라
-   한 개념에 한 단어를 사용하라
    -   똑같은 메서드를 클래스마다 fetch, retrieve, get처럼 제각각으로 부르는 것 :x:
    -   마찬가지로 controller, manager, driver를 혼재하여 사용 :x:
-   말장난을 하지 마라 (일관성을 잘못 적용하지 마라)
    -   산술 연산에 add라는 이름을 사용
    -   집합에 값 하나를 추가하는데 add 사용 :x: -> insert나 append를 사용하라
-   해법 영역에서 가져온 이름을 사용하라
    -   프로그래머에게 익숙한 기술 개념은 많다. 기술 개념에는 기술 이름을 선택하라
    -   JobQueue, AccontVisitor :white_check_mark:
-   문제 영역에서 가져온 이름을 사용하라
    -   적절한 '프로그래머 용어'가 없다면 문제 영역에서 이름을 가져온다
    -   문제 영역 개념과 관련이 깊은 경우에도 사용
-   의미 있는 맥락을 추가하라
    -   city, zipcode, state라는 변수가 있을 경우 state가 주소 일부라는 것을 알 수 있음
    -   그러나 어떤 메서드에서 state만 사용한다면 무슨 의미인지 파악하는것이 어렵다
    -   addrState로 변경 시 해결, 또는 Address 클래스를 추가하면 더욱 좋다
    -   Address가 IP 주소인지, 집 주소인지 헷갈릴 수 있으므로 PostalAddress로 할 수도 있겠다
-   불필요한 맥락을 없애라

    -   의미가 분명한 경우, 이름에 불필요한 맥락 추가 :x:
    -   Gas Station Deluxe라는 어플리케이션 개발을 위해 모든 클래스 이름을 'GSD'로 시작하겠다는 생각은 :x:

-

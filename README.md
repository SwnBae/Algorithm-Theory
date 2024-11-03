# java-racingcar-precourse
----------

### 1. 기능 요구 사항
* 자동차 이름 부여
  - 사용자는 자동차의 이름을 쉼표(,)로 구분하여 입력할 수 있다.
  - 자동차 이름은 5자 이하만 가능하다.  

* 이동 횟수 입력
  - 사용자는 자동차가 이동할 횟수를 입력할 수 있어야 한다.  

* 전진 조건
  - 각 자동차는 0에서 9 사이의 무작위 값을 생성한다.
  - 생성된 값이 4 이상인 경우에만 자동차가 전진한다.  

* 자동차 전진 출력
  - 레이스를 진행할 때, 각 차수별로 전진하는 자동차의 이름과 함께 전진 횟수를 '-' 기호로 표시하여 출력한다.  
    
* 우승자 결정
   - 모든 차수가 완료된 후, 가장 많은 전진 횟수를 기록한 자동차를 우승자로 결정한다.
   - 우승자가 여러 명일 경우, 자동차 이름을 쉼표(,)로 구분하여 출력한다.  


----------

### 2. 기능 구현 단위

* Domain : Car 클래스 구현
  - move(): 자동차를 전진시키는 메서드로, 전진할 때마다 카운트를 증가시킨다.
  - toString(): 자동차의 이름과 전진 횟수를 문자열로 반환한다.  
 
* Repository : CarRepository 인터페이스 및 CarRepositoryImpl 구현
  - save(): 주어진 자동차 객체를 저장한다.
  - findByName(): 이름으로 자동차를 찾는다.
  - findAll(): 저장된 모든 자동차를 반환한다.  

* Service : CarService 구현
  - joinCar(): 주어진 자동차를 등록한다.
  - validateDuplicateCar(): 주어진 자동차가 이미 저장된 자동차와 이름이 중복되는지를 확인한다.
  - moveCar() : 각 자동차의 전진 여부를 결정 후, 전진 횟수를 증가시킨다.
  - findWinners(): 전진횟수를 비교하여 우승자를 찾는다.  
 
* Controller : CarController 구현
  - startRace(): 자동차를 생성하고, 주어진 횟수만큼 레이스를 진행한 후, 최종 우승자를 발표한다.
  - createRace(): 사용자로부터 자동차 이름을 입력받아 등록한다.
  - raceRound(): 주어진 횟수만큼 자동차를 이동시키고, 현재 라운드 결과를 출력한다.
  - raceOver(): 레이스 종료 후 우승자를 발표한다.  
 
* View : Input 및 Output 구현
    + Input
      - cars(): 사용자로부터 자동차 이름을 입력받는다.
      - counts(): 사용자로부터 이동 횟수를 입력받는다.
    + OutPut
      - roundResult(): 각 라운드 결과를 출력한다.
      - raceWinner(): 최종 우승자를 출력한다.  

* Validator 클래스 구현
  - checkName() : 자동차 이름을 검증하고 유효한 이름들을 리스트로 반환한다.
  - checkCount() : 경기 횟수를 검증하고, int 형태로 반환한다.
  - isNull() : 입력값이 비어있는지 확인하여, 빈 문자열일 경우 IllegalArgumentException을 발생시킨다.
  - endsWithComma() : 입력값이 쉼표로 끝나는지 확인하여, 끝에 쉼표가 있을 경우 IllegalArgumentException을 발생시킨다.
  - nameLength() : 각 자동차 이름의 길이를 검사하여, 5자를 초과하는 경우 IllegalArgumentException을 발생시킨다.
  - isNumber() : 입력값이 숫자로 구성되어 있는지 확인하여, 숫자가 아닐 경우 IllegalArgumentException을 발생시킨다.
 
### 2. 기능 구현 단위

* **입출력**
  - **입력**: 구입 금액, 당첨 번호 및 보너스 번호 입력, 오류 발생 시 입력 재요청  
  - **출력**: 구입한 로또 개수 및 번호, 당첨 통계, 수익률 출력  

* **로또 관련**  
  - 사용자 로또, 당첨 번호 및 보너스 번호 저장
  - 사용자 로또 번호 랜덤 생성 : 중복 번호 불가, 오름차순 정렬
  - 당첨 등수 결정 : 유저 로또와 당첨 번호 비교를 통한 당첨 여부 반영
  - 당첨 로또 통계 계산
  - 당첨 로또 상금 합산

* **입력 유효성 검증**  
  - 입력 유효성 검증 및 예외 처리 구현
 
---------
### 3. 예외 처리

* 멤버가 중복인 경우  
``` ex) "pobi, pobi" -> IllegalArgumentException("중복된 회원 존재") ```
* 입력이 공백인 경우  
``` ex) "" -> IllegalArgumentException("빈 문자열") ```
* 입력의 마지막이 구분자(,)인 경우  
``` ex) "pobi,woni," -> IllegalArgumentException("마지막 입력이 구분자입니다.") ```
* 자동차 이름이 5글자를 초과하는 경우  
``` ex) "pobiwoni" -> IllegalArgumentException("이름은 5자 이하만 가능합니다.") ```
* 경기 횟수가 양수인 정수가 아닌 경우  
``` ex) "a", ";", "-1" -> IllegalArgumentException("경기 횟수는 양수로 입력되어야 합니다.") ```

### 3. 예외 처리

* 사용자가 입력한 값이 빈 문자열일 경우    
  ``` ex) "" → `IllegalArgumentException("[ERROR] 빈 문자를 입력했습니다.") ```
  
* 당첨 번호 입력 시, 입력한 값이 구분자(,)로 끝날 경우    
    ``` ex) "1,2,3,4,5," → `IllegalArgumentException("[ERROR] 마지막 입력이 구분자입니다.") ```
  
* 사용자가 입력한 금액이 1000원 단위가 아닐 경우  
  ``` ex) "1500" → `IllegalArgumentException("[ERROR] 금액은 1000원 단위여야 합니다.") ```  

* 사용자가 입력한 로또 번호가 1 이상의 정수가 아닐 경우  
  ``` ex) "-5" → `IllegalArgumentException("[ERROR] 입력은 1이상의 정수여야 합니다.") ```  

* 사용자가 입력한 로또 번호가 1에서 45 범위를 벗어날 경우  
  ``` ex) "50" → `IllegalArgumentException("[ERROR] 로또 번호는 1부터 45 이내여야 합니다.") ```  

* 보너스 번호가 이미 입력된 로또 번호에 포함될 경우  
  ``` ex) "5" (로또 번호에 5가 포함되어 있을 때) → `IllegalArgumentException("[ERROR] 보너스 번호가 로또 번호 내에 존재합니다.") ```
  
* 사용자가 입력한 로또 번호의 개수가 6개가 아닐 경우  
  ``` ex) "1,2,3,4,5" → `IllegalArgumentException("[ERROR] 로또 번호는 6개여야 합니다.") ```  

---------
### 4. 수정사항
* 테스트 케이스 추가
  - Car(domain): 자동차 전진 및 출력 테스트
  - Repository: 자동차 저장, 찾기, 반환 테스트
  - CarService: 자동차 등록, 중복 이름 등록 실패, 전진, 우승자, 공동 우승자 테스트
  - Validator: 자동차 이름, 경기 횟수 검증
    

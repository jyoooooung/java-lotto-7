# java-lotto-precourse

---

### 기능 구현 목록

- ##### Lotto
    - [ ] 제약 사항
        - 제공된 Lotto 클래스를 사용하여 구현
        - numbers 이외의 필드를 추가할 수 없다.
        - numbers의 접근 제어자 private은 변경할 수 없다.
    - 
    - 예외 처리 관련
        - [x] Lotto 번호 개수 확인 (6개가 맞게 입력되었는지) - Lotto 클래스에 제공되어 있음
        - [x] Lotto 숫자들의 범위 확인 (1~45 사이) - pickUniqueNumbersInRange()에 보장되어 있음
        - [x] Lotto 숫자들이 중복되지 않는지 확인 - pickUniqueNumbersInRange()에 보장되어 있음


- ##### lotto.domain.LottoFactory
    - 필드
        - [ ] List\<Lotto\> lottos : 로또를 관리하는 리스트

    - 메서드
        - [ ] publishLotto() : 로또를 발행하는 기능
        - [ ] validate() : 로또의 개수가 맞게 발행되었는지 확인하는 기능


- ##### LottoManager
    - [ ] purchaseLotto() : 구입 금액에 해당하는 만큼의 로또를 발행하는 기능
    - [ ] setWinningNumber() : 당첨 번호를 설정하는 기능
    - [ ] setBonusNumber() : 보너스 번호를 설정하는 기능
    - [ ] compareWinningNumber() : 당첨 번호와 로또를 비교하는 기능
    - [ ] compareBonusNumber() : 보너스 번호와 로또의 숫자를 비교하는 기능
        - (5개 이상 일치하는 경우)
    - [ ] lottoResult() : 로또의 당첨 내역을 계산하는 기능
    - [ ] profitRate() : 로또의 수익률을 계산하는 기능
        - 수익률은 소수점 둘째 자리에서 반올림
    - [ ] validation : 로또 진행 과정에서의 유효성 검증
        - [ ] validateBuyingLotto() : 구매 금액이 유효한지에 대한 검증
        - [ ] validateWinningNumber() : 당첨 번호의 입력에 대한 검증
        - [ ] validateBonusNumber() : 보너스 번호에 대한 검증


---


### 기능 요구 사항
간단한 로또 발매기를 구현한다.

- 로또 번호의 숫자 범위는 1~45까지이다.
- 1개의 로또를 발행할 때 중복되지 않는 6개의 숫자를 뽑는다.
- 당첨 번호 추첨 시 중복되지 않는 숫자 6개와 보너스 번호 1개를 뽑는다.
- 당첨은 1등부터 5등까지 있다. 당첨 기준과 금액은 아래와 같다.
    - 1등: 6개 번호 일치 / 2,000,000,000원
    - 2등: 5개 번호 + 보너스 번호 일치 / 30,000,000원
    - 3등: 5개 번호 일치 / 1,500,000원
    - 4등: 4개 번호 일치 / 50,000원
    - 5등: 3개 번호 일치 / 5,000원
- 로또 구입 금액을 입력하면 구입 금액에 해당하는 만큼 로또를 발행해야 한다.
- 로또 1장의 가격은 1,000원이다.
- 당첨 번호와 보너스 번호를 입력받는다.
- 사용자가 구매한 로또 번호와 당첨 번호를 비교하여 당첨 내역 및 수익률을 출력하고 로또 게임을 종료한다.
    - 사용자가 잘못된 값을 입력할 경우 IllegalArgumentException을 발생시키고,
    - "[ERROR]"로 시작하는 에러 메시지를 출력 후 그 부분부터 입력을 다시 받는다.
    - Exception이 아닌 IllegalArgumentException, IllegalStateException 등과 같은 명확한 유형을 처리한다.

---

### 입출력 요구 사항

##### 입력
1) 1,000원 단위로 로또 구입 금액 입력
    - 1,000원으로 나누어 떨어지지 않으면 예외 처리
```
14000
```
2) 당첨 번호 입력
    - 쉼표(,)를 기준으로 구분
```
1,2,3,4,5,6
```
3) 보너스 번호 입력
```
7
```

##### 출력
1) 발행한 로또 수량, 번호 출력
    - 로또 번호는 오름차순으로 정렬
```
8개를 구매했습니다.
[8, 21, 23, 41, 42, 43] 
[3, 5, 11, 16, 32, 38] 
[7, 11, 16, 35, 36, 44] 
[1, 8, 11, 31, 41, 42] 
[13, 14, 16, 38, 42, 45] 
[7, 11, 30, 40, 42, 43] 
[2, 13, 22, 32, 38, 45] 
[1, 3, 5, 14, 22, 45]
```
2) 당첨 내역 출력
```
3개 일치 (5,000원) - 1개
4개 일치 (50,000원) - 0개
5개 일치 (1,500,000원) - 0개
5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
6개 일치 (2,000,000,000원) - 0개
```
3) 수익률 출력
    - 소수점 둘째 자리에서 반올림
```
총 수익률은 62.5%입니다.
```

##### 예외 상황 출력
[ERROR] 에러 문구
```
[ERROR] 로또 번호는 1부터 45 사이의 숫자여야 합니다.
```

##### 예시
```
구입금액을 입력해 주세요.
 > 8000

8개를 구매했습니다.
[8, 21, 23, 41, 42, 43] 
[3, 5, 11, 16, 32, 38] 
[7, 11, 16, 35, 36, 44] 
[1, 8, 11, 31, 41, 42] 
[13, 14, 16, 38, 42, 45] 
[7, 11, 30, 40, 42, 43] 
[2, 13, 22, 32, 38, 45] 
[1, 3, 5, 14, 22, 45]

당첨 번호를 입력해 주세요.
 > 1,2,3,4,5,6

보너스 번호를 입력해 주세요.
 > 7

당첨 통계
---
3개 일치 (5,000원) - 1개
4개 일치 (50,000원) - 0개
5개 일치 (1,500,000원) - 0개
5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
6개 일치 (2,000,000,000원) - 0개
총 수익률은 62.5%입니다.
```

---

##### 참고 사항

Lotto 클래스
```
public class Lotto {
    private final List<Integer> numbers;

    public Lotto(List<Integer> numbers) {
        validate(numbers);
        this.numbers = numbers;
    }

    private void validate(List<Integer> numbers) {
        if (numbers.size() != 6) {
            throw new IllegalArgumentException("[ERROR] 로또 번호는 6개여야 합니다.");
        }
    }

    // TODO: 추가 기능 구현
}
```
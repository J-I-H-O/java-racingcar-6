# 미션 - 자동차 경주 (프리코스 2주차)
## 기능 요구사항

- **(1) 자동차 이름 입력**
  - 사용자는 경주 할 자동차의 이름을 쉼표로 구분하여 입력한다.
  - 사용자가 잘못된 값을 입력하는 경우, `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.
- **(2) 시도할 횟수 입력**
  - 사용자는 몇 번의 이동을 할 것인지 입력한다.
  - 사용자가 잘못된 값을 입력하는 경우, `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.
- **(3) 경주 진행**
  - 각 자동차별로 0~`9 사이의 무작위 값을 구해 무작위 값이 4 이상인 경우 전진 시킨다.`
  - 매 시도마다 자동차의 전진 상황을 출력한다.
- **(4) 결과 출력**
  - 가장 많이 전진한 자동차(우승자)를 출력한다.
  - 우승자는 한 명 이상일 수 있으며, 우승자가 여러 명일 경우 쉼표를 이용하여 구분한다.
- **(5) 게임 종료:** 
  - 애플리케이션을 완전히 종료한다.
  - 사용한 리소스는 모두 해제한다.

## 예외 상황
"사용자가 잘못된 값을 입력하는 경우"에 해당하는 예외 상황을 정리하였습니다.
- **(1) 자동차 이름 입력**
  - null인 경우
  - 입력이 빈 문자열인 경우
  - 어떤 자동차의 이름이 빈 문자열인 경우
  - 어떤 자동차의 이름의 길이가 5글자를 초과하는 경우
- **(2) 시도할 횟수 입력**
  - null인 경우
  - 입력이 빈 문자열인 경우
  - 입력한 값이 숫자가 아닌 경우
  - 입력한 값이 음수인 경우
  - 입력한 값이 int형 범위를 벗어나는 경우 (Integer.parseInt() 내부적으로 예외 발생시킴)
- 이 경우 `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.

## 미션 수행 중 고민한 내용
- 각 클래스 간 의존성 제거
  - 이전 미션에서는 각 클래스가 서로 복잡하게 의존하고 있었기 때문에 유지보수도 어려웠고, 테스트에도 어려움을 겪었습니다.   
  - 2주차 미션에서는 처음부터 클래스를 역할별로 분리하고, 각 클래스가 최대한 독립적으로 동작할 수 있도록 고민해보았습니다.
- 출력을 담당하는 클래스 분리
  - 이전 미션에서는 출력문들이 이곳저곳에 분포되어있어 호출 순서가 달라지게 되면 의도치 않게 출력이 잘못되는 상황이 발생했습니다.
  - 이번 미션에서는 위와 같은 상황을 피하기 위해 입력과 출력을 담당하는 별도의 클래스를 생성하였습니다.
- 자동차 이름을 입력할 때 빈 문자열의 처리
  - 사용자 입력을 문자열 리스트로 변환하는 `Parser#parseStringList()` 메서드 개발 도중, 쉼표를 이용해 빈 문자열을 입력하는 경우에 대한 처리가 필요했습니다.
  - 가령, 사용자 입력이 `",jiho"` 인 경우, 빈 문자열 `""`와 `"jiho"` 두 개의 문자열을 입력한 것으로 처리하고자 하였습니다.
  - 또 다른 예시로 사용자 입력이 `",,"` 인 경우, 빈 문자열 `""`, `""`, `""` 총 3개의 문자열을 입력한 것으로 처리하려 했습니다.
  - [공식 레퍼런스](https://docs.oracle.com/javase%2F7%2Fdocs%2Fapi%2F%2F/java/lang/String.html#split(java.lang.String,%20int))를 참고하여 `limit` 파라미터의 값으로 음수를 넘겨주면 빈 문자열도 분리한다는 것을 알게되었고, 이를 코드에 적용하였습니다.
- `MoveDecider` 클래스에서, 자동차가 이동할지 여부를 나타낼 때 enum 사용
  - 기존에는 자동차가 이동 가능한지 여부를 나타낼 때 boolean 값을 리턴했으나 조금 더 명확한 의미를 갖도록 하기 위해 enum 클래스를 도입하였습니다.
- 객체를 생성하지 않고 `static` 메서드만 사용하는 클래스들의 경우, `private` 생성자를 갖도록 하여 외부에서 생성할 수 없도록 막았습니다.
- 테스트를 작성할 때 어떤 예외 상황이 있을지 고민해보았으며, 실제로 테스트 코드를 작성해 예상하는 결과로 이어지는지 확인해보았습니다.
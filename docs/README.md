# 미션 - 자동차 경주 (프리코스 2주차)
## 기능 요구사항

- **(1) 자동차 이름 입력**
  - 사용자는 경주 할 자동차의 이름을 쉼표로 구분하여 입력한다.
  - 사용자가 잘못된 값을 입력하는 경우, `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.
- **(2) 시도할 횟수 입력**
  - 사용자는 몇 번의 이동을 할 것인지 입력한다.
  - 사용자가 잘못된 값을 입력하는 경우, `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.
- **(3) 경주 진행**
  - 각 자동차별로 0~9 사이의 무작위 값을 구해 무작위 값이 4 이상인 경우 전진 시킨다.
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
  - 어떤 자동차의 이름의 길이가 5글자를 초과하는 경우
- **(2) 시도할 횟수 입력**
  - null인 경우
  - 입력이 빈 문자열인 경우
  - 입력한 값이 숫자가 아닌 경우
- 이 경우 `IllegalArgumentException`을 발생시킨 후 애플리케이션을 종료한다.

## 미션 수행 중 고민한 내용
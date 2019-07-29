### Python: OPP / Class / Instance

20190723화

---

#### [목차]

1. OPP with python

2.  without OPP

3. Class & Instance

   * 용어 정리

   1. 클래스 정의하기 = 클래스 객체 생성하기
   2. 인스턴스 생성하기
   3. My list 만들기
   4. self : 인스턴스 객체 자기 자신
   5. 클래스 - 인스턴스간의 이름 공간
   6. 생성자 / 소멸자

4.  what I don't know

   1. class에 직접 attribute를 지정하는 것과 함수로 변수를 만드는 것의 차이
   2. 

---

#### 1. OPP with python

- python은 객체 지향 언어

- class는 여러 변수(attribute)나 함수(method)를 담고 있다.

- instance = 객체

- class의 복사본 &  class로부터 독립적인 memory공간 = instance

---

#### 2. without OPP

opp없이 코드를 작성하면...

같은 structure의 코드가 조금씩 다른 대상에 적용되는 경우에, opp를 안쓴다면, 코드를 직접 다 작성해야하는 번거로움과, 수정의 어려움을 겪을 수 있다.

---

#### 3. Class & Instance

- 용어정리

  정의, 멤버변수(data attribute), 멤버 메서드(method)

  ```python
  class Person:                 #=> 클래스 정의(선언) : 클래스 객체 생성
      name = 'unknown'          #=> 멤버 변수(data attribute)
      def greeting(self):       #=> 멤버 메서드(메서드)
          return f'{self.name}'
      
  richard = Person()      # 인스턴스 객체 생성
  tim = Person()          # 인스턴스 객체 생성
  tim.name                # 데이터 어트리뷰트 호출
  tim.greeting()          # 메서드 호출
  ```

  ##### 1. 클래스 정의하기, 클래스 객체 생성하기

  
10. equals()와 hashcode()에 대해 설명해 주세요.
> 면접
equals는 2개의 객체가 참조하는 것이 동일한지 검사하는 메소드이다.
hashCode는 런타임에 객체의 해시코드 값을 반환하는 메소드이다. 
해시코드는 유일한(고유하게 식별할 수 있는) integer값이다.

> 공부
자바의 모든 클래스는 Object 클래스 상속 > 자바의 모든 객체가 기본적으로 갖춰야 할 기능 제공
                                        Object 클래스에는 equals, hashCode, toString 등의 메서드 포함
                                        Java의 모든 객체는 Object 클래스에 정의된 equals와 hashCode 함수를 상속

equals : 2개의 객체가 동일한지 검사하기 위해 사용
         equals 메서드 재정의x -> 동등성 비교는 객체의 참조(주소)를 비교하는 것으로 제한
         => 2개의 객체가 참조(주소)하는 것이 동일하면 동등

Q1) 동일한 객체가 메모리 상에 여러 개 띄워져있는 경우 
서로 다른 메모리에 있으므로 동일한(Identity) 객체X
하지만 프로그래밍에서는 같은 값을 가지므로 같은 객체로 인식되어야 함.
=> 동등성(Equality)을 위해 값으로 객체를 비교하도록 equals 메소드를 오버라이딩

ex) String 클래스의 equals 메소드 오버라이드
String s1 = new String("Test");
String s2 = new String("Test");

System.out.println(s1 == s2);			// false
System.out.println(s1.equals(s2));		// true
=> String 클래스에서 equals 메소드를 오버라이드하여 객체가 같은 값을 가지는지 '동등성(Equality)'을 비교하도록 처리

Q2) 동일성(Identity) vs 동등성(Equality)
완전 동일한 것과 값이 같은 것의 차이랄까..?

hashCode :  객체의 해시코드 값을 반환 (해시코드 = 정수값, 객체를 고유하게 식별)
            런타임에 객체의 유일한(고유하게 식별) integer값을 반환
            ex) Object 클래스 -> heap에 저장된 객체의 메모리주소 반환 (메모리 주소도 고유하니까!)

해시 값의 저장 : 객체의 특정 필드에 저장x -> 호출할 때마다 계산
해시 기반 컬렉션 (예: HashMap, HashSet)에서 객체를 저장하고 검색하는 데 사용됨
public native int hashCode();
native 키워드 : java native interface 라는 native code를 이용해 구현
                native는 메소드에만 적용 가능
                java가 아닌 언어로 구현된 부분을 JNI를 통해 java에서 이용할 때 사용
                hashCode는 HashTable과 같은 자료구조를 사용할 때 데이터가 저장되는 위치를 결정하기 위해 사용

+) equals와 hashCode의 관계
- equals 메소드, hashCode 메소드 같이 오버라이드 => 일관성 유지
equals가 동일하다고 판단된 객체 -> hashCode의 값도 같아야함

- equals에서 동일성이 아닌 동등성을 판단했다면? 
그래도 hashCode가 같아야함! -> equals와 hashCode를 같이 오버라이드 하는 이유!

- 해시 코드만으로 2개의 객체가 동일하다고 판별하기는 어려움 -> 해시 충돌이 있을 수 있음!

-------------------

- 본인이 hashcode() 를 정의해야 한다면, 어떤 점을 염두에 두고 구현할 것 같으세요?
> 면접&공부
equals 메소드가 오버라이드 됐는지, 어떤 것을 비교하는 오버라이드인지 염두하며 구현할 것이다.
equals의 판단이 true일 경우 hashCode값도 같아야하니까.

Q) equals가 ture일 때 왜 hashCode도 꼭 같아야할까? -> 둘 다 동일한 객체인지 판단해주는 함수인데 둘이 다르면 혼란스러우니까?
해시 기반 컬렉션(HashMap, HashSet 등)에서 객체의 일관성과 성능을 보장하기 위해서
-> 일관성 : 동일한 논리적 의미를 갖는 객체를 여러 버킷에 저장하면 일관성이 깨짐 (-> 해시 기반 컬렉션에서 동일한 위치에 있어야함)
-> 성능 : equals가 true를 반환하는 2개의 객체가 다른 해시코드를 가지면 해시 기반 컬렉션이 불필요한 비교 수행

-------------------

- 그렇다면 equals() 를 재정의 해야 할 때, 어떤 점을 염두에 두어야 하는지 설명해 주세요.
> 면접&공부
equals 메소드는 객체가 동일한지 비교하는 것입니다.
오버라이드할 클래스에서 equals를 사용할 때 완전히 일치한가의 동일성을 비교할 것인지,
값의 일치에 대한 동등성을 비교할 것인지 그렇다면 어떤 부분을 비교할지 염두하여 오버라이드 해야합니다.

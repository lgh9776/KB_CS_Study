### final 키워드를 사용하면, 어떤 이점이 있나요?

꼬리질문

1. 생성자 안에서 final 필드를 초기화하는 것과, 선언 시 초기화하는 것의 차이가 무엇인가요?

2. 참조형 변수일 때 final 키워드를 사용해도 값 변경이 불가능한가요?



<개념>

사용 가능한 곳 : final 키워드는 변수, 메서드, 클래스에 사용 가능

- 변수에 사용 : 초기화 후 값 변경 불가

(초기화 시점 : 변수 선언과 동시에 초기화 or 생성자에서 초기화)

- 메서드에 사용

재정의 불가 → 서브클래스에서 오버라이드 불가

메서드의 동작을 서브클래스에서 변경하지 못하도록 할 때 사용

- 클래스에 사용

상속 불가

클래스의 구현을 확장/변경하지 못하도록 할 때 사용

<이점>

- 불변성 유지 : 객체의 상태나 동작을 변경할 수 없도록 보장

- 안전성 : 상속, 오버라이드를 막아 코드의 안전성 높임
    
⇒ 의도하지 않은 변경 막아 버그 방지
    
- 최적화 : final 변수를 상수처럼 취급할 수 있어 런타임 성능 향상
    
인라이닝 (변수 값을 코드에 직접 삽입) 가능 → 변수 접근 시간 감소

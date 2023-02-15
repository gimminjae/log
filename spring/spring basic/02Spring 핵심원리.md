# Spring 핵심 원리
## 관심사의 분리
- 애플리케이션을 하나의 공연이라고 생각하고, 각각의 인터페이스를 배우의 역할(로미오, 줄리엣 역할)이라고 생각해보자.
- 실제로 역할(배역)을 맡는 배우들은 누가 선택하는가?
- 클라이언트가 인터페이스가 아닌 구현체에 의존하는 것은 마치 로미오 역할을 맡은 실제 배우가 직접 상대 줄리엣 배우를 정하는 것과 같다.
- 로미오를 맡은 배우는 로미오의 역할 뿐만 아니라 여자 배우를 공연에 초빙해야 하는 책임도 생기게 된다.
- 따라서 로미오 역할의 배우는 **다양한 책임**을 가지게 된다.


- 배우는 본인의 역할(배역)을 수행하는 것에만 집중하도록 하자.
- 로미오를 맡은 배우는 줄리엣을 연기할 배우가 누가 되든 공연을 할 수 있어야 한다.
- 로미오와 줄리엣 역할을 할 배우는 배우들이 정하는 것이 아니라
- 전체적인 공연 기획자가 공연을 구성하고, 배우를 섭외하고, 역할에 배우를 지정하는 책임을 맡는 것이다.

## AppConfig
- 애플리케이션의 전체 동작 방식을 구성하기 위해, 구현 객체를 생성하고 연결하는 책임을 가지는 별도의 설정 클래스
- 애플리케이션의 실제 동작에 필요한 구현 객체를 생성한다.
- 생성한 객체 인스턴스의 참조값을 생성자를 통해서 주입(연결)해 준다.

생성자 주입
```java
public class MemberServiceImpl implements MemberService {
        private final MemberRepository memberRepository;
        public MemberServiceImpl(MemberRepository memberRepository) {
            this.memberRepository = memberRepository;
        }
        public void join(Member member) {
            memberRepository.save(member);
        }
        public Member findMember(Long memberId) {
            return memberRepository.findById(memberId);
        } 
}
```
위와 같이 설계를 변경하면 MemberServiceImpl은 구현체가 아닌 MemberRepository 인터페이스를 의존한다.

MemberServiceImpl은 생성자를 통해서 어떤 구현 객체가 들어올지(주입될지) 알 수 없다.

해당 사항은 외부(AppConfig)에서 결정된다.

MemberServiceImpl은 의존관계에 대한 고민은 외부(AppConfig)에 맡기고 자신의 역할에만 집중할 수 있다.

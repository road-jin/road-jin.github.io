---
title: 단일 책임 원칙-SingleResponsibilityPrinciple
tag:
- SingleResponsibilityPrinciple
- solid
- srp
aside:
  toc: true
---
## 단일 책임 원칙 이란?

> 클래스는 단 한개의 책임을 가져야 한다.  
> 클래스나 모듈을 변경할 이유가 하나, 단하나뿐이어야 한다는 원칙이다.  
> 동일한 이유로 변경되는 것들을 함께 모으고, 서로 다른 이유로 변경되는 것들은 분리시킨다.  
> -로버트 C. 마틴-

로버트 C 마틴은 클래스에 책임이라는 개념 정의하고, 책임은 변경하려는 이유라고 정의하였습니다.  
클래스는 책임, 즉 변경할 이유가 하나여야 한다는 의미라고 합니다.

<br>

## 책임의 오해

- 클래스가 여러가지의 (public) 메소드를 가진다면, 복수의 책임을 갖는가?
- 클래스가 다중상속 (혹은 다중구현)을 한다면, 복수의 책임을 갖는가?
- 해당 클래스를 의존하는 사용자(클라이언트)가 여럿이라면 변경되는 이유는 여러가지가 되는가?

> 하나의 모듈은 하나의, 오직 하나의 액터에 대해서만 책임져야 한다.   
> -로버트 C. 마틴-

액터는 클래스의 변경을 유발하는 사람입니다.   
책임은 특정 액터의 요구사항을 만족시키기 위한 함수의 집합입니다.

<br>

## 액터와 책임

```java
public class MemberManager { 
    public void save(Member member) {
        
    }
    
    public void findById(Long memberId) {
        
    }
    
    public void calculateMembershipPoint(Long memberId) {
        
    }
}
```

MemberManager라는 클래스가 있습니다.  
해당 클래스의 함수들의 액터를 정의해 봅시다.

**save, findByid**   
회원을 저장하고, 조회하는 행동을 합니다.  
회원의 데이터를 어떻게 관리할지에 따라 매번 변경되어야 합니다.  
그러므로 회원의 데이터를 관리하는 사람이 엑터로 정의됩니다.

**calculateMembershipPoint**    
회원의 멤버쉽 포인트를 계산하는 행동을 합니다.  
멤버쉽 포인트를 계산하는 방식이 바뀔 때 마다 변경되어야 합니다.  
그러므로 멤버쉽 포인트를 기획하는 사람이 엑터로 정의됩니다.

이렇게 MemberManager는 두개의 액터가 존재하고 책임이 2가지가 됩니다.  
책임이 여러개 일때 발생하는 문제들을 알아봅시다.

- 낮은 가독성: 클래스가 여러 책임을 가지고 있어 코드를 이해하기 어려워집니다.
- 낮은 재사용성 : 특정 기능만 재사용하고 싶은데, 전체 클래스를 가져와야 하며, 코드가 중복되고 불필요한 코드를 증가 시킬 수 있습니다.
- 변경에 대한 영향 : 변경 했을 때 다른 기능에도 영향을 줄수가 있어 예상치 못한 버그가 발생할 수 있습니다.
- 낮은 확장성 : 새로운 기능을 추가하려고 할 때마다 코드의 구조를 크게 변경해야 할 수도 있습니다.

<br>

## 단일 책임 원칙 적용 예제

```java
public class MemberRepository { 
    public void save(Member member) {
        
    }
    
    public void findById(Long memberId) {
      
    }
}

public class MemberShipService {
    public void calculateMembershipPoint(Long memberId) {
      
    }
}
```

책임을 클래스를 통해서 분리함으로써,  데이터의 저장소를 바꿀 경우에는 MemberRepository만 변경 하면 됩니다.  
또한 MemberShip에 대한 요구사항이 변경되거나 추가될 경우 MemberShipService만 변경하면 되기 때문에   
유지보수 및 가독성이 좋아졌습니다.

단일 책임 원칙은 액터를 정의하는게 중요합니다.  
액터들을 나누어 책임을 분리하는게 단일 책임 원칙의 핵심입니다.

<br>

## Reference

[The Single Responsibility Principle](http://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html)      
[SOLID 원칙 / SOLID는 구식인가?](https://sihyung92.oopy.io/oop/solid)   
[[SOLID] 단일 책임 원칙(SRP)이란?](https://steady-coding.tistory.com/370)    
[단일 책임 원칙(SRP)](https://jaeseongdev.github.io/development/2021/02/14/%EB%8B%A8%EC%9D%BC_%EC%B1%85%EC%9E%84_%EC%9B%90%EC%B9%99_SRP)       
[클린 코더스 강의 13. SRP(Single Responsibility Principle)](https://www.youtube.com/watch?v=AdANHDp5dTM&t=103)

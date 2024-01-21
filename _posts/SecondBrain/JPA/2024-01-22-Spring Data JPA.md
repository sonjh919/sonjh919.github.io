---
title: Spring Data JPA
date: 2024-01-20 10:04
categories:
  - JPA
tags:
  - jpa
image: 
path:
---

## Spring Data JPA
- Spring Data JPA는 JPA를 쉽게 사용할 수 있게 만들어놓은 하나의 모듈로, **JPA를 추상화**시킨 **Repository 인터페이스**를 제공한다.
- Repository 인터페이스는 Hibernate 같은 JPA구현체를 사용해서 구현한 클래스를 통해 사용된다.
- Spring Data JPA에서는 JpaRepository 인터페이스를 구현하는 [SimpleJpaRepository](https://sonjh919.github.io/posts/SimpleJpaRepository)클래스를 자동으로 생성하여 Bean에 등록해준다.

![](/assets/img/IMG/JPA/SpringDataJPA.png)
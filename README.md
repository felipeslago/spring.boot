## Spring Boot
Spring Boot é um projeto criado pela Spring, que facilita o processo de criação de aplicações com o mínimo de configurações necessárias, além de permitir a criação de aplicações stand-alone, rodando em seu proprio servidor.

Este projeto é apenas um overview de algumas das funcionalidades e módulos oferecidos pelo Spring Boot.

## Setup com Gradle

O Gradle é utilizado como sistema de automação de compilação para este projeto.

No arquivo build.gradle foram adicionados os seguintes plugins:

* java: adiciona a compilação do Java com as funcionalidades de teste e build no projeto atual
* idea: gera um diretorio/modulo de arquivos com as configurações atuais do projeto, facilitando o import futuro para o Intellij
* org.springframework.boot: agrupa todos os jars no classpath em um unico runnable jar; busca pelo metodo main deixando ele como runnable.
* io.spring.dependency-management: tem um gerenciador de dependencias interno, que resolve a versão necessária de cada dependencia para ser compaivel com a versao atual do Spring Boot.

## Módulos utilizados

Os módulos abaixo são utilizado neste projeto:

* spring-boot-starter-web: criação de aplicações web, incluindo aplicações RESTful, com o uso de Spring MVC e Tomcat como embedded container padrão.
* spring-boot-starter-data-jpa: uso de JPA com Hibernate
* spring-boot-starter-thymeleaf: uso do Thymeleaf em aplicações MVC
* spring-boot-starter-security: uso do Spring Security
* h2: banco de dados embedded
* spring-boot-starter-test: uso de bibliotecas como JUnit, Hamcrest e Mockito para o teste de aplicações Spring Boot
* rest-assured: facilitador de testes de serviços REST
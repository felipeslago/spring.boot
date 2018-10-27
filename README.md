## Spring Boot
Spring Boot � um projeto criado pela Spring, que facilita o processo de cria��o de aplica��es com o m�nimo de configura��es necess�rias, al�m de permitir a cria��o de aplica��es stand-alone, rodando em seu proprio servidor.

Este projeto � apenas um overview de algumas das funcionalidades e m�dulos oferecidos pelo Spring Boot.

## Setup com Gradle

O Gradle � utilizado como sistema de automa��o de compila��o para este projeto.

No arquivo build.gradle foram adicionados os seguintes plugins:

* java: adiciona a compila��o do Java com as funcionalidades de teste e build no projeto atual
* idea: gera um diretorio/modulo de arquivos com as configura��es atuais do projeto, facilitando o import futuro para o Intellij
* org.springframework.boot: agrupa todos os jars no classpath em um unico runnable jar; busca pelo metodo main deixando ele como runnable.
* io.spring.dependency-management: tem um gerenciador de dependencias interno, que resolve a vers�o necess�ria de cada dependencia para ser compaivel com a versao atual do Spring Boot.

## M�dulos utilizados

Os m�dulos abaixo s�o utilizado neste projeto:

* spring-boot-starter-web: cria��o de aplica��es web, incluindo aplica��es RESTful, com o uso de Spring MVC e Tomcat como embedded container padr�o.
* spring-boot-starter-data-jpa: uso de JPA com Hibernate
* spring-boot-starter-thymeleaf: uso do Thymeleaf em aplica��es MVC
* spring-boot-starter-security: uso do Spring Security
* h2: banco de dados embedded
* spring-boot-starter-test: uso de bibliotecas como JUnit, Hamcrest e Mockito para o teste de aplica��es Spring Boot
* rest-assured: facilitador de testes de servi�os REST
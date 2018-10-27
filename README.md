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

## Inicializa��o

Para inicializar essa aplica��o Spring Boot em um container Tomcat dedicado, basta criar uma classe principal (Application.class) e anot�-la com @SpringBootApplication

A anota��o @SpringBootApplication funciona como um atalho para o uso de tr�s anota��es diferentes: @Configuration, @EnableAutoConfiguration e @ComponentScan.

* @Configuration: indica que uma classe declara um ou mais m�todos Bean, que ser�o processados e criados pelo container em tempo de execu��o.
* @EnableAutoConfiguration: busca e configura beans necess�rias para a inicializa��o da aplica��o, geralmente definidas no classpath da aplica��o (por libs usadas) e as pr�prias beans criadas.
* @ComponentScam: busca por componentes no c�digo para serem inicializados junto com a @Configuration.

No arquivo application.properties foi definida a propriedade server.port, que � utilizada para especificar a porta em que o container ir� executar, sobrescrevendo a porta default 8080.

## MVC View

Para exibir p�ginas, utilizamos o Thymeleaf.

Duas propriedades importantes foram definidas no application.properties:

* spring.thymeleaf.prefix: especifica o local onde est�o as p�ginas View
* spring.thymeleaf.suffix: especifica a extens�o das views

A classe SimpleController cria uma controller simples atrav�s de algumas anota��es.

* @Controller: retorna uma view, ou seja, dadas as configura��es do Thymeleaf, ao retornarmos "home" no m�todo homePage, o Spring ir� procurar no diret�rio templates pelo arquivo home.html (conforme definido no application.properties em prefix e suffix).
* @Value: recupera um valor de um arquivo de propriedades ou vari�vel de contexto. No caso do atributo appName, recupera a propriedade spring.application.name, do arquivo application.properties atrav�s do uso de ${}.
* @GetMapping: cria um mapeamento para requisi��es do tipo get na URL "/", ou seja para o nosso caso http://localhost:8081/ (rodando em localhost).

O m�todo homePage utilizado o m�todo model.addAttribute e nele especifica o valor do appName. Dessa maneira, conseguimos passar informa��es para a view, que receber� esse objeto model. E na View, atrav�s do namespace th:text, conseguimos recuperar essa informa��o.

## Seguran�a

Atrav�s da classe SecurityConfig conseguimos configurar a seguran�a de nossos endpoints com o uso de uma anota��o:

* @EnableSecurity: busca por endpoints expostos na aplica��o e cria uma regra de seguran�a para o acesso controlado a eles, baseado nas configura��es que definirmos.

As configura��es customizadas de seguran�a podem ser definidas extendendo a classe WebSecurityConfigurerAdapter e fazendo o override de seus m�todos.

Note que no m�todo configure estamos definindo no objeto http que todas as requi��es devem ser permitidas.

## Persist�ncia de dados

Primeiramente definimos a classe Book com o uso de algumas anota��es:

* @Entity: especifica que a classe � uma entidade de um banco de dados
* @Id: define que o campo ser� a chave prim�ria da tabela
* @GeneratedValue: define como ser� o esquema de gera��o de chave prim�ria, que no nosso caso ser� AUTO, ou seja, cada registro novo ter� uma chave gerada automaticamente pelo pr�prio banco de dados, de maneira incremental
* @Column: define que o campo ser� uma coluna no banco de dados e para o nosso caso, temos configura��es adicionais de nullable e unique, que definem se esse campo pode ser nulo e se deve ser �nico, respectivamente

Definida a entidade, precisamos criar um reposit�rio que ser� utilizado para interagir com a tabela real do banco de dados, atrav�s do uso da nossa entidade mapeada no c�digo java.

    O Spring Data tr�s uma maneira muito simples de interagir com o banco de dados, atrav�s da cria��o de simples interfaces.

    A interface BookRepository extende da interface CrudRepository, que em tempo de execu��o, ter� seus m�todos criados em mem�ria e prontos para uso.

    Veja que definimos a assinatura de um m�todo chamado findByTitle(String title), mas n�o tem implementa��o, pois � a� que come�a a m�gica do Spring Data. Em tempo de execu��o, a implementa��o default desse m�todo ser� criada pelo Spring e deixada em mem�ria.

    Al�m da facilidade em definir apenas uma assinatura, o nome dessa assinatura interefe diretamente no que a implementa��o ir� fazer, no nosso caso, ser� criada uma implementa��o que fara uma busca por t�tulos e devolver� uma lista.

Ap�s a entidade e o reposit�rio serem criados, � preciso colocar mais duas anota��es na classe principal (Application.class):

* @EnableJpaRepositories: busca por reposit�rios no pacote especificado
* @EntityScan: busca por entidades no pacote especificado

## Rest Controllers

Diferentemente da anota��o @Controller, que devolve uma View, temos outras anota��es para auxiliar no uso de chamadas REST:

* @RestController: serializa o retorno e o transforma para a resposta de uma chamada REST
* @RequestMapping: define paths para a classe como um todo
* @PostMapping: cria um mapeamento para requisi��es do tipo post
* @DeleteMapping: cria um mapeamento para requisi��es do tipo delete
* @PutMapping: cria um mapeamento para requisi��es do tipo put
* @ResponseStatus: define o http status code que ser� retornado na resposta da requisi��o
* @PathVariable: recupera o valor de uma path variable passada na URL
* @RequestBody: deserializa o conte�do do body de uma requisi��o em uma classe

## Error Handling

Para o tratamento de erros da aplica��o, utilizamos de um Exception Handler, que no nosso caso extende de um ResponseEntityExceptionHandler, que j� prov� alguns m�todos default.

O uso de algumas anota��es se faz necess�rio para tratarmos os erros da aplica��o:

* @ControllerAdvice: facilita a captura e o retorno de respostas em caso de erro na aplica��o, serializando objeto junto do http status code
* @ExceptionHandler: facilita a captura das exce��es lan�adas, como se fosse um try/catch final, evitando que a exce��o estoure para o usu�rio na tela

> Este conte�do foi gerado a partir do tutorial dispon�vel em https://www.baeldung.com/spring-boot-start
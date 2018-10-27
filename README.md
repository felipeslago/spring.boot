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

## Inicialização

Para inicializar essa aplicação Spring Boot em um container Tomcat dedicado, basta criar uma classe principal (Application.class) e anotá-la com @SpringBootApplication

A anotação @SpringBootApplication funciona como um atalho para o uso de três anotações diferentes: @Configuration, @EnableAutoConfiguration e @ComponentScan.

* @Configuration: indica que uma classe declara um ou mais métodos Bean, que serão processados e criados pelo container em tempo de execução.
* @EnableAutoConfiguration: busca e configura beans necessárias para a inicialização da aplicação, geralmente definidas no classpath da aplicação (por libs usadas) e as próprias beans criadas.
* @ComponentScam: busca por componentes no código para serem inicializados junto com a @Configuration.

No arquivo application.properties foi definida a propriedade server.port, que é utilizada para especificar a porta em que o container irá executar, sobrescrevendo a porta default 8080.

## MVC View

Para exibir páginas, utilizamos o Thymeleaf.

Duas propriedades importantes foram definidas no application.properties:

* spring.thymeleaf.prefix: especifica o local onde estão as páginas View
* spring.thymeleaf.suffix: especifica a extensão das views

A classe SimpleController cria uma controller simples através de algumas anotações.

* @Controller: retorna uma view, ou seja, dadas as configurações do Thymeleaf, ao retornarmos "home" no método homePage, o Spring irá procurar no diretório templates pelo arquivo home.html (conforme definido no application.properties em prefix e suffix).
* @Value: recupera um valor de um arquivo de propriedades ou variável de contexto. No caso do atributo appName, recupera a propriedade spring.application.name, do arquivo application.properties através do uso de ${}.
* @GetMapping: cria um mapeamento para requisições do tipo get na URL "/", ou seja para o nosso caso http://localhost:8081/ (rodando em localhost).

O método homePage utilizado o método model.addAttribute e nele especifica o valor do appName. Dessa maneira, conseguimos passar informações para a view, que receberá esse objeto model. E na View, através do namespace th:text, conseguimos recuperar essa informação.

## Segurança

Através da classe SecurityConfig conseguimos configurar a segurança de nossos endpoints com o uso de uma anotação:

* @EnableSecurity: busca por endpoints expostos na aplicação e cria uma regra de segurança para o acesso controlado a eles, baseado nas configurações que definirmos.

As configurações customizadas de segurança podem ser definidas extendendo a classe WebSecurityConfigurerAdapter e fazendo o override de seus métodos.

Note que no método configure estamos definindo no objeto http que todas as requições devem ser permitidas.

## Persistência de dados

Primeiramente definimos a classe Book com o uso de algumas anotações:

* @Entity: especifica que a classe é uma entidade de um banco de dados
* @Id: define que o campo será a chave primária da tabela
* @GeneratedValue: define como será o esquema de geração de chave primária, que no nosso caso será AUTO, ou seja, cada registro novo terá uma chave gerada automaticamente pelo próprio banco de dados, de maneira incremental
* @Column: define que o campo será uma coluna no banco de dados e para o nosso caso, temos configurações adicionais de nullable e unique, que definem se esse campo pode ser nulo e se deve ser único, respectivamente

Definida a entidade, precisamos criar um repositório que será utilizado para interagir com a tabela real do banco de dados, através do uso da nossa entidade mapeada no código java.

    O Spring Data trás uma maneira muito simples de interagir com o banco de dados, através da criação de simples interfaces.

    A interface BookRepository extende da interface CrudRepository, que em tempo de execução, terá seus métodos criados em memória e prontos para uso.

    Veja que definimos a assinatura de um método chamado findByTitle(String title), mas não tem implementação, pois é aí que começa a mágica do Spring Data. Em tempo de execução, a implementação default desse método será criada pelo Spring e deixada em memória.

    Além da facilidade em definir apenas uma assinatura, o nome dessa assinatura interefe diretamente no que a implementação irá fazer, no nosso caso, será criada uma implementação que fara uma busca por títulos e devolverá uma lista.

Após a entidade e o repositório serem criados, é preciso colocar mais duas anotações na classe principal (Application.class):

* @EnableJpaRepositories: busca por repositórios no pacote especificado
* @EntityScan: busca por entidades no pacote especificado

## Rest Controllers

Diferentemente da anotação @Controller, que devolve uma View, temos outras anotações para auxiliar no uso de chamadas REST:

* @RestController: serializa o retorno e o transforma para a resposta de uma chamada REST
* @RequestMapping: define paths para a classe como um todo
* @PostMapping: cria um mapeamento para requisições do tipo post
* @DeleteMapping: cria um mapeamento para requisições do tipo delete
* @PutMapping: cria um mapeamento para requisições do tipo put
* @ResponseStatus: define o http status code que será retornado na resposta da requisição
* @PathVariable: recupera o valor de uma path variable passada na URL
* @RequestBody: deserializa o conteúdo do body de uma requisição em uma classe

## Error Handling

Para o tratamento de erros da aplicação, utilizamos de um Exception Handler, que no nosso caso extende de um ResponseEntityExceptionHandler, que já provê alguns métodos default.

O uso de algumas anotações se faz necessário para tratarmos os erros da aplicação:

* @ControllerAdvice: facilita a captura e o retorno de respostas em caso de erro na aplicação, serializando objeto junto do http status code
* @ExceptionHandler: facilita a captura das exceções lançadas, como se fosse um try/catch final, evitando que a exceção estoure para o usuário na tela

> Este conteúdo foi gerado a partir do tutorial disponível em https://www.baeldung.com/spring-boot-start
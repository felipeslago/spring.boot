## A Linguagem de Programa��o Java
Na linguagem de programa��o Java, todos os c�digos-fonte s�o escritos em arquivo de puro texto com a extens�o .java

Esses arquivos s�o processados pelo Java Compiler (javac) em arquivos com a extens�o .class

Os arquivos .class cont�m bytecodes, que s�o a linguagem de m�quina utilizada pela Java Virtual Machine (JVM)

Como a JVM est� dispon�vel em v�rios sistemas operacionais (Windows, MacOS, Solaris e Linux), os mesmos arquivos .class podem ser utilizados em qualquer um deles

## A Plataforma Java

A Plataforma Java � composta pela Java Virtual Machine (JVM) e pela Java Application Programming Interface (API)

A divis�o � feita da seguinte forma:

1. Na camada mais alta temos o nosso c�digo-fonte no arquivo .java
2. Esse programa utiliza as APIs do Java para escrever suas instru��es
3. Ap�s compilado, a JVM utiliza os arquivos .class
4. O hardware recebe as instru��es de m�quina vindas da JVM

## Compilando um Arquivo Java

1. Para compilar e executar arquivos Java � necess�rio ter a JVM ou JDK instalados na m�quina
2. A partir do terminal, ou um editor de textos, crie um arquivo, por exemplo HelloWorld.java
3. Acesso o terminal, caso j� n�o esteja nele, v� at� o diret�rio do seu arquivo e compile esse arquivo com a instru��o `javac HelloWorld.java`
4. Dentro do mesmo diret�rio verifique se foi criado o arquivo HelloWorld.class e, caso positivo, execute o arquivo com o comando `java HelloWorld`

## Conceitos Sobre Orienta��o a Objetos

* Objeto
    * � um agrupamento de c�digo que possu� estados e comportamentos. 
    * Um objeto de software � geralmente utilizado para modelar um objeto do mundo real, como por exemplo uma bicicleta e muitas outras coisas que vemos no dia a dia.
    * Os estados s�o armazenados em vari�veis e os comportamentos s�o expostos atrav�s de m�todos.
    * Os m�todos operam nos estados internos de um objeto e servem como mecanismo prim�rio de comunica��o entre objetos diferentes.
    * Esconder todos os estados de um objeto e exigir que toda intera��o com ele seja feita atrav�s dos m�todos � conhecido como encapsulamento de dados.
    * Exemplo: Uma bicicleta possu� estados (marcha atual, velocidade atual) e estados (mudan�a de marcha, utiliza��o do freio).

* Classe
    * � um prot�tipo a partir do qual cada objeto ser� criado.
    * Utilizando o exemplo da bicicleta, uma classe � um conjunto de c�digos de programa��o que definem os estados e comportamentos desse objeto.
    * Podemos fabricar mais de uma bicicleta (objeto) a partir de um mesmo modelo (classe), gerando assim inst�ncias de classes que se tornam objetos.

```java
class Bicycle {

    int speed = 0;
    int gear = 1;

    void changeGear(int newValue) {
        gear = value;
    }

    void speedUp(int increment) {
        speed = speed + increment;
    }

    void brake(int decrement) {
        speed = speed - decrement;
    }
}
```

> No exemplo acima, os campos speed e gear representam os estados do objeto e os m�todos speedUp e brake representam a intera��o com o objeto.

* Heran�a
    * Diferentes tipos de objetos geralmente possuem caracter�sticas em comum.
    * Por exemplo, bicicletas comuns, bicicletas para esporte e etc. compartilham de estados e intera��es em comum, como marcha e velocidade.
    * Atrav�s da heran�a, � poss�vel que uma classe herde os estados e intera��es de outra classe e se preocupe apenas em codificar o que a torna �nica

```java
class MountainBike extends Bicycle {

    // fields and methods uniques for mountain bikes
}
```

> No exemplo acima, a palavra reservada extends ir� herder todos os campos e m�todos da classe Bicycle

* Interface
    * Em um carro, as intera��es tem que seguir um padr�o (acelerar, frear, ligar o farol e etc.).
    * Por�m um carro pode ser criado por diversos fornecedores diferentes, mas que devem seguir um mesmo padr�o (contrato) ao criar esse carro, afinal todos os carros precisam frear, acelerar e etc.
    * Uma interface � um contrato estabelecido com uma classe para que ela tenha m�todos (intera��es) que s�o padr�o ao seu tipo.

```java
interface Car {

    void speedUp(int increment);
    void brake(int decrement);
    void turnHeadLightOn();
    void turnHeadLightOff();
}
```

> No exemplo acima, foi criada uma interface de carro que tem m�todos padr�o, por�m n�o implementados, ou seja, a interface define quais m�todos uma classe deve ter, mas n�o define como implement�-los.

```java
class CarX implements Car {

    int speed = 0;

    void speedUp(int increment) {
        speed = speed + increment;
    }

    void brake(int decrement) {
        // custom implementation goes here
    }

    void turnHeadLightOn() {
        // custom implementation goes here
    }

    void turnHeadLightOff() {
        // custom implementation goes here
    }
}
```

```java
class CarY implements Car {

    int speed = 0;

    void speedUp(int increment) {
        speed = speed + increment + 1;
    }

    void brake(int decrement) {
        // custom implementation goes here
    }

    void turnHeadLightOn() {
        // custom implementation goes here
    }

    void turnHeadLightOff() {
        // custom implementation goes here
    }
}
```

> Nos exemplos acima, foram criados dois carros (CarX e CarY), os dois implementam os m�todos da interface Car, por�m cada um implementa do seu jeito.

* Pacote
    * Um pacote � um nome (namespace) que organiza um conjunto de classes e interfaces.
    * Conceitualmente, um pacote pode ser entendido como um conjunto de pastas no computador que organizam e dividem arquivos.
    * A plataforma Java prov� uma biblioteca (conjunto de classes e interfaces divididas em pacotes) chamada "Application Programming Interface" (API), que auxiliam o desenvolvimento de aplica��es.

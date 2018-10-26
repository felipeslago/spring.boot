## A Linguagem de Programação Java
Na linguagem de programação Java, todos os códigos-fonte são escritos em arquivo de puro texto com a extensão .java

Esses arquivos são processados pelo Java Compiler (javac) em arquivos com a extensão .class

Os arquivos .class contém bytecodes, que são a linguagem de máquina utilizada pela Java Virtual Machine (JVM)

Como a JVM está disponível em vários sistemas operacionais (Windows, MacOS, Solaris e Linux), os mesmos arquivos .class podem ser utilizados em qualquer um deles

## A Plataforma Java

A Plataforma Java é composta pela Java Virtual Machine (JVM) e pela Java Application Programming Interface (API)

A divisão é feita da seguinte forma:

1. Na camada mais alta temos o nosso código-fonte no arquivo .java
2. Esse programa utiliza as APIs do Java para escrever suas instruções
3. Após compilado, a JVM utiliza os arquivos .class
4. O hardware recebe as instruções de máquina vindas da JVM

## Compilando um Arquivo Java

1. Para compilar e executar arquivos Java é necessário ter a JVM ou JDK instalados na máquina
2. A partir do terminal, ou um editor de textos, crie um arquivo, por exemplo HelloWorld.java
3. Acesso o terminal, caso já não esteja nele, vá até o diretório do seu arquivo e compile esse arquivo com a instrução `javac HelloWorld.java`
4. Dentro do mesmo diretório verifique se foi criado o arquivo HelloWorld.class e, caso positivo, execute o arquivo com o comando `java HelloWorld`

## Conceitos Sobre Orientação a Objetos

* Objeto
    * É um agrupamento de código que possuí estados e comportamentos. 
    * Um objeto de software é geralmente utilizado para modelar um objeto do mundo real, como por exemplo uma bicicleta e muitas outras coisas que vemos no dia a dia.
    * Os estados são armazenados em variáveis e os comportamentos são expostos através de métodos.
    * Os métodos operam nos estados internos de um objeto e servem como mecanismo primário de comunicação entre objetos diferentes.
    * Esconder todos os estados de um objeto e exigir que toda interação com ele seja feita através dos métodos é conhecido como encapsulamento de dados.
    * Exemplo: Uma bicicleta possuí estados (marcha atual, velocidade atual) e estados (mudança de marcha, utilização do freio).

* Classe
    * É um protótipo a partir do qual cada objeto será criado.
    * Utilizando o exemplo da bicicleta, uma classe é um conjunto de códigos de programação que definem os estados e comportamentos desse objeto.
    * Podemos fabricar mais de uma bicicleta (objeto) a partir de um mesmo modelo (classe), gerando assim instâncias de classes que se tornam objetos.

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

> No exemplo acima, os campos speed e gear representam os estados do objeto e os métodos speedUp e brake representam a interação com o objeto.

* Herança
    * Diferentes tipos de objetos geralmente possuem características em comum.
    * Por exemplo, bicicletas comuns, bicicletas para esporte e etc. compartilham de estados e interações em comum, como marcha e velocidade.
    * Através da herança, é possível que uma classe herde os estados e interações de outra classe e se preocupe apenas em codificar o que a torna única

```java
class MountainBike extends Bicycle {

    // fields and methods uniques for mountain bikes
}
```

> No exemplo acima, a palavra reservada extends irá herder todos os campos e métodos da classe Bicycle

* Interface
    * Em um carro, as interações tem que seguir um padrão (acelerar, frear, ligar o farol e etc.).
    * Porém um carro pode ser criado por diversos fornecedores diferentes, mas que devem seguir um mesmo padrão (contrato) ao criar esse carro, afinal todos os carros precisam frear, acelerar e etc.
    * Uma interface é um contrato estabelecido com uma classe para que ela tenha métodos (interações) que são padrão ao seu tipo.

```java
interface Car {

    void speedUp(int increment);
    void brake(int decrement);
    void turnHeadLightOn();
    void turnHeadLightOff();
}
```

> No exemplo acima, foi criada uma interface de carro que tem métodos padrão, porém não implementados, ou seja, a interface define quais métodos uma classe deve ter, mas não define como implementá-los.

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

> Nos exemplos acima, foram criados dois carros (CarX e CarY), os dois implementam os métodos da interface Car, porém cada um implementa do seu jeito.

* Pacote
    * Um pacote é um nome (namespace) que organiza um conjunto de classes e interfaces.
    * Conceitualmente, um pacote pode ser entendido como um conjunto de pastas no computador que organizam e dividem arquivos.
    * A plataforma Java provê uma biblioteca (conjunto de classes e interfaces divididas em pacotes) chamada "Application Programming Interface" (API), que auxiliam o desenvolvimento de aplicações.

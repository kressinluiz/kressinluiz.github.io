---
title: 'Expressões Lambda e Interfaces Funcionais'
description: 'Expressões Lambda são uma forma concisa de escrever funções sem nome (anônimas) e que foram introduzidas no Java 8 para simplificar o uso de interfaces funcionais.'
pubDate: 'Jul 18 2026'
heroImage: '../../assets/expressoes-lambda.jpg'
---

# Expressões Lambda

As expressões lambda têm como objetivo simplificar a implementação de interfaces funcionais, tornado o código mais legível e menos verboso.
Uma expressão lambda possui a seguinte sintaxe quando contém apenas uma única expressão:
```
(parâmetros) -> expressão

x -> x*x

(x,y) -> x*y 
```

Quando há mais de uma instrução, é necessário utilizar um bloco de código ({}) e, caso o método retorne um valor, a instrução `return`:
```
(parâmetros) -> {
    //Instrução 1
    //Instrução 2
}

(x,y) -> {
    int mult = x*y;
    return mult;
}
```

# Interfaces
Uma interface em Java é uma estrutura que especifica o que uma classe deve fazer, sem definir como deve ser feito. Uma interface pode conter métodos abstratos, métodos default, métodos static, métodos private e constantes.

Os métodos `default` possuem implementação dentro da interface. A classe que implementar essa interface pode utilizar o método já implementado na interface ou pode sobrescrever para implementar um comportamento específico.

Os métodos `static` pertencem à interface e não aos objetos, ou seja, é possível usar o método sem criar uma instância.

Os métodos `private` servem para reutilizar código entre métodos `default` e `static` e só pode ser chamado dentro da própria interface.

Todas as constantes que são declaradas em uma interface são automaticamente `public`, `static`, `final`. Isso significa que podem ser usadas de fora da interface, é possível usar a constante sem ciar um objeto e não pode ser atribuido outro valor.

Os métodos `abstratos` são métodos sem implementação. Quem implementa a interface deve fornecer a implementação:
```
public interface Animal {
    void andar();

    void comer();
}

public class Cachorro implements Animal {
    @Override
    public void andar() {
        System.out.println("Andando...");
    }

    @Override
    public void comer() {
        System.out.println("Comendo...");
    }
}

Animal animal = new Cachorro();
animal.andar();
```

# Interfaces Funcionais

Uma expressão lambda não existe sozinha. Ela sempre irá implementar uma interface funcional, ou seja, uma interface que possui apenas um método abstrato. A interface funcional pode conter vários métodos, desde que apenas um deles seja abstrato.

Se considerarmos a seguinte interface funcional:
```
@FunctionalInterface
interface Animal {
    public void andar();
}
```
Para implementar sem expressões lambda seria:
```
Animal gatoSemLambda = new Animal() {
    @Override
    public void andar() {
        System.out.println("Andando...");
    }
};

gatoSemLambda.andar();
```
Entretanto, a sintaxe com expressão lambda é mais enxuta:
```
Animal gatoComLambda = () -> System.out.println("Andando...");

gatoComLambda.andar();
```

Vale lembrar que a anotaçao `@FunctionalInterface` não é obrigatória, mas serve para validar a interface na compilação. O compilador irá lançar um erro caso a interface tiver mais de um método abstrato, por exemplo.

# Conclusão
As expressões lambda fornecem uma forma mais simples e menos verbosa de implementar interfaces funcionais, tornando o código mais legível, conciso e expressivo.
As interfaces funcionais são um tipo especial de interface que podem conter diversos métodos, desde que apenas um deles seja abstrato. 
Na prática raramente é preciso criar interfaces funcionais porque o Java possui interfaces funcionais prontas na biblioteca `java.util.function` que tratam dos casos mais comuns. Esse será o assunto do próximo artigo.

# Teste Unitário com JUnit, Maven, IntelliJ e Java

## **1. Introdução**
Os testes unitários são uma prática essencial no desenvolvimento de software para garantir a qualidade e a funcionalidade do código. Neste tutorial, abordaremos como configurar e executar testes unitários em Java usando JUnit, gerenciar dependências com Maven e utilizar o IntelliJ IDEA como ambiente de desenvolvimento. Também exploraremos como verificar a cobertura de testes.

---

## **2. Configuração do Ambiente**

### **2.1 Instalar o IntelliJ IDEA**
1. Acesse o site oficial do IntelliJ IDEA: [JetBrains IntelliJ IDEA](https://www.jetbrains.com/idea/).
2. Baixe a versão Community (gratuita) ou Ultimate (paga).
3. Instale o IntelliJ IDEA seguindo as instruções para o seu sistema operacional.

### **2.2 Instalar o Java JDK**
1. Baixe a versão mais recente do Java JDK: [Oracle JDK](https://www.oracle.com/java/technologies/javase-downloads.html) ou [OpenJDK](https://openjdk.org/).
2. Após instalar, configure a variável de ambiente `JAVA_HOME` com o caminho do JDK.

### **2.3 Instalar o Maven**
1. Baixe o Maven no site oficial: [Maven Downloads](https://maven.apache.org/download.cgi).
2. Extraia os arquivos e configure a variável de ambiente `MAVEN_HOME`.
3. Adicione o diretório `bin` do Maven ao `PATH` do sistema.

### **2.4 Verificar Instalações**
Abra o terminal e execute os seguintes comandos para confirmar as instalações:
```bash
java -version
mvn -version
```

---

## **3. Configuração do Projeto Maven no IntelliJ**

### **3.1 Criar um Projeto Maven**
1. Abra o IntelliJ IDEA.
2. Vá em **File > New > Project**.
3. Selecione **Maven** e clique em **Next**.
4. Defina o nome do projeto, o GroupId (e.g., `com.example`) e o ArtifactId (e.g., `junit-tutorial`).
5. Escolha o diretório onde o projeto será criado e clique em **Finish**.

### **3.2 Adicionar Dependência JUnit ao `pom.xml`**
Abra o arquivo `pom.xml` e adicione a dependência do JUnit 5:
```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.10.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Atualize o Maven clicando em **Reload Maven Project** na aba Maven do IntelliJ.

---

## **4. Criando Testes Unitários com JUnit**

### **4.1 Estrutura de Diretórios**
Certifique-se de que seu projeto tenha a seguinte estrutura:
```
src/
├── main/
│   └── java/
│       └── com/example/
│           └── Calculator.java
└── test/
    └── java/
        └── com/example/
            └── CalculatorTest.java
```

### **4.2 Criar a Classe `Calculator`**
No diretório `src/main/java/com/example`, crie a classe `Calculator`:
```java
package com.example;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public int divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Division by zero is not allowed");
        }
        return a / b;
    }
}
```

### **4.3 Criar a Classe de Teste `CalculatorTest`**
No diretório `src/test/java/com/example`, crie a classe `CalculatorTest`:
```java
package com.example;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    private final Calculator calculator = new Calculator();

    @Test
    void testAdd() {
        assertEquals(5, calculator.add(2, 3));
    }

    @Test
    void testSubtract() {
        assertEquals(1, calculator.subtract(3, 2));
    }

    @Test
    void testMultiply() {
        assertEquals(6, calculator.multiply(2, 3));
    }

    @Test
    void testDivide() {
        assertEquals(2, calculator.divide(6, 3));
    }

    @Test
    void testDivideByZero() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> calculator.divide(1, 0));
        assertEquals("Division by zero is not allowed", exception.getMessage());
    }
}
```

---

## **5. Executando os Testes**

### **5.1 Executar os Testes no IntelliJ**
1. Clique com o botão direito na pasta `test/java` ou na classe `CalculatorTest`.
2. Selecione **Run 'All Tests'**.

### **5.2 Executar os Testes pelo Maven**
No terminal, dentro do diretório do projeto, execute:
```bash
mvn test
```

---

## **6. Verificando a Cobertura de Testes**

1. Instale o plugin **Coverage** no IntelliJ (se não estiver instalado).
2. Execute os testes com cobertura:
   - Clique com o botão direito na classe de teste e selecione **Run 'CalculatorTest' with Coverage**.
3. A cobertura será exibida no editor e na aba **Coverage**.

---

## **7. Exemplos Práticos Avançados**

### **7.1 Testando Comportamento com Mocks**
Adicione a dependência Mockito ao `pom.xml`:
```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>5.5.0</version>
    <scope>test</scope>
</dependency>
```

Exemplo de teste com Mockito:
```java
package com.example;

import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

import static org.mockito.Mockito.*;

class ServiceTest {

    @Test
    void testServiceWithMock() {
        Calculator calculator = Mockito.mock(Calculator.class);
        when(calculator.add(2, 3)).thenReturn(5);

        assertEquals(5, calculator.add(2, 3));
        verify(calculator).add(2, 3);
    }
}
```

## **Como Funciona o Teste para Erros no JUnit**

No JUnit, podemos testar cenários onde esperamos que um método lance uma exceção específica ao encontrar uma condição inválida. Para isso, usamos o método estático `assertThrows`. Ele é utilizado para capturar e verificar se a exceção lançada pelo código testado é do tipo esperado, além de permitir validar a mensagem associada à exceção.

No caso do método `testModuloByZero`, ele verifica o seguinte:
1. O método `calculator.calculate` é chamado com argumentos que causam uma divisão por zero usando o operador `%` (módulo).
2. `assertThrows` monitora a execução do lambda (função anônima) fornecido.
3. Se a exceção `ArithmeticException` for lançada, o teste passa; caso contrário, o teste falha.
4. Após capturar a exceção, o código verifica se a mensagem da exceção corresponde à esperada, usando `assertEquals`.

#### **Passo a Passo do Teste**
```java
Exception exception = assertThrows(ArithmeticException.class, () -> calculator.calculate("6.0", "0.0", "%"));
```

1. **`assertThrows`**:
   - Primeiro argumento: a classe da exceção esperada (`ArithmeticException.class`).
   - Segundo argumento: um lambda que executa o código a ser testado.
   - Se o método chamado no lambda não lançar a exceção esperada, o teste falha.

2. **Lambda `() -> calculator.calculate(...)`**:
   - Define uma função que encapsula a execução do método a ser testado.
   - O lambda só será executado dentro do contexto do `assertThrows`.

3. **Validação da Mensagem**:
   ```java
   assertEquals("Divisão por zero não é permitida", exception.getMessage());
   ```
   - Após capturar a exceção, verificamos se sua mensagem corresponde à esperada.

---

### **O Que é um Lambda em Java?**

Um **lambda** em Java é uma forma concisa de implementar interfaces funcionais (interfaces com apenas um método abstrato). Ele é usado para representar funções anônimas e é amplamente utilizado em APIs como Streams, além de facilitar testes e callbacks.

#### **Sintaxe de um Lambda**
```java
(parameters) -> { body }
```

- **Parâmetros**: Variáveis que o lambda recebe como entrada.
- **`->`**: Um operador que separa os parâmetros do corpo da função.
- **Corpo**: Código a ser executado pelo lambda.

#### **Exemplos de Lambda**

1. **Lambda Simples**:
   ```java
   (int x, int y) -> x + y
   ```
   - Recebe dois inteiros (`x` e `y`) e retorna sua soma.

2. **Lambda Sem Parâmetros**:
   ```java
   () -> System.out.println("Hello, Lambda!");
   ```
   - Não recebe parâmetros e apenas executa um código.

3. **Lambda Com Um Parâmetro**:
   ```java
   x -> x * x
   ```
   - O tipo do parâmetro pode ser inferido, e o retorno é o quadrado de `x`.

4. **Lambda em uma Lista**:
   ```java
   List<Integer> numbers = Arrays.asList(1, 2, 3);
   numbers.forEach(n -> System.out.println(n));
   ```
   - Itera sobre uma lista e imprime cada elemento.

---

### **Como os Lambdas Funcionam no Contexto de Testes**

No exemplo de teste:
```java
() -> calculator.calculate("6.0", "0.0", "%")
```

1. **Lambda Como Código a Ser Testado**:
   - O código dentro do lambda é o que será executado durante o teste.
   - Ele encapsula a chamada ao método `calculator.calculate`.

2. **Benefício do Lambda**:
   - Permite que o método `assertThrows` execute o código e capture a exceção.
   - Substitui a necessidade de criar classes ou métodos específicos para encapsular essa lógica.

---

### **Por Que Usar Lambdas no JUnit?**

1. **Concisão**:
   - O código é mais curto e direto ao ponto.
   - Substitui a necessidade de criar classes anônimas para implementar o comportamento.

2. **Legibilidade**:
   - Fica claro qual trecho de código está sendo testado.

3. **Compatibilidade**:
   - Lambdas podem ser usados em qualquer lugar onde uma interface funcional seja esperada, como em `assertThrows`.

---

## Exercícios

### Exercício 1

```java

public double calcular(double num1, double num2, char operador) {
        double resultado;
        switch (operador) {
            case '+':
                resultado = num1 + num2;
                break;
            case '-':
                resultado = num1 - num2;
                break;
            case '*':
                resultado = num1 * num2;
                break;
            case '/':
                // Verifica se o segundo número é zero antes de realizar a divisão
                if (num2 == 0) {
                    System.out.println("Erro: Não é possível dividir por zero.");
                    return Double.NaN; // Retorna 'NaN' em caso de erro
                } else {
                    resultado = num1 / num2;
                }
                break;
            default:
                System.out.println("Operador inválido.");
                return Double.NaN; // Retorna 'NaN' caso o operador não seja válido
        }
        return resultado;
    }
```


### Exercício 2

```java
package com.example;

public class Calculator {

    public double calculate(String value1Str, String value2Str, String operator) {
        double result;

        // Validação de valores nulos ou vazios
        if (value1Str == null || value2Str == null || operator == null ||
            value1Str.isBlank() || value2Str.isBlank() || operator.isBlank()) {
            throw new IllegalArgumentException("Valores e operador não podem ser nulos ou vazios");
        }

        double value1;
        double value2;

        // Tentativa de conversão de Strings para números
        try {
            value1 = Double.parseDouble(value1Str);
        } catch (NumberFormatException e) {
            throw new IllegalArgumentException("O primeiro valor não é numérico");
        }

        try {
            value2 = Double.parseDouble(value2Str);
        } catch (NumberFormatException e) {
            throw new IllegalArgumentException("O segundo valor não é numérico");
        }

        // Operações disponíveis
        switch (operator) {
            case "+":
                result = value1 + value2;
                break;
            case "-":
                result = value1 - value2;
                break;
            case "*":
                result = value1 * value2;
                break;
            case "/":
                if (value2 == 0) {
                    throw new ArithmeticException("Divisão por zero não é permitida");
                }
                result = value1 / value2;
                break;
            case "%":
                if (value2 == 0) {
                    throw new ArithmeticException("Divisão por zero não é permitida");
                }
                result = value1 % value2;
                break;
            case "^":
                result = Math.pow(value1, value2);
                break;
            case "root":
                if (value1 < 0 && value2 % 2 == 0) {
                    throw new ArithmeticException("Raiz de número negativo com índice par não é permitida");
                }
                result = Math.pow(value1, 1 / value2);
                break;
            default:
                throw new IllegalArgumentException("Operador inválido. Operadores permitidos são: +, -, *, /, %, ^, root");
        }

        // Validação do resultado infinito ou NaN
        if (Double.isInfinite(result) || Double.isNaN(result)) {
            throw new ArithmeticException("Resultado inválido");
        }

        return result;
    }
}


```


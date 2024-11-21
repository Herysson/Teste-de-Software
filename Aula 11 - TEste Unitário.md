# Tutorial Completo sobre Teste Unitário com JUnit, Maven, IntelliJ e Java

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

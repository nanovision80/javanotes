# Tópicos Fundamentais da Linguagem Java

## (1) Identificadores: Restrições e Convenções de Nomenclatura

Na programação, a clareza do código começa pela correta nomeação de seus artefatos (variáveis, métodos, classes). Em Java, devemos distinguir entre o que é obrigatório (restrições do compilador) e o que é recomendado (convenções da comunidade / indústria).

### Restrições Sintáticas

O compilador Java impõe regras estritas para a criação de identificadores. A violação destas regras resulta em erro de compilação.

* **Dígitos Iniciais**: Um identificador não pode iniciar com um número.

* **Espaçamento**: Não são permitidos espaços em branco.

* **Caracteres Especiais**: Embora tecnicamente o `$` e `_` sejam permitidos, o uso de acentos ou til deve ser evitado para garantir interoperabilidade entre diferentes codificações de sistema.

### Convenções de Estilo

Para manter a legibilidade e padronização, utilizamos convenções de case (caixa alta/baixa):

* **Camel Case**: Inicia com letra minúscula e cada palavra subsequente inicia com maiúscula. Utilizado para variáveis, atributos e métodos.
  
  **Exemplo**: `lastName`, `salarioDoFuncionario`.

* **Pascal Case**: Similar ao Camel Case, mas a primeira letra também é maiúscula. Utilizado para classes.
  
  **Exemplo**: `ProductService`, `Account`.

**Exemplo de Código**:

```java
// --- Violações (Erros de Compilação ou Más Práticas) ---
int 5minutes;                    // Erro: Começa com dígito 
int salario do funcionario;     // Erro: Contém espaços [cite: 3]
int salário;                     // Evitar: Acentos [cite: 3]

// --- Correto e Convencional ---
int _5minutes;                   // Válido (embora _ inicial seja incomum, é permitido) [cite: 3]
int salarioDoFuncionario;         // Correto: Camel Case [cite: 3]

public class Account {           // Correto: Pascal Case para classes [cite: 5]
    private double balance;     // Correto: Camel Case para atributos [cite: 5]

    public void withdraw(double amount) { // Correto: Camel Case para métodos [cite: 7]
        // implementação
    }
}
```

## (2) Operadores Bitwise (*Bit* a *Bit*)

Os operadores *bitwise* permitem a manipulação direta de números em sua representação binária. Eles são fundamentais em programação de baixo nível, protocolos de rede e verificação de *flags*.

### Tipos de Operadores

* `E` (AND) `&`: Resulta em 1 (**verdadeiro**) apenas se ambos os *bits* forem 1.

* `OU` (OR) `|`: Resulta em 1 (**verdadeiro**) se pelo menos um dos *bits* for 1.

* `XOR` (OU-Exclusivo) `^`: Resulta em 1 (**verdadeiro**) se os *bits* forem diferentes entre si.

### Aplicação Prática: Máscara de Bits (*Bit Masking*)

Uma aplicação comum é verificar se um *bit* específico está "ligado" (valor 1). No exemplo abaixo, verificamos se o 6º *bit* de um número é verdadeiro utilizando uma máscara.

**Lógica Matemática**: Seja `n = 113` (binário `0111 0001`) e a máscara `mask = 32` (binário `0010 0000`, onde apenas o 6º *bit* é 1). A operação `n^mask` resultará em zero se o 6º *bit* de `n` for zero, ou diferente de zero se o 6º *bit* for 1.

**Exemplo de Código**:

```java
import java.util.Scanner;

public class Program {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int mask = 0b100000; // Representação binária de 32 (6º bit ativo) [cite: 16]
        int n = sc.nextInt();
        
        // Verifica se o 6º bit está ativo aplicando a operação AND
        if ((n & mask) != 0) {
            System.out.println("6th bit is true!"); [cite: 17]
        } else {
            System.out.println("6th bit is false");
        }
        
        sc.close();
    }
}
```

## (3) Manipulação de *Strings*

Em Java, `Strings` são objetos imutáveis que representam sequências de caracteres. A API padrão fornece diversos métodos para formatar, recortar, substituir e buscar elementos dentro de uma String.

### Principais Operações

* **Formatação**: Alterar caixa alta/baixa (`toLowerCase`, `toUpperCase`) ou remover espaços excedentes nas extremidades (`trim`).

* **Recorte e Substituição**: Extrair partes da string (`substring`) ou substituir caracteres/trechos (`replace`).

* **Busca**: Localizar a posição de um caractere ou substring (`indexOf`, `lastIndexOf`).

* **Divisão (*Split*)**: Quebrar uma string em um vetor com base em um separador.
  
  

**Exemplo de Código:**

```java
String original = "abcde FGHIJ ABC abc DEFG   ";

// Formatação
String s01 = original.toLowerCase();  // "abcde fghij abc abc defg   " [cite: 19]
String s03 = original.trim();         // Remove espaços do início e fim [cite: 19]

// Recorte
// substring(início): Pega do índice 2 até o fim
String s04 = original.substring(2);   // "cde FGHIJ ABC abc DEFG   " [cite: 19]
// substring(início, fim): Pega do índice 2 até o 9 (exclusivo)
String s05 = original.substring(2, 9); // "cde FGH" [cite: 19]

// Substituição
String s06 = original.replace('a', 'x'); // Troca todo 'a' por 'x' [cite: 19]

// Operação Split (Vetorização)
String s = "potato apple lemon";
String[] vect = s.split(" "); // Quebra a string onde houver espaço [cite: 21]
// vect[0] -> "potato", vect[1] -> "apple", vect[2] -> "lemon" [cite: 21]
```

## (4) Comentários e Documentação

O uso de comentários é vital para a manutenção do software. O compilador ignora estes trechos, permitindo que o programador deixe anotações sobre a lógica implementada.

* **Comentário de Linha**: Utiliza-se `//`. Ideal para notas breves.

* **Comentário de Bloco**: Utiliza-se `/* ... */`. Ideal para documentar cabeçalhos de arquivos ou lógicas complexas de múltiplas linhas.

**Exemplo de Código:**

```java
/*
Este programa calcula as raízes de uma equação do segundo grau.
Os valores dos coeficientes devem ser digitados um por linha.
*/ 
// 

double delta;
// cálculo do valor de delta
delta = Math.pow(b, 2.0) - 4*a*c; // [cite: 25]
```

## (5) Funções (Métodos) e Modularização

A modularização é um pilar da programação estruturada e orientada a objetos. Funções (ou métodos, no contexto de classes) representam um processamento que possui um significado semântico definido (ex: "calcular raiz", "mostrar resultado").

### Vantagens da Modularização

1. **Reaproveitamento**: O mesmo código pode ser chamado várias vezes.

2. **Delegação**: Retira a responsabilidade do método `main`, deixando o código mais limpo.

3. **Organização**: Separa a lógica em blocos menores e gerenciáveis.

### Sintaxe e Estrutura

Um método é definido por seu modificador de acesso (ex: `public`), tipo de retorno (ex: `int`, `void`), nome e parâmetros (dados de entrada).

**Estudo de Caso:** Encontrar o maior de três números. Ao invés de escrever toda a lógica de `if/else` dentro do `main`, criamos uma função `max` que recebe os números e retorna o maior, e uma função `showResult` para imprimir.

**Exemplo de Código (Modularizado):**

```java
public class Program {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Leitura de dados
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();

        // Chamada da função que processa a lógica
        int higher = max(a, b, c); // [cite: 33]
        
        // Chamada da função que exibe o resultado
        showResult(higher); // [cite: 33]
        
        sc.close();
    }

    // Função que retorna um inteiro (o maior valor)
    public static int max(int x, int y, int z) { // 
        int aux;
        if (x > y && x > z) {
            aux = x;
        } else if (y > z) {
            aux = y;
        } else {
            aux = z;
        }
        return aux; // Retorna o valor calculado [cite: 36]
    }

    // Função 'void' (não retorna valor, apenas executa uma ação)
    public static void showResult(int value) {
        System.out.println("Higher = " + value); // [cite: 36]
    }
}
```
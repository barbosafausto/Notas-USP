# Introdução à Programação Funcional em Java

Apesar de ser fundamentalmente Orientada a Objetos (POO), a partir do Java 8 a linguagem introduziu recursos poderosos de Programação Funcional, facilitando um estilo de código mais declarativo e conciso.

---

## 1. Fundamentos de POO: Herança e Polimorfismo
Antes de entrar no funcional, é essencial entender o comportamento de tipos em Java.
* **Herança:** Uma classe `B` que usa `extends A` herda seus métodos e pode sobrescrevê-los (`Override`).
* **Polimorfismo:** Podemos declarar uma variável do tipo "Pai" e instanciá-la como "Filho" (ex: `A a1 = new B();`). O Java decidirá em **tempo de execução** qual método chamar, priorizando a implementação do "Filho".
* **Segurança de Tipo:** O oposto (`B b1 = new A();`) não é permitido sem *casting* explícito, pois nem todo `A` é obrigatoriamente um `B`.

## 2. Tipos Genéricos (Generics)
O uso de `<T>` permite criar classes ou métodos que operam sobre qualquer tipo de objeto de forma segura.
* Ao instanciar `class A<T>`, podemos definir `T` no momento da criação: `A<String> a = new A<String>();`.
* Isso evita a necessidade de ficar fazendo conversões de tipos (*casting*) ao resgatar valores da estrutura.

---

## 3. Interfaces Funcionais e Expressões Lambda
A porta de entrada para o paradigma funcional em Java são as **Interfaces Funcionais**.
* **Definição:** É qualquer interface que possua **apenas um método abstrato**. Por exemplo: `interface I { int f(int x); }`.
* **Lambdas (`->`):** Em vez de criar uma classe inteira (`class A implements I`) só para implementar essa interface, podemos usar uma função anônima.
  * *Exemplo:* `I i1 = x -> (x * 3);` (Uma função que recebe `x` e retorna `x * 3`).
* **Higher-Order Functions:** Como os lambdas são tratados como instâncias da interface, podemos passar funções como parâmetros para outros métodos ou armazená-las em arrays `I v2[] = {x -> (x + 1), x -> (x - 1)};`.

---

## 4. Imperativo vs. Declarativo (Stream API)
A **Stream API** permite processar coleções de dados de forma funcional (declarativa), dizendo "O QUE" fazer, e não "COMO" fazer.

### Abordagem Imperativa (Clássica)
Usa blocos `for`, controle manual de iterações (`cnt += 1`), `if` aninhados e `break` para parar a execução. É mais verboso e focado no passo a passo.

### Abordagem Declarativa (Funcional / Streams)
As coleções são transformadas em um fluxo de dados (`stream()`), onde podemos encadear operações:
* **`filter(Predicate)`:** Deixa passar apenas os elementos que satisfazem uma condição (`p -> p.getQuantidade() > 5`).
* **`limit(n)`:** Pega apenas os primeiros `n` elementos, imitando o comportamento de um `break` no loop clássico.
* **`map(Function)`:** Transforma o dado (ex: extrai apenas o nome do Produto).
  * `mapToInt(Fuction)`: Transforma para uma stream de `Int`.
* **`forEach(Consumer)`:** Executa uma ação final em cada elemento restante, como imprimir na tela.
* **`peek(Consumer)`**: Usado para debugar streams (retorna `Stream`).
* **`findFirst(Consumer)`**: Pede 1 objeto da `Stream` (equivalente a `limit(1)`, porém é consumer).
  * Exige o tipo `Optional` (análogo do `Maybe`), na chance de não retornar nada.
  * Impressão exige `objeto.ifPresent`.

* **`orElse(Consumer)`**: retorna um valor se outro não estiver presente, em um tipo `Optional`.

❗O uso de variáveis locais em streams exige variáveis `final`.
# O que são as listas em Dart? 
Em Dart, as listas (`arrays` ou vetores) representa um conjunto de valores que podem ser acessados a partir de um índice. 

Isso significa que você pode ler, alterar ou remover os objetos da lista com facilidade, por meio de métodos específicos. 

Diferente de outras linguagens que podem chamar as listas de `array`, um dado do tipo Lista em Dart é chamado de `list`.

# Entendendo as Coleções de objetos em Dart
As listas são uma sub-classe de uma classe abstrata chamada `Iterable`. A classe Iterable represeta qualquer tipo de coleção de objetos em Dart. 

Enquanto uma classe abstrata, `Iterable` não pode instanciar nenhum objeto. Isso sigifnica que você não consegue criar uma nova coleção declarando-a apenas como uma `Iterable`. 

Porém, é certo que você pode explorar os atributos e métodos de `Iterable` em qualquer coleção de objetos. 

**Mas onde o tipo `list` entra nessa história?**

O tipo `list`, enquanto uma sub-classe de `Iterable`, é um dos tipos de coleções possíveis. As coleções comumente são de 3 tipos: 

- `List` → coleção de objetos usada para ler elementos a partir de um index. Esse tipo de coleção também permite adicionar, alterar, substituir e até remover itens por meio do uso do `index`;
- `Set` → coleção de objetos usada para conter elementos que ocorrem apenas uma vez dentro da lista. Ou seja, caso um elemento idêntico a outro já existente for inserido no Set, ainda assim a coleção só vai mostrar 1 desses elementos. É ótimo para usos em que você precisa ter certeza de que não haverão informações duplicadas;
- `Map` → coleção de objetos usada para ler e identificar elementos a partir de uma `Key`. Os Maps possuem uma `Key` que referenciam um valor associado. Um Map pode ser entendido como um dicionário, já que a busca por objetos dentro da coleção perpassa apenas pelo uso da `Key` que referencia o objeto.

Importante lembrar que todos esses tipos de coleções são sub-classes (ou filhas) de `Iterable`, e por isso contam com métodos e atributos em comum. Porém, cada uma também possui métodos e atributos específicos, e por isso são usadas em contextos diferentes. 

**Para saber mais sobre os métodos e atributos de `Iterable`, visite:**
- [Documentação oficial da classe](https://api.flutter.dev/flutter/dart-core/Iterable-class.html) - Lista todos os métodos e atributos de `Iterable` que você pode usar nos tipos `list` e `Set`
- [Guia oficial sobre Iterable Collections](https://dart.dev/codelabs/iterables) - Codelab com conteúdo teórico resumido e exercícios que ajudam a entender as coleções a fundo 


# Métodos de leitura e manipulação de Coleções
Os métodos citados aqui são métodos de `Iterable`, e por isso podem ser usadas em qualquer tipo de coleção de dados em Dart, incluindo `List` e `Set`.

Entre os métodos de `Iterable` temos alguns muito importantes e usados de forma recorrente em coleções do tipo `List` e `Set`, incluindo os métodos `reduce()` e `forEach()`.

Vale lembrar que `List` e `Set`, enquanto classes-filhas, possuem muitos outros métodos próprios. 

## Principais métodos de leitura e manipulação de Coleções
### Ler o primeiro e último objeto de uma coleção
- *first*: Lê o primeiro objeto da coleção
- *last*: Lê o último elemento da coleção
~~~dart
void main() {
  List<String> exemplo = ['primeiro item', 'segundo item', 'terceiro item'];
  print('O primeiro elemento é ${exemplo.first}');
  print('O último elemento é ${exemplo.last}');

}
~~~

A saída seria:
```
primeiro item
terceiro item
```

### Ler o primeiro objeto que satisfaz uma condição

- *firstWhere()*: mostra o primeiro elemento da coleção que satisfaz a condição. Assim que encontra o primeiro objeto que satisfaz a condição, o método para de rodar. 

Além disso, é preciso ter atenção: esse método exige que exista uma variável para receber o resultado do teste. 

~~~dart
void main() {
  List<String> exemplo = ['primeiro item', 'segundo item', 'terceiro item', 'maior item de todos'];
  var testeTamanho = exemplo.firstWhere((element) => element.length > 15); // teste para verificar o tamanho de cada um dos elementos

}
~~~

A saída seria:
```
maior item de todos
```

Atenção: Caso nenhum dos objetos da Coleção cumpra a condição, o código vai apontar um erro. Para evitar isso, podemos trabalhar com um código que sete um valor default para a variável caso o nenhum elemento passe no teste. Ficaria assim:

~~~dart
void main() {
  List<String> exemplo = ['primeiro item', 'segundo item', 'terceiro item', 'maior item de todos'];
  var testeTamanho = exemplo.firstWhere((element) => element.length > 20, 
  orElse: () => "Nenhum valor encontrado.");

}
~~~
A saída seria:
```
Nenhum valor encontrado.
```

### Filtrando todos os itens que satisfazem uma condição
- `where()` - método mais poderoso de filtro que mostra **todos** os itens da coleção que satisfazem um teste. Nesse caso, o dado retornado é um novo `Iterable` com os itens filtrados.  

~~~dart
void main() {
  List<String> exemplo = ['primeiro item', 'segundo   item', 'terceiro item', 'maior item de todos'];
  var testeTamanho = exemplo.where((element) => element.length > 12);
  print(testeTamanho);

}
~~~
A saída seria:
```
(primeiro item, terceiro item, maior item de todos)
```

### Transformando o tipo de dado de objetos de uma Coleção
Se você precisa transformar o tipo de dado de todos os elementos de uma lista (por exemplo, precisa transformar dados do tipo `int` em `double`), é possível usar o método do tipo `map()`

- `map()` - esse método retorna um novo iterável contendo todos os objetos da coleção transformados em objetos de um novo tipo. Exemplo prático: 

~~~dart 
void main() {
  List<String> exemplo = ['1', '2', '3']; // Lista de números, mas todos elementos são do tipo String
  var listaInt = exemplo.map(int.parse);
  print(listaInt);
~~~

A saída seria: 
```
(1, 2, 3) 
```

Nesse caso, o resultado é um `Iterable` com objetos do tipo `Int`. 

### Invocando um loop com ação sob cada elemento da Coleção
- `forEach()` - o método invoca uma ação em cima de cada um dos objetos da coleção, na ordem em que eles aparecem. 

~~~dart 
void main() {
  List<int> exemplo = [1, 2, 3]; 
  exemplo.forEach(print);
~~~

A saída seria: 
```
1
2
3
```
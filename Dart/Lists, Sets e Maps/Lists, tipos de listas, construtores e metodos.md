# List: imutabilidade, construtores e métodos de edição 
Em Dart, as listas (arrays ou vetores) representa um tipo de coleção de valores que podem ser acessados a partir de um índice.

Uma coleção do tipo `List` é uma sub-classe de uma classe abstrata chamada `Iterable`. 

## Imutabilidade de listas 
É possível implementar diferentes tipos de listas, a depender do uso que é esperado dela. Os tipos mais comuns de lista são:

### Listas do tipo `growable`
Quando criamos uma lista usando o padrão `[]`, estamos criando uma lista do tipo **growable**. Esse tipo de lista não tem o seu comprimento definido e fixo, e, na prática, podem receber mais elementos e modificações a qualquer momento. 

Para implementar uma lista do tipo growable, basta:

~~~dart
List<int> exemplo = [1, 2]; 
~~~

### Listas do tipo `fixed`
Esse tipo de lista possui um tamanho fixo, e não pode receber mais itens do que o seu tamanho permite. No caso de uma tentativa de adição de novo item, Dart vai apontar um erro. 

Atenção: Isso não significa que as listas do tipo **fixed** não podem ter os seus elementos alterados quando necessários. A lista fixed não é imutável, ela apenas não pode receber mais itens para além do seu tamanho definido durante a sua criação. 

Para implementar uma lista do tipo growable, basta:

~~~dart
final exemplo = List<int>.filled(3 , 0);  
~~~

Caso déssemos print na lista exemplo, a saída seria:
```
[0, 0, 0]
```

### Mas como ter uma lista imutável? 
Já que uma lista do tipo `fixed` não garante que a lista será imutável, como fazer para ter uma lista em que o seu conteúdo é impossível de ser modificado? 

No caso hipotético em que você precisa criar uma lista que não pode ter o seu conteúdo modificado depois, existem 2 maneiras: **criando a lista setando-a como `const`** ou **usando o construtor `List.unmodifiable`**. Dessa maneira: 

~~~dart
const List<int> exemplo = [1, 2, 3];
~~~

Nesse caso, os elementos da lista não poderão sofrer nenhuma alteração. Uma tentativa de alteração por meio de métodos (como o `.add()`, por exemplo) vai gerar um erro em tempo de execução. 

## Uso de construtores para criar listas 
### `List.empty`
- Por padrão, cria uma lista do tipo `fixed` vazia. Para criar uma lista vazia do tipo `growable`, é necessário:
~~~dart
final list = List.empty(growable: true);
~~~

### `List.filled`
- Cria uma lista do tipo `fixed`. Você pode setar o tamanho da lista, e, caso queira, pode setar um valor que vai ser repetido por todo tamanho da lista. 

Exemplo:
~~~dart
final list = List.filled(3, 2);
print(list);
~~~

Saída:
```
[2, 2, 2]
```

### `list.from`
- Permite que a lista atual recebe os elementos de uma outra lista. 

Exemplo:
~~~dart
final list = List.filled(3, 2);
final newList = List<int>.from(list);
~~~

## Métodos de edição de listas 
O tipo `List` conta com vários métodos que permitem ler, criar novos elementos, atualizar elementos e deletar elementos. 

Segue:

### Para atualizar ou criar elementos 
- `List.add()` - adiciona um novo elemento ao final da lista. Em listas do tipo **growable**, o tamanho da lista é acrescido em 1. Outro método parecido é o `list.addAll()`;
- `List.insert()` - adiciona um elemento em uma posição específica do índice. Outros métodos parecidos são o `List.insertAll()`;

Exemplo:
~~~dart
List<int> exemplo = [1, 2, 3];
exemplo.insert(0, 9);
print(exemplo);
~~~

Saída
```
[9, 1, 2, 3]
```

- `list[index] = newElement`: substitui um elemento da lista de índice X pelo novo elemento. 

Exemplo: 

~~~dart
List<int> exemplo = [1, 2, 3];
exemplo[0] = 9;
print(exemplo);
~~~

Saída
```
[9, 2, 3]
```

Nesse caso, o elemento de índice 0 é o número 1. Ele foi substituído pelo número 9 após o uso do método. 


### Para deletar elementos 
- `list.remove()` - remove a primeira ocorrência de um valor; 

Exemplo: 
~~~dart
List<int> exemplo = [1, 2, 3];
exemplo.remove(2);
print(exemplo);
~~~
Saída
```
[1, 3]
```
Nesse caso, o elemento `2` foi removido da lista. 

- `list.removeAt()` - remove o elemento que pertence ao índice passado como argumento do método; 

Exemplo: 
~~~dart
List<int> exemplo = [1, 2, 3];
exemplo.removeAt(2);
print(exemplo);
~~~
Saída
```
[1, 2]
```
Nesse caso, o elemento **de índice 2** foi removido da lista. 

- `list.removeLast()` - remove o último elemento da lista;

- `list.removeRange()` - remove um pedaço da lista pertencente ao range passado como argumento do método. **Atenção**: os elementos são removidos a partir do primeiro índice passado, até o segundo índice -1. 

Exemplo:
~~~dart
List<int> exemplo = [1, 2, 3, 4, 5];
exemplo.removeRange(0, 3);
print(exemplo);
~~~
Saída
```
[4, 5]
```
Nesse caso, foram removidos os 2 primeiros elementos da lista. Se atentando que: o elemento `1` faz parte do índice 0, o elemento `2` faz parte do índice 1. 

Assim, o método removeu todos os elementos que estão entre o índice 0 e o índice 2. 

- `list.clear` - remove todos os objetos da lista e a transforma em uma lista vazia, com um tamanho de 0. Porém, se a lista for do tipo **growable**, ela continua sendo deste tipo, podendo receber novos elementos. 

## Outros métodos úteis 
- `list.contains()` - verifica se a lista possui um elemento passado como argumento do método. O método retorna um valor **booleano**; 

- `list.sort()` - ordena os elementos da lista em ordem crescente;

Exemplo

~~~dart
List<int> exemplo = [3, 2, 1, 4, 5];
exemplo.removeRange(0, 3);
print(exemplo);
~~~
Saída
```
[1, 2, 3, 4, 5]
```

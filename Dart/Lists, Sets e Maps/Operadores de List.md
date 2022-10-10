# Lists: tipos de operadores, condicionais e Null ckeck
Só há 2 tipos de operadores possíveis de se usar entre Listas. Eles são os de adição (`+`) e igualdade (`==`).

## Adição (+)
Usar o sinal de adição na operação entre 2 listas significa que você está adicionando à uma lista todos os elementos da segunda lista. **Atenção**: a ordem em que as listas são somadas importa para o resultado final. 

~~~dart
List<int> exemple = [1, 2, 3];
  
List<int> exemple2 = [4, 5, 6];
  
var newList = exemple2 + exemple;
  
print(newList);
~~~

Saída
```
[4, 5, 6, 1, 2, 3]
```

## Igualdade (==)
O sinal de igualdade serve para comparar 2 listas e entrega um valor booleano. 

Porém, comparar 2 listas com o sinal de igualdade em Dart **não** compara os elementos das listas. No caso das listas, a igualdade compara o lugar de memória em que a variável do tipo Lista está armazenada. 

Para tornar mais claro, vamos ver 2 exemplos: 

**Exemplo 1**
~~~dart
List<int> exemple = [1, 2, 3];
  
List<int> exemple2 = [1, 2, 3];
  
var result = exemple2 == exemple;
  
print(result);
~~~

Saída
```
false
```

**Exemplo 2**
~~~dart
List<int> exemple = [1, 2, 3];
  
List<int> exemple2 = exemple;
  
var result = exemple2 == exemple;
  
print(result);
~~~

Saída
```
true
```

Nesse caso, o `exemple2` recebe todos os valores de `exemple` E passa a refenciar `exemple`, de forma que ambas listas estão ocupando o mesmo lugar de memória. Por isso, quando comparamos as 2 listas com ==, o resultado é true. 


## Condicionais em listas 
É possível criar condicionais dentro de Listas que alteram os elementos a depender da lógica utilizada. 

Exemplo simples
~~~dart
final logica = false;
final list1 = [1, 2, 3, if(logica) 4];
final list2 = [1, 2, 3, if(logica) 4 else 5];

print(list1);
print(list2);
~~~

Saída
```
[1, 2, 3]
[1, 2, 3, 5]
```

Nos 2 casos (list1 e list2), Dart entende que o elemento 4 só será adicionado se a lógica dentro do `if` for verdadeira. Como a lógica é falsa, o elemento não é adicionado. 


## Null check (??)
O Null check usado dentro de listas adiciona um valor padrão caso o elemento receber nulo. 

Exemplo: 
~~~dart
int? forthMember;
int fifthMember = 7;
final list = [1, 2, 3, forthMember ?? 4, fifthMember ?? 7];
print(list);
~~~

Saída
```
[1, 2, 3, 4, 7]
```

Nesse caso, como `forthMember` é nulo, o Null Check permitiu que fosse adicionado o elemento 4 na lista. Agora, como `fifthMember` não é nulo, a lista recebeu o elemento contido na variável normalmente. 


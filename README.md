# Anotações do básico

# Notação BIG O
- A notação big O é uma notação que diz quão rápido é um algoritimo

## Pesquisa Simples
- A pesquisa simples tem um grande tempo de execução devido a sua necessidade de contar 1 elemento de cada vez
- Exemplo: Para medir o tempo de execução de 100 elementos com a pesquisa simples, ela irá verificar cada elemento um de cada vez demorando 100 ms(millisegundos), se for necessário verificar 1 milhão de elementos, ela irá demorar 1 milhão de segundos !!!

## Pesquisa binária
- A pesquisa binária tem um menor tempo de execução, pois ela conta metade dos elementos por etapa.
- Exemplo: Para medir o tempo de execução de 100 elementos com a pesquisa binária, ela irá contar metade dos elementos por vez: 100 -> 50,25,13,7,4,2,1 são necessários apenas 7 etapas para verificar, ou seja 7ms
- É arrendondado para um número acima pois os resultados são aproximados.

# Alocação de memória
- A alocação e memória são espaços(slots) da memória do computador onde você guarda elementos e em cada espaço(slot) você pode guardar 1(um) elemento.
- fe0ffeeb é um endereço de um slot na memória, cada vez que você armazenar um elemento na memória, o mesmo terá um endereço
- A contagem de slots de memória sempre começa em 00. Assim segue a sequência -> 00,01,02,03,04,05.. etc

## Arrays
- Um array armazena elementos nos slots da memória do computador em sequência, porém é necessário reservar slots antes, pois não é possível reservar mais slots caso o slot seguinte esteja "ocupado"
- Exemplo: Digamos que você queira armazenar 10 elementos na memória e utiliza um ARRAY, neste caso você reserva 10 slots, porém o slot seguinte está ocupado, e se você depois quiser adicionar mais 5 ? não será possível pois os elementos precisam estar armazenados em slots de memória em sequência. Neste caso, se tivessem sido reservados 20 slots de memória teriam os slots para mais 5 elementos e ainda sobrariam 5. O ideal é sempre reservar mais slots de memória do que irá utilizar no momento para que em casos futuros não ocorra nenhum problema de falta de slots de memória em sequência.
- Arrays são o ideia para realizar buscas aleatórias, pois possibilita buscar o elemento que deseja em qualquer slots, devido ao fato dos slots estarem em sequência basta contar os slots para que encontre o slot desejado.
- Todos os elementos de um ARRAY, precisam ser do mesmo tipo.
- Arrays permitem buscas rápidas.

## Lista encadeadas
- Listas encadeadas podem armazenar elementos em diferentes slots de memória, independente de estar em sequência ou não.
- Digamos que você tenha elementos armazenados em 10 slots de memória em forma de uma lista encadeada, cada slot terá o endereço do slot seguinte, assim é possível realizar o armazenamento de elementos em diferentes slots de memória, porém caso você queira realizar uma busca aleatória não será tão rápido quanto um ARRAY.
- Exemplo: Victor quer pegar o elemento que está no slot 9, neste caso, apenas o slot 8 tem o endereço do slot 9 e ele irá precisar percorrer todo o caminho seguindo slot por slot até chegar no slot 8 que tem o endereço do slot 9, assim possibilitando que ele pegue o elemento desejado. O mesmo aconteceria caso ele quisesse pegar o elemento que está armazenado no ultimo slot(10), pois apenas o slot anterior tem o endereço do slot seguinte. É assim que a lista encadeada funciona.
- Listas encadeadas são o ideal para buscas em sequência e permitem rápidas inserções e eliminações.


# Recursão
- A recursão é quando uma função chama a si mesma, ela é usada para tornar uma resposta mais clara, ela serve para que não haja a necessidade de utilizar um loop.
- Não há beneficio de desempenho ao utilizar a recursão, em alguns casos os loopings são melhores para o desempenho de um programa.
- Frase de Leigh Caldwell: "Os loops podem melhorar o desempenho do programa. A recursão melhora o desempenho do seu programador, escolha o que for mais importante para a situação.

## Caso base e Caso recursivo

- Looping infinito
```
def regressiva(i):
    print(i)
    regressiva(i - 1) //devido ao fato de nao ter uma condição irá executar "infinitamente" - será interrompido ao dar erro de estouro de pilha(stack overflow).

regressiva(10)
```
- Função recursiva
```
def regressiva(i):
    print (i)
    if i <= 1: //Ao adicionar uma condição fará com que o problema do looping infinito seja resolvido, assim se torna uma função recursiva.
        return
    else:
        regressiva(i - 1)

regressiva(10) 
```
- Quando escrever uma função recursiva, precisa informar quando a recursão deve parar.
- Toda função recursiva tem duas partes -> Caso-base e Caso-recursivo
- Caso-recursivo -> é quando a função chama a si mesma
- Caso-base -> é quando a função não chama a si mesma novamente, assim evitando se tornar um looping infinito

# Pilha de chamada(Call Stack)
- Está é um estrutura de dados que chama as funções que você definiu em um código de acordo com o modo que seu código foi estruturado.
- Possui duas ações PUSH(inserir) e POP(remover e ler)

- Abaixo podemos ver exemplos de como a pilha de chamada é utilizada.

- Ao chamar a função base, ou seja, a primeira função do código sauda(nome) em sauda("victor"), o computador aloca um slot de memória para esta chamada e armazena que a variável *nome* está definida como "Victor". Cada vez que o seu código chamar uma nova função após a primeira, o computador salva todos os valores das variáveis e é criado um novo slot de memória para armazenar a próxima função, este slot que vamos de slot 2 ele é inserido(PUSH) acima do slot 1 que é a base da pilha de chamada, após a segunda função ser chamada, a mesma é lida e removida(POP), após isto o slot de memória da função que foi inserida(PUSH), lida e executada(POP) é removido e o mesmo processo é feito para cada nova função chamada, ou seja, o slot de memória da primeira função que é a base, sempre irá se manter pausada e parcialmente completa e o slot 2 que armazena as próximas funções é sempre inserido,lido e removido, até que não restem mais funções.

### Esta é a pilha de chamada, ao imaginar que temos a função base e acima dela é sempre inserida, lida e removida uma nova função, conseguimos entender como funciona.

```
def sauda2(nome): #necessário definir as funções sauda2 e tchau para que a função sauda chame as mesmas ao ser executada.
    print("Como vai " + nome + "?") 

def tchau():
    print("ok, tchau!")

def sauda(nome): # Ao chamar a função "sauda" definindo a varial nome como "Victor" é criado o slot de memória base "sauda(Victor)" 
    print ("Olá, " + nome + "!") # A mensagem é retornada
    sauda2(nome) # Agora inserimos a função *sauda2* em um novo slot de memória acima de *sauda*, o mesmo é lido(executado) e removido. 
    print ("Preparando para dizer tchau...") # é retornada a mensagem com "print"
    tchau() # E o mesmo processo feito com "sauda2" é realizado com a está nova função

sauda("Victor")  # está parte é necessário pois é preciso chamar a função sauda(nome) para que o código rode
```

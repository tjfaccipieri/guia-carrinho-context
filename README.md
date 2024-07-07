# Guia do Carrinho de Compras pela ContextAPI

## Ajuste da model de Produto
Para trabalharmos com o nosso carrinho, pensando que o usuário pode querer comprar mais de uma quantia do mesmo produto, precisaremos ajustar a nossa model de produto no front, para simular a quantidade comprada, fazendo o seguinte ajuste:<br />
![enter image description here](https://i.ibb.co/G7RtdMh/model-produto.png)
>O atributo `qtd` não existe no backend, será um valor de controle do front, e ele é opcional, pois irá existir apenas no momento em que o item estiver no carrinho.

## Configurações iniciais da context

### Criando o CarrinhoContext.tsx
Embora pudéssemos reaproveitar a nossa AuthContext para aplicar também as funcionalidades do carrinho, iremos criar um novo contexto, de uso único, para o carrinho. 
> isso evita uma bagunça gigante de código, e trabalha com o principio de responsabilidade única de um componente, que é uma boa pratica para programação no geral.

### Passo 1 - Criar o arquivo
Dentro da pasta `contexts` que já temos no projeto, iremos criar um novo arquivo, que eu irei chamar de `CarrinhoContext.tsx`. (O nome pode ser qualquer um, não tem obrigatoriedade de ser esse mesmo nome) <br />
![jkhjk](https://i.ibb.co/bP2s4Bp/1.png)

<hr />

### Passo 2 - Estrutura básica da context
Iremos agora, criar a estrutura básica do arquivo da Context, conforme o print abaixo:
![Context Básica](https://i.ibb.co/fx0tVB1/2.png)

<hr />

### Passo 3 - Criar as funcionalidades do Carrinho na Context
Iremos agora, criar as funcionalidades do carrinho, uma por uma.

 1. **listaCarrinho -> Estado global para o carrinho, que será um Array iniciando vazio**
 ![enter image description here](https://i.ibb.co/VvZPtBN/3.png)
>Para criar a nossa listaCarrinho, iremos criar, dentro do `CarrinhoProvider`, um useState, que será um array de produtos (linha 20 no exemplo acima), depois iremos declarar a tipagem dele na nossa interface `CarrinhoContextProps` (linha 7), e fornecer ele como um valor que os componentes do projeto poderão acessar, dentro do return da linha 23.
<hr />

 2. **Adicionar items no carrinho**
A função abaixo, tem 2 aplicações, sendo elas, adicionar um item novo no carrinho, e aumentar em +1 a quantidade de um item, caso ele já esteja no carrinho, conforme os comentários estão explicando:
![AdicionarItem](https://i.ibb.co/RHFLgP7/4.png)
Depois de criarmos a função, iremos declarar a mesma na nossa interface:
![enter image description here](https://i.ibb.co/n0q6R2b/5.png)
<br />E iremos também passa-la dentro do `value={{}}` do nosso retorno:
![enter image description here](https://i.ibb.co/3WBt3sS/6.png)
<hr />

 3. **Diminuir a quantidade de um item**
Iremos agora, criar uma nova função, para poder diminuir a quantidade de um item no carrinho, e caso a quantidade chegue a zero, o item automaticamente é removido do nosso carrinho, da seguinte forma:
![enter image description here](https://i.ibb.co/Wz3WmtG/7.png)
Iremos também, declarar a função na nossa interface, do seguinte modo:
![enter image description here](https://i.ibb.co/m4TPD8v/8.png)
**Também precisamos colocar a função dentro do campo `value` do retorno, do mesmo modo que fizemos na função anterior.**
<hr />

 4. **Remover totalmente um item**
Para a função responsável por remover diretamente um item do nosso carrinho, iremos reaproveitar uma parte da função criada anteriormente, que removia o item caso a quantidade chegasse a zero, da seguinte forma:
![enter image description here](https://i.ibb.co/n6PQRZt/9.png)
E iremos novamente declarar a função na nossa interface, de modo muito similar as anteriores:
![enter image description here](https://i.ibb.co/J5QN3yd/10.png)
<br />
**Também precisamos colocar a função dentro do campo `value` do retorno, do mesmo modo que fizemos nas funções anteriores.**

<hr />

 5. **Fechar a compra**
Por ultimo, iremos fazer a função de "finalizar" a nossa compra, que nada mais é do que uma função que irá retornar o nosso Array de listaCarrinho para o seu estado inicial, de um Array vazio, conforme o print abaixo:<br />
![enter image description here](https://i.ibb.co/SnHNb7B/11.png)
E como sempre, iremos declarar essa função dentro da nossa interface:<br />
![enter image description here](https://i.ibb.co/tLYPfsZ/12.png)
<br />
E por fim, declarar a função no `value` do nosso retorno.

### Finalizamos a context do carrinho 🎉🎉

<hr />

## Ajustando o App.tsx
Por fim, precisamos liberar o contexto do carrinho para o nosso projeto, do mesmo jeito que foi feito com o contexto de autenticação, dentro no nosso App.tsx, conforme a imagem abaixo:
![enter image description here](https://i.ibb.co/M6FBtRG/13.png)
>Vale falar que a ordem entre `AuthProvider` e `CarrinhoProvider` pode ser qualquer uma, o que realmente importa, é que os providers fiquem por volta de todos os outros componentes do projeto, que precisarão ter acesso aos mesmos.

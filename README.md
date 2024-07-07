# Guia do Carrinho de Compras pela ContextAPI

## Ajuste da model de Produto
Para trabalharmos com o nosso carrinho, pensando que o usuário pode querer comprar mais de uma quantia do mesmo produto, precisaremos ajustar a nossa model de produto no front, para simular a quantidade comprada, fazendo o seguinte ajuste:
![enter image description here](https://i.ibb.co/G7RtdMh/model-produto.png)
>O atributo `qtd` não existe no backend, será um valor de controle do front, e ele é opcional, pois irá existir apenas no momento em que o item estiver no carrinho.

## Configurações iniciais da context

### Criando o CarrinhoContext.tsx
Embora pudéssemos reaproveitar a nossa AuthContext para aplicar também as funcionalidades do carrinho, iremos criar um novo contexto, de uso único, para o carrinho. 
> isso evita uma bagunça gigante de código, e trabalha com o principio de responsabilidade única de um componente, que é uma boa pratica para programação no geral.

### Passo 1 - Criar o arquivo
Dentro da pasta `contexts` que já temos no projeto, iremos criar um novo arquivo, que eu irei chamar de `CarrinhoContext.tsx`. (O nome pode ser qualquer um, não tem obrigatoriedade de ser esse mesmo nome) 
![jkhjk](https://i.ibb.co/bP2s4Bp/1.png)

### Passo 2 - Estrutura básica da context
Iremos agora, criar a estrutura básica do arquivo da Context, conforme o print abaixo:
![Context Básica](https://i.ibb.co/fx0tVB1/2.png)

### Passo 3 - Criar as funcionalidades do Carrinho na Context
Iremos agora, criar as funcionalidades do carrinho, uma por uma.

* **listaCarrinho -> Estado global para o carrinho, que será um Array iniciando vazio**
	* ![enter image description here](https://i.ibb.co/VvZPtBN/3.png)
>Para criar a nossa listaCarrinho, iremos criar, dentro do `CarrinhoProvider`, um useState, que será um array de produtos (linha 20 no exemplo acima), depois iremos declarar a tipagem dele na nossa interface `CarrinhoContextProps` (linha 7), e fornecer ele como um valor que os componentes do projeto poderão acessar, dentro do return da linha 23.

* **Adicionar items no carrinho**
A função abaixo, tem 2 aplicações, sendo elas, adicionar um item novo no carrinho, e aumentar em +1 a quantidade de um item, caso ele já esteja no carrinho, conforme os comentários estão explicando:
![AdicionarItem](https://i.ibb.co/RHFLgP7/4.png)

# API do velh.io

## Sobre o projeto

Hackenge (Hackathon + Challenge) proposta pela cadeira IF977 - Engenharia de Software, cujo objetivo é implementar um projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.

## Projeto da API

### Ver tabuleiros abertos:

Rota: ```GET /board```

Retorno:
~~~javascript
[
  {
    id: 1
    owner: "Pedro"
  },
  {
    id: 2
    owner: "Marcela"
  }
]
~~~

Comentários:

> A ideia dessa rota é informar ao jogador os tabuleiros abertos, portanto precisamos retornar um array de objetos contendo ao menos o id e o nome do dono do tabuleiro. Tomamos a decisão de mostrar apenas os tabuleiros abertos, já que um usuário só pode se conectar a um deles. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

### Criar tabuleiro:

Rota: ```POST /board```

Corpo:
~~~javascript
{
  user: "sonson"
}
~~~

Retorno:
~~~javascript
{
  id: 3,
  mark: "O"
}
~~~

Exceções:
- Quando um usuário tenta criar um tabuleiro sem passar todas informações necessárias

Comentários:

> A ideia dessa rota é permitir ao jogador criar um novo tabuleiros, portanto precisamos retornar apenas o id do tabuleiro que foi criado e o símbolo que o dono da sala irá jogar. O usuário precisa passar seu nome no corpo da requisição, para que ele possa ser mostrado na lista de tabuleiros. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor.

### Entrar em um tabuleiro:

Rota: ```POST board/{id}```

Corpo:
~~~javascript
{
  user: "sonson"
}
~~~

Retorno:
~~~javascript
{
  mark: "X",
  opponent: "Carlos",
  turn: "sonson"
}
~~~

Exceções:
- Quando um usuário tenta entrar em um tabuleiro que já está cheio
- Quando um usuário tenta entrar em um tabuleiro que não existe
- Quando um usuário tenta entrar em um tabuleiro sem passar todas informações necessárias

Comentários:

> A ideia dessa rota é permitir ao jogador entrar em um tabuleiro que esteja aberto, portanto precisamos retornar o símbolo que o usuário irá jogar, o nome do oponente e quem começará jogando. O usuário precisa passar seu nome no corpo da requisição, para que o outro jogador seja capaz de vê-lo. Pensamos em retornar o estado atual do tabuleiro (incluindo quem venceu), mas essas informações são redundantes. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor.

### Ler estado do tabuleiro:

Rota: ```GET board/{id}```

Retorno:
~~~javascript
{
  board: [["_", "_", "_"], ["X", "_", "_"], ["O", "X", "_"]],
  winner: null,
  opponent: "Carlos",
  turn: "sonson"
}
~~~

Exceções:
- Quando um usuário tenta ler o estado de um tabuleiro que ele não entrou
- Quando um usuário tenta ler o estado de um tabuleiro que não existe

Comentários:

> A ideia dessa rota é informar ao jogador o estado atual que o tabuleiro se encontra, portanto precisamos retornar a matriz do tabuleiro, se algum dos jogadores venceu, o nome do oponente e de quem é o turno. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

### Atualizar tabuleiro (fazer jogada):

Rota: ```PUT board/{id}```

Corpo:
~~~javascript
{
  x: 1,
  y: 0,
  mark: "X",
  user: "sonson"
}
~~~

Retorno:
~~~javascript
{
  board: [["_", "X", "_"], ["X", "_", "_"], ["O", "X", "_"]],
  winner: null,
  opponent: "Carlos",
  turn: "Carlos"
}
~~~

Exceções:
- Quando um usuário tenta fazer uma jogada mas não é seu turno
- Quando um usuário tenta fazer uma jogada em uma posição que já está ocupada
- Quando um usuário tenta fazer uma jogada num tabuleiro que não existe
- Quando um usuário tenta fazer uma jogada sem passar todas informações necessárias

Comentários:

> A ideia dessa rota é permitir ao usuário fazer uma jogada, portanto precisamos retornar o estado completo do tabuleiro com a nova jogada. O usuário precisa passar seu nome, seu símbolo e a posição da sua jogada no corpo da requisição. Escolhemos o verbo PUT pois essa rota busca atualizar um recurso do servidor.

### Finalizar (apagar) um tabuleiro:

Rota: ```DELETE board/{id}```

Corpo:
~~~javascript
{
  user: "sonson"
}
~~~

Exceções:
- Quando um usuário tenta apagar um tabuleiro que ele não é o dono
- Quando um usuário tenta apagar um tabuleiro que não existe
- Quando um usuário tenta apagar um tabuleiro sem passar todas informações necessárias

Comentários:

> A ideia dessa rota é permitir ao usuário encerre um tabuleiro. O usuário precisa passar apenas seu nome no corpo da requisição. Escolhemos o verbo DELETE pois essa rota busca apagar um recurso do servidor.

## Equipe
- Alexandre Burle (aqb)
- Danilo Vaz (dvma)
- Matheus Vinícius (mvtna)
- Uanderson Ricardo (urfs)

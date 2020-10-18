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
  board: [["_", "_", "_"], ["X", "_", "_"], ["O", "X", "_"]],
  winner: null,
  mark: "X",
  opponent: "Carlos",
  turn: "sonson"
}
~~~

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

### Finalizar (apagar) um tabuleiro:

Rota: ```DELETE board/{id}```

Corpo:
~~~javascript
{
  user: "sonson"
}
~~~

## Equipe
- Alexandre Burle (aqb)
- Danilo Vaz (dvma)
- Matheus Vinícius (mvtna)
- Uanderson Ricardo (urfs)

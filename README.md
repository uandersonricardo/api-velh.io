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
  id: 3
}
~~~

### Entrar/ver estado do tabuleiro:

Rota: ```GET board/{id}```

Retorno:
~~~javascript
{
  board: [[0, 0, 0], [1, 0, 0], [2, 1, 0]],
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
  user: "sonson"
}
~~~

Retorno:
~~~javascript
{
  board: [[0, 1, 0], [1, 0, 0], [2, 1, 0]],
  winner: null,
  opponent: "Carlos",
  turn: "Carlos"
}
~~~

### Finalizar/apagar tabuleiro:

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

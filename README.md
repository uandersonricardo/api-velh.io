# API do velh.io

## Sobre o projeto

Hackenge (Hackathon + Challenge) proposta pela cadeira IF977 - Engenharia de Software, cujo objetivo é implementar um projeto de uma API RESTful para um Jogo da velha que será implementado em Node+Express.

## Projeto da API

### Autenticação

#### Autenticar no sistema:

Rota: ```POST /auth```

Corpo:
~~~javascript
{
  username: "sonson",
  password: "123456"
}
~~~

Retorno:
~~~javascript
{
  user: {
    id: 1,
    username: "sonson",
    email: "sonson@cin.ufpe.br",
    birthday: "1999-04-24",
    wins: 32,
    ranking: 2
  },
  access_token: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Exceções:
- Quando os dados do corpo são inválidos ou insuficientes

Comentários:

> A ideia dessa rota é permitir a autenticação de usuários, portanto precisamos retornar o token de acesso e os dados do usuário. O jogador precisa passar seu usuário e senha no corpo da requisição. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor (além da segurança de passar os parâmetros pelo corpo da requisição).

#### Encerrar sessão no sistema:

Rota: ```DELETE /auth```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Exceções:
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir o "logout" do usuário. Na prática, ele invalida o token de acesso fornecido pelo usuário. Escolhemos o verbo DELETE pois essa rota busca apagar um recurso do servidor.

### Usuários

#### Cadastrar usuário:

Rota: ```POST /user```

Corpo:
~~~javascript
{
  username: "sonson",
  password: "123456",
  email: "sonson@cin.ufpe.br",
  birthday: "1999-04-24"
}
~~~

Retorno:
~~~javascript
{
  id: 1
}
~~~

Exceções:
- Quando os dados do corpo são insuficientes ou inválidos

Comentários:

> A ideia dessa rota é permitir o cadastro de usuários, portanto precisamos retornar o id do usuário que foi criado. O jogador precisa passar seu usuário, senha, e-mail e data de nascimento no corpo da requisição. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor.

#### Ver amigos:

Rota: ```GET /user```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Retorno:
~~~javascript
[
  {
    user: {
      id: 2,
      username: "Carlos",
      email: "crlf@cin.ufpe.br",
      birthday: "1999-06-01",
      wins: 43,
      ranking: 1
    },
    pending: false
  },
  {
    user: {
      id: 3,
      username: "joao",
      email: "joao@cin.ufpe.br",
      birthday: "1999-01-03",
      wins: 20,
      ranking: 3
    },
    pending: true
  }
]
~~~

Exceções:
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir ao usuário ver sua lista de amigos. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

#### Ver usuário pelo id:

Rota: ```GET /user/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Retorno:
~~~javascript
{
  id: 2,
  username: "Carlos",
  email: "crlf@cin.ufpe.br",
  birthday: "1999-06-11",
  wins: 43,
  ranking: 1
}
~~~

Exceções:
- Quando o id do usuário não existe
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é ver os detalhes de um usuário específico. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

#### Solicitação de amizade:

Rota: ```POST /user/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Exceções:
- Quando o id do usuário não existe
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é enviar uma solicitação de amizade para algum usuário. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo POST pois essa rota busca criar um recurso do servidor.

#### Atualizar usuário:

Rota: ```PUT /user/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Corpo:
~~~javascript
{
  username: "sonson2",
  password: "1234567",
  email: "sonson2@cin.ufpe.br",
  birthday: "1999-04-25"
}
~~~

Exceções:
- Quando o id do usuário não existe
- Quando o token do usuário não tem permissão de alterar o usuário do id informado
- Quando os dados do corpo da requisição são inválidos
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é alterar os dados de algum usuário. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo PUT pois essa rota busca atualizar um recurso do servidor.

#### Apagar usuário:

Rota: ```DELETE /user/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Exceções:
- Quando o id do usuário não existe
- Quando o token do usuário não tem permissão de apagar o usuário do id informado
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é apagar um usuário. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo DELETE pois essa rota busca apagar um recurso do servidor.

### Tabuleiros

#### Ver tabuleiros abertos:

Rota: ```GET /board```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Retorno:
~~~javascript
[
  {
    id: 1
    owner: {
      id: 2,
      username: "Carlos",
      email: "crlf@cin.ufpe.br",
      birthday: "1999-06-01",
      wins: 43,
      ranking: 1
    }
  },
  {
    id: 2
    owner: {
      id: 3,
      username: "joao",
      email: "joao@cin.ufpe.br",
      birthday: "1999-01-03",
      wins: 20,
      ranking: 3
    }
  }
]
~~~

Exceções:
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é informar ao jogador os tabuleiros abertos, portanto precisamos retornar um array de objetos contendo ao menos o id e o nome do dono do tabuleiro. Tomamos a decisão de mostrar apenas os tabuleiros abertos, já que um usuário só pode se conectar a um deles. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

#### Criar tabuleiro:

Rota: ```POST /board```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
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
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir ao jogador criar um novo tabuleiros, portanto precisamos retornar apenas o id do tabuleiro que foi criado e o símbolo que o dono da sala irá jogar. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor.

#### Entrar em um tabuleiro:

Rota: ```POST board/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Retorno:
~~~javascript
{
  mark: "X",
  opponent: {
    id: 2,
    username: "Carlos",
    wins: 43,
    ranking: 1
  },
  turn: "X"
}
~~~

Exceções:
- Quando um usuário tenta entrar em um tabuleiro que já está cheio
- Quando um usuário tenta entrar em um tabuleiro que não existe
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir ao jogador entrar em um tabuleiro que esteja aberto, portanto precisamos retornar o símbolo que o usuário irá jogar, o dados do oponente e quem começará jogando. Pensamos em retornar o estado atual do tabuleiro (incluindo quem venceu), mas essas informações são redundantes. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo POST pois essa rota busca criar um recurso no servidor.

#### Ler estado do tabuleiro:

Rota: ```GET board/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Retorno:
~~~javascript
{
  board: [["_", "_", "_"], ["X", "_", "_"], ["O", "X", "_"]],
  winner: null,
  opponent: {
    id: 2,
    username: "Carlos",
    wins: 43,
    ranking: 1
  },
  turn: "X"
}
~~~

Exceções:
- Quando um usuário tenta ler o estado de um tabuleiro que ele não entrou
- Quando um usuário tenta ler o estado de um tabuleiro que não existe
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é informar ao jogador o estado atual que o tabuleiro se encontra, portanto precisamos retornar a matriz do tabuleiro, se algum dos jogadores venceu, os dados do oponente e de quem é o turno. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

#### Atualizar tabuleiro (fazer jogada):

Rota: ```PUT board/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Corpo:
~~~javascript
{
  x: 1,
  y: 0,
  mark: "X"
}
~~~

Retorno:
~~~javascript
{
  board: [["_", "X", "_"], ["X", "_", "_"], ["O", "X", "_"]],
  winner: null,
  opponent: {
    id: 2,
    username: "Carlos",
    wins: 43,
    ranking: 1
  },
  turn: "O"
}
~~~

Exceções:
- Quando um usuário tenta fazer uma jogada mas não é seu turno
- Quando um usuário tenta fazer uma jogada em uma posição que já está ocupada
- Quando um usuário tenta fazer uma jogada num tabuleiro que não existe
- Quando um usuário tenta fazer uma jogada sem passar todas informações necessárias
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir ao usuário fazer uma jogada, portanto precisamos retornar o estado completo do tabuleiro com a nova jogada. O usuário precisa passar seu símbolo e a posição da sua jogada no corpo da requisição. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo PUT pois essa rota busca atualizar um recurso do servidor.

#### Finalizar (apagar) um tabuleiro:

Rota: ```DELETE board/{id}```

Cabeçalhos:
~~~javascript
{
  Authorization: "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ0b3B0YWwuY29tIiwiZXhwIjoxNDI2NDIwODAwLCJodHRwOi8vdG9wdGFsLmNvbS9qd3RfY2xhaW1zL2lzX2FkbWluIjp0cnVlLCJjb21wYW55IjoiVG9wdGFsIiwiYXdlc29tZSI6dHJ1ZX0.yRQYnWzskCZUxPwaQupWkiUzKELZ49eM7oWxAQK_ZXw"
}
~~~

Exceções:
- Quando um usuário tenta apagar um tabuleiro que ele não é o dono
- Quando um usuário tenta apagar um tabuleiro que não existe
- Quando o token de autenticação é inválido ou inexistente

Comentários:

> A ideia dessa rota é permitir ao usuário encerrar um tabuleiro. O token de acesso fornece os dados do usuário logado e garante a segurança da rota. Escolhemos o verbo DELETE pois essa rota busca apagar um recurso do servidor.

### Ranking

#### Ver ranking:

Rota: ```GET /ranking```

Retorno:
~~~javascript
[
  {
    ranking: 1,
    wins: 43,
    id: 3,
    user:  {
      id: 2,
      username: "Carlos",
      email: "crlf@cin.ufpe.br",
      birthday: "1999-06-01"
    }
  },
  {
    ranking: 2,
    wins: 32,
    id: 1,
    user: {
      id: 1,
      username: "sonson",
      email: "sonson@cin.ufpe.br",
      birthday: "1999-04-24"
    }
  }
]
~~~

Comentários:

> A ideia dessa rota é permitir que um usuário veja as maiores pontuações dos outros jogadores. Decidimos manter o acesso a essa rota livre, sem a necessidade do token de acesso. Escolhemos o verbo GET pois essa rota busca ler um recurso do servidor.

## Equipe
- Alexandre Burle (aqb)
- Danilo Vaz (dvma)
- Matheus Vinícius (mvtna)
- Uanderson Ricardo (urfs)

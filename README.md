# Plataforma de Avaliação de Filmes

Modelagem lógica de um banco de dados para uma plataforma de avaliação de filmes. Usuários podem registrar os filmes que assistiram, dar notas, escrever avaliações e comentar nas avaliações de outros usuários.


## Visão geral

O modelo é composto por **6 entidades** principais:

| Entidade | Descrição |
|---|---|
| **Usuários** | Pessoas cadastradas na plataforma, com perfil público e hierarquia (Básico ou Premium). |
| **Filmes** | Catálogo de filmes com título, sinopse, idioma, classificação indicativa, duração e data de lançamento. |
| **Pessoas** | Profissionais do cinema (diretores, roteiristas e atores). |
| **Avaliações** | Nota e texto de um usuário sobre um filme, com a data em que foi assistido. |
| **Comentários** | Respostas e discussões escritas por usuários nas avaliações. |
| **Gêneros** | Categorias dos filmes (ação, drama, comédia etc.). |

## Dicionário de dados

### Usuários

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_usuario` | Numérico | – | Chave primária | Código do usuário |
| `username` | Texto | 20 | Índice único | Username único do usuário |
| `nome_exibicao` | Texto | 20 | – | Nome de exibição no perfil |
| `e-mail` | Texto | 50 | – | E-mail do usuário |
| `biografia` | Texto | 100 | Opcional | Biografia no perfil |
| `data_cadastro` | Data | – | – | Data de criação do perfil |

**Hierarquia de usuários:** `Básico` e `Premium` (especializações da entidade Usuários).

### Filmes

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filmes` | Numérico | – | Chave primária | Código do filme |
| `titulo` | Texto | 50 | – | Título do filme |
| `sinopse` | Texto | 100 | – | Sinopse do filme |
| `idioma` | Texto | 20 | – | Idioma original do filme |
| `classificacao_indicativa` | Texto | 20 | – | L, 10, 12, 14, 16 ou 18 anos |
| `duracao` | Numérico | – | – | Duração em minutos |
| `data_lancamento` | Data | – | – | Data de lançamento |

### Pessoas

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_pessoa` | Numérico | – | Chave primária | Código da pessoa |
| `nome` | Texto | 50 | – | Nome da pessoa |
| `data_nascimento` | Data | – | – | Data de nascimento |
| `biografia` | Texto | 100 | – | Biografia da pessoa |

### Avaliações

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_avaliacao` | Numérico | – | Chave primária | Código da avaliação |
| `nota` | Numérico | – | Entre 1 e 5 | Nota dada ao filme |
| `texto_avaliacao` | Texto | 100 | Opcional | Texto da avaliação |
| `data_assistido` | Data | – | – | Data em que o filme foi assistido |

### Comentários

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_comentario` | Numérico | – | Chave primária | Código do comentário |
| `texto` | Texto | 100 | – | Texto do comentário |
| `data_criacao` | Data | – | – | Data em que o comentário foi postado |

### Gêneros

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_genero` | Numérico | – | Chave primária | Código do gênero |
| `nome` | Texto | 20 | Único | Nome do gênero |

## Relacionamentos e cardinalidades

| Entidade A | Relacionamento | Entidade B | Cardinalidade | Descrição |
|---|---|---|---|---|
| Usuários | Avaliação | Filmes | (0,N) / (0,N) | Um usuário pode avaliar nenhum ou vários filmes; um filme pode ser avaliado por nenhum ou vários usuários. |
| Avaliações | Recebem | Comentários | (1,1) / (0,N) | Um comentário pertence a uma única avaliação; uma avaliação pode ter nenhum ou vários comentários. |
| Usuários | Autoria | Comentários | (1,1) / (0,N) | Um comentário é escrito por um único usuário; um usuário pode escrever nenhum ou vários comentários. |
| Filmes | Categorização | Gêneros | (1,N) / (0,N) | Um filme tem um ou vários gêneros; um gênero pode estar em vários filmes. |
| Filmes | Direção | Pessoas | (0,N) / (0,N) | Um filme pode ter várias pessoas na direção; uma pessoa pode dirigir vários filmes. |
| Filmes | Roteiro | Pessoas | (0,N) / (0,N) | Um filme pode ter vários roteiristas; uma pessoa pode roteirizar vários filmes. |
| Filmes | Elenco | Pessoas | (0,N) / (0,N) | Um filme pode ter vários atores; uma pessoa pode atuar em vários filmes. |

## Regras de negócio

- O `username` de cada usuário deve ser único na plataforma.
- A nota de uma avaliação é um valor de **1 a 5**.
- O texto da avaliação e a biografia do usuário são **opcionais**.
- Todo comentário pertence a **uma única avaliação** e tem **um único autor**.
- Todo filme possui **pelo menos um gênero**.
- Uma mesma pessoa pode ter funções diferentes (direção, roteiro e elenco), inclusive no mesmo filme.
- A classificação indicativa segue os valores: `L`, `10 anos`, `12 anos`, `14 anos`, `16 anos` e `18 anos`.

## Estrutura do repositório

```
.
├── README.md
└── Modelagem_Lógica_BAN_1.xlsx   # Entidades, atributos e relacionamentos
```


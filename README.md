# Plataforma de Avaliação de Filmes

Projeto de banco de dados para uma rede social voltada ao cinema, na qual usuários registram os filmes que assistiram, atribuem notas, escrevem avaliações e comentam nas avaliações de outros usuários.

**Usuários.** Para participar da plataforma, a pessoa se cadastra informando um *username* único, um nome de exibição e um e-mail, podendo preencher opcionalmente uma biografia para o seu perfil. O sistema registra a data de cadastro. Todo usuário é de um dos dois tipos, **Básico** ou **Premium**.

**Filmes.** A plataforma mantém um catálogo de filmes, cada um com título, sinopse, idioma original, classificação indicativa (L, 10, 12, 14, 16 ou 18 anos), duração em minutos e data de lançamento. Cada filme é classificado em um ou mais **gêneros** (por exemplo, drama, comédia ou ficção científica), e um mesmo gênero pode reunir vários filmes.

**Pessoas.** Os profissionais envolvidos nas produções são cadastrados com nome, data de nascimento e biografia. Cada pessoa pode ser associada aos filmes em três funções: **direção**, **roteiro** e **elenco**. Uma mesma pessoa pode exercer funções diferentes, inclusive no mesmo filme, e um filme pode ter várias pessoas em cada função.

**Avaliações.** Ao assistir a um filme, o usuário registra uma avaliação contendo uma nota de 1 a 5, um texto opcional e a data em que o filme foi assistido. A avaliação é o elo entre um usuário e um filme: um usuário pode avaliar vários filmes, e um filme pode ser avaliado por vários usuários.

**Comentários.** As avaliações podem ser comentadas pelos usuários. Cada comentário contém um texto e a data em que foi postado, pertence a uma única avaliação e é escrito por um único usuário. Uma avaliação pode ter vários comentários ou nenhum.

## 1. Esquema conceitual (EER)

<img width="1244" height="778" alt="BanModelo" src="https://github.com/user-attachments/assets/f14e85a3-a1e6-4316-9e04-a1aa24340ccc" />

### Restrições de integridade (RI)

| Nº | Restrição / observação |
|---|---|
| RI1 | O `username` do usuário deve ser único. |
| RI2 | A `nota` da avaliação deve estar entre 1 e 5. |
| RI3 | A `classificacao_indicativa` do filme deve ser um dos valores: L, 10, 12, 14, 16 ou 18 anos. |
| RI4 | `texto_avaliacao` e `biografia` de usuários são opcionais. |
| RI5 | Todo usuário deve ser Básico ou Premium. |
| RI6 |  Enquanto `Básico` for verdadeiro (1), `Premium` deve ser falso (0). | 
| RI7 |  Enquanto `Premium` for verdadeiro (1), `Básico` deve ser falso (0). |

---

## 2. Dicionário de dados

#### Usuários

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_usuario` | Numérico | – | Chave primária | Código do usuário |
| `username` | Texto | 20 | Índice único | Username único do usuário |
| `nome_exibicao` | Texto | 20 | – | Nome de exibição no perfil |
| `e-mail` | Texto | 50 | – | E-mail do usuário |
| `biografia` | Texto | 100 | Opcional | Biografia no perfil |
| `data_cadastro` | Data | – | – | Data de criação do perfil |

#### Básico

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_usuario` | Booleano | – | Chave primária/estrangeira | Usuário do tipo Básico (referencia Usuários) |

#### Premium

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_usuario` | Booleano | – | Chave primária/estrangeira | Usuário do tipo Premium (referencia Usuários) |

#### Filmes

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filmes` | Numérico | – | Chave primária | Código do filme |
| `titulo` | Texto | 50 | – | Título do filme |
| `sinopse` | Texto | 100 | – | Sinopse do filme |
| `idioma` | Texto | 20 | – | Idioma original do filme |
| `classificacao_indicativa` | Texto | 20 | – | L, 10, 12, 14, 16 ou 18 anos |
| `duracao` | Numérico | – | – | Duração em minutos |
| `data_lancamento` | Data | – | – | Data de lançamento |

#### Pessoas

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_pessoa` | Numérico | – | Chave primária | Código da pessoa |
| `nome` | Texto | 50 | – | Nome da pessoa |
| `data_nascimento` | Data | – | – | Data de nascimento |
| `biografia` | Texto | 100 | – | Biografia da pessoa |

#### Gêneros

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_genero` | Numérico | – | Chave primária | Código do gênero |
| `nome` | Texto | 100 | – | Nome do gênero |

#### Avaliações

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_avaliacao` | Numérico | – | Chave primária | Código da avaliação |
| `nota` | Numérico | – | Entre 1 e 5 | Nota da avaliação |
| `texto_avaliacao` | Texto | 100 | Opcional | Texto da avaliação |
| `data_assistido` | Data | – | – | Data em que o filme foi assistido |

#### Comentários

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_comentario` | Numérico | – | Chave primária | Código do comentário |
| `texto` | Texto | 100 | – | Texto do comentário |
| `data_criacao` | Data | – | – | Data em que o comentário foi postado |

#### Relação Direção

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filme` | Numérico | – | Chave primária/estrangeira | Filme dirigido (referencia Filmes) |
| `ID_pessoa` | Numérico | – | Chave primária/estrangeira | Pessoa que dirigiu (referencia Pessoas) |

#### Relação Roteiro

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filme` | Numérico | – | Chave primária/estrangeira | Filme roteirizado (referencia Filmes) |
| `ID_pessoa` | Numérico | – | Chave primária/estrangeira | Pessoa que roteirizou (referencia Pessoas) |

#### Relação Elenco

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filme` | Numérico | – | Chave primária/estrangeira | Filme em que atuou (referencia Filmes) |
| `ID_pessoa` | Numérico | – | Chave primária/estrangeira | Pessoa que atuou (referencia Pessoas) |

#### Relação Categorização

| Atributo | Domínio | Tamanho | Restrição | Descrição |
|---|---|---|---|---|
| `ID_filme` | Numérico | – | Chave primária/estrangeira | Filme (referencia Filmes) |
| `ID_genero` | Numérico | – | Chave primária/estrangeira | Gênero do filme (referencia Gêneros) |

---

## 3. Relacionamentos e cardinalidades

| Entidade A | Relacionamento | Entidade B | Cardinalidade | Descrição |
|---|---|---|---|---|
| Usuários | Avaliação | Filmes | (0,N) / (0,N) | Um usuário pode avaliar nenhum ou vários filmes; um filme pode ser avaliado por nenhum ou vários usuários. |
| Avaliações | Recebem | Comentários | (1,1) / (0,N) | Um comentário pertence a uma única avaliação; uma avaliação pode ter nenhum ou vários comentários. |
| Usuários | Autoria | Comentários | (1,1) / (0,N) | Um comentário é escrito por um único usuário; um usuário pode escrever nenhum ou vários comentários. |
| Filmes | Categorização | Gêneros | (1,N) / (0,N) | Um filme tem um ou vários gêneros; um gênero pode estar em vários filmes. |
| Filmes | Direção | Pessoas | (0,N) / (0,N) | Um filme pode ter várias pessoas na direção; uma pessoa pode dirigir vários filmes. |
| Filmes | Roteiro | Pessoas | (0,N) / (0,N) | Um filme pode ter vários roteiristas; uma pessoa pode roteirizar vários filmes. |
| Filmes | Elenco | Pessoas | (0,N) / (0,N) | Um filme pode ter vários atores; uma pessoa pode atuar em vários filmes. |

---

# Kopa do Mundo
## Descrição do projeto

Este projeto é constituído de uma API desenvolvida com base em testes, como atividade do módulo de Python da Kenzie Academy.

A API consiste na criação e gerenciamento de seleções de futebol, onde é feita a validação do número de títulos, se o ano em que a seleção iniciou é válido e se a quantidade de títulos possuído é possível, de acordo com as datas.
É possível realizar também a leitura de todas as seleções e a atualização, deleção e leitura individual por id.

## Rotas de times

### Registro de time POST /teams/
Padrão de corpo

```json
{
  "name": "Brasil",
  "titles": 5,
  "top_scorer": "Pelé",
  "fifa_code": "BRA",
  "first_cup": "1930-07-13"
}
```

Padrão de resposta (STATUS 201)

```json
{
  "id": 1,
  "name": "Brasil",
  "titles": 5,
  "top_scorer": "Pelé",
  "fifa_code": "BRA",
  "first_cup": "1930-07-13"
}
```

#### Possíveis erros

400 BAD REQUEST - Títulos negativos

```json
{
  "error": "titles cannot be negative"
}
```

400 BAD REQUEST - Ano da primera copa inválido

```json
{
  "error": "there was no world cup this year"
}
```

400 BAD REQUEST - Número de títulos maior do que o possível

```json
{
  "error": "impossible to have more titles than disputed cups"
}
```

### Leitura de times GET /teams/

Padrão de resposta (STATUS: 200)

```json
[
  {
    "id": 1,
    "name": "Brasil",
    "titles": 5,
    "top_scorer": "Pelé",
    "fifa_code": "BRA",
    "first_cup": "1930-07-13"
  }
]
```

URL Search Params

| Parâmetro | Exemplo de uso | Descrição                                                          |
| --------- | -------------- | ------------------------------------------------------------------ |
|  team_id  | /teams/1/      | Forneça o "id" do time para trazer somente o time do id definido   |

#### Possíveis erros:

STATUS (404) - id inválido

```json
{
  "message": "Team not found"
}
```

### Atualizar time PATCH /teams/<int:team_id>/

Padrão de corpo

Os atributos dessa requisição são todos opcionais.

```json
{
  "name": "Brasil",
  "titles": 6,
  "top_scorer": "Pelé",
  "fifa_code": "BRA",
  "first_cup": "1930-07-13"
}
```

Padrão de resposta (STATUS: 200)

```json
{
	"id": 2,
	"name": "Brasil",
	"titles": 6,
	"top_scorer": "Pelé",
	"fifa_code": "BRA",
	"first_cup": "1930-07-13"
}
```

#### Possíveis erros

STATUS (404) - id inválido

```json
{
  "message": "Team not found"
}
```

### Excluir time DELETE /teams/<int:team_id>/

Esta rota não tem um corpo de resposta (STATUS: 204)

#### Possíveis erros

STATUS (404) - id inválido

```json
{
  "message": "Team not found"
}
```

## Preparando ambiente para execução dos testes
### Procedimentos para rodar os testes da tarefa 1
1. Faça a instalação das bibliotecas de teste:
```shell
pip install pytest-testdox pytest-django
```
2. Use o comando abaixo para rodar os testes referentes à tarefa 1:
```shell
pytest --testdox -vvs tests/tarefas/tarefa_1/
```
---
### Procedimentos para rodar os testes a partir da tarefa 2
1. Verifique se os pacotes pytest, pytest-testdox e/ou pytest-django estão instalados globalmente em seu sistema:
```shell
pip list
```
2. Caso eles apareçam na listagem, rode os comandos abaixo para realizar a desinstalação:

```shell
pip uninstall pytest pytest-testdox pytest-django -y
```
3. Após isso, crie seu ambiente virtual:
```shell
python -m venv venv
```

4. Ative seu ambiente virtual:

```shell
# Linux e Mac:
source venv/bin/activate

# Windows (PowerShell):
.\venv\Scripts\activate

# Windows (GitBash):
source venv/Scripts/activate
```


5. Instale as bibliotecas necessárias:

```shell
pip install pytest-testdox pytest-django
```

6. Como, a partir da tarefa 2, você utilizará Django, é necessário criar um arquivo bem importante: **pytest.ini**. Crie-o na raiz do projeto e adicione dentro dele o seguindo texto:
```python
[pytest]
DJANGO_SETTINGS_MODULE = kopa_do_mundo.settings
```

Após isso, você pode executar os comandos abaixo para rodar os testes (inclusive da tarefa 1):
- Tarefa 1

```shell
pytest --testdox -vvs tests/tarefas/tarefa_1/
```

- Tarefa 2

```shell
pytest --testdox -vvs tests/tarefas/tarefa_2/
```

- Tarefa 3

```shell
pytest --testdox -vvs tests/tarefas/tarefa_3/
```

- Tarefa 4

```shell
pytest --testdox -vvs tests/tarefas/tarefa_4/
```

---

Você também pode rodar cada método de teste isoladamente:

```shell
pytest --testdox -vvs caminho/para/o/arquivo/de/teste::NomeDaClasse::nome_do_metodo_de_teste
```

Exemplo: executar somente "test_object_representation"

```shell
pytest --testdox -vvs tests/tarefas/tarefa_1/test_model.py::TeamModelTest::test_object_representation
```

Caso queira, também é possível rodar todos os testes de uma vez:
```shell
pytest --testdox -vvs
```

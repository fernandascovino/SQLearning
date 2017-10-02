### Gerando o BD

```sql
CREATE TABLE table(
  column1 TYPE,
  ...
  columnK TYPE
)
```

#### Entradas SQL

| Tipo | Info |
|---|---|
| `_ PRIMARY KEY` | Coluna com valores únicos não-nulos |
| `INTEGER` | Número |
| `TEXT`| Texto |
| `CHAR(size)` | Sequência de caracteres de tamanho fixo |
| `VARCHAR(size)` | Sequência de caracteres de tamanho variável |
| `DATA` | YYYY-MM-DD |
| `TIMESTAMP` | YYYY-MM-DD HH:MM:SS |


```sql
INSERT INTO table (column1, ..., columnK) VALUES (val1, ... valK);

/* Pode-se selecionar colunas específicas para popular */
```

```sql
SELECT column1, ..., columnK INSERT INTO table2 (column1, ..., columnK) FROM table1;

/* Copia colunas de table1 para table2 */
```

### Fazendo Query

#### Comandos básicos

| Name | Funcion |
|---|---|
| `SELECT _ (AS) _ FROM` | Seleção dos itens na tabela |
| `AS` | Personaliza o nome da coluna na tabela de resultado |
| `DISTINCT`| *No BQ, é realizado por GROUP BY table* |
| `COUNT/SUM/MIN/MAX/AGV(_)` | Contagem |
| `ROUND(int, n)` | Arredonda em n casas |
| `WHERE _ LIKE _ /BETWEEN` | Itens específicos/num range específico |
| `AND/OR/NOT` | Itens sob condições |
| `ORDER/GROUP BY _ DESC/ASC` | CLassificação/agregação dos itens |
| `LIMIT n` | Amostra de tamanho n |

Exemplos

```sql
SELECT column, COUNT(*) FROM table GROUP BY column DESC;

/* Ocorrência de itens únicos na coluna */
```
```sql
SELECT name, category, MAX(downloads) FROM apps GROUP BY category;

/* Máximo de downloads por categoria */
```

#### WildCards

| Char | Funcion |
|---|---|
| `*` | Seleciona todos os itens |
| `%` | Substitui letras numa string |
| _ | Substitui um caractere numa string |

 Exemplo
 
```sql
SELECT * FROM table WHERE colunm LIKE 'A%'

/* Itens na coluna que começam com A */
```

```sql
SELECT * FROM table WHERE colunm LIKE '![x-z]%'

/* Itens na coluna que não ncomeçam com X, Y ou Z */
```

#### Tabelas múltiplas

> A foreign key is a column that contains the primary key of another table in the database. 
> We use foreign keys and primary keys to connect rows in two different tables.
> Unlike primary keys, foreign keys do not need to be unique and can be NULL.

| Name | Funcion |
|---|---|
| `(INNER) JOIN` | Cruza dados a partir da interseção das tabelas (sintaxe completa no exemplo1) |
| `LEFT JOIN` | Cruza dados a partir dos itens da tabela 1 |
| `RIGHT JOIN` | Cruza dados a partir dos itens da tabela 2 |
| `FULL JOIN` | Cruza dados a partir dos itens de ambas as tabelas |

Exemplo

```sql
CREATE TABLE artits(
  id INTEGER PRIMARY KEY,
  name TEXT
)

CREATE TABLE albums(
  id INTEGER
  artist_id INTEGER FOREIGN KEY REFERENCES artists (id),
  name TEXT
  year INTEGER
)

/* Cada artista pode ter vários albuns diferentes */

SELECT * FROM albums
JOIN artists ON albums.artist_id = artists.id;

/* Lista os albums cruzando infos de artista e ano da tabela artistas */

```

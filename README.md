# DIO - Trilha .NET - Banco de Dados
www.dio.me

## Desafio de projeto
Para este desafio, você precisará usar seus conhecimentos adquiridos no módulo de banco de dados, da trilha .NET da DIO.

## Contexto
Você é responsável pelo banco de dados de um site de filmes, onde são armazenados dados sobre os filmes e seus atores. Sendo assim, foi solicitado para que você realize uma consulta no banco de dados com o objetivo de trazer alguns dados para análises.

## Proposta
Você precisará realizar 12 consultas ao banco de dados, cada uma retornando um tipo de informação.
O seu banco de dados está modelado da seguinte maneira:

![Diagrama banco de dados](Imagens/diagrama.png)

As tabelas sao descritas conforme a seguir:

**Filmes**

Tabela responsável por armazenar informações dos filmes.

**Atores**

Tabela responsável por armazenar informações dos atores.

**Generos**

Tabela responsável por armazenar os gêneros dos filmes.

**ElencoFilme**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e atores, ou seja, um ator pode trabalhar em muitos filmes, e filmes
podem ter muitos atores.

**FilmesGenero**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e gêneros, ou seja, um filme pode ter mais de um gênero, e um genêro pode fazer parte de muitos filmes.

## Preparando o banco de dados
Você deverá executar o arquivo **Script Filmes.sql** em seu banco de dados SQL Server, presente na pasta Scripts deste repositório ([ou clique aqui](Script%20Filmes.sql)). Esse script irá criar um banco chamado **Filmes**, contendo as tabelas e os dados necessários para você realizar este desafio.

## Objetivo
Você deverá criar diversas consultas, com o objetivo de retornar os dados a seguir. Abaixo de cada pedido tem o retorno esperado. O seu retorno deve ser igual ao da imagem.

## 1 - Buscar o nome e ano dos filmes

![Exercicio 1](Imagens/1.png)

### Solução
```SQL
select 
nome,
ano
from filmes
```

## 2 - Buscar o nome e ano dos filmes, ordenados por ordem crescente pelo ano

![Exercicio 2](Imagens/2.png)

### Solução
```SQL
select 
nome,
ano
from filmes
order by ano asc
```

## 3 - Buscar pelo filme de volta para o futuro, trazendo o nome, ano e a duração

![Exercicio 3](Imagens/3.png)

### Solução
```SQL
select 
ano,
nome,
duracao
from filmes
where nome = 'De volta para o Futuro'
```

## 4 - Buscar os filmes lançados em 1997

![Exercicio 4](Imagens/4.png)

### Solução
```SQL
select 
ano,
nome,
duracao
from filmes
where ano = 1997
```

## 5 - Buscar os filmes lançados APÓS o ano 2000

![Exercicio 5](Imagens/5.png)

### Solução
```SQL
select 
ano,
nome,
duracao
from filmes
where ano > 2000
```
## 6 - Buscar os filmes com a duracao maior que 100 e menor que 150, ordenando pela duracao em ordem crescente

![Exercicio 6](Imagens/6.png)

### Solução
```SQL
select 
ano,
nome,
duracao
from filmes
where duracao > 100 and duracao < 150
order by duracao asc
```
## 7 - Buscar a quantidade de filmes lançadas no ano, agrupando por ano, ordenando pela duracao em ordem decrescente

![Exercicio 7](Imagens/7.png)

### Solução
```SQL
select 
ano,
count(*) as Quantidade
from filmes
group by ano
order by max(duracao) desc
```
## 8 - Buscar os Atores do gênero masculino, retornando o PrimeiroNome, UltimoNome

![Exercicio 8](Imagens/8.png)

### Solução
```SQL
select 
id,
PrimeiroNome,
UltimoNome,
Genero
from Atores
where Genero = 'M'
```
## 9 - Buscar os Atores do gênero feminino, retornando o PrimeiroNome, UltimoNome, e ordenando pelo PrimeiroNome

![Exercicio 9](Imagens/9.png)

### Solução
```SQL
select 
id,
PrimeiroNome,
UltimoNome,
Genero
from Atores
where Genero = 'F'
order by PrimeiroNome
```
## 10 - Buscar o nome do filme e o gênero

![Exercicio 10](Imagens/10.png)

### Solução
```SQL
select 
nome,
g.Genero
from Filmes f
inner join FilmesGenero fg on fg.Id = f.Id
inner join Generos g on g.id = fg.IdGenero
```
## 11 - Buscar o nome do filme e o gênero do tipo "Mistério"

![Exercicio 11](Imagens/11.png)

### Solução
```SQL
select 
nome,
g.Genero
from Filmes f
inner join FilmesGenero fg on fg.Id = f.Id
inner join Generos g on g.id = fg.IdGenero
where g.Genero = 'Mistério'
```
## 12 - Buscar o nome do filme e os atores, trazendo o PrimeiroNome, UltimoNome e seu Papel

![Exercicio 12](Imagens/12.png)

### Solução
```SQL
select 
f.Nome,
a.PrimeiroNome,
a.UltimoNome,
e.Papel
from Filmes f
inner join ElencoFilme e on e.IdFilme = f.Id
inner join Atores a on a.Id = e.IdAtor
```

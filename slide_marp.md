---
marp: true
author: Gabrielly Cariman
theme: uncover
class: invert
header: '[![width:200px](https://elogroup.com.br/wp-content/uploads/2021/10/20210621-v1-01-Marca-Principal.jpg)](https://elogroup.com.br/)'
---

<!-- _footer: '[Gabrielly Barcelos Cariman](https://github.com/gabriellybc)' -->
<!-- _class: default -->

# Avaliação de modelo de dados de vendas de uma loja de e-commerce

---

O modelo de dados tem 5 tabelas, entidades, sendo elas:

- DIM_Produto
- Tempo
- Loja
- Cliente
- Vendas

---

- A entidade **DIM_Produto** tem 6 atributos, em que um é uma chave primária, primary key (PK), surrogada ou substituta (valores numéricos sequenciais únicos usados como chave primária que não possui significado para o usuário).

- Não é ideal usar essa categoria de chave quando há uma chave candidata (atributo ou grupo de atributos com o potencial para se tornarem uma chave primária) com valores únicos como o atributo Cod_produto que tem já sentido por si só.

---

- A entidade **Tempo** tem 5 atributos todos de tipo, dominio, Integer. O que não é adequado, porque dificulta a query, consulta ao banco de dados. Datas devem ser armazeadas como Date.

- Para normalizar na primeira forma é preciso separar atributos compostos. Como salvar separadamente nome e sobrenome. Porém, não é necessário salvar dia, mês e ano separado. O SQL pode fornecer funções que retornam dia, mês e ano.

---

- A entidade **Loja** tem 3 atributos, em que um é uma chave primária substituta.

- O ideal seria usar o atributo Cod_loja como chave primária, porque ele identifica de forma exclusiva todos os itens de uma tabela, não tem repetição.

---

- A entidade **Cliente** tem 4 atributos, em que um é uma chave primária substituta do tipo Integer e as outras 3 são Varchar.

---

- A entidade **Vendas** tem 6 atributos, em que 4 são chaves estrangeiras, foreign key (FK). Essas chaves estabelecem um relacionamento forte com a chave primária (PK) das tabelas citadas acima. Elas apresentam cardinalidade de um para muitos com Vendas.

- Essa tabela tem um erro grave e não possui um identificador único, uma chave primária.

- O Decimal está armazenando valores monetários.

---

<!-- _class: default -->

# SQL

---

Se os valores estivem armazenados como Date:

```SQL
SELECT COUNT(*)
FROM Vendas
    LEFT JOIN Tempo
      ON Vendas.ID_tempo = Tempo.ID_tempo
    WHERE Tempo.data >= '2020-04-01'
      AND Tempo.data < '2021-04-01';
```

---

```SQL
SELECT COUNT(DISTINCT sexo, estado_civil)
FROM Cliente
    WHERE sexo LIKE "Feminino"
      AND estado_civil LIKE "Divorciada";
```

---

```SQL
SELECT receita_venda
FROM Vendas
    INNER JOIN Loja ON Vendas.id_loja = Loja.id_loja
    INNER JOIN Tempo ON Vendas.id_tempo = Tempo.id_tempo
    WHERE cod_loja = 32
      AND Tempo.data >= '2021-04-01';
```

---

<!-- _class: default -->

# Melhorias

- Usar cod_produto como PK de Produto;

- Mudar o tipo de dado de Tempo de integer para Date e armazenar apenas a Data;

- Fazer uma PK ID_Venda em vendas;

- Usar cod_loja como PK em loja.

---

<!-- _footer: '[Gabrielly Barcelos Cariman](https://github.com/gabriellybc)' -->

# Obrigada!

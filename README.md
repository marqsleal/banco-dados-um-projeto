# Projeto para Diciplina Banco de Dados I

_Este projeto consiste no trabalho final do 3º módulo da trilha de Data Science do Programa Santander Coders 2024.1._ 

* **Módulo** Banco de Dados I
* **Instrutor:** Prof. Lucas Ximenes
* **Grupo**: Gabriel Marques ([GitHub](https://github.com/marqsleal) / [LinkedIn](https://www.linkedin.com/in/marqsleal/)), Marcos Carvalho ([GitHub](https://github.com/MarcosFN2014) / [LinkedIn](https://www.linkedin.com/in/marcos-carvalho-8173a2241/)), Mateus Cunha ([GitHub](https://github.com/Mateusclm) / [LinkedIn](https://www.linkedin.com/in/mateusclm/)) e Mille Amorim ([GitHub](https://github.com/4m0r1m) / [LinkedIn](https://www.linkedin.com/in/mille-amorim/)).

## Modelagem e normalização de bancos de dados relacionais

Certo dia, um dos gestores do banco em que você trabalha como cientista de dados procurou você pedindo ajuda para projetar um pequeno banco de dados com o objetivo de mapear os clientes da companhia pelos diferentes produtos financeiros que eles contrataram.

O gestor explicou que o banco tinha uma grande quantidade de clientes e oferecia uma variedade de produtos financeiros, como cartões de crédito, empréstimos, seguros e investimentos. No entanto, eles estavam tendo dificuldades para entender quais produtos eram mais populares entre os clientes e como esses produtos estavam interagindo entre si.

Como ponto de partida, o gestor deixou claro que um cliente pode contratar vários produtos diferentes, ao passo que um mesmo produto pode também estar associado a vários clientes diferentes e elaborou um rústico esboço de banco de dados com duas tabelas, da seguinte forma:

### Tabela 1

**Nome da tabela:** cliente  
**Colunas:** `codigo_cliente`, `nome_cliente`, `sobrenome_cliente`, `telefone_cliente`, `municipio_cliente`, `codigo_tipo_cliente`, `tipo_cliente`

### Tabela 2

**Nome da tabela:** produto  
**Colunas:** `codigo_produto`, `nome_produto`, `descricao_produto`, `codigo_tipo_produto`, `tipo_produto`, `codigo_diretor_responsavel`, `nome_diretor_responsavel`, `email_diretor_responsavel`

### Perguntas:

### 1. Ainda sem fazer normalizações, apresente o modelo conceitual deste esboço oferecido pelo gestor, destacando atributos chaves e apresentando também a cardinalidade dos relacionamentos.

<p align="center">
  <img src="images/questao_um.png" alt="Primeira Questão">
</p>

Relação Cliente(1,N) - Contrata - (N,1) Produto. Um cliente pode contratar vários produtos e um produto pode ser contratador por vários clientes. Construindo, portanto, uma relação total muitos para muitos (N,N), sendo necessário uma tabela para coordenar esta relação.

### 2. Agora apresente um modelo lógico que expresse as mesmas informações e relacionamentos descritos no modelo original, mas decompondo-os quando necessário para que sejam respeitadas as 3 primeiras formas normais. Destaque atributos chaves e apresente também a cardinalidade dos relacionamentos.

**Formas normais**:

**1ª Forma normal (1FN)**: Todos os atributos contém valores atômicos, indivisíveis, não podendo haver conjuntos, listas ou múltiplos valores em uma única coluna.  
**2ª Forma normal (2FN)**: Todos os atributos não-chave devem depender totalmente da chave primária, não podendo haver dependência parcial.  
**3ª Forma normal (3FN)**: Nenhum atributo não-chave deve depender de outro atributo não-chave, não podendo haver dependência transitiva.  

<p align="center">
  <img src="images/questao_dois.png" alt="Segunda Questão">
</p>

**Resumo das Cardinalidades**:

**1. Cliente - Contrata - Produto**
- **Cliente (1:N)** - **Contrata (N:1)** - **Produto**
  - Um **Cliente** pode contratar vários **Produtos**.
  - Um **Produto** pode ser contratado por vários **Clientes**.
  - Relacionamento **N:N** resolvido pela tabela associativa **Contrata**.

**2. Tipo_Cliente - Cliente**
- **Tipo_Cliente (1:N)** - **Cliente (N:1)**
  - Um **Tipo_Cliente** pode estar associado a vários **Clientes**.
  - Um **Cliente** tem apenas um **Tipo_Cliente**.

**3. Tipo_Produto - Produto**
- **Tipo_Produto (1:N)** - **Produto (N:1)**
  - Um **Tipo_Produto** pode estar associado a vários **Produtos**.
  - Um **Produto** tem apenas um **Tipo_Produto**.

**4. Diretor_Responsavel - Produto**
- **Diretor_Responsavel (1:N)** - **Produto (N:1)**
  - Um **Diretor_Responsavel** pode ser responsável por vários **Produtos**.
  - Um **Produto** tem apenas um **Diretor_Responsavel**.
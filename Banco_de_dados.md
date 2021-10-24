O presente texto não é um material autoral. É apenas um resumo do material fornecido pelo Senac.

[1. Sistema de gerenciamento de banco de dados (SGBD)](https://senacsp.blackboard.com/bbcswebdav/pid-7582902-dt-content-rid-230701907_1/courses/STBDCAS2DA_2103-2103-686276/Template/Rise/Aula_01/content/index.html#/)

Um sistema de gerenciamento de banco de dados (SGBD) é um software  projetado para auxiliar a aplicação na manutenção e utilização de  grandes conjuntos de dados. Quando falamos de manutenção, estamos nos referindo principalmente à  **escrita** (inserção, alteração e deleção); já a **utilização** está  relacionada principalmente à leitura (buscas).

Algumas das vantagens de utilizar **SGBDs** são:

- As aplicações (e os programadores) não precisam conhecer os detalhes de como os dados são armazenados em disco.

- O SGBD fornece diversas funcionalidades e implementa diversos algoritmos e otimizações para que as buscas possam ser realmente rápidas.

- O SGBD ajuda bastante a proteção da integridade e a segurança dos dados.

- O SGBD fornece meios de acesso concorrente (múltiplos usuários acessando os dados).

- O SGBD auxilia a recuperação de falhas (falhas da aplicação, do próprio  SGBD, do sistema operacional e até mesmo do hardware da máquina).

- A utilização de um SGBD reduz o tempo de desenvolvimento de uma aplicação.

  

**Importante**: o conhecimento diz respeito à associação que uma pessoa faz entre conceitos, dados e informações.

No projeto de um SGBD, há dois grandes tipos de decisão a tomar:  decisões no nível físico e no nível conceitual dos dados, este último  também chamado de nível lógico. O nível  físico diz respeito a como os dados são estruturados, ou seja, como os  arquivos são gravados em disco. Já o nível conceitual diz respeito à  visão que o usuário do SGBD (a aplicação e seu desenvolvedor) terá sobre os dados.

No presente texto focaremos quase que exclusivamente na modelagem relacional, um tipo de modelagem na qual um banco de dados é organizado em tabelas bidimensionais que se relacionam entre si. Os SGBDs que adotam esse modelo são chamados de SGBDs  relacionais, sendo o tipo mais popular de SGBD. Em   um   banco   relacional,   cada   tipo   de   entidade   define   um   conjunto   uniforme de atributos possíveis para as  ocorrências daquele tipo de entidade.   Dito   de   outra   forma:    cada   tabela   define   um   conjunto   de   colunas,   e cada registro possui um valor para cada coluna.

**Importante**: Em geral é considerada uma boa prática a não utilização de acentos em nomes de colunas e tabelas de um banco  de dados, assim como em variáveis de um programa. Essa prática pode  evitar alguns aborrecimentos. Também é costume utilizar apenas letras  minúsculas em nomes de colunas e utilizar o underscore (“_”) como  separador de palavras. 

Geralmente   o   desenvolvedor escreve comandos  que o SGBD entenda para a construção de um banco de dados. Usando a  linguagem   do   SGBD,   o   desenvolvedor   define   as   tabelas   que   existirão   e   os campos de cada tabela. Uma   vez   criada   a   estrutura   do   banco   de   dados   (definição   de   tabelas   e campos), a aplicação desenvolvida  interage com o banco para manipular (incluir, alterar, excluir e  consultar) os registros. Via de regra, o usuário   final   interage   com   a   aplicação,   e   não   diretamente   com   o   banco    de dados.

**Importante**: As operações típicas de manipulação de dados são “inserir, alterar,  excluir e consultar”. Essas operações são referidas em conjunto como  CRUD (create, retrieve, update, delete).

**Atenção:** É fortemente recomendado utilizar Linux nesses próximos passos, mas o windows10 fornece uma alternativa o WSL (https://docs.microsoft.com/pt-br/windows/wsl/install). Com o wsl será fornecido um terminal linux e você poderá executar todos os comandos que serão expostos.

Após instalar e configurar o mySQL (tutorial Passos 1 e 2: https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04-pt), ative o super user (basta escrever su em um prompt linux, ou abrir no modo admistrador no windows) e siga os passos:

```mysql
#1 - Para se conectar ao banco, execute o comando a seguir:
$ mysql -u root -p

#2 - Como acabamos de instalar o MySQL, vamos executar alguns procedimentos de praxe: criar um novo usuário e um novo banco de dados:
> CREATE USER 'marco'@'localhost' 'identified by 'senha';
> grant all privileges on * . * to 'marco'@'localhost';

#3 - Saia do prompt do MySQL (com o atalho ctrl+d ou com o comando exit) e se reconecte como o usuário criado:
$ mysql -u marco -p

#4 - Agora vamos criar um banco de dados:
> create database brasil;
> use brasil;

#5 - Para ver as tabelas existentes:
>show tables;

#6 - Criando uma tabela:
>create table municipios(nome text, uf varchar(2));

#7 - Inserindo Registros:
>insert into municipios (nome,uf) values ('Sorocaba','SP'), ('Recife', 'PE'), ('Santa Maria', 'RS'), ('Rio de Janeiro','RJ'), ('São Paulo','SP');

#8 - Para visualizar o estado corrente da tabela:
>table municipios;

#9 - Corrigindo erros:
>update municipios set uf = 'XX' where nome = 'Xxxx'

#10 - Deletando um registro:
>delete from municipios where nome = 'Xxxx';
```

**Obs.:** Instalar o apache (https://dev.to/alexandrefreire/como-instalar-e-otimizar-o-apache-no-ubuntu-1n20) e o adminer (https://www.vivaolinux.com.br/artigo/Instalando-o-Adminer-do-jeito-certo-no-Debian/) usando o prompt.

Para acessar o adminer:

No Terminal: /etc/init.d/apache2 restart (só executar esse comando se o próximo passo não funcionar)

No Navegador: http://127.0.0.1/adminer/

**1.2 - Docker e Docker-compose**

O Docker é uma que cria contêineres, que são sistemas Linux que podem ser executados em uma mesma máquina, mas de forma  isolada.  Já o Docker Compose é uma forma facilitada de se orquestrar a execução  de múltiplos contêineres que se comunicam.

**Atenção:** Instalar Docker (https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt) e Docker-Compose (https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04-pt) na máquina.

Baixar os arquivos que estão nas aulas (kit_aluno) e **executar o terminal de dentro da pasta** com o .yml (segure shift e clique com o botão do lado direito do mouse dentro da pasta e escolha abrir o terminal aqui). 



**Antenção:** Antes de executar o script, pode ser preciso também que o sistema  operacional conceda permissão de execução para o script. Isso é feito  com o comando chmod +x script.sh.

```dockerfile
#não esqueça de usar o comando su
$ docker-compose up

# se der um erro de permissão usar o comando: sudo chown $USER /var/run/docker.sock (no prompt linux)
#você não deve fechar o prompt ao executar o comando anterior, abra um novo prompt e digite o código a seguir.

$ docker-compose exec db mysql -p
# usar as credenciais configuradas na etapa anterior.
```

Quando você inicia os contêineres (run.sh), o terminal fica "preso", não é possível mais executar comandos naquele terminal. Para executar os  comandos de connect, por exemplo, é preciso abrir um novo terminal. Para parar os contêineres, basta teclar ctrl+c no terminal onde se iniciou  os contêineres.

**Alguns comandos do Docker:**

```dockerfile
# Para executar um comando do Linux dentro do contêiner, o comando é:
$ docker-compose exec db <comando>

# Por exemplo, para listar os diretórios na raiz do contêiner:
$ docker-compose exec db ls /

# Para "entrarmos dentro contêiner" basta executar o shell dentro do contêiner:
$ docker-compose exec db bash

# Mas o comando que mais utilizaremos será para nos conectarmos ao banco de dados que está rodando dentro do contêiner:
$ docker-compose exec db mysql <nome_do_banco> -p

# Se você quiser limpar os dados (exemplo: apagar tudo o que você alterou no banco de dados para voltar ao ponto inicial da aula), deve executar o seguinte comando:
$ docker-compose down -v

#Para fazer uma limpeza global no espaço em disco ocupado pelo Docker: 
$ docker image list | grep none | tr -s " " | cut -f 3 -d ' ' | xargs docker image rm -f
```

[2. Projeto lógico](https://senacsp.blackboard.com/bbcswebdav/pid-7582902-dt-content-rid-230701953_1/courses/STBDCAS2DA_2103-2103-686276/Template/Rise/Aula_02/content/index.html#/)

Uma das capacidades mais importantes para um desenvolvedor de sistemas    é   a   de   abstração.   Isso   significa   ser   capaz   de    isolar   o   problema   em diferentes níveis de detalhe e  considerar apenas os aspectos envolvidos que importam para a resolução  do problema. O nível mais alto de abstração é conhecido como “espaço do  problema”. Já o nível de abstração mais baixo é o nível físico, que diz  respeito à máquina. No contexto de bancos de dados, o nível físico é  tudo aquilo que o SGBD esconde de seu usuário, inclusive como os dados  são organizados nos arquivos do sistema operacional.

<img src="/home/matmj/Documents/Banco de Dados - Senac/imgs/Screenshot from 2021-10-24 00-24-34.png" style="zoom: 67%;" />

Um **modelo descritivo** é gerado pela “análise de requisitos”, sendo sua principal característica a informalidade. 

Os dois próximos níveis, no contexto dos bancos relacionais, ambos os níveis estão ligados à  abstração de tabela, com linhas e colunas. Contudo, o **nível  computacional** é dependente de detalhes da tecnologia e deve dialogar  diretamente com os recursos e definições providos por um SGBD em particular, como o MySQL. Já   o   **nível conceitual** é mais abstrato. Um mesmo modelo conceitual  para bancos relacionais deve ser igualmente aplicável a qualquer SGBD  relacional, como   o   PostgreSQL   ou   o   SQL   Server,  normalmente o projeto conceitual é expresso por meio de um diagrama entidade-relacionamento (ou “diagrama ER”). Uma entidade também pode possuir atributos, o que equivale às colunas das tabelas, um modelo entidade-relacionamento também modela relacionamentos entre entidades. 

**Para fixar:** Uma   forma   de   definir   uma   tabela   no nível conceitual é  por meio de um diagrama; já no nível computacional, devemos utilizar o  comando CREATE TABLE da SQL.

A representação completa de um modelo de bancos de dados (entidades,  atributos, relacionamentos, etc.) é chamada de esquema. Um esquema  conceitual é representado por um diagrama ER ou um conjunto de diagramas ER. Já   o   esquema   do   modelo   computacional   é   a   definição   precisa   das   tabelas da base de dados, normalmente  feita em linguagem SQL.

Por mais que computadores sejam rápidos, bancos de dados podem ser muito grandes e percorrer milhões de itens pode levar alguns segundos, o que é um tempo   muito   alto   para   que   o   usuário   fique   esperando.   A   solução   para   esse    problema são os índices, que são estruturas que tornam as consultas  mais rápidas. Um   índice   possibilita   a   busca   eficiente   nas   linhas    da   tabela   a   partir   de   um   valor   da   coluna   (SETZER; SILVA, 2005). 

No MySQL, índices podem ser criados com o seguinte comando:

```sql
CREATE INDEX nome_do_indice ON nome_da_tabela (nome_da_coluna(comprimento_do_texto));

#Note    que    para    criar    um    índice    para    uma    coluna    textual    é    preciso    definir quantos caracteres iniciais do texto o índice considerará.Exemplo:

CREATE INDEX index_nome_cliente ON cliente (nome(10));
```

A utilização de índices também apresenta desvantagens.  Mesmo para um computador, é mais rápido simplesmente inserir um novo   registro   no   fim   da   tabela   do   que   reorganizar   a    estrutura   de   índice   a   cada inserção de dados. Além disso, a utilização de índices aumenta o tamanho (em bytes) da base de dados (o  índice é uma estrutura à parte que deve ser armazenada).

**Atenção:** a criação de muitos índices pode tornar a inserção de dados lenta. Mas a ausência de índices pode tornar a consulta de dados lenta. 

Exemplo do Vídeo: Após baixar o kit_aluno_aula_02 e executar o terminal de dentro da pasta:

```dockerfile
#Não esqueça de usar o comando su
$ docker-compose up
#Não fechar o prompt atual e abrir um novo

#No novo prompt digite
$ docker-compose exec db mysql -p

#Exibir todos os bancos que foram carregados do kit aula 02
> SHOW databases;

#Acessar o database voos_eua_2016
> USE voos_eua_2016;

#Exibir todas as tables do database
> SHOW tables;

#Exibir os elementos da table flights
> SELECT * from flights limit 15;

#Mostrar o tamanho das tabelas
> SELECT database_name, table_name, index_name,
ROUND(stat_value * @@innodb_page_size / 1024 / 1024, 2) size_in_mb
FROM mysql.innodb_index_stats
WHERE stat_name = 'size' AND index_name != 'PRIMARY'
ORDER BY size_in_mb DESC; 

#Contar os registros da tabela flights
> select count(*) from flights;

#Contar os registros de uma empresa
> select count(*) from flights where unique_carrier = 'AA';
```


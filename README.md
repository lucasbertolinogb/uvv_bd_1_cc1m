# uvv_bd_1_cc1m
Olá, sou Lucas Bertolino Santos Costa , estudante de ciência da computação da UVV. 

Esta é uma atividade(pset1) dada pelo professor de banco de dados: Abrantes Araújo Silva Filho.

Nela eu mostrarei como resolverei os códigos e problemas propostos.

>*OBS: SE FOR COPIAR TUDO FAÇA ISSO NO ARQUIVO* foto elmasri-architect(código)
>OBS2: NÂO tem dados INSERIDOS no POSTGRES

>Voltando ao trabalho ....Foto da tabela elmasri traduzida (obs:ela é feita para o terminal mysql)
>
CREATE DATABASE empresa;

USE empresa;

>Até aqui eu crei um banco de dados (create database) e comecei a usa-lo (use empresa).

CREATE TABLE projeto (
                nome_projeto/*Como ele e chamdo*/ VARCHAR(15) NOT NULL ,
                numero_projeto/*O identificador de projeto*/ INT NOT NULL ,               
                local_projeto/*Local do projeto*/ VARCHAR(15),
                numero_departamento/*Numero do departamento*/ INT NOT NULL,
                PRIMARY KEY (numero_projeto)
);

>Uma tabela (table) com as configurações e suas especificações.

CREATE UNIQUE INDEX projeto_idx
 ON projeto
 ( nome_projeto );
 
 >Chave única em nome_projeto.

CREATE TABLE localizacoes_departamento (
                numero_departamento/*Numero do departamento*/ INT NOT NULL,
                local/*local do departamento*/ VARCHAR(15) NOT NULL,
                PRIMARY KEY (numero_departamento, local)
);

>Tabela de localização dos departamento é um bom banco de dados para se ter na mão quando não se sabe o local de trabalho.

CREATE TABLE funcionario (
                primeiro_nome/*Nome formal*/ VARCHAR(15) NOT NULL,
                nome_meio/*primeiro sobrenome*/ CHAR(1),
                ultimo_nome/*ultimo sobrenome*/ VARCHAR(15) NOT NULL,
                cpf /*Cadastro de pessoa fisica*/ CHAR(11) NOT NULL,          
                data_nascimento/*dia que nasceu*/ DATE,
                endereco/*onde mora*/ VARCHAR(50),
                sexo/*F (femenino) ou M(masculino)*/ CHAR(1),
                salario /*quanto recebe o funcionario*/ DECIMAL(10,2),
                cpf_supervisor/*cpf do supervisor do funcionario*/ CHAR(11) NOT NULL,
                numero_departamento/*numero do departamento*/ INT NOT NULL,
                PRIMARY KEY (cpf)
);

>Tabela com as informações gerais do funcionário .

CREATE TABLE departamento (
                nome_departamento/*nome do departamento*/ VARCHAR(15) NOT NULL,
                numero_departamento/*numero do departamento*/ INT NOT NULL,
                cpf_gerenete/*cpf do gerente do departamento*/ CHAR(11) NOT NULL,
                data_inicio_gerente/*quando o gerente entrou no departamento*/ DATE,
                PRIMARY KEY (numero_departamento)
);

>Tabela sobre os departamento gerais e quem é seu gerente.

CREATE UNIQUE INDEX departamento_idx
 ON departamento
 ( nome_departamento );

>Chave única da tabela departamento em nome_departamento.

CREATE TABLE trabalha_em (
                cpf_funcionario/*cpf do funcionario*/ CHAR(11) NOT NULL,
                numero_projeto/*numero do projeto */ INT NOT NULL,
                horas/*expediente do funcionario*/ DECIMAL(3,1) NOT NULL,
                PRIMARY KEY (cpf_funcionario, numero_projeto)
);

>Tabela trabalha_em referece a carga horária de cada funcionário.

CREATE TABLE dependente (
                cpf_funcionario/*cpf do funcionario*/ CHAR(11) NOT NULL,
                nome_dependente/*nome do dependente*/ VARCHAR(15) NOT NULL,
                sexo/*F(femenino) ou M(masculino)*/ CHAR(1),
                data_nascimento/*quando o funcionario nasceu*/ DATE,
                parentesco/*relacao sanguinea*/ VARCHAR(15) ,
                PRIMARY KEY (cpf_funcionario, nome_dependente)
);

>Tabela dependente ,de modo simples,são pessoas com relação sanguínea com os funcionarios (se tiver) na empresa.

INSERT INTO funcionario values (
                "João", "B", "Silva", 12345678966, '1965-01-09' , "Rua das Flores,751, São Paulo ,SP", "M", 30.000, 33344555587, 5            
);

INSERT INTO funcionario values (
                "Fernando", "T", "Wong", 33344555587, '1955-12-08', "Rua da Lapa, 34, São Paulo, SP", "M", 40.000, 88866555576, 5
);

INSERT INTO funcionario values (
                 "Alice", "J", "Zelaya", 99955777767, '1968-01-19', "Rua Souza Lima, 35, Curutiba, PR", "F", 43.000, 88866555576, 4
);

INSERT INTO funcionario values (
                 "Jennifer", "S", "Souza", 98765432168, '1941-06-20', "Av. Arthur de Lima, 54, Santo André, SP", "F", 43.000, 88866555576, 4
);

INSERT INTO funcionario values (
                "Ronaldo", "K", "Lima", 66688444476, '1962-09-15', "Rua Rebouças, 65, Piracicaba, SP", "M", 38.000, 33344555587, 5
);

INSERT INTO funcionario values (
                 "Joice", "A", "Leite", 45345345376, '1972-07-31', "Av. Lucas Obes, 74, São Paulo, SP", "F", 25.000, 33344555587, 5
);                 

INSERT INTO funcionario values (
                 "André", "V", "Pereira", 98798798733, '1969-03-29', "Rua Timbira, 35, São Paulo, SP", "M", 25.000, 98765432168, 4
);           

INSERT INTO funcionario values (
                 "Jorge", "E", "Brito", 88866555576, '1937-11-10', "Rua do Horto, 35, São Paulo, SP" , "M",55.000, 0 , 1
);           

>São 'valores' inseridos na tabela funcionário como exemplo : jorge (primeiro_nome), E (nome_meio), Brito (ultimo_nome), 88866555576 (cpf), 1937-11-10 (data_nascimento), Rua do Horto, 35, São Paulo, SP (endereco), M (sexo), 55.000(salario), 0(cpf_supervisor)*-obs: esse é um valor NULL ou 'vazio'*, 1 (numero_departamento)

>Agora é inserindo valores no departamento , ... o que você esta lendo? *não* vou fazer a mesma coisa de cima.
>
INSERT INTO departamento values (
                "Pesquisa", 5, 33344555587, '1988-05-22'
);

INSERT INTO departamento values (
                "Administração", 4, 98765432168, '1955-01-01'
);

INSERT INTO departamento values (
                "Matriz", 1 , 88866555576, '1981-06-19'
);

>Inserindo valores em localizações do departamento

INSERT INTO localizacoes_departamento values (
                1, "São Paulo"
);

INSERT INTO localizacoes_departamento values (
               4, "Mauá"
);

INSERT INTO localizacoes_departamento values (
               5, "Santo André"
);

INSERT INTO localizacoes_departamento values (
               5, "Itu"
);

INSERT INTO localizacoes_departamento values (
               5, "São Paulo"
);

INSERT INTO projeto values (
               "ProdutoX", 1, "Santo André", 5
);

INSERT INTO projeto values (
               "ProdutoY", 2, "Itu", 5
);

INSERT INTO projeto values (
               "ProdutoZ", 3, "São Paulo", 5
);

INSERT INTO projeto values (
               "Informatização", 10, "Mauá", 4
);

INSERT INTO projeto values (
               "Reorganização", 20, "São Paulo", 1
);

INSERT INTO projeto values (
               "Novosbeneficios", 30, "Mauá", 4
);

>Injetando informações em dependente 

INSERT INTO dependente values (
               33344555587, "Alicia", "F", '1986-04-05', "Filha"
);

INSERT INTO dependente values (
               33344555587, "Tiago", "M", '1983-10-25', "Filho"
);

INSERT INTO dependente values (
               33344555587, "Janaína", "F", '1958-05-03', "Esposa"
);

INSERT INTO dependente values (
               98765432168, "Antonio", "M", '1942-02-28', "Marido"
);

INSERT INTO dependente values (
               12345678966, "Michael", "M", '1988-01-04', "Filho"
);

INSERT INTO dependente values (
               12345678966, "Alicia", "F", '1988-12-30', "Filha"
);

INSERT INTO dependente values (
             12345678966, "Elizabeth", "F", '1967-05-05', "Esposa"
);

>Adiocionando valore me trabalha_em

INSERT INTO trabalha_em values (
             12345678966, 1, 32.5
);

INSERT INTO trabalha_em values (
             12345678966, 2, 7.5
);

INSERT INTO trabalha_em values (
             66655444476, 3, 40.0
);

INSERT INTO trabalha_em values (
             45345345376, 1, 20.0
);

INSERT INTO trabalha_em values (
             45345345376, 2, 20.0
);

INSERT INTO trabalha_em values (
             33344555587, 2, 10.0
);

INSERT INTO trabalha_em values (
             33344555587, 3, 10.0
);

INSERT INTO trabalha_em values (
             33344555587, 10, 10.0
);

INSERT INTO trabalha_em values (
             33344555587, 20, 10.0
);

INSERT INTO trabalha_em values (
             99988777767, 30, 30.0
);

INSERT INTO trabalha_em values (
             99988777767, 10, 10.0
);

INSERT INTO trabalha_em values (
             98798798733, 10, 35.0
);

INSERT INTO trabalha_em values (
             98798798733, 30, 5.0
);

INSERT INTO trabalha_em values (
             98765432168, 30, 20.0
);

INSERT INTO trabalha_em values (
             98765432168, 20, 15.0
);

INSERT INTO trabalha_em values (
             88866555576, 20, 0
);

>OBS: tem algumas chaves que estão com problema e por isso quem for copiar terá que resolve-la.Qual o motivo disso ? Resposta= preguiça

ALTER TABLE dependente ADD CONSTRAINT funcionario_dependente_fk 
FOREIGN KEY (cpf_funcionario) 
REFERENCES funcionario (cpf) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;

ALTER TABLE funcionario ADD CONSTRAINT funcionario_funcionario_fk 
FOREIGN KEY (cpf_supervisor) 
REFERENCES funcionario (cpf) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;
>obs: essa parte não funciona , pois, necessita de outra tabela intermediária para somente cpf_supervisor (que no caso *não fiz*)


ALTER TABLE trabalha_em ADD CONSTRAINT funcionario_trabalha_em_fk 
FOREIGN KEY (cpf_funcionario) 
REFERENCES funcionario (cpf) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;

ALTER TABLE departamento ADD CONSTRAINT funcionario_departamento_fk 
FOREIGN KEY (cpf_gerenete) 
REFERENCES funcionario (cpf) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;

ALTER TABLE localizacoes_departamento ADD CONSTRAINT departamento_localizacoes_departamento_fk 
FOREIGN KEY (numero_departamento) 
REFERENCES departamento (numero_departamento) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;

ALTER TABLE projeto ADD CONSTRAINT departamento_projeto_fk 
FOREIGN KEY (numero_departamento) 
REFERENCES departamento (numero_departamento) 
ON DELETE NO ACTION 
ON UPDATE NO ACTION;

ALTER TABLE trabalha_em ADD CONSTRAINT projeto_trabalha_em_fk
FOREIGN KEY (numero_projeto) 
REFERENCES projeto (numero_projeto) 
ON DELETE NO ACTION;

>término da tabela de elmasri usando o terminal Mysql


>Agora é usando o terminal de PostgreSQL (ou elefante do BD)
>Obs: não tem os dados inseridos em nenhuma parte deste pset-1 do Postgres

CREATE TABLE funcionario (
                cpf CHAR(11) NOT NULL,
                primeiro_nome VARCHAR(15) NOT NULL,
                nome_meio CHAR(1),
                ultimo_nome VARCHAR(15) NOT NULL,
                data_nascimento DATE,
                endereco VARCHAR(30),
                sexo CHAR(1),
                salario NUMERIC(10,2),
                cpf_supervisor CHAR(11) NOT NULL,
                numero_departamento INTEGER NOT NULL,
                CONSTRAINT cpf_pk PRIMARY KEY (cpf)
);

>Para para COMMENT em postgres é necessários para cada linha , ao contrário do Mysql o Postgres é mais lento em escrever os comentários


COMMENT ON TABLE funcionario IS 'É uma tabela para os funcionários da empresa como suas informações gerais';

CREATE TABLE departamento (
                numero_departamento INTEGER NOT NULL,
                nome_departamento VARCHAR(15) NOT NULL,
                cpf_gerenete CHAR(11) NOT NULL,
                data_inicio_gerente DATE,
                CONSTRAINT numero_departamento PRIMARY KEY (numero_departamento)
);


CREATE UNIQUE INDEX departamento_idx
 ON departamento
 ( nome_departamento );

CREATE TABLE projeto (
                numero_projeto INTEGER NOT NULL,
                nome_projeto VARCHAR(15) NOT NULL,
                local_projeto VARCHAR(15),
                numero_departamento INTEGER NOT NULL,
                CONSTRAINT numero_projeto PRIMARY KEY (numero_projeto)
);


CREATE UNIQUE INDEX projeto_idx
 ON projeto
 ( nome_projeto );

CREATE TABLE localizacoes_departamento (
                numero_departamento INTEGER NOT NULL,
                local VARCHAR(15) NOT NULL,
                CONSTRAINT numero_departamento PRIMARY KEY (numero_departamento, local)
);


CREATE TABLE trabalha_em (
                cpf_funcionario CHAR(11) NOT NULL,
                numero_projeto INTEGER NOT NULL,
                horas NUMERIC(3,1) NOT NULL,
                CONSTRAINT cpf_funcionario PRIMARY KEY (cpf_funcionario, numero_projeto)
);


CREATE TABLE dependente (
                cpf_funcionario CHAR(11) NOT NULL,
                nome_dependente VARCHAR(15) NOT NULL,
                sexo CHAR(1),
                data_nascimento DATE,
                parentesco VARCHAR(15),
                CONSTRAINT nome_dependente PRIMARY KEY (cpf_funcionario, nome_dependente)
);

ALTER TABLE dependente ADD CONSTRAINT funcionario_dependente
FOREIGN KEY (cpf_funcionario)
REFERENCES funcionario (cpf)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE funcionario ADD CONSTRAINT funcionario_funcionario
FOREIGN KEY (cpf_supervisor)
REFERENCES funcionario (cpf)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE trabalha_em ADD CONSTRAINT funcionario_trabalha_em
FOREIGN KEY (cpf_funcionario)
REFERENCES funcionario (cpf)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE departamento ADD CONSTRAINT funcionario_departamento
FOREIGN KEY (cpf_gerenete)
REFERENCES funcionario (cpf)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE localizacoes_departamento ADD CONSTRAINT departamento_localizacoes_departamento
FOREIGN KEY (numero_departamento)
REFERENCES departamento (numero_departamento)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE projeto ADD CONSTRAINT departamento_projeto
FOREIGN KEY (numero_departamento)
REFERENCES departamento (numero_departamento)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE trabalha_em ADD CONSTRAINT projeto_trabalha_em
FOREIGN KEY (numero_projeto)
REFERENCES projeto (numero_projeto)
ON DELETE NO ACTION
ON UPDATE NO ACTION
>término da tabela usando o terminal de Postgresql 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Agora é sobre o PSET-2 e seus desafios , diferentemente da parte de cima eu vou colocar as questões e mostrar como eu resolvi elas e é claro os códigos estarão no arquivo pset-2

``QUESTÃO 01: prepare um relatório que mostre a média salarial dos funcionários de cada departamento.``

SELECT numero_departamento AS "numero do departamento" ,AVG(salario) AS "média do salário"
>Estou selecionando de numero_departamento (que vai aparecer como numero do departamento usando a função AS) e fazer uma AVG(averege) ,ou media, da tupla salário ( e usando o mesmo AS para chama-lo de média do salário).

FROM funcionario 
>Agora é o uso do FROM que é usado para indicar a tabela , que no caso é funcionario,  que é onde eu retiro os meus dados do SELECT.

GROUP BY numero_departamento;
>GROUP BY é o *coringa* da minha seleção que vai juntar os salários dos funcionarios com o mesmo departamento e mostrar no relatório.

``QUESTÃO 02: prepare um relatório que mostre a média salarial dos homens e das mulheres``

SELECT sexo, AVG(salario) AS "média salarial" 
>Nesta parte é bem parecido com a 1º questão,logo substitui numero_departamento por sexo e continuei com salario e mudei média do salário para média salarial somente para ficar diferente, servindo somente como um cosmético.

FROM funcionario 

GROUP BY sexo;
>Neste GROUP BY eu deixei ela para juntar os que estão com o mesmo sexo , no caso da consulta m e f.
 
``QUESTÃO 03: prepare um relatório que liste o nome dos departamentos e, para cada departamento, inclua as seguintes informações de seus funcionários: o nome completo, a data de nascimento, a idade em anos completos e o salário.``

SELECT f.numero_departamento , primeiro_nome, nome_meio, ultimo_nome ,data_nascimento , salario 
FROM funcionario AS f 
INNER JOIN departamento 
ON f.numero_departamento = departamento.numero_departamento 
ORDER BY ;

SELECT f.numero_departamento , primeiro_nome, nome_meio, ultimo_nome ,data_nascimento , TIMESTAMPDIFF(YEAR , data_nascimento, CURRENT_DATE) AS "Ano" , salario 
FROM funcionario AS f 
INNER JOIN departamento 
ON f.numero_departamento = departamento.numero_departamento 
ORDER BY ;

SELECT 

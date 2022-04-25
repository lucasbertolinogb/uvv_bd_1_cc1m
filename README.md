# uvv_bd_1_cc1m
Olá, sou Lucas Bertolino Santos Costa , estudante de ciência da computação da UVV. 

Esta é uma atividade(pset1) dada pelo professor de banco de dados: Abrantes Araújo Silva Filho.

Nela eu mostrarei como resolverei os códigos e problemas propostos.

>Foto da tabela elmasri traduzida (obs:ela é feita para o terminal mysql)

CREATE DATABASE empresa;

USE empresa;


CREATE TABLE projeto (
                numero_projeto/*O identificador de projeto*/ INT NOT NULL ,
                nome_projeto/*Como ele e chamdo*/ VARCHAR(15) NOT NULL ,
                local_projeto/*Local do projeto*/ VARCHAR(15),
                numero_departamento/*Numero do departamento*/ INT NOT NULL,
                PRIMARY KEY (numero_projeto)
);


CREATE UNIQUE INDEX projeto_idx
 ON projeto
 ( nome_projeto );

CREATE TABLE localizacoes_departamento (
                numero_departamento/*Numero do departamento*/ INT NOT NULL,
                local/*local do departamento*/ VARCHAR(15) NOT NULL,
                PRIMARY KEY (numero_departamento, local)
);


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
>obs:o endereço esta com VARCHAR(50) pois para inser as informações é necessário algo entre *30* e *40*

CREATE TABLE departamento (
                numero_departamento/*numero do departamento*/ INT NOT NULL,
                nome_departamento/*nome do departamento*/ VARCHAR(15) NOT NULL,
                cpf_gerenete/*cpf do gerente do departamento*/ CHAR(11) NOT NULL,
                data_inicio_gerente/*quando o gerente entrou no departamento*/ DATE,
                PRIMARY KEY (numero_departamento)
);


CREATE UNIQUE INDEX departamento_idx
 ON departamento
 ( nome_departamento );

CREATE TABLE trabalha_em (
                cpf_funcionario/*cpf do funcionario*/ CHAR(11) NOT NULL,
                numero_projeto/*numero do projeto */ INT NOT NULL,
                horas/*expediente do funcionario*/ DECIMAL(3,1) NOT NULL,
                PRIMARY KEY (cpf_funcionario, numero_projeto)
);


CREATE TABLE dependente (
                cpf_funcionario/*cpf do funcionario*/ CHAR(11) NOT NULL,
                nome_dependente/*nome do dependente*/ VARCHAR(15) NOT NULL,
                sexo/*F(femenino) ou M(masculino)*/ CHAR(1),
                data_nascimento/*quando o funcionario nasceu*/ DATE,
                parentesco/*relacao sanguinea*/ VARCHAR(15) ,
                PRIMARY KEY (cpf_funcionario, nome_dependente)
);


ALTER TABLE trabalha_em ADD CONSTRAINT projeto_trabalha_em_fk 
FOREIGN KEY (numero_projeto)
REFERENCES projeto (numero_projeto)
;

ALTER TABLE dependente ADD CONSTRAINT funcionario_dependente_fk 
FOREIGN KEY (cpf_funcionario)
REFERENCES funcionario (cpf)
;

ALTER TABLE funcionario ADD CONSTRAINT funcionario_funcionario_fk 
FOREIGN KEY (cpf_supervisor)
REFERENCES funcionario (cpf)
;

ALTER TABLE trabalha_em ADD CONSTRAINT funcionario_trabalha_em_fk 
FOREIGN KEY (cpf_funcionario)
REFERENCES funcionario (cpf)
;

ALTER TABLE departamento ADD CONSTRAINT funcionario_departamento_fk 
FOREIGN KEY (cpf_gerenete)
REFERENCES funcionario (cpf)
;

INSERT INTO funcionario values (
                "João", "B", "Silva", 12345678966, '09-01-1965' , "Rua das Flores,751, São Paulo ,SP", "M", 30.000, 33344555587, 5
            
);

>término da tabela de elmasri usando o terminal Mysql--------------------------------------------------------------------------------------------
-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-
#######################################################################################################################################################################
*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
>usando a mesma foto agora com o terminal de Postgresql--------------------------------------------------------------------------------------------

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

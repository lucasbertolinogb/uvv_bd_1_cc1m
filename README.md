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
OBS: Esses são códigos para *Mysql* 

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

SELECT dep.nome_departamento , CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" ,data_nascimento , 
>*OBS:Essa parte vai ser meio complicado de explicar então talvez tenha algo que eu falarei "abobrinhas"*
>Nessa seleção de tem algo novo o dep.alguma_coisa , esse dep esta referente ao AS na parte FROM para diminuir o nome escrito , mas porque eu iria usar isso ao inves de so escrever o nome da tabela? Simples, já que eu tenho mais de uma tabela e nela por coincidência tem duas tabelas com o mesmo nome , o sistema não saberia qual tabela eu pegaria a informação resultando em uma ambiguidade. 
>O CONCAT é o que podemos dizer ser um tipo de juntador de caracterer ,ou seja, eu estou pegando as tabelas de nomes e juntado elas e uma única tabela "Nome_completo".

TIMESTAMPDIFF (YEAR , data_nascimento,   CURRENT_DATE) AS "Ano" , salario 
>Esse "TIMESTAMDIFF", não é dilf e sim diff com dois "ff" , tem quase a mesma função que o CONCAT , entretanto serve somente para calcular data.

FROM funcionario AS f , departamento AS dep 
>Agora temos duas tabelas sendo usadas , e como expliquei em cima é aconselhável o uso de "<nome_da_tabela>.coluna"

WHERE f.numero_departamento = dep.numero_departamento 
>O finalizamento que é iqualar o numero_departamento entre as tabelas funcionario e departamento o que me retornar o resultado final da questão

ORDER BY dep.nome_departamento ;
>Eu usei esse ORDER BY , pois estava muito embolado.

``QUESTÃO 04: prepare um relatório que mostre o nome completo dos funcionários, a idade em anos completos, o salário atual e o salário com um reajuste que obedece ao seguinte critério: se o salário atual do funcionário é inferior a 35.000 o reajuste deve ser de 20%, e se o salário atual do funcionário for igual ou superior a
35.000 o reajuste deve ser de 15%. ``

 SELECT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , TIMESTAMPDIFF (YEAR , data_nascimento,   CURRENT_DATE) AS "Idade", salario ,(salario + salario * 0.2) AS "salario com reajuste" 
 >Usei o mesmo select para calcular data e trazer o nome completo 
 
 FROM funcionario 
 WHERE salario < 35.000 
 UNION 
 >Agora o "pulo do gato" usei a union com o mesmo select até funcionario (ctrl C + ctrl V)
 
 SELECT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , TIMESTAMPDIFF (YEAR , data_nascimento,   CURRENT_DATE) AS "Idade", salario ,(salario + salario * 0.15) AS "salario com reajuste" 
 FROM funcionario 
 WHERE salario > 35.000 ; 
 >E nessa parte que é diferente de cima que é o > e < no valor 35.000 que faz com que somente os valores sejam alterados em 20% ou 15%
 
 ``QUESTÃO 05: prepare um relatório que liste, para cada departamento, o nome do gerente e o nome dos funcionários. Ordene esse relatório por nome do departamento (em ordem crescente) e por salário dos funcionários (em ordem decrescente).``
 >*OBS:Essa por incrível que pareça foi a que eu fiz mais rápida deu no máximo 30 minutos*

SELECT dep.nome_departamento AS "nome do departamento" , s.primeiro_nome AS supervisor ,f.primeiro_nome AS funcionario 
>Usei uma seleção nome_departamento da tabela departamento ( o AS foi para deixar mais apresentável) , chamei a mesma tabela duas vezes

FROM funcionario AS f , funcionario AS s , departamento as dep 
>Agora vem a sacada : usei duas vezes a mesma tabela e para não dar um erro eu usei AS para diferencia-las e é claro tive que colocar a nomenclatura para diferencia.

WHERE f.cpf_supervisor = s.cpf AND s.numero_departamento = dep.numero_departamento 
>É nesta parte onde o uso de duas tabelas entra , para eu não deixar o cpf_supervisor multiplicar a tabela eu faço dela iqual a funcionario , logo ela vai retornar apenas uma vez , em seguida tem o numero_departamento sendo iqualado na tabela funcionario s e f o que faz o resultado ser o que a questão pede

ORDER BY dep.nome_departamento ASC , s.salario DESC , f.salario DESC ;
>Finalizando com order by com asc (ascedente) que no caso é de A -> Z e desc (descender) para o salario MAIOR -> menor.

``QUESTÃO 06: prepare um relatório que mostre o nome completo dos funcionários que têm dependentes, o departamento onde eles trabalham e, para cada funcionário, também liste o nome completo dos dependentes, a idade em anos de cada dependente e o sexo (o sexo NÃO DEVE aparecer como M ou F, deve aparecer como “Masculino” ou  “Feminino”).``

(SELECT DISTINCT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo", dep.nome_departamento , d.nome_dependente , TIMESTAMPDIFF (YEAR , d.data_nascimento, CURRENT_DATE) AS "Idade do dependente", REPLACE(d.sexo , 'F', 'femenino ')sexo 
>Nesta parte eu selecionei com DISTINC , pois não aguentava dar triplicidade de valores , usei o mesmo CONCAT e TIMESTAMPDIFF das questôes anteriores, usei o REPLACE que tem a função de substituir APENAS uma palavra por outra, além do nome_departamento que TEM que vir com <dep.> para não ter anbiguidade entre as tabelas (que me aborreceu muito nesta questão)

FROM funcionario AS f , dependente AS d , departamento AS dep , trabalha_em as trab 
WHERE f.cpf = d.cpf_funcionario AND f.cpf = trab.cpf_funcionario AND d.sexo = 'f' AND f.numero_departamento = dep.numero_departamento 
) 
UNION 
>O coringa que eu usei sabendo que não iria dar para usar o replace em duas palavras foram : d.sexo = 'f' no WHERE o que me faz retornar somente dentro de <>(quer dizer "diferente" em sql) sexo a palavra f e a outra sacada foi UNION para pegar o resto da seleção .

((SELECT DISTINCT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo", dep.nome_departamento , d.nome_dependente , TIMESTAMPDIFF (YEAR , d.data_nascimento, CURRENT_DATE) AS "Idade do dependete", REPLACE(d.sexo , 'M', 'masculino ')sexo 
FROM funcionario AS f , dependente AS d , departamento AS dep , trabalha_em as trab 
WHERE f.cpf = d.cpf_funcionario AND f.cpf = trab.cpf_funcionario AND d.sexo = 'm' AND f.numero_departamento = dep.numero_departamento
)
ORDER BY Nome_completo;
>Por fim , foi ordenado em Nome_completo para deixar visualmente mais bonito e fácil de ver

``QUESTÃO 07: prepare um relatório que mostre, para cada funcionário que NÃO TEM dependente, seu nome completo, departamento e salário.``

SELECT DISTINCT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , f.numero_departamento , salario 
>Usei o cansado nome_completo e chamei as colunas numero_departamento e salario

FROM funcionario AS f 
>Vem da tabela funcionario que eu apelidei de f 

INNER JOIN departamento AS dep ON f.numero_departamento = dep.numero_departamento 
>INNER JOIN ou junção de tabela , ou seja, ele tem a função de A+B e usando ON eu posso especificar onde eu junto funcionario e departamento em numero_departamento

LEFT JOIN dependente AS d ON f.cpf = d.cpf_funcionario 
>LEFT JOIN tem quase a mesma função de INNER JOIN que seria de fazer todas as combinações possiveis com a esquerda o que poderia retornar null

WHERE d.nome_dependente IS NULL;
>Já essa parte é onde eu retiro o desnecessário valor null da LEFT JOIN 

``QUESTÃO 08: prepare um relatório que mostre, para cada departamento, os projetos desse departamento e o nome completo dos funcionários que estão alocados em cada projeto. Além disso inclua o número de horas trabalhadas por cada funcionário, em cada projeto``

SELECT  d.nome_departamento AS "Nome do Departamento" ,CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , p.nome_projeto AS "Nome do Projeto" , t.horas 
>Usei o bom nome_completo (eu já usei antes então não irei explicar , se quiser minha explicação vá ler a 4º questão), chamei nome_departamento em departamento, nome_projeto em projeto e horas em trabalha_em e usei o AS como função de estética.


FROM departamento AS d , funcionario AS f, trabalha_em AS t , projeto AS p 
>Agora o AS realmente mostra seu valor e deixar de seu um produto estético e passar a ser um otimizador na linguagem SQL fazendo seu código ser mais rápido de ser lido

WHERE d.numero_departamento = f.numero_departamento AND f.cpf = t.cpf_funcionario AND t.numero_projeto = p.numero_projeto 
>.O numero_departamento sendo iqualados nas tabelas departamento e funcionario faz com que a seleção sai de 2304 rolls (pode ser traduzida em lista) para 768 rolls (é muito bom para prática manualmente, vulgo trabalho braçal) ,ou seja , ele só seleciona partes em que as duas tabelas tem a o mesmo numero_departamento , seguindo essa lógica em cpf (768 -> 128) e numero_projeto (128 -> 16) temos a relação que a questão pede.

ORDER BY d.nome_departamento, Nome_completo, p.nome_projeto; 
>E finalmente  uma organização para deixar mais coerente , onde nome_departamento esta sendo a base da ordenação (neste caso de A -> Z), seguido de Nome_completo e p.nome_projeto .

``QUESTÃO 09: prepare um relatório que mostre a soma total das horas de cada projeto em cada departamento. Obs.: o relatório deve exibir o nome do departamento, o nome do projeto e a soma total das horas.``

SELECT dep.nome_departamento, p.nome_projeto, SUM(horas)
>Selecionei nome_departamento da tabela departamento , nome_projeto da tabela projeto e SUM(somar) horas da tabela trabalha_em 
>OBS: como nenhuma delas tem tabelas iquais e não usei "nometabela.algumacoisa", mas é sempre bom lembrar que se ocorrer ambuiguidade é culpa de seu sql (é culpa do sistema não trabalhar direito)

FROM departamento AS dep , projeto AS p, trabalha_em AS t 
>Aqui eu chamei as tabelas e nomei elas para encurtar os códigos

WHERE t.numero_projeto = p.numero_projeto AND dep.numero_departamento = p.numero_departamento 
GROUP BY nome_projeto 
>Esse é o climáx da questão (o que me fez tirar o UNION que causou o encurtou e resolveu o problema) o GROUP BY que agrupou no relatória o pedido da questão

ORDER BY nome_departamento ASC;
>ORDER BY para acabamento 

``QUESTÃO 10: prepare um relatório que mostre a média salarial dos funcionários de cada departamento.``
>OBS: é identico a questão 2 ... 

SELECT nome_departamento AS "Nome do Departamento" , AVG(salario) AS "Média Salarial" 
> Selecionei nome_departamento da tabela departamento e salario , para o AS usei como cosmético para aparecer no relatório Nome do Departamento e Média Salarial.

FROM funcionario, departamento
> Já que os dois não possuem colunas iquais eu não precisei dar um funionario.salario e por isso não adcionei AS , pois nesse caso não me serviria para nada. 

GROUP BY nome_departamento ;
>GROUP BY usado ´para agrupar os resultados em três grupos e para não aparecer uma coluna por causa de AVG.

``QUESTÃO 11: considerando que o valor pago por hora trabalhada em um projeto é de 50 reais, prepare um relatório que mostre o nome completo do funcionário, o nome do projeto e o valor total que o funcionário receberá referente às horas trabalhadas naquele projeto.``
>OBS : consulta incompleta , pois, falta 3 funcionario ... mais tarde vejo o problema

SELECT DISTINCT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo", p.nome_projeto , (horas * 50) AS "Valor do trabalho" 
FROM funcionario AS f , trabalha_em AS t , projeto AS p 
WHERE f.cpf = t.cpf_funcionario AND p.numero_projeto = t.numero_projeto ;

``QUESTÃO 12: seu chefe está verificando as horas trabalhadas pelos funcionários nos projetos e percebeu que alguns funcionários, mesmo estando alocadas à algum projeto, não registraram nenhuma hora trabalhada. Sua tarefa é preparar um relatório que liste o nome do departamento, o nome do projeto e o nome dos funcionários que, mesmo estando alocados a algum projeto, não registraram nenhuma hora trabalhada.``
  
SELECT DISTINCT d.nome_departamento AS "Nome do Departamento" , p.nome_projeto AS "Nome do Projeto" , CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , horas
>Usei SELECT DISTINCT para não ter valores duplicados, o resto você já sabe (se não , olhe a questão 1 sobre o uso do AS nesse select) 
 
FROM departamento AS d , projeto AS p , funcionario AS f , trabalha_em AS t 
>Chamei 4 tabelas ,e já que usei mais de 3 tabelas, é uma ideia viável para não se perder em anbiguidade (simplificando, é quando tem duas tabelas que possuem colunas iquais e causaria uma dúvida no sistema) usando AS apelido.
  
WHERE t.horas = 0 AND p.numero_projeto = t.numero_projeto AND d.numero_departamento = f.numero_departamento AND f.cpf = t.cpf_funcionario ;
>Finalmente um monte de iqualdade ,para não ter 2304 rolls , onde a principal iqualdade esta em t.horas = 0 para receber somente funcionario qua com 0 horas.

``QUESTÃO 13:durante o natal deste ano a empresa irá presentear todos os funcionários e todos os dependentes (sim, a empresa vai dar um presente para cada funcionário e um presente para cada dependente de cada funcionário) e pediu para que você preparasse um relatório que listasse o nome completo das pessoas a serem presenteadas (funcionários e dependentes), o sexo e a idade em anos completos (para poder comprar um presente adequado). Esse relatório deve estar ordenado pela idade em anos completos, de forma decrescente.``

(SELECT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , sexo , TIMESTAMPDIFF (YEAR , data_nascimento, CURRENT_DATE) AS "Idade" 
FROM funcionario
)
>Peguei o Nome_completo, sexo e Idade de funcionario

UNION 
>Para desvender a charada da questão usei UNION que tem como função juntar duas consultas iquais (A/B)-um em cima do outro.

(SELECT nome_dependente AS "Nome_completo",  sexo , TIMESTAMPDIFF (YEAR , data_nascimento, CURRENT_DATE) AS "Idade"
FROM dependente 
)
>Para terminar de vez é necessário iqualar nome_dependete como Nome_completo para ter as duas juntas.

ORDER BY Idade DESC;
>E finalizar como pede a questão usando ORDER BY para deixar a ordem em Idade decrescente.


``QUESTÃO 14: prepare um relatório que exiba quantos funcionários cada departamento tem.``

SELECT nome_departamento AS "Nome do Departamento" ,COUNT(*) as "Numero de funcionario" 
>Troxe para o select nome_departamento como Nome do Departamento e COUNT (contar) * (poderia ser qualquer nome de coluna de funcionario) como Numero de funcionario.

FROM funcionario AS f , departamento AS dep 
>Chamei funcionario e departamento.

WHERE f.numero_departamento = dep.numero_departamento 
>É nesta parte onde a solução começa , onde só pode ser chamado no relatório onde o numero_departamento se repete , o que não me causa a maldita multiplicação , e me retornar um funcionario.

GROUP BY nome_departamento;
>E para acabar de vez na questão é preciso do GROUP BY para juntar somente com o mesmo nome_departamento e não uma COUNT com 8 funcionarios.

``QUESTÃO 15: como um funcionário pode estar alocado em mais de um projeto, prepare um relatório que exiba o nome completo do funcionário, o departamento desse funcionário e o nome dos projetos em que cada funcionário está alocado. Atenção: se houver algum funcionário que não está alocado em nenhum projeto, o nome completo e o departamento também devem aparecer no relatório.``
>OBS:Eu acho que não fiz o relatório certo e como esta dando o mesmo resultado deixei como esta 

(SELECT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , d.nome_departamento , p.nome_projeto 
>usei o mesmo nome_completo das questões anteriores , nome_departamento ligado a departamento e nome_projeto ligado a projeto .


FROM funcionario as f, departamento AS d, projeto AS p , trabalha_em AS t 
>Nesta parte brilha o "AS" e faz com que o código tenha um tamanho menor 

WHERE d.numero_departamento = f.numero_departamento AND t.numero_projeto = p.numero_projeto AND f.cpf = t.cpf_funcionario 
>Várias iqualdade para não ter os mais de 2304 rolls (e não transformar o computador em um avião)

GROUP BY Nome_completo , nome_projeto 
) 
>O "(" e ")" serve para saber onde esta o select na função


UNION 
>E este é o motivo de ter "("-o o-")" para ter a noção de onde estão os selects 

(SELECT CONCAT(primeiro_nome,' ' , nome_meio, ' ' , ultimo_nome ) AS "Nome_completo" , d.nome_departamento , p.nome_projeto 
FROM funcionario as f , departamento AS d, projeto AS p , trabalha_em AS t 
WHERE d.numero_departamento = f.numero_departamento AND 
      t.numero_projeto = p.numero_projeto AND NOT EXISTs (SELECT * 
                                                          FROM funcionario AS f , trabalha_em AS t 
                                                          WHERE f.cpf = t.cpf_funcionario 
                                                          )
>Aqui esta o erro/falha que eu não descobri comomudar.

)
GROUP BY Nome_completo , nome_projeto
)


FALTOU:
Ronaldo , jennifer  e andré nesta consulta + os que não trabalham


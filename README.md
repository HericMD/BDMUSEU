# BDMUSEU
-- Geração de Modelo físico
-- Sql ANSI 2003 - brModelo.
-- Alunos: José Augusto Veridiana, Marcus Vinicius de Oliveira, Heric Matheus Damasio

CREATE DATABASE 	banco_museu;
USE banco_museu;


CREATE TABLE autor (
cod_autor int PRIMARY KEY,
nacionalidade_autor char(3) not null,
nome_autor varchar(80) not null
);

CREATE TABLE salao (
cod_salao int PRIMARY KEY,
num_salao int not null,
andar_museu int not null,
salao varchar(80) not null
);

CREATE TABLE salao_obra (
salao_cod_salao int not null,
obra_cod_obra int not null,
posicao_salao varchar(80) not null,
FOREIGN KEY(salao_cod_salao) REFERENCES salao (cod_salao)
);

CREATE TABLE atividade (
ob_cod_obra int not null,
func_id_funcionario int not null,
hora_entrada time not null,
hora_saida time not null,
data_atividade date not null
);

CREATE TABLE tipo_funcionario (
cod_tipo_funcionario int PRIMARY KEY,
tipo_funcionario varchar(80) not null
);

CREATE TABLE materia_prima (
cod_mat_prima int PRIMARY KEY,
qtd_est_mat int not null,
nome_mat_prima varchar(80) not null
);

CREATE TABLE funcionario (
id_funcionario int PRIMARY KEY,
nome_funcionario varchar(80) not null,
salario_funcionario decimal(10,2) not null,
cpf_funcionario varchar(14) not null unique,
cod_tipo_funcionario int not null,
FOREIGN KEY(cod_tipo_funcionario) REFERENCES tipo_funcionario (cod_tipo_funcionario)
);

CREATE TABLE manutencao (
mnt_obra int PRIMARY KEY,
data_termi_mnt date not null,
custo_mnt decimal(10,2) not null,
data_ini_mnt date not null,
desc_mnt varchar(80) not null,
cod_obra int not null,
func_id_funcionario int not null,
FOREIGN KEY(func_id_funcionario) REFERENCES funcionario (id_funcionario)
);

CREATE TABLE obra (
cod_obra int PRIMARY KEY,
ano_obra year not null,
titu_obra varchar(80) not null unique,
peso_obra decimal(10,2) null,
material_obra varchar(80) null,
desc_estilo_obra varchar(80) null,
cod_autor int not null,
cod_tipo_obra int not null,
FOREIGN KEY(cod_autor) REFERENCES autor (cod_autor)
);

CREATE TABLE tipo_obra (
cod_tipo_obra int PRIMARY KEY,
desc_tipo_obra varchar(80) not null
);

CREATE TABLE manu_mat (
Campo_1 int not null,
Campo_2 int not null,
qtd_mat_mnt varchar(15) not null,
FOREIGN KEY(Campo_1) REFERENCES manutencao (mnt_obra),
FOREIGN KEY(Campo_2) REFERENCES materia_prima (cod_mat_prima)
);

ALTER TABLE salao_obra ADD FOREIGN KEY(obra_cod_obra) REFERENCES obra (cod_obra);
ALTER TABLE atividade ADD FOREIGN KEY(ob_cod_obra) REFERENCES obra (cod_obra);
ALTER TABLE atividade ADD FOREIGN KEY(func_id_funcionario) REFERENCES funcionario (id_funcionario);
ALTER TABLE manutencao ADD FOREIGN KEY(cod_obra) REFERENCES obra (cod_obra);
ALTER TABLE obra ADD FOREIGN KEY(cod_tipo_obra) REFERENCES tipo_obra (cod_tipo_obra);

insert into tipo_funcionario(cod_tipo_funcionario, tipo_funcionario)
values
(01, "Guarda"),
(02, "Restauradores de obras"),
(03, "Operários de limpeza")
;

insert into autor(cod_autor, nacionalidade_autor, nome_autor)
values
(14, "ITA", "Leonardo da Vinci"),
(12, "EUA", "Jackson Pollock"),
(13, "FRA", "Éduoard Manet"),
(20, "FRA", "Claude Monet"),
(01, "ESP", "Pablo Picasso"),
(10, "ITA", "Michelangelo"),
(09, "BRA", "Tarsila do Amaral"),
(08, "BRA", "Aleijadinho"),
(19, "BRA", "Vik Muniz"),
(11, "COL", "Fernando Botero"),
(05, "ITA", "Donatello"),
(17, "AUS", "Ron Mueck"),
(02, "HOL", "Vincent Van Gogh"),
(16, "HOL", "Frans Post"),
(15, "ESP", "Salvador Dalí"),
(04, "ESP", "Joan Miró"),
(03, "ARG", "Emílio Pettoruti"),
(18, "JAP", "Katsushika Hokusai"),
(06, "BEL", "René Magritte"),
(07, "DEU", "Rudolf Belling");

insert into tipo_obra(cod_tipo_obra, desc_tipo_obra)
values
(1, "Pintura"),
(2, "Escultura");

select * from tipo_obra;

insert into atividade(ob_cod_obra, func_id_funcionario, hora_entrada, hora_saida, data_atividade) 
values 
(11, 14, "15:32:15", "22:41:21", "2022-11-19"),
(20, 12, "02:31:01", "14:15:53", "2021-12-01"),
(13, 13, "11:14:42", "11:15:43", "2022-10-04"),
(01, 20, "00:00:00", "23:59:59", "2020-02-28"),
(04, 01, "13:22:44", "15:43:21", "2012-05-10"),
(03, 10, "11:21:24", "11:33:11", "2015-06-23"),
(19, 09, "23:01:58", "23:39:04", "2022-06-09"),
(15, 08, "12:00:00", "13:13:13", "2019-03-25"),
(12, 19, "08:45:06", "17:22:13", "2022-08-31"),
(09, 11, "09:03:00", "09:37:00", "2011-09-11"), 
(18, 05, "16:13:35", "20:20:19", "2015-07-13"),
(02, 17, "03:00:00", "03:33:33", "2003-03-30"),
(10, 02, "09:23:15", "23:10:42", "2022-01-05"),
(17, 16, "13:12:11", "14:13:12", "2022-05-11"),
(05, 15, "01:55:56", "18:16:15", "2022-06-04"),
(06, 04, "04:44:44", "14:04:40", "1995-04-01"),
(16, 03, "10:14:50", "19:01:32", "2000-01-01"),
(07, 18, "23:11:43", "23:15:06", "2009-05-15"),
(14, 06, "11:15:00", "17:00:00", "2016-12-25"),
(08, 07, "05:43:21", "23:15:23", "2017-07-11")
;

select * from atividade;

# BDMUSEU
-- Geração de Modelo físico
-- Sql ANSI 2003 - brModelo.
-- Alunos: José Augusto Veridiana, Marcus Vinicius de Oliveira, Heric Matheus Damasio

CREATE DATABASE BD_MUSEU_MJH;
USE BD_MUSEU_MJH;


CREATE TABLE autor (
cod_autor int PRIMARY KEY AUTO_INCREMENT,
nacionalidade_autor char(3) not null,
nome_autor varchar(80) not null
);

CREATE TABLE salao (
cod_salao int PRIMARY KEY AUTO_INCREMENT,
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
cod_tipo_funcionario int PRIMARY KEY AUTO_INCREMENT,
tipo_funcionario varchar(80) not null
);

CREATE TABLE materia_prima (
cod_mat_prima int PRIMARY KEY AUTO_INCREMENT,
qtd_est_mat int not null,
nome_mat_prima varchar(80) not null
);

CREATE TABLE funcionario (
id_funcionario int PRIMARY KEY AUTO_INCREMENT,
nome_funcionario varchar(80) not null,
salario_funcionario decimal(10,2) not null,
cpf_funcionario varchar(14) not null unique,
cod_tipo_funcionario int not null,
FOREIGN KEY(cod_tipo_funcionario) REFERENCES tipo_funcionario (cod_tipo_funcionario)
);

CREATE TABLE manutencao (
mnt_obra int PRIMARY KEY AUTO_INCREMENT,
data_termi_mnt date not null,
custo_mnt decimal(10,2) not null,
data_ini_mnt date not null,
desc_mnt varchar(80) not null,
cod_obra int not null,
func_id_funcionario int not null,
FOREIGN KEY(func_id_funcionario) REFERENCES funcionario (id_funcionario)
);

CREATE TABLE obra (
cod_obra int PRIMARY KEY AUTO_INCREMENT,
ano_obra int not null,
titu_obra varchar(80) not null unique,
peso_obra decimal(10,2) null,
material_obra varchar(80) null,
desc_estilo_obra varchar(80) null,
cod_autor int not null,
cod_tipo_obra int not null,
FOREIGN KEY(cod_autor) REFERENCES autor (cod_autor)
);

CREATE TABLE tipo_obra (
cod_tipo_obra int PRIMARY KEY AUTO_INCREMENT,
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

insert into tipo_funcionario(tipo_funcionario)
values
("Operários de limpeza"),
("Guarda"),
("Restauradores de obras");
;

insert into funcionario(nome_funcionario, salario_funcionario, cpf_funcionario, cod_tipo_funcionario)
values
("Rogério", 2009.15, "255.662.580-50", 2),
("Julia", 2541.64, "906.726.060-62", 3), #2
("Pablo", 2498.77, "020.709.690-29", 3), #3
("Paola", 1443.15, "126.773.170-28", 1),
("Cleiton", 1452.74, "072.254.270-40", 1),
("Jorge", 1436.98, "619.864.050-79", 1),
("Píter", 1444.44, "692.698.170-16", 1),
("Mariana", 2000.00, "090.414.970-64", 2),
("Sélço", 1894.05, "558.215.420-57", 2),
("Lurdes", 2052.54, "209.641.620-59", 2),
("Daniela", 1473.04, "183.434.320-88", 1),
("Luana", 1432.52, "107.970.800-66", 1),
("Carlos", 2031.73, "954.722.330-54", 2),
("Lucas", 1999.69, "568.774.250-65", 2),
("Manuela", 2034.68, "633.496.180-22", 2),
("Neusa", 2503.81, "459.159.230-89", 3), #16
("Roberto", 2536.95, "806.181.570-26", 3), #17
("Fernando", 2022.23, "897.775.970-61", 2),
("Otávio", 1450.00, "594.958.540-24", 1),
("Lucas", 2520.11, "411.579.300-77", 3) #20
;

insert into autor(nacionalidade_autor, nome_autor)
values
("ITA", "Leonardo da Vinci"),
("EUA", "Jackson Pollock"),
("FRA", "Éduoard Manet"),
("FRA", "Claude Monet"),
("ESP", "Pablo Picasso"),
("ITA", "Michelangelo"),
("BRA", "Tarsila do Amaral"),
("BRA", "Aleijadinho"),
("BRA", "Vik Muniz"),
("COL", "Fernando Botero"),
("ITA", "Donatello"),
("AUS", "Ron Mueck"),
("HOL", "Vincent Van Gogh"),
("HOL", "Frans Post"),
("ESP", "Salvador Dalí"),
("ESP", "Joan Miró"),
("ARG", "Emílio Pettoruti"),
("JAP", "Katsushika Hokusai"),
("BEL", "René Magritte"),
("ALE", "Rudolf Belling");

insert into tipo_obra(desc_tipo_obra)
values
("Pintura"),
("Escultura")
;

insert into obra(ano_obra, titu_obra, desc_estilo_obra, cod_autor, cod_tipo_obra)
values
(1503, "Mona Lisa", "renascentista", 1, 1),
(1928, "Abaporu", "modernista", 7, 1),
(1964, "O Filho do Homem", "surrealista", 19, 1),
(1908, "San Giorgino Maggiore", "impressionista", 4, 1),
(1650, "Cachoeira de Paulo Afonso", "paisagista", 14, 1),
(1889, "A Noite Estrelada", "modernista", 13, 1),
(1937, "Guernica", "surrealista", 5, 1),
(1922, "La Granja","naïf", 16, 1),
(1952, "Convergencce", "abstrata", 2, 1),
(1961, "Farfalla", "abstrata", 17, 1),
(1931, "A Persistência da Memória", "surrealista", 15, 1),
(1481, "Capela sistina", "afresco", 6, 1),
(1831, "A Grande Onda de Kanagawa", "gravura", 18, 1),
(1863, "Olympia", "impressionista", 3, 1),
(1978, "Mona Lisa (releitura)", "naïf", 10, 1),
(1996, "Sugar Children: Valicia Bathes in Sunday Clothes", "fotografia", 9, 1)
;

insert into obra(ano_obra, titu_obra, peso_obra, material_obra, cod_autor, cod_tipo_obra)
values
(1972, "Schuttblume", 330.00, "madeira", 20, 2),
(2005, "In bed", 1000.00, "argila & silicone", 12, 2),
(1440, "David", 6000.00, "mármore", 11, 2),
(1771, "Igreja de São Francisco de Assis (Ouro Preto)", 500000.00, "madeira & pedra", 8, 2)
;

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

insert into materia_prima(qtd_est_mat, nome_mat_prima)
values
(7164, "argila"),
(5123, "madeira"),
(1764, "cera"),
(36234, "tinta"),
(1826, "pedra"),
(39421, "óleo"),
(21922, "aquarela"),
(7810, "ferro"),
(1542, "bronze"),
(3128, "cobre"),
(8349, "gesso"),
(2133, "silicone"),
(3991, "mármore"),
(5312, "carvão"),
(4830, "grafite"),
(2022, "alumínio"),
(5076, "plástico"),
(248, "ouro"),	
(7777, "barro"),
(2048, "resina")
;

insert into manutencao(data_termi_mnt, custo_mnt, data_ini_mnt, desc_mnt, cod_obra, func_id_funcionario)
values
("2021-10-30", 5123.12, "2021-09-04", "Restaurar", 1, 2),
("2022-04-01", 1421.53, "2022-03-23", "Conservar", 2, 3),
("2022-02-14", 4325.13, "2022-01-26", "Identificar", 3, 16),
("2015-11-23", 3289.41, "2013-09-29", "Restaurar", 4, 17),
("2020-05-17", 4011.69, "2020-04-11", "Restaurar", 5, 20),
("2022-03-16", 2376.15, "2022-02-27", "Restaurar", 6, 2),
("2022-05-07", 1874.64, "2022-05-01", "Identificar", 7, 3),
("2022-09-11", 9382.73, "2022-04-15", "Restaurar", 8, 16),
("2022-10-29", 7421.42, "2022-06-28", "Identificar", 9, 17),
("2022-08-30", 8712.30, "2022-04-04", "Restaurar", 10, 20),
("2022-03-01", 5312.51, "2022-01-01", "Restaurar", 11, 2 ),
("2022-05-24", 3962.37, "2022-03-05", "Conservar", 12, 3),
("2022-02-28", 7311.11, "2021-10-12", "Restaurar", 13, 16),
("2022-04-04", 5656.56, "2022-01-05", "Restaurar", 14, 17),
("2022-01-11", 1234.56, "2021-12-10", "Restaurar", 15, 20),
("2022-11-22", 3566.94, "2022-08-15", "Conservar", 16, 2),
("2022-07-09", 2564.33, "2022-05-21", "Restaurar", 17, 3),
("2022-06-11", 4682.16, "2022-02-15", "Identificar", 18, 16),
("2022-12-24", 9732.12, "2022-02-10", "Resturar", 19, 17),
("2022-05-12", 5000.00, "2021-12-12", "Restaurar", 20, 20)
; 
insert into manu_mat(Campo_1, Campo_2, qtd_mat_mnt)
values
(1, 20, "231 resinas"),
(2, 19, "633 barros"),
(3, 18, "57 ouros"),
(4, 17, "164 plásticos"),
(5, 16, "76 alumínios"),
(6, 15, "210 grafietes"),
(7, 14, "241 carvões"),
(8, 13, "187 mármores"),
(9, 12, "99 silicones"),
(10, 11, "500 gessos"),
(11, 10, "162 cobres"),
(12, 9, "81 bronzes"),
(13, 8, "255 ferros"),
(14, 7, "1005 aquarelas"),
(15, 6, "2560 óleos"),
(16, 5, "173 pedras"),
(17, 4, "1046 tintas"),
(18, 3, "120 ceras"),
(19, 2, "231 madeiras"),
(20, 1, "412 argilas")
;

insert into salao(num_salao, andar_museu, salao)
values
(101, 1, "S101"),
(102, 1, "S102"),
(103, 1, "S103"),
(104, 1, "S104"),
(105, 1, "S105"),
(201, 2, "S201"),
(202, 2, "S202"),
(203, 2, "S203"),
(204, 2, "S204"),
(205, 2, "S205"),
(301, 3, "S301"),
(302, 3, "S302"),
(303, 3, "S303"),
(304, 3, "S304"),
(305, 3, "S305"),
(401, 4, "S401"),
(402, 4, "S402"),
(403, 4, "S403"),
(404, 4, "S404"),
(405, 4, "S405")
;

insert into salao_obra(salao_cod_salao, obra_cod_obra, posicao_salao)
values
(1, 20, "primeiro andar, primeira esquerda"),
(2, 19, "primeiro andar, primeira direita"),
(3, 18, "primeiro andar, segunda esquerda"),
(4, 17, "primeiro andar, segunda direita"),
(5, 16, "primeiro andar, última porta"),
(6, 15, "segundo andar, primeira esquerda"),
(7, 14, "segundo andar, primeira direita"),
(8, 13, "segundo andar, segunda esquerda"),
(9, 12, "segundo andar, segunda direita"),
(10, 11, "segundo andar, última porta"),
(11, 10, "terceiro andar, primeira esquerda"),
(12, 9, "terceiro andar, primeira direita"),
(13, 8, "terceiro andar, segunda esquerda"),
(14, 7, "terceiro andar, segunda direita"),
(15, 6, "terceiro andar, última porta"),
(16, 5, "quarto andar, primeira esquerda"),
(17, 4, "quarto andar, primeira direita"),
(18, 3, "quarto andar, segunda esquerda"),
(19, 2, "quarto andar, segunda direita"),
(20, 1, "quarto andar, última porta")
;

# 1. CRUC que retorne: nome_funcionario, cpf_funcionario, tipo_funcionario, salario_funcionario, de todos os funcionários cadastrados na entidade funcionario.

select nome_funcionario, cpf_funcionario, salario_funcionario, tipo_funcionario
from funcionario, tipo_funcionario
where funcionario.cod_tipo_funcionario = tipo_funcionario.cod_tipo_funcionario;

# 2.CRUC que retorne: título da obra, ano da obra, nome autor, nacionalidade do autor, descrição estilo da obra, para as obras do tipo pintura.

select titu_obra, ano_obra, nome_autor, nacionalidade_autor, desc_estilo_obra as estilo_obra
from obra, autor, tipo_obra
where obra.cod_autor = autor.cod_autor and
obra.cod_tipo_obra = tipo_obra.cod_tipo_obra and
tipo_obra.cod_tipo_obra = 1;

# 3. CRUC que retorne: custo manutenção, data início manutenção, data término manutenção, descrição da manutenção, de todas as manutenções cadastradas.

select custo_mnt, data_ini_mnt, data_termi_mnt, desc_mnt
from manutencao;

# 4. CRUC que retorne: nome matéria prima, quantidade da matéria prima na manutenção, descrição da manutenção, custo da manutenção, título obra, ano obra, nome funcionário responsável pela manutenção, filtrando pelo nome do autor da obra.

select autor.nome_autor, materia_prima.nome_mat_prima, manu_mat.qtd_mat_mnt, manutencao.desc_mnt, manutencao.custo_mnt, obra.titu_obra, obra.ano_obra, funcionario.nome_funcionario
from materia_prima, manutencao, manu_mat, obra, funcionario, autor
where materia_prima.cod_mat_prima = manu_mat.campo_2
and manu_mat.campo_1 = manutencao.mnt_obra
and obra.cod_obra = manutencao.cod_obra
and autor.cod_autor = obra.cod_autor
and funcionario.id_funcionario = manutencao.func_id_funcionario
#group by autor.cod_autor
and autor.nome_autor = "Claude Monet"
;

select * from autor;

# 5. CRUC que retorne: título obra e o cálculo do custo total da manutenção agrupando por título da obra. (Considerar a soma de todas as manutenções de cada obra)

select obra.titu_obra, sum(custo_mnt)
from obra, manutencao
where obra.cod_obra = manutencao.cod_obra
group by obra.titu_obra
;

# 6. CRUC que retorne: hora entrada, hora saída, data atividade, filtrando pelo número do salão.

select hora_entrada, hora_saida, data_atividade
from atividade, obra, salao, salao_obra
where atividade.ob_cod_obra = obra.cod_obra
and obra.cod_obra = salao_obra.obra_cod_obra
and salao_obra.salao_cod_salao = salao.cod_salao
and salao.num_salao = 101 #Filtro
;
select num_salao from salao;

# 7. CRUC que retorne: nacionalidade do autor, ano obra, título obra, descrição estilo obra, filtrando pelo tipo da obra.

select nacionalidade_autor, ano_obra, titu_obra, desc_estilo_obra
from autor, obra, tipo_obra
where autor.cod_autor = obra.cod_autor
and tipo_obra.cod_tipo_obra = obra.cod_tipo_obra
#and tipo_obra.desc_tipo_obra = "Escultura"
and tipo_obra.desc_tipo_obra = "Pintura"
; 

# 8. CRUC que retorne: quantidade de obras agrupando pela descrição do tipo de cada obra.

select tipo_obra.desc_tipo_obra as "tipo_obra", count(obra.cod_obra) as "qtd_obras"
from obra, tipo_obra
where obra.cod_tipo_obra = tipo_obra.cod_tipo_obra
group by tipo_obra.cod_tipo_obra;
;

# 9. CRUC que retorne: quantidade de obras expostas, agrupando pelo andar do museu.

select salao.andar_museu, count(obra.cod_obra)
from salao, salao_obra, obra
where obra.cod_obra = salao_obra.obra_cod_obra
and salao_obra.salao_cod_salao = salao.cod_salao
group by salao.andar_museu
; 

# 10. CRUC que retorne: número salão, andar museu, salão, descrição estilo obra, título obra, ano obra, nome autor, filtrando pela posição do salão.

select salao.salao, salao.num_salao, salao.andar_museu, obra.desc_estilo_obra, obra.titu_obra, obra.ano_obra, autor.nome_autor
from salao, obra, autor, salao_obra
where salao.cod_salao = salao_obra.salao_cod_salao
and obra.cod_obra = salao_obra.obra_cod_obra
and autor.cod_autor = obra.cod_autor
group by salao.salao
;

CREATE DATABASE clinica_medica;

use clinica_medica;

CREATE TABLE MEDICO(
 CRM INT PRIMARY KEY,
 NOME VARCHAR(50) NOT NULL,
 EMAIL VARCHAR(20) NOT NULL,
 TELEFONE INT UNIQUE,
 DATA_NASC DATE,
 ESPECIALIZACAO VARCHAR(25) 
 CHECK (ESPECIALIZACAO IN ('CARDIOLOGISTA', 'NUTRICIONISTA'))
);

CREATE TABLE PACIENTE(
    ID int primary key,
    CPF int unique,
    Nome varchar(100),
    Endereco varchar (75),
    Telefone int unique,
    Tipo_Exame varchar(25) 
    check (Tipo_Exame in ('laboratorial', 'clinico'))
);

CREATE TABLE CONSULTA (
    ID_MEDICO INT NOT NULL,
    ID_PACIENTE INT NOT NULL,
    FOREIGN KEY (ID_MEDICO) REFERENCES MEDICO(CRM),
    FOREIGN KEY (ID_PACIENTE) REFERENCES PACIENTE(ID), 
    DATA_CONSULT DATE NOT NULL,
    VALOR DOUBLE NOT NULL,
    TIPO_PAG VARCHAR(20) UNIQUE
);

CREATE TABLE EXAME (
    ID_MEDICO INT NOT NULL,
    ID_PACIENTE INT NOT NULL,
    FOREIGN KEY (ID_MEDICO)
        REFERENCES MEDICO (CRM),
    FOREIGN KEY (ID_PACIENTE)
        REFERENCES PACIENTE (ID),
    DATA_EXAME DATE,
    HORARIO TIME,
    VALOR DOUBLE NOT NULL,
    TIPO_PAG VARCHAR(20) UNIQUE,
    TIPO_EXAME VARCHAR(50) UNIQUE
);


insert into PACIENTE (CPF,Nome,Endereco,Telefone,Tipo_Exame)
values 
(12345678901, 'Maria Silva', 'Rua das Flores, 120', 11988887777, 'laboratorial'),
(98765432100, 'João Pereira', 'Av. Brasil, 450', 11999990000, 'clinico'),
(45678912355, 'Ana Sousa', 'Rua Central, 55', 11977776666, 'laboratorial'),
(11223344556, 'Carlos Menezes', 'Rua Paraná, 300', '11966665555', 'clinico'),
(22334455667, 'Fernanda Ribeiro', 'Av. Paulista, 2000', 11955554444, 'clinico'),
(33445566778, 'Lucas Andrade', 'Rua Bela Vista, 89', 11944443333, 'laboratorial');


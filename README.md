CREATE DATABASE clinica_medica;
USE clinica_medica;

CREATE TABLE MEDICO (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    crm VARCHAR(20) UNIQUE NOT NULL,
    especialidade VARCHAR(50) NOT NULL
        CHECK (especialidade IN ('Cardiologia', 'Dermatologia', 'Ortopedia', 'Pediatria'))
);

CREATE TABLE PACIENTE (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    data_nascimento DATE NOT NULL,
    telefone VARCHAR(20)
);

CREATE TABLE CONSULTA (
    id INT AUTO_INCREMENT PRIMARY KEY,
    data_consulta DATE NOT NULL,
    valor DECIMAL(10,2) NOT NULL,
    medico_id INT NOT NULL,
    paciente_id INT NOT NULL,
    FOREIGN KEY (medico_id) REFERENCES MEDICO(id),
    FOREIGN KEY (paciente_id) REFERENCES PACIENTE(id)
);

CREATE TABLE EXAME (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome_exame VARCHAR(100) NOT NULL,
    paciente_id INT NOT NULL,
    FOREIGN KEY (paciente_id) REFERENCES PACIENTE(id)
);

INSERT INTO MEDICO (nome, crm, especialidade) VALUES
('Dr. Arnaldo Silva', 'CRM-123', 'Cardiologia'),
('Dra. Beatriz Souza', 'CRM-456', 'Dermatologia'),
('Dr. Carlos Alberto', 'CRM-789', 'Cardiologia');

INSERT INTO PACIENTE (nome, cpf, data_nascimento, telefone) VALUES
('Marcos Oliveira', '111.111.111-11', '1995-05-10', '(11) 9999-9999'),
('Ana Paula', '222.222.222-22', '2005-08-15', '(11) 8888-8888'),
('Ricardo Santos', '333.333.333-33', '1980-01-20', '(11) 7777-7777'),
('Luciana Lima', '444.444.444-44', '2010-12-30', '(11) 6666-6666'),
('Fernando Vaz', '555.555.555-55', '1990-03-25', '(11) 5555-5555');

INSERT INTO CONSULTA (data_consulta, valor, medico_id, paciente_id) VALUES
('2024-03-01', 250.00, 1, 1),
('2024-03-02', 300.00, 2, 2),
('2024-03-05', 200.00, 1, 4),
('2024-03-10', 350.00, 3, 5);

DELETE FROM PACIENTE
WHERE id = 3;

UPDATE PACIENTE
SET telefone = '(11) 91234-5678'
WHERE id = 2;

SELECT * FROM PACIENTE;

SELECT nome, especialidade
FROM MEDICO;

SELECT *
FROM CONSULTA
WHERE id = 1;

SELECT *
FROM PACIENTE
WHERE data_nascimento > '2000-12-31';

SELECT *
FROM MEDICO
WHERE especialidade = 'Cardiologia';

SELECT COUNT(*) AS total_pacientes
FROM PACIENTE;

SELECT MIN(data_consulta) AS consulta_mais_antiga
FROM CONSULTA;

SELECT AVG(valor) AS media_valor_consultas
FROM CONSULTA;

SELECT *
FROM PACIENTE
ORDER BY nome;

SELECT medico_id, COUNT(*) AS total_consultas
FROM CONSULTA
GROUP BY medico_id;

SELECT PACIENTE.nome, CONSULTA.data_consulta
FROM PACIENTE
INNER JOIN CONSULTA ON PACIENTE.id = CONSULTA.paciente_id;

SELECT MEDICO.nome AS medico, MEDICO.especialidade, PACIENTE.nome AS paciente
FROM CONSULTA
INNER JOIN MEDICO ON CONSULTA.medico_id = MEDICO.id
INNER JOIN PACIENTE ON CONSULTA.paciente_id = PACIENTE.id;

SELECT MEDICO.nome, CONSULTA.data_consulta
FROM MEDICO
LEFT JOIN CONSULTA ON MEDICO.id = CONSULTA.medico_id;


CREATE DATABASE biblioteca_online;
USE biblioteca_online;


CREATE TABLE usuario (
    id_usuario INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telefone VARCHAR(20),
    nome_usuario VARCHAR(50) UNIQUE NOT NULL,
    senha VARCHAR(255) NOT NULL,
    tipo ENUM('Administrador','Usuário') DEFAULT 'Usuário'
);


CREATE TABLE categoria (
    id_categoria INT AUTO_INCREMENT PRIMARY KEY,
    nome_categoria VARCHAR(100) NOT NULL,
    descricao TEXT
);


CREATE TABLE livro (
    id_livro INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(200) NOT NULL,
    autor VARCHAR(150) NOT NULL,
    resumo TEXT,
    id_categoria INT NOT NULL,
    status ENUM('Disponível','Emprestado','Reservado') DEFAULT 'Disponível',
    FOREIGN KEY(id_categoria) REFERENCES categoria(id_categoria)
);


CREATE TABLE emprestimo (
    id_emprestimo INT AUTO_INCREMENT PRIMARY KEY,
    id_usuario INT NOT NULL,
    id_livro INT NOT NULL,
    data_emprestimo DATE NOT NULL,
    data_prevista DATE NOT NULL,
    data_devolucao DATE,
    status ENUM('Ativo','Finalizado','Atrasado') DEFAULT 'Ativo',
    FOREIGN KEY(id_usuario) REFERENCES usuario(id_usuario),
    FOREIGN KEY(id_livro) REFERENCES livro(id_livro)
);


CREATE TABLE devolucao (
    id_devolucao INT AUTO_INCREMENT PRIMARY KEY,
    id_emprestimo INT UNIQUE NOT NULL,
    data_devolucao DATE NOT NULL,
    multa DECIMAL(10,2) DEFAULT 0.00,
    observacoes TEXT,
    FOREIGN KEY(id_emprestimo) REFERENCES emprestimo(id_emprestimo)
);


CREATE TABLE reserva (
    id_reserva INT AUTO_INCREMENT PRIMARY KEY,
    id_usuario INT NOT NULL,
    id_livro INT NOT NULL,
    data_reserva DATE NOT NULL,
    status ENUM('Ativa','Cancelada','Efetivada') DEFAULT 'Ativa',
    FOREIGN KEY(id_usuario) REFERENCES usuario(id_usuario),
    FOREIGN KEY(id_livro) REFERENCES livro(id_livro)
);


INSERT INTO usuario (nome, email, telefone, nome_usuario, senha, tipo)
VALUES
('João Pereira', 'joao@example.com', '11999990001', 'joaop', 'senha123', 'Usuário'),
('Maria Silva', 'maria@example.com', '11999990002', 'mariasilva', 'senha123', 'Usuário'),
('Carlos Almeida', 'carlos@example.com', '11999990003', 'carlosadm', 'admin123', 'Administrador');


INSERT INTO categoria (nome_categoria, descricao)
VALUES
('Tecnologia', 'Livros sobre informática e tecnologia'),
('Literatura', 'Livros clássicos e modernos de literatura'),
('História', 'Livros sobre fatos históricos e civilizações');


INSERT INTO livro (titulo, autor, resumo, id_categoria, status)
VALUES
('O Programador Pragmático', 'Andrew Hunt', 'Boas práticas em desenvolvimento', 1, 'Disponível'),
('Dom Quixote', 'Miguel de Cervantes', 'Um clássico da literatura mundial', 2, 'Disponível'),
('A Segunda Guerra Mundial', 'Anthony Beevor', 'Relato completo do conflito', 3, 'Disponível');


INSERT INTO emprestimo (id_usuario, id_livro, data_emprestimo, data_prevista, status)
VALUES
(1, 2, '2025-10-15', '2025-10-30', 'Ativo'),
(2, 1, '2025-10-10', '2025-10-25', 'Atrasado');


UPDATE livro SET status='Emprestado' WHERE id_livro IN (1,2);


INSERT INTO devolucao (id_emprestimo, data_devolucao, multa, observacoes)
VALUES
(2, '2025-10-28', 5.00, 'Devolução com atraso');


INSERT INTO reserva (id_usuario, id_livro, data_reserva, status)
VALUES
(1, 3, '2025-10-19', 'Ativa'),
(2, 2, '2025-10-20', 'Ativa');


-- 1) Listar usuários
SELECT * FROM usuario;

-- 2) Listar livros com categorias
SELECT l.id_livro, l.titulo, l.autor, c.nome_categoria, l.status
FROM livro l
JOIN categoria c ON l.id_categoria = c.id_categoria;

-- 3) Histórico de empréstimos
SELECT e.id_emprestimo, u.nome AS usuario, l.titulo AS livro,
       e.data_emprestimo, e.data_prevista, e.status
FROM emprestimo e
JOIN usuario u ON e.id_usuario = u.id_usuario
JOIN livro l ON e.id_livro = l.id_livro;

-- 4) Devoluções
SELECT d.id_devolucao, u.nome AS usuario, l.titulo AS livro,
       d.data_devolucao, d.multa
FROM devolucao d
JOIN emprestimo e ON d.id_emprestimo = e.id_emprestimo
JOIN usuario u ON e.id_usuario = u.id_usuario
JOIN livro l ON e.id_livro = l.id_livro;

-- 5) Livros disponíveis
SELECT titulo, autor FROM livro WHERE status = 'Disponível';

-- 6) Reservas
SELECT r.id_reserva, u.nome AS usuario, l.titulo AS livro, r.data_reserva, r.status
FROM reserva r
JOIN usuario u ON r.id_usuario = u.id_usuario
JOIN livro l ON r.id_livro = l.id_livro;

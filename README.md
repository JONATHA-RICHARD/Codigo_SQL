-- Tabela Curso
CREATE TABLE Curso (
    curso_id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome_curso VARCHAR(100) NOT NULL,
    codigo_curso VARCHAR(10) UNIQUE NOT NULL,
    duracao INT NOT NULL, -- duração em anos
    ementa TEXT
);

-- Tabela Disciplina
CREATE TABLE Disciplina (
    disciplina_id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome_disciplina VARCHAR(100) NOT NULL,
    codigo_disciplina VARCHAR(10) UNIQUE NOT NULL,
    carga_horaria INT NOT NULL -- carga horária em horas
);

-- Tabela Professor
CREATE TABLE Professor (
    professor_id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome_completo VARCHAR(100) NOT NULL,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    formacao_academica VARCHAR(100),
    carga_horaria INT NOT NULL -- carga horária semanal
);

-- Tabela Aluno
CREATE TABLE Aluno (
    aluno_id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome_completo VARCHAR(100) NOT NULL,
    numero_matricula VARCHAR(20) UNIQUE NOT NULL,
    data_nascimento DATE NOT NULL,
    curso_id INT NOT NULL,
    status_matricula TEXT CHECK( status_matricula IN ('ativo', 'inativo') ),
    FOREIGN KEY (curso_id) REFERENCES Curso(curso_id)
);

-- Tabela Turma
CREATE TABLE Turma (
    turma_id INTEGER PRIMARY KEY AUTOINCREMENT,
    disciplina_id INT NOT NULL,
    professor_id INT NOT NULL,
    horario_aula VARCHAR(50),
    sala_aula VARCHAR(20),
    FOREIGN KEY (disciplina_id) REFERENCES Disciplina(disciplina_id),
    FOREIGN KEY (professor_id) REFERENCES Professor(professor_id)
);

-- Tabela Aluno_Turma (Relacionamento entre Aluno e Turma)
CREATE TABLE Aluno_Turma (
    aluno_id INT NOT NULL,
    turma_id INT NOT NULL,
    nota DECIMAL(4,2),
    PRIMARY KEY (aluno_id, turma_id),
    FOREIGN KEY (aluno_id) REFERENCES Aluno(aluno_id) ON DELETE CASCADE,
    FOREIGN KEY (turma_id) REFERENCES Turma(turma_id) ON DELETE CASCADE
);

-- Tabela Log_Alteracoes (Controle de alterações nos dados)
CREATE TABLE Log_Alteracoes (
    log_id INTEGER PRIMARY KEY AUTOINCREMENT,
    usuario VARCHAR(50) NOT NULL,
    alteracao TEXT NOT NULL,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    tabela_alterada VARCHAR(50) NOT NULL
);

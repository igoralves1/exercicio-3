# exercicio-3

CREATE TABLE IF NOT EXISTS disciplinas(
	numdisp serial not null,
	nome varchar(90),
	quantcredito int,
	CONSTRAINT disciplinas_pkey PRIMARY KEY (numdisp)
);

CREATE TABLE IF NOT EXISTS cursos(
	numcurso serial not null,
	totalcreditos int,
	nome varchar(90),
	
	CONSTRAINT cursos_pkey PRIMARY KEY (numcurso)

);

CREATE TABLE IF NOT EXISTS professores(
	numprof serial not null,
	nome varchar(90),
	areapesquisa varchar(30),
	
	CONSTRAINT professores_pkey PRIMARY KEY (numprof)
);

CREATE TABLE alunos(
	numaluno serial not null,
	nome varchar(90),
	endereço varchar(255),
	cidade varchar (60),
	telefone varchar (15),
	
	CONSTRAINT alunos_pkey PRIMARY KEY (NUMALUNO)

);

CREATE TABLE IF NOT EXISTS matricula(
	curso int,
	aluno int,
	
	CONSTRAINT matricula_pkey PRIMARY KEY (curso, aluno),
	
	CONSTRAINT curso_fkey FOREIGN KEY (curso) REFERENCES cursos(numcurso),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno)


);

CREATE TABLE aula(
	semestre int,
	nota int,
	aluno int,
	professor int,
	disciplina int REFERENCES disciplinas(numdisp),
	
	CONSTRAINT aula_pkey PRIMARY KEY (semestre,nota),
	
	CONSTRAINT aluno_fkey FOREIGN KEY (aluno) REFERENCES alunos(numaluno),
	CONSTRAINT professor_fkey FOREIGN KEY (professor) REFERENCES professores (numprof)

);

CREATE TABLE contem(
	id SERIAL NOT NULL,
	idcurso int,
	iddisciplinas int,
	
	
	CONSTRAINT contem_pkey PRIMARY KEY (id),
	
	CONSTRAINT curso_fkey FOREIGN KEY (idcurso) REFERENCES cursos(numcurso),
	CONSTRAINT disciplina_fkey FOREIGN KEY (iddisciplinas) REFERENCES disciplinas(numdisp)

);

INSERT INTO cursos(totalcreditos, nome) VALUES (80, 'Ciencia_computacao'), (80, 'Sistemas_informacao'), (70, 'Matematica'); 
INSERT INTO cursos(totalcreditos, nome) VALUES (60, 'História');

INSERT INTO alunos(nome, endereço, cidade, telefone) VALUES ('Marcos João Casanova ', 'Rua da torre', 'Cascais', '9519-6262'), ('Ailton Castro','Rua da Amargura', 'Timbucutu', '9999-6666'), ('Edvaldo Carlos Silva', ' av. Joana Angélica', 'Salvador', '2345-4496'), ('Juvenal', 'av. da abolição', 'Redenção', '4444-2222');

INSERT INTO disciplinas (nome, quantcredito) values('calculo numerico',6),('banco de dados', 4),('Engenharia da computação',4),('teoria geral da administraçao',4),('História Antiga', 4), ('História das artes', 4);

INSERT INTO professores(nome, areapesquisa) VALUES (' Ramon Travanti', 'calculo numerico'), (' Marcos Salvador','teoria geral da administraçao'), ('Juk', ' Banco de Dados'), (' Ramon Travanti', ' Engenharia de Software'), (' Abgair ', 'calculo numerico');


--respondido 5
create view questao5_CERTA(curso,numcurso, disciplina)
AS
SELECT DISTINCT C.nome, C.numcurso, D.nome FROM cursos C, disciplinas D, contem T
WHERE C.numcurso = 1
ORDER BY c.NOME ;

--respondida 6
create view questao6_CERTA(curso, disciplina)
AS
SELECT DISTINCT C.nome, D.nome FROM cursos C, disciplinas D, contem T
WHERE D.numdisp = 1
ORDER BY D.nome;

CREATE VIEW visao_professor_aluno (numaluno, numprofessor)
AS
SELECT A.numaluno, P.numprofessor FROM alunos A, professores P
WHERE A.numaluno = P.professor
ORDER BY A.numaluno;

CREATE VIEW visao_professor_aluno_nomes (numaluno, numprofessor, aluno, professor)
AS
SELECT A.numaluno,A.nome, P.numprof,P.nome  FROM alunos A, professores P
WHERE A.numaluno = P.numprof
ORDER BY A.numaluno;




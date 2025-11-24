# SoftLab

SoftLab é um sistema de gestão de alunos e projetos desenvolvido em Python, com interface gráfica em Tkinter e banco de dados SQLite.  
Ele foi pensado para apoiar um Laboratório Maker ou espaço similar, permitindo cadastro de alunos, controle de projetos e materiais usados, com perfis de administrador e aluno.

---

## Visão geral

O sistema oferece um painel principal com vários botões, onde é possível:

- cadastrar novos alunos
- fazer login como administrador ou aluno
- listar alunos e filtrar por instituição
- cadastrar projetos vinculados a cada aluno
- registrar os materiais usados em cada projeto
- consultar informações de alunos e projetos
- editar dados do aluno logado
- remover projetos e alunos
- limpar completamente o banco de dados (apenas administrador)
- ouvir música ambiente enquanto usa o sistema, com opção de pausar ou retomar

O banco `softlab.db` é criado automaticamente na primeira execução.

---

## Funcionalidades principais

### Autenticação e perfis

- Login como administrador  
  - usuário fixo: `Admin`  
  - senha fixa: `pe-de-moleque`  

- Login como aluno  
  - por instituição  
  - por matrícula  
  - validação de senha pelo banco de dados  

- Logout com confirmação  
- Recuperação de senha de aluno (somente após login de administrador)

### Gestão de alunos

- Cadastro de aluno com:
  - instituição
  - nome
  - e-mail
  - matrícula
  - data de nascimento (usada para calcular idade)
  - sexo
  - senha com confirmação

- Validações:
  - matrícula deve ser numérica
  - nome deve conter apenas letras
  - datas inválidas são tratadas com erro

- Listagem de alunos:
  - lista geral, ordenada por nome
  - listagem por instituição

- Edição de dados do aluno logado:
  - nome
  - e-mail
  - data de nascimento
  - sexo

- Remoção de aluno:
  - remove aluno, projetos associados e materiais relacionados

### Gestão de projetos

Cada projeto pertence a um aluno (por matrícula) e pode ter vários materiais associados.

O aluno logado pode:

- cadastrar novos projetos, informando:
  - nome do projeto
  - descrição
  - lista de materiais (separados por vírgula)

- listar seus projetos
- visualizar detalhes de cada projeto:
  - nome
  - descrição
  - lista de materiais cadastrados

- remover um ou mais projetos pela interface de seleção múltipla, com remoção dos respectivos materiais

### Banco de dados

O sistema usa SQLite, com três tabelas principais:

- `alunos`
- `projetos`
- `materiais`

Há também a opção de o administrador limpar todo o banco de dados, incluindo:

- dados de alunos
- projetos
- materiais
- reinício da sequência de IDs de projetos e materiais

### Interface gráfica

- Interface principal em Tkinter, com botões organizados em um frame central
- Janela principal com logo do projeto
- Várias janelas secundárias (`Toplevel`) para:
  - registro
  - login
  - alteração de dados
  - cadastro de projetos
  - remoção de projetos
  - listagem por instituição

### Música de fundo

- Reprodução em loop de um arquivo de áudio (`./src/music/contato.mp3`) usando `pygame.mixer`
- Botão para pausar e retomar a música

---

## Tecnologias utilizadas

- Python 3.x
- Tkinter
- SQLite3
- Pygame
- Pillow (PIL)
- Módulo `datetime` da biblioteca padrão

---

## Estrutura do projeto

Um possível layout de pastas para o SoftLab é:

```text
SOFTLAB/
├── src/
│   ├── img/
│   │   └── logo.png
│   └── music/
│       └── contato.mp3
├── venv/                 # ambiente virtual (opcional)
├── softlab.db            # banco SQLite gerado automaticamente
├── SoftLab.py            # código principal
├── requirements.txt
└── README.md
````

Certifique-se de que o `logo.png` e o arquivo de música estejam nos caminhos esperados pelo código:

* `./src/img/logo.png`
* `./src/music/contato.mp3`

---

## Como executar

### 1. Clonar o repositório

```bash
git clone https://github.com/cidade-felipe/softlab.git
cd softlab
```

### 2. Criar ambiente virtual (opcional)

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / macOS
.\.venv\Scripts\activate    # Windows
```

### 3. Instalar dependências

Se você já tiver um `requirements.txt`, use:

```bash
pip install -r requirements.txt
```

Caso contrário, certifique-se de instalar pelo menos:

```bash
pip install pygame pillow
```

Tkinter e sqlite3 costumam vir junto com a instalação padrão do Python em muitas distribuições.

### 4. Executar o SoftLab

```bash
python SoftLab.py
```

A janela principal será aberta, já com a música de fundo e o menu de opções.

---

## Fluxo sugerido de uso

1. Fazer login como administrador

   * usuário `Admin`
   * senha `pe-de-moleque`

2. Cadastrar um aluno em "REGISTRE-SE"

3. Fazer logout

4. Fazer login como aluno, usando instituição, matrícula e senha cadastradas

5. Cadastrar projetos, listar projetos e visualizar materiais

6. Explorar funções de alteração de dados, remoção de projetos e remoção de aluno

7. Quando necessário, limpar o banco de dados pelo menu de administrador

---

## Melhorias futuras

Algumas ideias de evolução para o SoftLab:

* Separar o código em múltiplos módulos para organização por responsabilidade
* Adicionar validações mais completas de e-mail e senha
* Criar relatórios simples de projetos por instituição
* Implementar exportação de dados para CSV ou PDF
* Tornar configuráveis o usuário e senha de administrador
* Internacionalizar a interface para outros idiomas

---

## Autores

Projeto desenvolvido por:

* Felipe Cidade Soares
* Ivy Oliveira dos Reis
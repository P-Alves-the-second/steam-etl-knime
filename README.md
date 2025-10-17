# 🎮 Steam ETL - KNIME Project

**Disciplina:** Integração de Sistemas de Informação  
**Curso:** Licenciatura em Engenharia de Sistemas Informáticos  
**Ano Letivo:** 2025/2026  

Este projeto tem como objetivo demonstrar um processo completo de **ETL (Extract, Transform, Load)** utilizando a ferramenta **KNIME Analytics Platform**, com integração à **Steam Web API** e a uma **base de dados Microsoft SQL Server**.

---

## 🧭 Descrição Geral

O workflow implementa um processo de integração de dados que recolhe informações sobre utilizadores e jogos da Steam, realiza transformações e limpeza, e carrega os resultados em uma base de dados relacional.  
Por fim, é feita a visualização e análise dos dados, incluindo:

- Valor estimado da conta (soma dos preços dos jogos possuídos)  
- Tempo total de jogo por utilizador (em horas)  
- Gêneros mais jogados e jogos mais populares entre os utilizadores  

O sistema também inclui um **módulo de logs** e suporte a **envio automático de emails** com as informações do perfil do utilizador.

---

## ⚙️ Funcionalidades Principais

- 🔍 **Extração** de dados via API pública da Steam (`ISteamApps`, `IPlayerService`, etc.)
- 🔄 **Transformação** e normalização dos dados (remoção de nulos, parsing de JSON, split e join de tabelas)
- 💾 **Carga** em uma base de dados SQL Server (`SteamDB`)
- 🧩 **Controle de duplicados** (merge inteligente de gêneros e jogos)
- 🧮 **Conversão automática de moedas** para Euro
- 🧰 **Sistema de logs**: grava o número de linhas processadas, rejeitadas e salvas
- 📧 **Envio de emails automáticos** aos utilizadores com resumo do perfil
- 📊 **Dashboard** final com estatísticas agregadas e indicadores de conta

---

## 🧱 Estrutura do Projeto
```
knime-workspace/
│
├── resources/                  # (fora do repositório Git!)
│   ├── apikey.txt              # Contém a chave Steam Web API
│   ├── steam_users.txt         # Contém SteamID e email de cada utilizador
│   └── ...
│
└── KNIME_project/              # Diretório do projeto (este é o repositório Git)
    ├── workflow.knime          # Ficheiro principal do fluxo ETL
    ├── README.md               # Este ficheiro
    ├── .gitignore
    └── (outros ficheiros KNIME)
```

---

## 📄 Arquivos de Configuração

Crie a pasta `resources` dentro do diretório knime-workspace (acima do projeto) e adicione os seguintes ficheiros:

### 🔑 `apikey.txt`
Contém apenas a **Steam API Key** em texto simples:
```
12123ASDASDASFDAF112
```

### 👥 `steam_users.txt`
Contém os **SteamIDs** e os **emails** dos utilizadores a serem processados:
```
76561324213123122,abc@gmail.com
76346232421334252,dfg@gmail.com
```


---

## 🧩 Configuração dos Nós

### 🔹 Microsoft SQL Server Connector
Deve ser configurado manualmente antes da execução:
- **Database URL:** `jdbc:sqlserver://localhost:1433;databaseName=SteamDB`
- **Username:** `<seu_usuario>`
- **Password:** `<sua_senha>`

### 🔹 Send Email Node
Configure o servidor SMTP do seu provedor de email:
- **Host:** `smtp.gmail.com`
- **Port:** `587`
- **Username / Password:** suas credenciais
- **Use StartTLS:** ✅

> ⚠️ Por motivos de segurança, esses campos devem permanecer **vazios** no repositório GitHub.  
> Configure-os localmente antes de executar o workflow.

---

## 🧮 Execução do Workflow

1. **Abra o KNIME** e importe o projeto (`File → Import KNIME Workflow...`)
2. Verifique se os ficheiros `apikey.txt` e `steam_users.txt` estão na pasta `resources/`
3. Configure os nós de conexão (SQL e Email)
4. Caso precise execute os nós de criação ou drop da base de dados
5. Execute o workflow completo certificando-se que os nós de criação e drop da BD estão desconectados(Ctrl + A → F7) 

---

## 📊 Dashboard e Resultados

O projeto inclui dashboards com:
- Tabela de utilizadores e resumo do perfil
- Valor estimado da conta (€)
- Total de horas jogadas
- Jogos mais jogados
- Gêneros mais jogados (por quantidade de jogos, não tempo)
- Logs do processo de ETL

---

## 🧾 Sistema de Logs

Durante a execução, o processo gera uma pasta de logs no mesmo diretório da chave da api e steam_users com informações como:
- Data e hora da execução  
- Nome do nó ou etapa  
- Número de linhas processadas, rejeitadas e salvas  
- Mensagens de erro (se existirem)

---

## 🧠 Tecnologias Utilizadas

- KNIME Analytics Platform  
- Microsoft SQL Server  
- Steam Web API  
- JSON & XML Parsing  
- SMTP (Email automation)

---

## 👨‍💻 Autoria

**Aluno:** Pedro Alves  
**Disciplina:** Integração de Sistemas de Informação  
**Docentes:** Luís Ferreira & Óscar Ribeiro  
**Ano Letivo:** 2025/2026  


## 📚 Referências

- [Steam Web API Documentation](https://developer.valvesoftware.com/wiki/Steam_Web_API)
- [KNIME Documentation](https://docs.knime.com/)
- [Microsoft SQL Server JDBC](https://learn.microsoft.com/en-us/sql/connect/jdbc/)
- [Python Regular Expressions](https://docs.python.org/3/library/re.html)

---


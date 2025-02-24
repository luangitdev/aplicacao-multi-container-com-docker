# **Aplicação Multi-Container com Docker**

![GitHub](https://img.shields.io/badge/Docker-Supported-blue) ![Python](https://img.shields.io/badge/Python-3.9-blue) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13-blue)

Este projeto demonstra como criar uma aplicação Flask que se conecta a um banco de dados PostgreSQL usando múltiplos containers Docker. A aplicação é configurada com `docker-compose` para facilitar a execução e o gerenciamento dos serviços.

---

## **Índice**

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Tecnologias Utilizadas](#tecnologias-utilizadas)
3. [Pré-requisitos](#pré-requisitos)
4. [Estrutura do Projeto](#estrutura-do-projeto)
5. [Passo a Passo para Executar o Projeto](#passo-a-passo-para-executar-o-projeto)
6. [Como Funciona a Aplicação](#como-funciona-a-aplicação)
7. [Contribuição](#contribuição)
8. [Licença](#licença)

---

## **Descrição do Projeto**

Este projeto consiste em uma aplicação Flask simples que se conecta a um banco de dados PostgreSQL. A aplicação é dividida em dois serviços principais:

- **Serviço Web**: Uma API Flask que exibe uma mensagem confirmando a conexão com o banco de dados.
- **Serviço de Banco de Dados**: Um container PostgreSQL que armazena os dados da aplicação.

Ambos os serviços são gerenciados pelo `docker-compose`, permitindo que você inicie e pare todos os componentes de forma fácil e rápida.

---

## **Tecnologias Utilizadas**

- **Python 3.9**: Linguagem de programação utilizada para desenvolver a aplicação Flask.
- **Flask**: Framework web minimalista para Python.
- **PostgreSQL**: Sistema de gerenciamento de banco de dados relacional.
- **Docker**: Plataforma usada para criar, implantar e executar a aplicação em containers.
- **Docker Compose**: Ferramenta para orquestrar múltiplos containers.

---

## **Pré-requisitos**

Antes de iniciar, certifique-se de ter as seguintes ferramentas instaladas:

- **Docker**: Para executar os containers.
- **Docker Compose**: Para gerenciar os serviços do projeto.
- **Git**: Para clonar o repositório (opcional).

Você pode verificar se o Docker está instalado corretamente executando:

```bash
docker --version
docker-compose --version
```

---

## **Estrutura do Projeto**

Aqui está a estrutura básica do projeto:

```
aplicacao-multi-container-com-docker/
│
├── app.py              # Código da aplicação Flask
├── requirements.txt    # Dependências Python
├── Dockerfile          # Instruções para criar a imagem do serviço web
├── docker-compose.yml  # Configuração do Docker Compose
└── README.md           # Documentação do projeto
```

---

## **Passo a Passo para Executar o Projeto**

### **Passo 1: Clone o Repositório**

Clone este repositório para sua máquina local:

```bash
git clone https://github.com/seu-usuario/aplicacao-multi-container-com-docker.git
cd aplicacao-multi-container-com-docker
```

### **Passo 2: Construa e Inicie os Containers**

Use o `docker-compose` para construir as imagens e iniciar os containers:

```bash
docker-compose up --build
```

- O comando `--build` força a reconstrução das imagens, garantindo que as últimas alterações sejam aplicadas.

### **Passo 3: Acesse a Aplicação**

Abra o navegador e acesse:

```
http://localhost:5000
```

Você deverá ver a mensagem:

```
Conectado ao Banco de Dados!
```

### **Passo 4: Pare os Containers**

Para parar os containers, pressione `CTRL+C` no terminal onde o `docker-compose` está sendo executado.

Ou, para executar os containers em segundo plano:

```bash
docker-compose up -d
```

Para parar os containers em segundo plano:

```bash
docker-compose down
```

---

## **Como Funciona a Aplicação**

### **Código da Aplicação Flask**

O arquivo `app.py` contém a lógica da aplicação Flask. Ele tenta conectar ao banco de dados PostgreSQL e retorna uma mensagem indicando se a conexão foi bem-sucedida.

```python
import psycopg2
from flask import Flask

app = Flask(__name__)

def connect_db():
    return psycopg2.connect(
        dbname="mydb",
        user="user",
        password="pass",
        host="db"
    )

@app.route("/")
def home():
    conn = connect_db()
    return "Conectado ao Banco de Dados!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

### **Configuração do Docker Compose**

O arquivo `docker-compose.yml` define os dois serviços:

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - db
  
  db:
    image: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
```

- **Serviço `web`**:
  - Constrói a imagem a partir do `Dockerfile`.
  - Expõe a porta `5000` para acessar a aplicação Flask.
  - Depende do serviço `db` e aguarda até que o banco de dados esteja pronto.

- **Serviço `db`**:
  - Usa a imagem oficial do PostgreSQL.
  - Define variáveis de ambiente para configurar o usuário, senha e banco de dados.

---

## **Contribuição**

Contribuições são bem-vindas! Siga estas etapas:

1. Faça um fork deste repositório.
2. Crie uma nova branch:
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
3. Faça suas alterações e commit:
   ```bash
   git commit -m "Adiciona nova funcionalidade"
   ```
4. Envie suas alterações:
   ```bash
   git push origin feature/nova-funcionalidade
   ```
5. Abra um Pull Request neste repositório.

---

## **Licença**

Este projeto está licenciado sob a **MIT License**. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## **Contato**

Se tiver dúvidas ou sugestões, entre em contato:

- **Nome**: Luan Castro
- **Email**: luandecastrosilva@gmail.com
- **LinkedIn**: [linkedin.com/in/luancastrosilva](https://www.linkedin.com/in/luancastrosilva/)
- **GitHub**: [github.com/luangitdev](https://github.com/luangitdev)

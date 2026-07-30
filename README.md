# 💈 Barber Shop API

API REST para gerenciamento de **clientes e agendamentos de uma barbearia**, desenvolvida com Java e Spring Boot.

> Projeto baseado em uma API de agendamento e preparado para evoluir para um sistema completo de barbearia, com cadastro de clientes, agenda, serviços, barbeiros e uma interface web.

---

## ✨ Sobre o projeto

O **Barber Shop API** é o backend responsável por controlar os dados e regras de negócio de uma barbearia.

Atualmente, o projeto possui:

- 👤 Cadastro de clientes
- ✏️ Atualização de clientes
- 🔎 Consulta de cliente por ID
- 📋 Listagem de clientes
- 🗑️ Exclusão de clientes
- 📅 Criação de agendamentos
- 🗓️ Consulta de agendamentos por mês
- ❌ Cancelamento de agendamentos
- ✅ Validação dos dados recebidos pela API
- 🚫 Validação de e-mail e telefone duplicados
- 🚫 Controle de conflitos de horários
- 🗃️ Banco de dados PostgreSQL
- 🔄 Versionamento do banco com Flyway
- 🐳 Ambiente de desenvolvimento com Docker

---

## 🛠️ Tecnologias

| Tecnologia | Utilização |
|---|---|
| ☕ Java 21 | Linguagem principal |
| 🌱 Spring Boot 3.4.2 | Framework da aplicação |
| 🌐 Spring Web | Criação da API REST |
| 🗄️ Spring Data JPA | Persistência de dados |
| 🐘 PostgreSQL | Banco de dados |
| 🔄 Flyway | Migrations do banco |
| 🧩 MapStruct | Mapeamento entre objetos |
| 🏷️ Lombok | Redução de código boilerplate |
| 🐳 Docker | Ambiente de desenvolvimento |
| 🐘 Gradle | Build e gerenciamento de dependências |

---

## 📁 Estrutura do projeto

```text
barber-shop-api/
├── src/
│   └── main/
│       ├── java/br/com/dio/barbershopui/
│       │   ├── config/
│       │   ├── controller/
│       │   │   ├── request/
│       │   │   └── response/
│       │   ├── entity/
│       │   ├── exception/
│       │   ├── exceptionhandler/
│       │   ├── mapper/
│       │   ├── repository/
│       │   └── service/
│       │       ├── impl/
│       │       └── query/
│       │
│       └── resources/
│           ├── db/migration/
│           ├── application.yml
│           └── application-dev.yml
│
├── Dockerfile
├── docker-compose.yml
├── build.gradle.kts
├── gradlew
└── README.md
```

A aplicação segue uma separação por responsabilidades:

```text
Controller
   ↓
Service
   ↓
Repository
   ↓
PostgreSQL
```

Os `Mapper`, `Request`, `Response` e `ExceptionHandler` ajudam a manter a API organizada e desacoplada das entidades do banco.

---

# 🚀 Como executar

## Pré-requisitos

Você pode executar o projeto utilizando:

- Java 21
- Docker + Docker Compose

Para a forma mais simples, recomendamos utilizar Docker.

---

## 🐳 Executando com Docker

Na raiz do projeto:

```bash
docker network create barber-shop-net
```

Depois:

```bash
docker compose up --build
```

A API ficará disponível em:

```text
http://localhost:8080
```

O PostgreSQL ficará disponível em:

```text
localhost:5432
```

### Banco de dados

```text
Database: barber-shop-api
User:     barber-shop-api
Password: barber-shop-api
Host:     localhost
Port:     5432
```

---

# 🔌 Endpoints

## 👤 Clientes

### Criar cliente

```http
POST /clients
```

Exemplo:

```json
{
  "name": "João Silva",
  "email": "joao@email.com",
  "phone": "81999999999"
}
```

---

### Listar clientes

```http
GET /clients
```

---

### Buscar cliente

```http
GET /clients/{id}
```

Exemplo:

```http
GET /clients/1
```

---

### Atualizar cliente

```http
PUT /clients/{id}
```

Exemplo:

```json
{
  "name": "João da Silva",
  "email": "joao@email.com",
  "phone": "81999999999"
}
```

---

### Excluir cliente

```http
DELETE /clients/{id}
```

---

# 📅 Agendamentos

### Criar agendamento

```http
POST /schedules
```

Exemplo:

```json
{
  "startAt": "2026-07-30T14:00:00Z",
  "endAt": "2026-07-30T15:00:00Z",
  "clientId": 1
}
```

---

### Consultar agenda do mês

```http
GET /schedules/{year}/{month}
```

Exemplo:

```http
GET /schedules/2026/7
```

---

### Cancelar agendamento

```http
DELETE /schedules/{id}
```

---

# 🧠 Regras atuais

O backend já possui algumas regras importantes:

- E-mail do cliente não pode ser duplicado.
- Telefone do cliente não pode ser duplicado.
- Cliente precisa existir para receber um agendamento.
- Um intervalo de horário não pode ser cadastrado novamente.
- Os campos obrigatórios são validados pela API.
- O e-mail precisa possuir formato válido.
- O banco utiliza migrations do Flyway.
- O Hibernate trabalha com `ddl-auto: validate`, evitando que a aplicação altere automaticamente a estrutura do banco.

---

# 🗃️ Migrations

As migrations ficam em:

```text
src/main/resources/db/migration/
```

Atualmente existem migrations para:

- criação da tabela de clientes;
- criação da tabela de agendamentos.

Para gerar uma nova migration:

```bash
./gradlew generateFlywayMigrationFile -PmigrationName=nome_da_migration
```

No Windows:

```bash
gradlew.bat generateFlywayMigrationFile -PmigrationName=nome_da_migration
```

---

# 🧪 Build e testes

Para gerar o build:

```bash
./gradlew build
```

No Windows:

```bash
gradlew.bat build
```

Para executar os testes:

```bash
./gradlew test
```

---

# 🌐 CORS

A API possui configuração de CORS para permitir integração com uma aplicação frontend.

Atualmente, durante o desenvolvimento, a configuração permite requisições de diferentes origens.

Isso facilita a integração futura com:

- React
- Next.js
- Vue
- Angular
- HTML/CSS/JavaScript

---

# 💈 Próxima evolução do projeto

A ideia é transformar esta API em um sistema completo de gerenciamento para barbearia.

### 📌 Gestão

- Dashboard
- Clientes
- Barbeiros
- Serviços
- Agendamentos
- Horários disponíveis
- Histórico de atendimentos

### 💇 Serviços

Exemplos:

- Corte masculino
- Corte + barba
- Barba
- Sobrancelha
- Acabamento
- Platinado
- Outros serviços personalizados

### 📅 Agenda

- Visualização diária
- Visualização semanal
- Visualização mensal
- Horários disponíveis
- Horários ocupados
- Cancelamento
- Reagendamento
- Bloqueio de horários

### 👤 Clientes

- Cadastro
- Edição
- Exclusão
- Histórico de agendamentos
- Telefone
- E-mail
- Observações

### 📊 Dashboard

Futuramente podemos adicionar indicadores como:

```text
Agendamentos hoje
Clientes cadastrados
Atendimentos realizados
Horários disponíveis
Faturamento
Serviços mais realizados
```

---

# 🖥️ Interface web

> ⚠️ Atualmente este repositório é **somente o backend/API**. Ele não possui uma interface gráfica de barbearia.

A API pode ser acessada diretamente pelo navegador através dos endpoints `GET`, mas para visualizar e utilizar o sistema como uma aplicação real será necessário criar um **frontend**.

A próxima etapa recomendada é criar uma interface web moderna conectada a esta API.

Uma possível estrutura será:

```text
                 ┌─────────────────────┐
                 │   FRONTEND WEB      │
                 │   Barber Shop       │
                 └──────────┬──────────┘
                            │
                         HTTP/JSON
                            │
                 ┌──────────▼──────────┐
                 │   SPRING BOOT API   │
                 │      :8080          │
                 └──────────┬──────────┘
                            │
                         JPA/Hibernate
                            │
                 ┌──────────▼──────────┐
                 │     PostgreSQL      │
                 │       :5432         │
                 └─────────────────────┘
```

---

# 🎯 Objetivo

Evoluir o projeto de uma API de agendamento para uma plataforma completa de gestão de barbearia, mantendo uma arquitetura organizada, escalável e preparada para receber uma interface web profissional.

---

## 👨‍💻 Desenvolvimento

Projeto desenvolvido para estudos e evolução prática em:

- Java
- Spring Boot
- APIs REST
- PostgreSQL
- Docker
- Arquitetura de software
- Integração Frontend + Backend

---

## 📄 Licença

Este projeto é destinado a fins educacionais e de desenvolvimento.

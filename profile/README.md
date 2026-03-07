# 🎬 ClipToZip - Sistema de Processamento de Vídeos

![Logo ClipToZip](/docs/cliptozip.png)

> **Projeto de Pós-Graduação em Arquitetura de Software - Hackathon FIAP**
> 
> Sistema distribuído para processamento de vídeos com extração de frames, construído com arquitetura de microsserviços e boas práticas de engenharia de software.

---

## 📋 Sobre o Projeto

O **ClipToZip** é um ecossistema completo de processamento de vídeos que permite aos usuários fazer upload de arquivos de vídeo e receber automaticamente um arquivo ZIP contendo os frames extraídos. O projeto foi desenvolvido como trabalho de conclusão do curso de Pós-Graduação em Arquitetura de Software, aplicando padrões e práticas modernas de desenvolvimento.

### ✨ Funcionalidades

- 🔐 **Autenticação e Autorização** com JWT
- 📤 **Upload de Vídeos** para armazenamento em nuvem
- ⚙️ **Processamento Assíncrono** de vídeos
- 🖼️ **Extração Automática de Frames**
- 📦 **Geração de ZIP** com imagens processadas
- 📧 **Notificações por E-mail** (sucesso/falha)
- 📊 **Acompanhamento de Status** em tempo real

### 📹 Vídeo de demonstração

- **[Clique aqui](https://www.youtube.com/watch?v=_FwtyjIWAEA)**

---

## 🏗️ Arquitetura

O sistema segue uma arquitetura de **microsserviços** escalável e desacoplada, utilizando mensageria para comunicação assíncrona e armazenamento distribuído.

### Diagrama de Arquitetura

![Desenho de Arquitetura](/docs/Desenho%20de%20Arquitetura.png)

### Fluxo Funcional

![Desenho Funcional](/docs/Desenho%20Funcional.png)

### Rascunho Inicial

![Rascunho de Arquitetura](/docs/Rascunho%20de%20Arquitetura.png)

---

## 🔧 Microsserviços

### 1️⃣ Serviço de Autenticação
**Tecnologias:** Java 21 | Spring Boot 3

**Responsabilidades:**
- Cadastro de novos usuários
- Geração de tokens JWT
- Validação de tokens de acesso
- Gerenciamento de sessões

### 2️⃣ Serviço de Vídeo
**Tecnologias:** Java 17 | Spring Boot 4

**Responsabilidades:**
- Upload de vídeos para S3
- Publicação de mensagens na fila de processamento
- Persistência de registros no banco de dados
- Endpoints REST para consulta de status
- Disponibilização de links para download do ZIP

### 3️⃣ Processador de Vídeos
**Tecnologias:** Python | FastAPI

**Responsabilidades:**
- Consumo de mensagens da fila de processamento
- Download de vídeos do S3
- Extração de frames do vídeo
- Compactação das imagens em arquivo ZIP
- Upload do ZIP processado para S3
- Atualização do status no banco de dados
- Publicação na fila de notificações

### 4️⃣ Serviço de Notificação
**Tecnologias:** Java 17 | Spring Boot 3

**Responsabilidades:**
- Consumo de mensagens da fila de notificações
- Envio de e-mails de sucesso no processamento
- Envio de e-mails de erro/falha
- Templates personalizados de notificação

---

## 🗄️ Banco de Dados

O sistema utiliza **PostgreSQL** (via Amazon RDS) para armazenamento de dados persistentes e **Redis** (via Amazon ElastiCache) para cache e gerenciamento de sessões.

### Modelo de Dados

![Banco de dados](/docs/Banco%20de%20dados.png)

---

## ☁️ Infraestrutura AWS

A infraestrutura é totalmente provisionada na AWS utilizando **Terraform** e segue as melhores práticas de segurança e escalabilidade.

### Componentes Provisionados

#### 🌐 Infraestrutura Base
- **VPC** (Virtual Private Cloud)
- **Subnets** públicas e privadas
- **Internet Gateway**
- **NAT Gateway** com Elastic IP
- **Security Groups** configurados
- **RDS PostgreSQL** multi-AZ
- **ElastiCache Redis** cluster
- **S3 Buckets** para armazenamento de vídeos e ZIPs

#### ⚙️ Infraestrutura de Aplicação
- **Amazon EKS** (Kubernetes)
- **Node Groups** auto-scaling
- **Load Balancers**
- **Amazon SQS** para filas de mensagens
- **Amazon ECR** para armazenamento de imagens Docker

### Deployment

Todos os serviços são containerizados e orquestrados via **Kubernetes (EKS)**, permitindo:
- 🔄 Auto-scaling horizontal
- 🛡️ Alta disponibilidade
- 🚀 Deploy zero-downtime
- 📊 Monitoramento centralizado

---

## 🚀 CI/CD e Qualidade

### GitHub Actions
Todos os repositórios possuem pipelines automatizados que:
- ✅ Executam testes unitários e de integração
- 📊 Analisam cobertura de código (mínimo 80%)
- 🔍 Validam qualidade via **SonarQube**
- 🐳 Constroem imagens Docker
- 📦 Publicam imagens no Amazon ECR
- 🚀 Realizam deploy automático no EKS

### Qualidade de Código - SonarQube

Todos os serviços atendem aos critérios de qualidade estabelecidos:

#### Serviço de Autenticação
![Sonar Auth Service](/docs/sonar-authsvc.png)

#### Serviço de Vídeo
![Sonar Video Service](/docs/sonar-videosvc.png)

#### Processador de Vídeos
![Sonar Video Processor](/docs/sonar-videoprc.png)

#### Serviço de Notificação
![Sonar Notification Service](/docs/sonar-notification.png)

**Métricas garantidas:**
- ✅ Cobertura de testes ≥ 80%
- ✅ 0 vulnerabilidades de segurança críticas
- ✅ 0 bugs críticos
- ✅ Índice de manutenibilidade A

---

## 📦 Repositórios da Organização

| Repositório | Descrição | Tecnologias | Link  |
|-------------|-----------|-------------|-------|
| **hackaton-soat11-authsvc** | Serviço de Autenticação | Java 21, Spring Boot 3 | [link](https://github.com/ClipToZip/hackaton-soat11-authsvc) |
| **hackaton-soat11-videosvc** | Serviço de Upload e Gestão de Vídeos | Java 17, Spring Boot 4 | [link](https://github.com/ClipToZip/hackaton-soat11-videosvc) |
| **hackaton-soat11-videoprc** | Processador de Vídeos | Python, FastAPI | [link](https://github.com/ClipToZip/hackaton-soat11-videoprc) |
| **hackaton-soat11-notification** | Serviço de Notificações | Java 17, Spring Boot 3 | [link](https://github.com/ClipToZip/hackaton-soat11-notification) |
| **hackaton-soat11-infra** | Infraestrutura base AWS (Terraform) | Terraform, AWS | [link](https://github.com/ClipToZip/hackaton-soat11-infra) |
| **hackaton-soat11-k8s** | Cluster EKS e Deploy (Terraform) | Terraform, Kubernetes | [link](https://github.com/ClipToZip/hackaton-soat11-k8s) |

---

## 🎯 Padrões e Boas Práticas Aplicadas

### Arquitetura
- ✅ Arquitetura de Microsserviços
- ✅ Event-Driven Architecture
- ✅ API Gateway Pattern
- ✅ Database per Service
- ✅ Circuit Breaker Pattern

### Desenvolvimento
- ✅ Clean Architecture
- ✅ SOLID Principles
- ✅ RESTful API Design
- ✅ Twelve-Factor App
- ✅ GitFlow Workflow

### DevOps
- ✅ Infrastructure as Code (IaC)
- ✅ Continuous Integration/Deployment
- ✅ Containerização com Docker
- ✅ Orquestração com Kubernetes
- ✅ Gestão de Secrets

### Qualidade
- ✅ Test-Driven Development (TDD)
- ✅ Code Coverage ≥ 80%
- ✅ Static Code Analysis (SonarQube)
- ✅ Peer Code Review
- ✅ Documentação técnica

---

## 🛠️ Tecnologias Utilizadas

### Backend
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)

### Cloud & Infraestrutura
![AWS](https://img.shields.io/badge/Amazon_AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

### Banco de Dados
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

### CI/CD & Qualidade
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=for-the-badge&logo=sonarqube&logoColor=white)

---

## 👥 Autores - Grupo 13

| Nome | RM |
|------|------|
| **Fabiana Casagrande Costa** | RM362339 |
| **Felipe Costacurta Paruce** | RM364868 |
| **Rafael Fonseca Hermes Azevedo** | RM361445 |
| **Samuel Videira** | RM363405 |

---

## 📄 Licença

Este projeto foi desenvolvido como trabalho acadêmico para o curso de Pós-Graduação em Arquitetura de Software da FIAP.

---

<div align="center">

**Desenvolvido com ❤️ pelo Grupo 13**

**FIAP - Pós-Graduação em Arquitetura de Software | 2026**

</div>

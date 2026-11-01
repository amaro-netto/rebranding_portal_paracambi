# 🏛️ Gov Tech Stack

![Next.js](https://img.shields.io/badge/Next.js-black?style=for-the-badge&logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![Vite](https://img.shields.io/badge/Vite-%23646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-%23E0234E.svg?style=for-the-badge&logo=nestjs&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![pgvector](https://img.shields.io/badge/pgvector-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Alarik](https://img.shields.io/badge/Alarik-S3--compatible-FF6B35?style=for-the-badge&logo=amazons3&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![NGINX](https://img.shields.io/badge/NGINX-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![ZITADEL](https://img.shields.io/badge/ZITADEL-000000?style=for-the-badge&logo=go&logoColor=white)
![Segurança](https://img.shields.io/badge/Security-Zero_Trust-red?style=for-the-badge&logo=security)
![LGPD](https://img.shields.io/badge/Conformidade-LGPD-green?style=for-the-badge)
![Acessibilidade](https://img.shields.io/badge/Acessibilidade-VLibras%20%7C%20WCAG-blue?style=for-the-badge)

<p>&nbsp;</p>

### **Índice**

1. [📝 Visão Executiva do Projeto](#1--visão-executiva-do-projeto)
2. [⚙️ Arquitetura e DevSecOps](#2--arquitetura-e-devsecops)
3. [📁 Topologia e Módulos (Monorepo)](#3--topologia-e-módulos-monorepo)
4. [🔄 Fluxo de Dados e Rede](#4--fluxo-de-dados-e-rede)
5. [🚀 Módulos e Funcionalidades Core](#5--módulos-e-funcionalidades-core)
6. [🛡️ Governança, Segurança e LGPD](#6-️-governança-segurança-e-lgpd)
7. [💻 Guia de Implantação e Operação](#7--guia-de-implantação-e-operação)
8. [👥 Liderança Técnica](#8--liderança-técnica)

<p>&nbsp;</p>

## 1. 📝 Visão Executiva do Projeto

O **Gov Tech Stack** é uma plataforma unificada e conteinerizada, projetada para modernizar a presença digital e a operação interna de entidades governamentais. 

Longe de ser apenas um site institucional, trata-se de um ecossistema robusto que centraliza:
* **Portal de Transparência e Comunicação:** Atendimento ao cidadão com alta performance, indexação (SEO) e gestão de conteúdo dinâmica.
* **Gestão Pública (Backoffice):** Painéis administrativos focados em Gestão de Pessoas (RH), processamento de Folha de Pagamento e controle de documentação oficial.
* **Módulos Setoriais:** Como a vertical de Educação, acoplada ao mesmo ecossistema, mas com banco de dados lógico e API isolados.
* **Serviços ao Cidadão e Inteligência:** Ouvidoria automatizada com IA e comunicação de riscos (Defesa Civil).

Construída sobre o paradigma *Cloud Native*, a plataforma garante escalabilidade horizontal, alta disponibilidade e segurança por design, mitigando riscos de vazamento de dados e paradas de serviço.

---

## 2. ⚙️ Arquitetura e DevSecOps

A stack tecnológica foi selecionada com foco em engenharia de software de nível corporativo (Commercial-Grade), seguindo os princípios SOLID e Clean Architecture nas APIs:

* **Frontend (Cidadão / SEO):** Desenvolvido em **Next.js**. O uso de *Server-Side Rendering (SSR)* garante conformidade com os *Core Web Vitals* do Google. Totalmente **Mobile-First**, garantindo responsividade absoluta para todos os dispositivos e tamanhos de tela. Em conformidade com as exigências governamentais, possui **Acessibilidade Universal (WCAG 2.1 AA)**, incluindo navegação por teclado, alto contraste e integração nativa com **VLibras**.
* **Frontend (Gestão / Backoffice):** Desenvolvido em **React + Vite**. *Single Page Applications (SPAs)* garantem navegação ultra-rápida e sem recarregamentos para operadores de RH e finanças que lidam com formulários complexos.
* **Backend (Microsserviços):** **NestJS (Node.js)** com **Prisma ORM**. Arquitetura modular e tipagem estrita (TypeScript) para prevenção de erros em tempo de compilação.
* **Inteligência Artificial (IA):** Contêiner dedicado ao processamento de LLM (Large Language Models) e RAG (Retrieval-Augmented Generation), responsável por analisar documentos do portal e responder à ouvidoria.
* **Armazenamento de Dados:** **PostgreSQL**. Utiliza isolamento lógico por banco (hoje `bd_site`; novos módulos ganham o seu) para evitar que uma falha ou sobrecarga em um departamento afete o processamento de folha de pagamento de outro.
* **Soberania de Arquivos:** **MinIO (S3-Compatible)**. Armazenamento de PDFs, Diários Oficiais e documentos de transparência em infraestrutura própria.
* **Gestão de Identidade (IdP):** **ZITADEL**. Implementação de *Single Sign-On (SSO)* governamental. Preparado para futuras integrações de federação (ex: Gov.br, Active Directory).

---

## 3. 📁 Topologia e Módulos (Monorepo)

O ecossistema é orquestrado via `docker-compose` e dividido estruturalmente por domínios de negócio (Domain-Driven Design):

```text
/gov-tech-stack
├── domains/
│   ├── institucional/
│   │   ├── web-next/      # Next.js: portal público (conteúdo em src/data/*.json)
│   │   ├── web/           # React + Vite: CRM de notícias e usuários (/admin/)
│   │   └── api/           # NestJS + Prisma: notícias, login e usuários do CRM
│   └── ouvidoria/
│       └── ia/            # FastAPI: assistente da Ouvidoria (Gemini + pgvector)
├── infra/
│   ├── nginx/             # Gateway (nginx.conf = dev, nginx.prod.conf = produção)
│   ├── database/          # init.sql do Postgres
│   ├── backup/            # Backup diário do banco e das imagens
│   ├── scripts/           # Utilitários (ex.: treinar-ia.sh)
│   └── data/              # Dados do Postgres (fora do git)
├── docker-compose.yml       # Desenvolvimento
└── docker-compose.prod.yml  # Produção/homologação
```

---

## 4. 🔄 Fluxo de Dados e Rede

Para garantir a blindagem do banco de dados e das APIs, o projeto adota uma arquitetura de rede Zero-Trust (Rede fechada Docker `net_paracambi`):

1. **Borda (Cloudflare WAF):** Todo o tráfego da internet passa primeiro por um Web Application Firewall.
2. **Gateway (NGINX):** O contêiner `dev_gateway` atua como o **único ponto de entrada** da infraestrutura (Portas 80/443). Ele roteia o tráfego para os contêineres corretos (ex: `/api` -> `api_publica:3001`, `/admin/` -> CRM).
3. **Isolamento Interno:** Contêineres críticos como o PostgreSQL e o Zitadel não expõem portas para a internet. Eles só podem ser acessados internamente pelas APIs do NestJS aprovadas.
4. **IPS Automático:** O contêiner do **CrowdSec** monitora os logs do NGINX em tempo real. Se um bot tentar acesso de força bruta aos painéis de RH, o IP é banido instantaneamente na camada do Host.

---

## 5. 🚀 Módulos e Funcionalidades Core

### 🏛️ Módulo de Transparência e Portal
Site voltado ao cidadão, com foco em inclusão digital (VLibras) e performance.
* **Gestão de Notícias e Conteúdo Estático:** CMS próprio integrado ao painel de gestão corporativo. Permite a criação, edição e publicação rápida de informações institucionais dinâmicas, sem necessidade de intervenção técnica ou *deploy*.
* **Portal da Transparência:** Publicação de editais, leis e diários oficiais com indexação profunda.

### 🤖 Módulo de Ouvidoria Inteligente (IA)
Um contêiner dedicado à Inteligência Artificial atua como um concierge para o cidadão.
* **Leitura Dinâmica de Documentos:** A IA consome e processa os PDFs armazenados no MinIO (Leis, Editais, Diários Oficiais) e o próprio conteúdo do portal institucional.
* **Simplificação de Linguagem:** O modelo traduz o "juridiquês" ou textos complexos governamentais em respostas simples e diretas, respondendo dúvidas da população com alta precisão e linguagem acessível, 24/7.

### 🚨 Módulo de Defesa Civil e Alertas de Risco
Sistema crítico de utilidade pública focado na segurança da população.
* **Monitoramento e Previsão:** Integração com APIs meteorológicas para exibição da previsão do tempo atualizada em tempo real no portal.
* **Gestão de Alertas:** A partir do Painel de Gestão (Backoffice), os operadores da Defesa Civil podem disparar "Alertas Vermelhos". Isso aciona imediatamente *banners* de aviso no topo do site e notificações para os cidadãos sobre situações de risco, como chuvas intensas, enchentes ou desastres naturais.

### 💼 Módulo de Gestão (Core Business)
O coração administrativo do governo.
* **Gestão de Pessoas (RH):** Cadastro de servidores, progressão de carreira e controle de lotação.
* **Folha de Pagamento:** Motor de cálculo e auditoria financeira isolada em ambiente seguro.
* **Documentação Oficial:** Assinatura e tramitação eletrônica de documentos em conformidade com as leis de arquivística, armazenados com versionamento no MinIO.

### 🛡️ Módulo de Identidade Unificada
Login universal robusto para alunos e funcionários gerenciado pelo **ZITADEL**. O servidor público recebe um token JWT criptografado que dita seus níveis de permissão em todos os outros subsistemas da infraestrutura.

---

## 6. 🛡️ Governança, Segurança e LGPD

Este projeto atende rigorosamente aos padrões de Auditoria de TI:
* **Zero Hardcoded Secrets:** Nenhuma senha de banco ou chave de API reside no código. Tudo é injetado em tempo de execução via `.env` ou Secret Managers.
* **Auditoria de Logs:** O banco de dados preserva a rastreabilidade completa (quem acessou a folha de pagamento, quando e o que alterou).
* **Minimização de Dados (LGPD):** APIs implementadas com DTOs (*Data Transfer Objects*) estritos no NestJS, garantindo que o frontend só receba os dados necessários, mascarando dados sensíveis (PII) por padrão.
* **Disaster Recovery:** A infraestrutura conta com um contêiner *Sidecar* que realiza o backup automatizado dos bancos de dados e do storage (MinIO), empacotando e enviando para nuvem externa diariamente.

---

## 7. 💻 Guia de Implantação e Operação

### Pré-requisitos
* Servidor Linux (Ubuntu/Debian) com Kernel 5.4+
* Docker Engine (v24+) e Docker Compose (v2+)
* Min. 4GB RAM (Recomendado 8GB para produção total) e 50GB SSD.

### Passo 1: Clone e Configuração Segura
```bash
git clone [https://github.com/](https://github.com/)[org-governo]/gov-tech-stack.git
cd gov-tech-stack

# Geração do arquivo de variáveis de ambiente
# ATENÇÃO: Preencha com credenciais fortes antes de subir.
cp .env.example .env
```

### Passo 2: Inicialização da Infraestrutura
O orquestrador fará o build das imagens, instalará dependências e subirá os serviços na ordem correta.
```bash
docker-compose up -d --build
```

### Passo 3: Setup Automático e Verificação
O contêiner `storage_minio_setup` rodará um script temporário para provisionar os buckets iniciais do MinIO de forma autônoma. Monitore a saúde do ecossistema geral com:
```bash
docker-compose logs -f
```

*(Para execução local de desenvolvimento sem Docker, consulte o arquivo `README-DEV.md` dentro de cada domínio).*

---

## 8. 👥 Liderança Técnica
Arquitetura, DevOps e padronização mantidas por:
* **Amaro Netto Soluções** - *Desenvolvimento Full-Stack, Infraestrutura Cloud e Auditoria de Dados.*

> **"Segurança e Manutenibilidade precedem a Conveniência."** - *Protocolo Interno de Engenharia.*

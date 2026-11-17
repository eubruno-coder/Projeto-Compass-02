# ☁️ Projeto Compass 02 — WordPress em AWS

> Laboratório de arquitetura AWS para execução conteinerizada de WordPress com rede segmentada, banco gerenciado, armazenamento persistente, balanceamento e automação de infraestrutura.

[![Status](https://img.shields.io/badge/status-projeto%20acadêmico-blue)](#status)
[![Cloud](https://img.shields.io/badge/cloud-AWS-orange)](#arquitetura)
[![Containers](https://img.shields.io/badge/containers-Docker-2496ED)](#docker-e-wordpress)
[![OS](https://img.shields.io/badge/os-Ubuntu%2024.04-E95420)](#ec2)

---

## Sobre o projeto

O **Projeto Compass 02** documenta a construção de um ambiente AWS para hospedar uma aplicação WordPress de forma estruturada, utilizando serviços gerenciados e componentes de infraestrutura distribuídos em sub-redes públicas e privadas.

O objetivo principal foi praticar conceitos de **Cloud Computing, redes, segurança, armazenamento persistente, containers e alta disponibilidade**.

## Arquitetura

A solução utiliza, entre outros componentes:

- Amazon VPC
- Subnets públicas e privadas
- Security Groups
- Amazon EC2
- Amazon RDS / MySQL
- Amazon EFS
- Load Balancer
- NAT Gateway
- Docker / Docker Compose
- `user_data.sh`
- Launch Template

Conceitualmente:

```text
Internet
   │
   ▼
Load Balancer
   │
   ▼
EC2 / WordPress
   │       │
   │       └──────────► EFS
   │
   └──────────────────► RDS / MySQL

Subnets privadas
   │
   └──────────► NAT Gateway ──► Internet
```

## Componentes principais

### 1. VPC

A rede foi estruturada com **quatro subnets**, distribuídas entre zonas de disponibilidade, contemplando segmentos públicos e privados.

A separação busca reduzir a exposição direta dos recursos internos e organizar o fluxo de comunicação entre aplicação, banco e armazenamento.

### 2. Security Groups

Os grupos de segurança controlam a comunicação entre os componentes da arquitetura.

A proposta separa os recursos conforme sua função e restringe portas e origens de acesso de acordo com o fluxo necessário.

### 3. Amazon RDS

O RDS é utilizado como banco de dados gerenciado para o WordPress, com **MySQL** como mecanismo de banco.

A configuração deve utilizar credenciais próprias e nunca publicar senhas reais no repositório.

### 4. Amazon EFS

O EFS fornece armazenamento de arquivos persistente e compartilhado para os componentes que precisam acessar os arquivos da aplicação.

### 5. EC2

A aplicação é executada em instâncias EC2 baseadas em Ubuntu, com Docker como camada de execução dos containers.

### 6. Docker e WordPress

O Docker Compose organiza a execução da aplicação WordPress e sua comunicação com os serviços de persistência.

Arquivos auxiliares do projeto incluem `docker-compose.yaml` e `user_data.sh`.

### 7. Launch Template

O Launch Template padroniza parâmetros para criação de instâncias e serve como base para automatização da infraestrutura.

### 8. Load Balancer

O balanceador distribui o tráfego entre as instâncias disponíveis e permite trabalhar com verificações de saúde dos recursos.

### 9. NAT Gateway

O NAT Gateway permite que recursos em subnets privadas realizem conexões de saída para a internet sem necessariamente receberem conexões externas diretamente.

## Estrutura do projeto

```text
Projeto-Compass-02/
├── README.md
├── docker-compose.yaml
├── user_data.sh
└── Images/
    └── diagramas e capturas da implementação
```

Os arquivos e imagens documentam as etapas práticas realizadas durante o laboratório.

## Segurança

O projeto demonstra conceitos de segmentação de rede e controle de acesso, mas uma implementação real deve ser revisada antes de ser utilizada em produção.

Boas práticas importantes:

- nunca publicar chaves privadas;
- nunca versionar senhas reais;
- restringir Security Groups ao mínimo necessário;
- utilizar IAM com princípio do menor privilégio;
- proteger dados em trânsito e em repouso quando aplicável;
- revisar custos e exposição pública dos serviços;
- evitar credenciais diretamente em scripts versionados.

## Documentação

O README funciona como registro do laboratório e passo a passo da arquitetura construída. As capturas presentes no diretório `Images/` complementam a documentação visual.

## Objetivos de aprendizagem

- Estruturar uma VPC AWS;
- compreender subnets públicas e privadas;
- configurar Security Groups;
- utilizar RDS e EFS;
- executar WordPress com Docker;
- automatizar configuração via user data;
- trabalhar com Launch Templates;
- configurar balanceamento de tráfego;
- compreender o uso de NAT Gateway;
- documentar uma arquitetura Cloud.

## Roadmap

### V1 — Laboratório AWS

- [x] VPC
- [x] Subnets públicas e privadas
- [x] Security Groups
- [x] RDS
- [x] EFS
- [x] EC2
- [x] Docker / Docker Compose
- [x] Load Balancer
- [x] NAT Gateway
- [x] Launch Template
- [x] Documentação da implementação

### V2 — Maturidade técnica

- [ ] Infraestrutura como código
- [ ] Terraform ou CloudFormation
- [ ] Pipeline CI/CD
- [ ] Monitoramento com CloudWatch
- [ ] Estratégia formal de backup
- [ ] Gestão segura de secrets

## Status

📚 **Projeto acadêmico / laboratório técnico concluído e mantido como material de estudo.**

O foco do repositório é documentar a arquitetura e os conhecimentos adquiridos durante a implementação.

## Autor

Desenvolvido por **Bruno Silva** no contexto dos estudos e atividades relacionadas à formação em Cloud Computing.

GitHub: `eubruno-coder`

---

**Projeto:** Compass 02 — WordPress em AWS  
**Categoria:** Cloud / AWS / Infraestrutura  
**Status:** Laboratório técnico documentado

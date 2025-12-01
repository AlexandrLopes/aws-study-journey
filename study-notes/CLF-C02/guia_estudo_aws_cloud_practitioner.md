# Guia Estratégico de Estudos para a Certificação AWS Certified Cloud Practitioner

Este guia foi elaborado a partir de resumos de cursos preparatórios, focado nos quatro domínios de conhecimento da prova AWS Certified Cloud Practitioner. O objetivo é transformar suas anotações em um material de estudo estratégico, detalhado e bem estruturado.

A prova exige uma pontuação mínima de **700 em 1000 pontos** para aprovação. É importante notar que não há penalidade para respostas erradas, e é possível solicitar a prova em português com 30 minutos adicionais [1].

## Distribuição dos Domínios da Prova

A sua estratégia de estudo deve priorizar os domínios com maior peso na prova.

| Domínio | Porcentagem | Foco Estratégico |
| :--- | :--- | :--- |
| **Domínio 3: Tecnologia** | **33%** | Serviços de computação, armazenamento, banco de dados e rede. **Maior peso.** |
| **Domínio 1: Conceitos de Nuvem** | **26%** | Benefícios, modelos de implantação e infraestrutura global da AWS. |
| **Domínio 2: Segurança e Conformidade** | **25%** | Modelo de Responsabilidade Compartilhada, IAM e serviços de segurança. |
| **Domínio 4: Cobrança e Preços** | **16%** | Princípios de preços, suporte e ferramentas de gerenciamento de custos. |
| **Total** | **100%** | |

---

## Domínio 3: Tecnologia (33%)

Este é o domínio mais extenso e com maior peso. O foco é entender a **função** de cada serviço e o **caso de uso** ideal.

### 1. Serviços de Computação

| Serviço | Função Principal | Casos de Uso e Dicas |
| :--- | :--- | :--- |
| **Amazon EC2** (Elastic Compute Cloud) | Fornece capacidade computacional segura e redimensionável na nuvem (máquinas virtuais - instâncias). | **Instâncias = Servidores.** É o serviço base para IaaS (Infraestrutura como Serviço). |
| **EC2 Auto Scaling** | Adiciona ou remove automaticamente instâncias EC2 com base em condições definidas (ex: uso de CPU). | Garante a **disponibilidade** e otimiza custos. Tipos: **Dinâmico** (acompanha métrica) e **Preditivo** (usa Machine Learning). |
| **Elastic Load Balancing (ELB)** | Distribui o tráfego de entrada automaticamente entre várias instâncias EC2. | Atua como **ponto de contato único**. Realiza **Health Check** para enviar tráfego apenas para instâncias saudáveis. **Application Load Balancing (ALB)** trabalha na Camada 7 (aplicação). |
| **AWS Lambda** | Computação **Serverless** (sem servidor). Executa código em resposta a eventos (gatilhos). | Pague apenas pelo tempo de execução do código. Limites importantes: execução máxima de 15 minutos e memória máxima de 10 GB. |
| **Amazon ECS / EKS / Fargate** | Serviços de **Containers**. ECS e EKS (Kubernetes) orquestram containers. | **Fargate** é a opção **Serverless** para containers (não precisa gerenciar instâncias EC2 subjacentes). |

**Tipos de Instâncias EC2 (Estratégia de Preço):**
*   **On-Demand:** Pague pela capacidade por hora ou segundo. Ideal para cargas de trabalho imprevisíveis.
*   **Spot:** Capacidade não utilizada da AWS, com descontos de até 90%. Ideal para testes ou cargas de trabalho flexíveis que podem ser interrompidas (aviso de 2 minutos).
*   **Reservadas (Reserved Instances - RIs):** Reserva de capacidade por 1 a 3 anos. Oferece o maior desconto (até 72%) em troca de um compromisso de longo prazo.

### 2. Serviços de Armazenamento

É crucial diferenciar os três tipos principais de armazenamento:

| Serviço | Tipo de Armazenamento | Caso de Uso e Dicas |
| :--- | :--- | :--- |
| **Amazon S3** (Simple Storage Service) | **Objeto** (Buckets) | Armazenamento virtualmente ilimitado para qualquer tipo de dado (imagens, vídeos, backups). É altamente **durável** e suporta **controle de versão**. |
| **Amazon EBS** (Elastic Block Store) | **Bloco** (Volumes) | Discos de alto desempenho (SSD, HDD) anexados a uma única instância EC2. Se a instância for removida, o volume EBS é **persistente**. |
| **Amazon EFS** (Elastic File System) | **Arquivo** (Compartilhado) | Sistema de arquivos simples e escalável que pode ser **compartilhado** entre várias instâncias EC2 em diferentes Zonas de Disponibilidade. |

**Diferença-chave:** O EBS é para uma única instância (como um disco rígido local), enquanto o EFS permite que várias instâncias acessem o mesmo sistema de arquivos simultaneamente.

### 3. Serviços de Banco de Dados

| Serviço | Tipo | Características e Dicas |
| :--- | :--- | :--- |
| **Amazon RDS** (Relational Database Service) | **Relacional** (SQL) | Gerenciado pela AWS. Suporta Aurora, MySQL, PostgreSQL, etc. Use **Multi-AZ** para **alta disponibilidade** (failover automático) e **Réplicas de Leitura** para desafogar a instância principal em cargas de trabalho intensivas de leitura. |
| **Amazon DynamoDB** | **Não Relacional** (NoSQL - Chave-Valor/Documento) | Serviço **Serverless**. Desempenho de milissegundos de um dígito em qualquer escala. Ideal para aplicações móveis, jogos e web sem servidor. |
| **AWS DMS** (Database Migration Service) | Migração | Migra bancos de dados (relacionais e não relacionais) para a AWS com segurança, mantendo o banco de dados de origem operacional durante a migração. |
| **Outros (Palavras-chave):** | | **Redshift** (Data Warehouse), **DocumentDB** (MongoDB), **Neptune** (Grafo), **ElastiCache** (Cache), **DAX** (Acelerador DynamoDB). |

### 4. Redes e Entrega de Conteúdo

| Serviço | Função Principal | Dicas de Estudo |
| :--- | :--- | :--- |
| **Amazon VPC** (Virtual Private Cloud) | Rede virtual isolada e definida pelo usuário na AWS. | **Sub-redes** podem ser **Públicas** (acesso à Internet via Internet Gateway) ou **Privadas** (isoladas, para bancos de dados). |
| **Amazon Route 53** | Serviço de **DNS** (Sistema de Nomes de Domínio) altamente disponível e escalável. | Converte nomes de domínio em endereços IP. Roteia o tráfego para destinos íntegros. |
| **Amazon CloudFront** | Serviço de **CDN** (Content Delivery Network) global. | Usa **Locais de Borda (PoPs)** para armazenar cópias de conteúdo em cache, reduzindo a latência e melhorando a velocidade de entrega ao cliente. |
| **AWS Direct Connect** | Conexão de rede **DEDICADA** e privada entre o seu *datacenter on-premises* e a AWS. | Usado para reduzir custos de rede e aumentar a largura de banda em comparação com a Internet pública. |
| **AWS Transit Gateway** | Conecta suas VPCs e redes *on-premises* globalmente, simplificando o gerenciamento de rede. | |

**Segurança de Rede (VPC):**
*   **ACL de Rede (NACL):** Firewall virtual para a **Sub-rede**. É **Stateless** (precisa de regras de entrada e saída). Por padrão, a ACL padrão permite todo o tráfego.
*   **Grupo de Segurança (Security Group):** Firewall virtual para a **Instância EC2**. É **Stateful** (basta criar uma regra de entrada, a de saída é automática). Por padrão, nega todo o tráfego de entrada e permite todo o tráfego de saída.

---

## Domínio 2: Segurança e Conformidade (25%)

### 1. Modelo de Responsabilidade Compartilhada

Este é um conceito central e de alta incidência na prova.

> **AWS (A Nuvem):** Responsável pela **Segurança DA Nuvem** (infraestrutura global, hardware, software, rede, instalações).
>
> **Cliente (Na Nuvem):** Responsável pela **Segurança NA Nuvem** (dados, sistema operacional convidado, aplicações, configurações de segurança, Grupos de Segurança, ACLs).

### 2. Gerenciamento de Identidade e Acesso (IAM)

*   **AWS IAM (Identity and Access Management):** Controla o acesso aos serviços e recursos da AWS. Baseado no **Princípio do Menor Privilégio** (dar apenas as permissões necessárias).
*   **Usuário IAM:** Representa uma pessoa ou aplicação.
*   **Política IAM:** Documento JSON que define as permissões.
*   **Role IAM (Função):** Identidade que pode ser assumida temporariamente para conceder permissões a serviços ou usuários.

### 3. Serviços de Segurança

| Serviço | Função Principal |
| :--- | :--- |
| **AWS WAF** (Web Application Firewall) | Protege aplicações web e APIs contra explorações comuns da web (ex: injeção de SQL, XSS). |
| **AWS Shield** | Proteção contra ataques de **Negação de Serviço Distribuída (DDoS)**. |
| **Amazon GuardDuty** | Detecção inteligente de ameaças e monitoramento contínuo de atividades maliciosas. |
| **AWS KMS** (Key Management Service) | Ajuda a criar e gerenciar chaves de criptografia. |
| **Amazon Inspector** | Avaliações de segurança automatizadas em suas aplicações. |
| **AWS Organizations** | Consolida e gerencia várias contas AWS. Usa **SCPs (Service Control Policies)** para controlar centralmente as permissões em todas as contas. |
| **AWS Artifact** | Acesso sob demanda a relatórios de segurança e conformidade da AWS. |

---

## Domínio 1: Conceitos de Nuvem (26%)

### 1. Infraestrutura Global

*   **Região:** Localização geográfica física onde a AWS agrupa seus *datacenters*.
*   **Zona de Disponibilidade (AZ):** Um ou mais *datacenters* discretos com energia, rede e conectividade redundantes. **Cada Região deve ter no mínimo 3 AZs.**
*   **Locais de Borda (Edge Locations):** Usados pelo CloudFront para armazenar conteúdo em cache e reduzir a latência.
*   **Fatores de Seleção de Região:** Conformidade com requisitos legais/governança de dados e proximidade com os clientes.

### 2. Benefícios da Nuvem

*   **Economia de Custos:** Pague apenas pelo que usar (Pay-as-you-go), eliminação de gastos de capital (CapEx).
*   **Agilidade e Elasticidade:** Capacidade de escalar recursos para cima (scale up) e para baixo (scale down) rapidamente, acompanhando a demanda.
*   **Alta Disponibilidade e Tolerância a Falhas:** Uso de múltiplas AZs e Regiões.

---

## Domínio 4: Cobrança e Preços (16%)

### 1. Princípios de Preços

*   **Pay-as-you-go:** Pague apenas pelos serviços que consumir.
*   **Economia de Escala:** Quanto mais você usa, mais você economiza (descontos por volume).
*   **Free Tier:** Nível gratuito disponível por 12 meses para novos clientes.

### 2. Ferramentas de Gerenciamento de Custos

*   **AWS Budgets:** Permite definir limites para o uso e os custos. **Apenas informa**, não altera automaticamente os serviços.
*   **AWS Cost Explorer:** Visualiza e analisa seus custos e uso ao longo do tempo.
*   **AWS Trusted Advisor:** Conselheiro que analisa seu ambiente em cinco pilares, incluindo **Otimização de Custos** e **Limites de Serviços**.

### 3. Suporte

*   **Planos de Suporte:** Existem vários níveis (Basic, Developer, Business, Enterprise). O plano **Basic** é gratuito para todos os clientes [2].

---

## Dicas Finais para a Prova

1.  **Foco em Palavras-Chave:** A prova Cloud Practitioner é focada em **conceitos** e **casos de uso**.
    *   Se a pergunta envolve **Serverless** (sem gerenciar servidores), pense em **Lambda** ou **DynamoDB**.
    *   Se envolve **DDoS**, pense em **AWS Shield**.
    *   Se envolve **CDN** ou **baixa latência global**, pense em **CloudFront**.
    *   Se envolve **conexão dedicada** entre *on-premises* e AWS, pense em **Direct Connect**.
    *   Se envolve **segurança de aplicação web**, pense em **WAF**.
2.  **Recursos Adicionais:**
    *   Consulte os *whitepapers* oficiais da AWS, especialmente a **Visão Geral da AWS** [3] e **Como os Preços da AWS Funcionam** [4].
    *   Utilize o **AWS Skill Builder** e os **AWS Builder Labs** para prática [5] [6].

***

## Referências

[1] AWS Certified Cloud Practitioner: https://aws.amazon.com/pt/certification/certified-cloud-practitioner/
[2] Comparar planos de AWS Support: https://aws.amazon.com/premiumsupport/plans
[3] Visão Geral da AWS (Whitepaper): https://d1.awsstatic.com/whitepapers/aws-overview.pdf
[4] Como os Preços da AWS Funcionam (Whitepaper): https://docs.aws.amazon.com/whitepapers/latest/how-aws-pricing-works/welcome.html
[5] Preparação para prova (Skill Builder): https://aws.amazon.com/pt/certification/certification-prep/?ch=cta&cta=header&p=2
[6] AWS Builder Labs: https://aws.amazon.com/pt/training/digital/aws-builder-labs/

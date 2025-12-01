# 📘 AWS Cloud Practitioner (CLF-C02)

## 🏆 Domínio 3: Tecnologia (33%) - *Onde você ganha o jogo*

Este domínio cobre os serviços principais. Você precisa saber **o que é** e **quando usar**.

### 1. Computação (Compute)
* **Amazon EC2 (Elastic Compute Cloud):** Servidores virtuais. Você gerencia o sistema operacional (IaaS).
    * **Instâncias On-Demand:** Preço fixo, sem compromisso, flexível. (Ideal para: curto prazo, testes).
    * **Reserved Instances (Reservadas):** Contrato de 1 ou 3 anos. Desconto de até 72%. (Ideal para: uso constante, banco de dados).
    * **Spot Instances:** Capacidade ociosa da AWS. Desconto de até 90%. **Risco:** A AWS pode encerrar com aviso de **2 minutos**. (Ideal para: processamento em lote, tolerante a falhas).
    * **Dedicated Hosts:** Servidor físico dedicado a você (por licenças de software ou compliance).
* **Auto Scaling:** Aumenta (Scale Out) ou diminui (Scale In) a quantidade de instâncias EC2 automaticamente baseada em demanda (CPU, Rede). Garante elasticidade.
* **Elastic Load Balancer (ELB):** Distribui o tráfego de entrada entre várias instâncias EC2, containers ou zonas. Faz o *Health Check* (se a instância falhar, ele para de mandar tráfego para ela).
* **AWS Lambda:** **Serverless** (Sem servidor). Você sobe o código, define um gatilho (evento) e roda. Limite de 15 min. Paga por milissegundo de execução.
* **Amazon ECS & EKS:** Orquestração de Containers (Docker). ECS é o padrão AWS, EKS é para Kubernetes.
* **AWS Fargate:** É o "Serverless para Containers". Roda ECS ou EKS sem precisar gerenciar as instâncias EC2 por baixo.

### 2. Armazenamento (Storage)

* **Amazon S3 (Simple Storage Service):** Armazenamento de **Objetos** (arquivos, fotos, vídeos).
    * *Estrutura:* Buckets (baldes). Nome universalmente único.
    * *Classes:*
        * **Standard:** Acesso frequente.
        * **Standard-IA (Infrequent Access):** Acesso raro, mas precisa ser rápido quando solicitado.
        * **Glacier:** Arquivamento de longo prazo (barato, mas demora minutos/horas para recuperar).
        * **Intelligent-Tiering:** Move automaticamente os dados entre as classes para economizar dinheiro (Usa IA).
* **Amazon EBS (Elastic Block Store):** Armazenamento em **Bloco**. É o "HD/SSD" da EC2.
    * *Regra de Ouro:* Preso a **uma** Zona de Disponibilidade (AZ). Uma instância EC2 só pode montar um EBS por vez (geralmente). Se a instância morre, os dados persistem (diferente do Instance Store).
* **Amazon EFS (Elastic File System):** Armazenamento de **Arquivos** (Linux).
    * *Regra de Ouro:* Compartilhado. Várias EC2 podem acessar ao mesmo tempo. Multi-AZ.
* **Storage Gateway:** Conecta seu servidor físico (on-premise) ao armazenamento da nuvem (Híbrido).

### 3. Banco de Dados (Database)
* **Amazon RDS:** Relacional (SQL). Estruturado (Tabelas).
    * *Engines:* MySQL, PostgreSQL, Oracle, SQL Server, MariaDB.
    * *Amazon Aurora:* O RDS proprietário da AWS (compatível com MySQL/Postgres). Mais rápido e caro.
* **Amazon DynamoDB:** Não-Relacional (NoSQL). Chave-Valor. **Serverless**.
    * *Características:* Milissegundos de latência. Escala infinita.
* **Amazon Redshift:** Data Warehouse. Para análise de dados (BI) e consultas complexas em petabytes de dados (OLAP).
* **DMS (Database Migration Service):** Migra bancos de dados para a AWS (inclusive convertendo tipos com o Schema Conversion Tool).


### 4. Redes (Networking)


* **VPC (Virtual Private Cloud):** Sua rede privada isolada na AWS.
* **Subnets:** Divisões da VPC (Pública = tem acesso à internet; Privada = isolada).
* **Internet Gateway (IGW):** A "porta" que conecta a VPC à Internet.
* **Security Groups:** Firewall **da Instância (EC2)**. *Stateful* (Se liberar entrada, a saída é automática).
* **Network ACL (NACL):** Firewall **da Subnet**. *Stateless* (Tem que criar regra de entrada E de saída).
* **Route 53:** Serviço de DNS. Transforma `google.com` em IP. Faz Health Checks e roteamento de tráfego global.
* **CloudFront:** CDN (Content Delivery Network). Entrega conteúdo (vídeo, imagens) através de **Locais de Borda (Edge Locations)** para diminuir a latência (cache).
* **Direct Connect:** Cabo de fibra dedicado do seu escritório para a AWS (não usa a internet pública). Seguro e estável.

---

## ☁️ Domínio 1: Conceitos de Nuvem (26%) - *A Base Teórica*

### 1. Vantagens da Nuvem (Decore isso!)
* **Trocar CAPEX por OPEX:** Não gasta com data center físico (Capital), paga despesa variável mensal (Operacional).
* **Economia de Escala:** Como a AWS compra muito, fica mais barato para você.
* **Pare de adivinhar capacidade:** Escala conforme a necessidade.
* **Agilidade e Velocidade:** Inove rápido.
* **Alcance Global:** Implante em minutos no mundo todo.

### 2. Tipos de Nuvem
* **Publica:** AWS, Azure (infraestrutura compartilhada).
* **Privada:** Seu data center ou nuvem dedicada.
* **Híbrida:** Conecta pública + privada (Ex: Direct Connect, Storage Gateway).

### 3. Infraestrutura Global
* **Regiões:** Locais físicos geográficos (Ex: us-east-1, sa-east-1). Contém 2 ou mais AZs.
* **Zonas de Disponibilidade (AZs):** Um ou mais data centers físicos (prédios). Isolados por energia e rede, mas conectados por fibra rápida.
* **Edge Locations (Locais de Borda):** Só para cache (CloudFront) e DNS (Route53). Tem muito mais locais de borda do que regiões.

### 4. AWS Well-Architected Framework (6 Pilares)
1.  Excelência Operacional (Automação, monitoramento).
2.  Segurança (Proteger dados).
3.  Confiabilidade (Recuperação de falhas).
4.  Eficiência de Performance (Usar o recurso certo).
5.  Otimização de Custos (Pagar o mínimo necessário).
6.  Sustentabilidade (Reduzir impacto ambiental).

---

## 🛡️ Domínio 2: Segurança e Conformidade (25%) - *Muito importante*

### 1. Modelo de Responsabilidade Compartilhada (Shared Responsibility)


[Image of AWS Shared Responsibility Model]

* **AWS (Segurança DA Nuvem):** Hardware, Prédios, Rede física, Hypervisor. "Do concreto até o software de virtualização".
* **Cliente (Segurança NA Nuvem):** Seus dados, Criptografia, Sistema Operacional (patching), Configuração de Firewall, Senhas.

### 2. IAM (Identity and Access Management)
* **Usuário:** Uma pessoa ou aplicação.
* **Grupo:** Coleção de usuários (Facilita administração).
* **Role (Função):** Um "chapéu" de permissão temporária. Instâncias EC2 e Lambda usam Roles para acessar o S3, por exemplo. (Não tem senha fixa).
* **Policies (Políticas):** Documentos JSON que definem as permissões (Allow/Deny).
* **MFA (Multi-Factor Auth):** Camada extra de segurança (Token/Google Auth). **Recomendação #1 para o usuário Raiz (Root).**

### 3. Ferramentas de Segurança
* **AWS WAF:** Firewall para aplicações Web. Bloqueia SQL Injection, XSS.
* **AWS Shield:** Proteção contra **DDoS** (Negação de Serviço).
    * *Standard:* Grátis para todos.
    * *Advanced:* Pago, proteção 24/7 e reembolso de custos de ataque.
* **Inspector:** Avalia vulnerabilidades **dentro** da EC2 (Sistema Operacional).
* **GuardDuty:** "Cão de guarda". Detecta ameaças inteligentes analisando logs (CloudTrail, DNS). Avisa se tiver comportamento estranho.
* **Macie:** Usa Machine Learning para descobrir dados sensíveis (CPF, Cartão de Crédito) no **S3**.
* **Artifact:** Portal de downloads de relatórios de auditoria e conformidade (ISO, PCI-DSS). É aqui que você prova para o auditor que a AWS é segura.

---

## 💰 Domínio 4: Cobrança e Preços (16%) - *Detalhes finais*

### 1. Ferramentas de Custo
* **AWS Budgets:** Define um **orçamento**. Se passar do valor (ou for passar), ele te manda um **alerta** (email/SNS). *Palavra-chave: Alerta.*
* **Cost Explorer:** Visualiza gráficos, histórico e faz **previsões** de gastos futuros. *Palavra-chave: Gráfico/Análise.*
* **Cost & Usage Report:** Relatório mais detalhado possível (CSV gigante).

### 2. Planos de Suporte (Support Plans)
* **Basic:** Grátis. Só acesso a docs e Trusted Advisor limitado.
* **Developer:** Para testes. Email em horário comercial.
* **Business:** Produção. Chat 24/7. Acesso total ao Trusted Advisor.
* **Enterprise:** Missão crítica. Tem um **TAM (Technical Account Manager)** dedicado. Resposta em 15 min.

### 3. AWS Organizations
* Gerenciamento central de múltiplas contas AWS.
* **Consolidated Billing (Cobrança Consolidada):** Paga uma conta só. Combina o uso de todas as contas para ganhar descontos por volume.

---

### 💡 Dicas de Ouro para a Prova (Cheat Sheet Mental)

1.  **Leu "Serverless"?** Pense em: Lambda, DynamoDB, Fargate.
2.  **Leu "Global"?** Pense em: IAM, Route53, CloudFront. (A maioria dos outros serviços é Regional).
3.  **Leu "Desacoplar" (Decouple)?** Pense em: SQS (Fila) ou SNS (Notificação).
4.  **Leu "Banco de dados rápido/chave-valor"?** DynamoDB.
5.  **Leu "Armazenar objetos/arquivos estáticos"?** S3.
6.  **Leu "Monitorar performance"?** CloudWatch.
7.  **Leu "Monitorar quem fez o que (autoria)"?** CloudTrail.
8.  **Leu "Criptografia"?** KMS (Key Management Service).

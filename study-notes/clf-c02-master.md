# 📘 AWS Cloud Practitioner (CLF-C02) - O Guia Mestre

**Objetivo:** Aprovação na Certificação Inicial da AWS
**Estrutura:** Dividido pelos 4 Domínios Oficiais da Prova

---

## 🏆 DOMÍNIO 1: CONCEITOS DE NUVEM (26%)

### 1.1 O que é Computação em Nuvem?
É a entrega de recursos de TI sob demanda via internet com preços de pagamento conforme o uso.
* **Pare de adivinhar capacidade:** Você escala para cima ou para baixo conforme necessário.
* **Aumente a velocidade e agilidade:** Recursos novos em minutos, não semanas.
* **Economia de Escala:** A AWS compra tanto hardware que o preço cai para você.
* **Troque CAPEX por OPEX:**
    * **CAPEX (Despesa de Capital):** Comprar servidores físicos, data centers (Investimento alto e antecipado).
    * **OPEX (Despesa Operacional):** Pagar mensalmente pelo que usa (Custo variável).

### 1.2 Tipos de Implantação
1.  **Nuvem Pública:** Tudo roda na AWS (Azure, GCP). Infraestrutura compartilhada.
2.  **Nuvem Privada (On-Premises):** Tudo roda no seu data center local. Você gerencia tudo.
3.  **Nuvem Híbrida:** Conecta a Pública com a Privada (Ex: manter dados sensíveis no escritório e o site na AWS).

### 1.3 Infraestrutura Global da AWS
* **Região:** Um local físico no mundo (ex: `us-east-1` N. Virginia, `sa-east-1` São Paulo). Cada região é independente (se uma cair, a outra não cai).
* **Zona de Disponibilidade (AZ):** Um ou mais data centers físicos dentro de uma Região. Têm energia e refrigeração redundantes. Conectadas por fibra de baixa latência.
    * *Regra:* Para Alta Disponibilidade, use **pelo menos 2 AZs**.
* **Local de Borda (Edge Location):** Usado APENAS para cache de conteúdo (CloudFront) e DNS (Route 53) para diminuir a latência para o usuário final. Tem muito mais Edge Locations do que Regiões.

### 1.4 AWS Well-Architected Framework (6 Pilares)
Se a prova perguntar sobre "boas práticas", é sobre isso:
1.  **Excelência Operacional:** Executar e monitorar sistemas, melhorar processos. (Ex: Infraestrutura como Código).
2.  **Segurança:** Proteger dados e sistemas. (Ex: Gerenciar permissões, criptografia).
3.  **Confiabilidade:** Recuperar-se de falhas. (Ex: Backup, Multi-AZ).
4.  **Eficiência de Performance:** Usar recursos de TI de forma eficiente. (Ex: Escolher o tipo certo de EC2, usar Serverless).
5.  **Otimização de Custos:** Evitar gastos desnecessários. (Ex: Usar Spot Instances, apagar recursos ociosos).
6.  **Sustentabilidade:** Minimizar o impacto ambiental. (Ex: Modelo de responsabilidade compartilhada para sustentabilidade).

---

## 🛡️ DOMÍNIO 2: SEGURANÇA E CONFORMIDADE (25%)

### 2.1 Modelo de Responsabilidade Compartilhada (Vital!)
Quem cuida do quê?

**Responsabilidade da AWS (Segurança DA Nuvem):**
* "Do concreto ao Hypervisor".
* Segurança física dos Data Centers.
* Hardware (Servidores, Discos, Cabos).
* Software de virtualização.
* Rede física.

**Responsabilidade do CLIENTE (Segurança NA Nuvem):**
* Dados do cliente (Criptografia).
* Sistema Operacional (Patching, Atualizações do Windows/Linux).
* Configuração de Firewall (Security Groups).
* Gerenciamento de Identidade (Senhas, MFA).

### 2.2 IAM - Identity and Access Management
Controle de quem pode fazer o que. **Serviço Global.**
* **Usuário (User):** Uma pessoa ou serviço.
* **Grupo (Group):** Coleção de usuários. As permissões são aplicadas ao grupo.
* **Função (Role):** Uma identidade temporária. *Ex: Uma EC2 precisa acessar um S3. Ela "veste" uma Role. Não tem senha fixa.*
* **Política (Policy):** Documento JSON que diz "Permitir" ou "Negar".
* **MFA (Multi-Factor Authentication):** Token de segurança. **OBRIGATÓRIO** ativar para o usuário Raiz (Root User).

### 2.3 Serviços de Segurança (Palavras-Chave)
* **AWS WAF:** Firewall para Aplicação Web. Protege contra SQL Injection e ataques comuns.
* **AWS Shield:** Proteção contra **DDoS** (ataques de negação de serviço).
    * *Standard:* Grátis para todos.
    * *Advanced:* Pago, proteção 24/7.
* **Amazon Inspector:** Avalia segurança dentro da EC2. Procura vulnerabilidades no SO.
* **Amazon GuardDuty:** Detecção de ameaças inteligente. Analisa logs para achar comportamentos estranhos (Ex: mineração de bitcoin não autorizada).
* **Amazon Macie:** Usa IA para descobrir dados sensíveis (CPF, Cartão de Crédito) no **S3**.
* **AWS Artifact:** Portal onde você baixa relatórios de conformidade (ISO, PCI, HIPAA). É a "prova" de que a AWS é segura.
* **AWS KMS:** Gerencia chaves de criptografia.

---

## ⚙️ DOMÍNIO 3: TECNOLOGIA (33%)

### 3.1 Computação (Compute)
* **EC2 (Elastic Compute Cloud):** Servidores virtuais (IaaS).
    * **On-Demand:** Preço fixo, sem contrato. (Flexível).
    * **Reserved:** Contrato de 1 ou 3 anos. Desconto alto (72%). (Cargas constantes).
    * **Spot:** Leilão de capacidade ociosa. Desconto gigante (90%). **Risco:** Pode ser interrompido com aviso de 2 min. (Processamento em lote, testes).
    * **Dedicated Host:** Servidor físico exclusivo para você (Licenças de software/Compliance).
* **Auto Scaling:** Adiciona ou remove EC2 automaticamente baseado na demanda (CPU). Garante Elasticidade.
* **Elastic Load Balancer (ELB):** Distribui o tráfego entre várias instâncias. Garante Alta Disponibilidade.
* **AWS Lambda:** **Serverless**. Executa código sem servidor. Acionado por eventos. Cobrado por tempo de execução (ms). Limite de 15 minutos.
* **AWS Fargate:** Serverless para Containers (Docker). Você não gerencia a EC2 por baixo.

### 3.2 Armazenamento (Storage)
* **S3 (Simple Storage Service):** Armazenamento de **Objetos** (arquivos).
    * *S3 Standard:* Acesso frequente.
    * *S3 IA (Infrequent Access):* Acesso raro, mas rápido. Mais barato que Standard.
    * *S3 Glacier:* Arquivamento (Backup frio). Recuperação lenta (minutos/horas). Muito barato.
    * *S3 Intelligent-Tiering:* Move arquivos automaticamente entre as classes para economizar.
* **EBS (Elastic Block Store):** Armazenamento em **Bloco**. É o "HD" da EC2. **Preso a uma AZ.** Persistente (dados não somem se reiniciar).
* **EFS (Elastic File System):** Armazenamento de **Arquivo** (Linux). Compartilhado entre várias EC2. Multi-AZ.
* **Storage Gateway:** Conecta o on-premises à nuvem (Híbrido).

### 3.3 Redes (Networking)
* **VPC (Virtual Private Cloud):** Sua rede privada na AWS.
* **Subnet:** Divisão da VPC.
    * *Pública:* Tem acesso à Internet (via Internet Gateway).
    * *Privada:* Sem acesso direto à Internet (Banco de dados).
* **Security Group:** Firewall da **Instância**. "Stateful" (Permitiu entrada, saída é automática).
* **NACL (Network ACL):** Firewall da **Subnet**. "Stateless" (Tem que configurar entrada E saída).
* **Route 53:** Serviço de DNS. Transforma `google.com` em IP. Alta disponibilidade.
* **CloudFront:** CDN. Entrega conteúdo rápido usando Edge Locations (Cache).
* **Direct Connect:** Link de fibra dedicado (físico) da sua empresa até a AWS. Segurança e velocidade. Não usa internet pública.

### 3.4 Banco de Dados (Databases)
* **RDS:** Relacional (SQL). Tabelas. Você gerencia otimização, AWS gerencia infra. (MySQL, Postgres, Oracle).
* **Aurora:** O RDS "turbo" da AWS. Mais caro, muito mais rápido, réplicas automáticas.
* **DynamoDB:** Não-Relacional (NoSQL). Chave-Valor. **Serverless**. Rapidez extrema (milissegundos). Escala infinita.
* **Redshift:** Data Warehouse. Para análise de dados pesada (BI/Analytics).
* **DMS (Database Migration Service):** Migra bancos para a AWS com o banco original rodando (sem downtime).

### 3.5 Integração de Aplicações (Desacoplamento)
* **SNS (Simple Notification Service):** Envia notificações (Email, SMS). Modelo Pub/Sub (Um para muitos).
* **SQS (Simple Queue Service):** Fila de mensagens. Desacopla componentes. Garante que mensagens não se percam.

---

## 💰 DOMÍNIO 4: COBRANÇA E PREÇOS (16%)

### 4.1 Estrutura de Preços
* **Pague pelo que usar:** Sem contrato longo (exceto Reserved).
* **Reserve capacidade:** Pague menos comprometendo-se por 1 ou 3 anos.
* **Pague menos usando mais:** Descontos por volume (S3 e Data Transfer).

### 4.2 Ferramentas de Custo
* **AWS Budgets:** Define um orçamento e **ALERTA** se você passar dele. (Ação proativa).
* **Cost Explorer:** Visualiza gráficos dos gastos passados e **PREVÊ** gastos futuros (Forecast).
* **Cost and Usage Report (CUR):** Relatório mais detalhado possível (CSV com cada linha de cobrança).
* **AWS Pricing Calculator:** Ferramenta web para estimar custos antes de criar os recursos.

### 4.3 Suporte AWS (Support Plans)
1.  **Basic:** Grátis. Só acesso ao Trusted Advisor (limitado) e Health Dashboard.
2.  **Developer:** Para testes. Email em horário comercial.
3.  **Business:** Para produção. Chat 24/7. Trusted Advisor completo.
4.  **Enterprise:** Missão crítica. Tem um **TAM (Technical Account Manager)**. Resposta em 15 minutos.

### 4.4 AWS Organizations
* Gerencia múltiplas contas AWS em um só lugar.
* **Cobrança Consolidada (Consolidated Billing):** Paga uma fatura única para todas as contas e ganha descontos por volume somando o uso de todas.

---

### 💡 DICAS FINAIS (CHEAT SHEET)

* **Migração de DB com schema diferente?** AWS Schema Conversion Tool + DMS.
* **Gerenciar infra como código?** CloudFormation.
* **Automatizar deploy de código?** CodeDeploy / CodePipeline.
* **Serviço para auditoria (Quem fez o quê)?** CloudTrail.
* **Serviço para monitorar métricas (CPU/Memória)?** CloudWatch.
* **Consultor de boas práticas?** Trusted Advisor.
* **Chaves de acesso programático?** Access Key ID & Secret Access Key (Nunca compartilhe!).

**Família AWS SNOW**

Os dispositivos da Família AWS Snow permitem a captura e o transporte de dados o
offline para a AWS a partir de ambientes desconectados ou robustos

**FamilIa AWS Outpost**

É aquele servidor tradicional que ficará dentro da empresa.

AWS Outpost traz serviços, infraestrutura e modelos operacionais nativos da AWS para o local  para uma experiência h[híbrida consistente.

**Relatório de Custos e Uso da AWS (CUR)** 




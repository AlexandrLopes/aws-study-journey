# Resumo Cloud Practitioner

## Modelo: Cliente - Servidor

Um cliente faz uma solicitação e o servidor atende o pedido.
**Computação em Nuvem** trabalha sob demanda; só paga o que for utilizado.
Modelo perfeito para **startup’s**.

## Amazon EC2 - Amazon Elastic Computer Cloud

EC2 é uma **máquina virtual/servidor** que está na nuvem.
Usa capacidade computacional redimensionável e segura.
Inicia instância de servidor em minutos.
Pague somente pelo que usar.

### Tipos de Instâncias (modelo do servidor) (CAI NA PROVA)

[https://aws.amazon.com/pt/ec2/instance-types/](https://aws.amazon.com/pt/ec2/instance-types/)

*   **De uso Geral**: Equilibra Recursos de Computação, Memória e Rede, adequada para uma ampla variedade de cargas de trabalho.
*   **Otimizada para Computação**: Para Computadores de Alto Desempenho.
*   **Otimizada para Memória**: Banco de Dados de Alto Desempenho.
*   **Computação acelerada**: Usa Aceleradores de Hardware como GPU ou TCU para realizar tarefas específicas mais rápido que computadores convencionais.
*   **Otimizada para armazenamento**: Adequada para aplicações de Data Warehouse.

> **Data Warehouse**: É um Repositório Centralizado e Organizado que coleta dados de diversas fontes, como banco de dados transacionais e sistemas de marketing, para suportar análises de negócios e tomada de decisões estratégicas.

### Preços

*   **On Demand**: Não tem custos antecipados, nem contratos mínimos.
*   **Spot**: Ideal para testes e cargas de trabalho que toleram interrupções e não exigem disponibilidade contínua. (**90% de desconto**).
*   **Reservada**: Fornece um desconto na cobrança. Faz contrato de 1 ou 3 anos. (**até 72% de desconto**). Você se compromete com uma configuração específica de máquina. O desconto **NÃO** se aplica se você mudar a família da instância.
*   **Compute Saving Plans**: Faz contrato de 1 ou 3 anos e oferece até **66% de economia** em relação aos custos sob demanda. Você se compromete com um valor em dinheiro por hora. O desconto aplica-se automaticamente mesmo se você mudar a família da instância.
*   **Instância dedicada**: Uma instância do EC2 que é executada em uma VPC/VM em hardware físico isolado para um único cliente (custo alto em comparação com a Instância Padrão).
*   **Host dedicado**: Um servidor físico exclusivo, que nunca muda, com capacidade de instância de EC2 para um único cliente (opção mais cara).

## Escalonamento

*   **Scaling Manual**: Cabe ao Cliente colocar e parar Instâncias de forma manual.
*   **EC2 Auto Scaling**: É o dimensionamento de forma automática, **Scaling Preditivo** (cria). O Auto Scaling Preditivo usa Machine Learning para analisar o histórico e já deixa as máquinas criadas e prontas antes do tráfego aumentar, para não haver lentidão no início do pico.

### Amazon EC2 Auto Scaling:

Adiciona ou remove automaticamente (por i.a) Instâncias do EC2 de acordo com as condições definidas por você.

*   Entrega Capacidade Computacional.
*   Mantém a disponibilidade do aplicativo.
*   Beneficia-se do **Scaling dinâmico** (acompanha uma métrica) e **preditivo**.
*   Defino o tamanho do Grupo definindo os Limites que coloquei.
*   Pago somente o que for usado.

**Exemplo:**

*   **Dinâmico**: Coloco uso de CPU em 80%, e quando chegar em 80%, ele cria mais servidores.
*   **Preditivo**: Por meio de Machine Learning ele aprende o comportamento e aprende a fazer o aumento ou diminuição automaticamente.

> **Obs.:** É interessante criar um Grupo com 4 instâncias - funcionando 1 ou 2, e outras 2 que só vão ativar quando a demanda estiver maior.

## Balanceamento de Carga (fora do EC2)

### Elastic Load Balancing

É um serviço (que direciona) do AWS.

*   Distribui o tráfego automaticamente entre vários recursos.
*   Fornece um único ponto de contato para seu grupo do Auto Scaling.
*   Passa a ser o ponto de contato, as solicitações chegam nele, e ele que distribui o tráfego para os Servidores.
*   Pode distribuir o Tráfego para Servidores em Zonas diferentes.
*   Faz **Health Check** - olha para a saúde das instâncias, e caso uma falhe, ele corta a comunicação.
*   Só é direcionado para Instâncias saudáveis, para evitar prejuízos.
*   Trabalha no nível da aplicação, direciona o Tráfego para um Servidor que executa uma ação específica (**Camada 7 das Redes**).

No exemplo da Black Friday, ele usa tanto o **Autoscaling** quanto o **Elastic Load Balance**:

*   O Autoscaling cria as Instâncias de acordo com o volume necessário, e quem faz o direcionamento das cargas dessas Instâncias é o Elastic Load Balance.

## Arquitetura da Aplicação

### AWS Well-Architected Tool (AWS WA Tool)

É um **framework** (conjunto de boas práticas) criado para ajudar arquitetos de nuvem a construir infraestruturas seguras, resilientes, eficientes e de alto desempenho, e para identificar áreas de melhoria de cargas de trabalho. Funciona como um guia para avaliar e melhorar suas arquiteturas.

Ele se baseia em **6 Pilares**:

1.  **Excelência Operacional** / Operational Excellence
2.  **Segurança** / Security
3.  **Confiabilidade** / Reliability
4.  **Eficiência de Performance** / Performance Efficiency
5.  **Otimização de Custos** / Cost Optimization
6.  **Sustentabilidade** / Sustainability

> **Ferramenta relacionada**: O **AWS Well-Architected Tool** é o serviço no Console onde você responde a perguntas sobre sua arquitetura e recebe um relatório de melhorias baseado nesses pilares.

### Estilos de Arquitetura:

*   **Aplicação Monolítica** (**Fortemente Acoplada**): Todos os componentes estão interligados. Se um falha, o sistema todo pode cair. Para escalar, você precisa duplicar o servidor inteiro. Se 1 atualizar, tem que atualizar os outros.
*   **Microsserviços** (**Fracamente Acoplados**): Componentes independentes que conversam entre si (geralmente via API/SQS). Se um falha, o resto continua funcionando. Você escala e atualiza apenas o serviço que precisa. Só tem que atualizar 1.

> **Recomendação AWS**: A AWS recomenda **Microsserviços** para atingir os pilares de Confiabilidade e Excelência Operacional.

## Amazon SNS - Simple Notification Service (Tópicos)

É onde se torna fácil configurar, operar, e enviar notificações a partir da Nuvem.

*   Permite aos desenvolvedores com uma alta, flexível e com capacidade de custo-efetivo a publicarem mensagens a partir de aplicações e imediatamente entregá-las aos seus inscritos.
*   Os inscritos podem receber essas notificações em um ambiente ou em outra aplicação.
*   Resolve o problema de inscritos apropriados não receberem informação importante que eles deveriam estar cientes, como eventos ocorridos nas aplicações ou nas infraestruturas.

**Modelo**: **Tópico** (**Pub/Sub** - Publicar/Assinar).
**Ação**: **Empurra** (**Push**) a mensagem imediatamente para todos os assinantes.
**Fluxo**: de **1 para Muitos** (**Fan-out**). Uma mensagem enviada chega simultaneamente para vários destinos (Email, Lambda, SMS).

## Amazon SQS - Amazon Simple Queue Service (Filas)

Envio, armazenamento de Filas de mensagem.
Envia, Armazena e Recebe mensagens entre eles.

**Modelo**: **Fila** (**Queue**).
**Ação**: **Armazena** (**Buffer**) mensagens até que o consumidor vá lá buscá-las (**Pull**).
**Fluxo**: **1 para 1** (Um envia, um processa). Usado para **desacoplar** componentes que têm velocidades diferentes.

# Módulo 3

## Serviço de Computação Sem Servidor (Serverless)

### AWS Lambda

É um Ambiente Computacional **sem servidor** que você pode usar para rodar código sem um provisionamento ou gerenciamento. Você pode usar Lambda para rodar funções de código para virtualmente qualquer tipo de aplicação de backend.

*   Completamente gerenciado pela AWS.
*   Você sobe o código e o Lambda cuida de praticamente tudo requerido para rodar e escalar o seu código com alta disponibilidade.
*   Não precisa se preocupar com a capacidade de processamento do servidor.
*   Executa código sem provisionar ou gerenciar servidores.
*   Pague apenas pelo tempo de computação durante a execução do Código.
*   Use outros servidores da AWS para acionar o código automaticamente.

> **Obs**: Precisa de um **gatilho** para começar a rodar o código.
> **Obs**: Pode ser usado em várias linguagens.
> **Obs**: Não pode ser usado por mais de **15min** e nem ultrapassar **10gb de ram**.

### Contêiner

Um **contêiner** é uma unidade padrão de software que empacota o código e todas as suas dependências, permitindo que o aplicativo seja executado de forma rápida e confiável em diferentes ambientes computacionais.

Uma **imagem de contêiner** é um pacote de software leve, independente e executável, que inclui tudo o que é necessário para executar um aplicativo: código, ambiente de execução, ferramentas de sistema, bibliotecas de sistema e configurações.

*   Depende de um **Host** (instância EC2 ou EKS).
*   Depende de um acionador/gestor de containers = **Docker** (mais usado).
*   Contêiner - Aplicações + Bibliotecas independentes do HW/SW.

### Amazon Elastic Container Service (Amazon ECS)

*   Serviço de **orquestração de contêineres**.
*   Executa e dimensiona contêineres na AWS.
*   Usa chamadas de API simples para iniciar e para Aplicativos habilitados para Docker.

### Elastic Kubernets Service (Amazon EKS)

*   Executa e dimensiona aplicações em **Kubernets**.
*   Depende de Instância EC2.

> **Obs.: Kubernets** é uma plataforma de código aberto que automatiza a implantação, o escalonamento e o gerenciamento de aplicativos conteinerizados.

### AWS Fargate

Mecanismo de computação **serverless**, permitindo rodar aplicações Docker sem precisar provisionar, configurar ou escalar servidores, focando apenas no seu código e pagando apenas pelos recursos usados (CPU/Memória por segundo), com segurança e isolamento por contêiner.

*   Execute Contêineres sem servidor com o Amazon ECS ou Amazon EKS.
*   Pague somente o que usar.
*   Serviço de Contêineres **Serveless** (sem instância EC2) **Fargate**.

## Infraestrutura Global e Confiabilidade

*   Cada região tem que ter no mínimo **3 AZ’s**.
*   Tem que atender os requisitos legais do local.
*   Quanto mais perto do cliente melhor.
*   Tem no mundo todo.

### Fatores Considerados ao Selecionar uma Região:

*   Conformidade com governança de dados e requisitos legais.
*   Proximidade com Clientes.

### AWS Outpost

Traz serviços, infraestrutura e modelos operacionais nativos da AWS para o local para uma experiência **híbrida** consistente.

*   **Família AWS Outpost**: É aquele servidor tradicional que ficará dentro da empresa.

### Amazon CloudFront

*   **Serviço de Content Delivery Network (CDN)** - Leva o Conteúdo para os mais de 700 locais de borda para que o serviço fique próximo ao cliente e o cliente consuma com mais velocidade e mais qualidade.
*   Armazena em cache o conteúdo em **Edge Locations** (locais de borda) ao redor do mundo.
*   Melhora a **latência** (velocidade) e a **disponibilidade**.
*   Usado para entregar conteúdo estático (imagens, vídeos, HTML) e dinâmico.
*   Integra-se com o **AWS Shield** para proteção contra ataques DDoS.

> **Edge Location**: Local físico onde o CloudFront armazena cópias do seu conteúdo (cache) para que os usuários finais possam acessá-lo mais rapidamente.

### AWS Global Accelerator

*   Se uma empresa quer melhorar a disponibilidade e o desempenho das aplicações hospedadas na AWS é ele que usam. Ele usa a rede global da AWS para rotear o tráfego para o endpoint regional ideal com base na integridade, na localização do cliente e em outras políticas personalizadas.
*   Melhora a **disponibilidade** e o **desempenho** de suas aplicações usando a rede global da AWS.
*   Usa **endereços IP estáticos** de entrada que atuam como um ponto de entrada fixo para seus aplicativos.
*   Direciona o tráfego para o endpoint mais saudável e mais próximo.
*   **Não usa cache**.

> **Diferença entre CloudFront e Global Accelerator (CAI NA PROVA)**:
>
> | Característica | CloudFront | Global Accelerator |
> | :--- | :--- | :--- |
> | **Função Principal** | **CDN** (Cache de Conteúdo) | **Otimização de Rede** (Desempenho e Disponibilidade) |
> | **Usa Cache?** | Sim (em Edge Locations) | Não |
> | **Tipo de Conteúdo** | Estático e Dinâmico | Principalmente Dinâmico e APIs |
> | **Endpoint** | URL do CloudFront | Endereços IP Estáticos |

### AWS Direct Connect

*   Conexão de rede **dedicada** (privada) entre sua infraestrutura local e a AWS.
*   **Não passa pela internet pública**.
*   Reduz custos de transferência de dados e aumenta a largura de banda.

### AWS VPN (Virtual Private Network)

*   Conexão **criptografada** (túnel) entre sua rede local e a AWS **pela internet pública**.
*   Mais flexível e rápido de configurar que o Direct Connect, mas depende da qualidade da internet.

> **Diferença entre Direct Connect e VPN**:
>
> | Característica | Direct Connect | VPN |
> | :--- | :--- | :--- |
> | **Meio** | Conexão Dedicada (Privada) | Internet Pública (Criptografada) |
> | **Latência** | Mais Baixa e Consistente | Variável |
> | **Custo** | Mais Alto (Requer Infraestrutura) | Mais Baixo |

# Módulo 5

## Armazenamento e Banco de Dados

### em BLOCOS

No armazenamento **em bloco** os arquivos são separados em partes de tamanho iguais de dados, é usado em instâncias do EC2.

Chamados de **Elastic Block Storage - EBS** ou Armazenamentos em Instâncias.

#### Amazon Elastic Block Store (EBS)

Armazenamento **em Bloco** de Alto Desempenho são feitos em Discos da minha Instância (SSD/HD/etc).
Aumenta verticalmente em minutos.

Quatro tipos de Volume para optimizar preço e desempenho:

*   SSD de uso geral
*   SSD de IOPS, provisionado
*   Disco Rígido (HD) com taxa de transferência otimizada
*   HDD de baixa atividade (frio)

> **Obs**: Posso ter uma Instância com 1 arquivo, e outra com 2 arquivos. Uma não pode entrar e pegar esses arquivos uma da outra por meio do EBS. Só com o Amazon EFS.

*   A principal diferença entre **Instance Store** e **EBS**:
    *   **EBS**: **Persistente** - Dados ficam salvos por padrão nos volumes adicionais.
    *   **Instance Store** (Armazenamento de Instância): **Efêmero/Temporário** - Se a Instância parar ou for terminada, os dados são perdidos.

#### Amazon Elastic File System (Amazon EFS)

Sistema de arquivo simples, dimensionável e totalmente gerenciado.

> **Obs**: Faz justamente o que a Obs da EBS não consegue fazer.

*   Dimensiona de acordo com a demanda.
*   Armazena dados entre várias ou outras instâncias em zonas de disponibilidade diferentes.
*   Elasticidade dinâmica.
*   Armazenamento de arquivos **compartilhado**.
*   Econômico (pago só o utilizado).

### em Objetos

#### Amazon S3 (Simple Storage Service)

*   Armazenar e acessar qualquer tipo de dados pela internet a qualquer hora e qualquer lugar.
*   Você não precisa estimar quando de storage space você vai precisar, cria o **bucket** e adiciona quantos arquivos for precisar, é elástico e escala automaticamente de acordo com o storage requirements.
*   Arquivos upados no Amazon S3 são automaticamente **replicados** entre as múltiplas AZ's na Região.
*   Virtualmente **ilimitado** e no formato **serverless**.
*   Tem **Versionamento**, mas não vem ativado por padrão. No caso de acionamento, você paga por todas versões de forma acumulativa.
*   Evite exclusões acidentais.
*   Paga pela hospedagem e pela retirada dos dados.
*   No armazenamento de objetos, cada objeto consiste em **Value**, **Metadata** e uma **Key**.

Essa é a estrutura fundamental de um objeto no Amazon S3:

*   **Key**: O nome único (identificador) do arquivo.
*   **Value** (Dados): O conteúdo do arquivo em si (bytes).
*   **Metadata**: Informações sobre o arquivo (ex: tamanho, tipo, data).

#### Tipos de Armazenamento S3

*   **S3 Standard**: Uso geral, acesso frequente.
*   **S3 intelligent-Tiering**: Padrões de acesso imprevisíveis ou variáveis (ele move os dados sozinhos para economizar).
*   **S3 Standard-IA**: Acesso infrequente, mas precisa de recuperação rápida.
*   **S3 One Zone-IA**: Acesso infrequente, dados recriáveis (se a AZ cair, perde os dados).
*   **S3 Glacier Instant Retrieval**: Arquivamento de longa duração com acesso imediato.
*   **S3 Glacier Flexible Retrieval**: Arquivamento onde você pode esperar minutos ou horas para recuperar.
*   **S3 Deep Archive**: O mais barato de todos. Para dados que você quase nunca acessa e pode esperar **12 a 48 horas** para recuperar.

> **Obs**: Esse tempo é o tempo de espera entre o momento que eu solicitei o arquivo e o momento que ele fica disponível para uso.
> **Obs**: Todos estão em **3 Zonas de Disponibilidade**, exceto o **S3 One Zone de IA**.
> **Obs**: Prova, saber o **S3 básico** e **Glacier**, **Inteligent-Tiering**.

## Banco de Dados

Dividido em:

*   **Amazon Relational Database Service (Amazon RDS)** - Relacional
*   **Amazon DynamoDB** - Não relacional (baseado em key e value)
*   **AWS Database Migration Service (DMS)** - Pode levar/migrar o Banco de dados para nuvem (no modelo híbrido, por exemplo)

### Amazon Relational Database Service (AWS RDS)

*   Automatiza tarefas de Administração.
*   Totalmente gerenciado pela AWS.
*   Existem vários mecanismos otimizados para memória (**Amazon Aurora**, MySQL, Oracle, etc).
*   Trabalha com **TABELAS** com LINHAS e COLUNAS (**dado estruturado**).
*   Cloud-Base e desenhado para simplificar o Setup, Operação, e Escalar o Database relacional.
*   Automatiza tarefas de administração como patching, backing up databases e enabling point-in-time recovery.
*   Fácil de administrar pois não precisa de infraestrutura provisionada e nem instalar e manter database software’s, é rápido e suporta a maioria das aplicações para Banco de Dados.

**Provisionamento**:

*   Pode ser criado uma implantação **Multi-AZ** (roda a sua aplicação ou Banco de Dados em 2 ou mais Zonas de Disponibilidades).
*   Contém **Cluters** (servidores, instâncias ou BD que trabalham juntos como um sistema único).
*   No caso de **Failover** (uma AZ cair) o sistema muda automaticamente para a outra sem intervenção manual.
*   Altos níveis de disponibilidade e confiabilidade.
*   Use **réplicas de leitura** para cargas de trabalho do banco de dados com uso intenso de leitura. Para desafogar o uso da instância principal.
*   Bancos de Dados Relacionais organizam dados estruturados em tabelas (linhas e colunas), seguindo um esquema pré-definido e usando **SQL**.

**Banco de Dados Suportados pela Amazon**:

*   **Amazon Aurora**: Banco de Dados proprietário da AWS (não é open-source). É compatível com MySQL e PostgreSQL, mas oferece **5x mais desempenho** que o MySQL padrão e custa **1/10 dos bancos comerciais**. Possui tolerância a falhas automática (repara dados sozinho).

Os itens abaixo são "Motores de Banco de Dados" (**Database Engines**) que você pode escolher para rodar dentro do serviço Amazon RDS:

*   **PostgreSQL**: Relacional, Open-Source e avançado. Focado em extensibilidade e conformidade rigorosa com padrões SQL.
*   **MySQL**: Relacional, open-source e o mais popular do mundo para aplicações web. Simples e confiável.
*   **MariaDB**: Relacional, open-source. É um "fork" (derivado) do MySQL, criado pelos fundadores originais do MySQL.
*   **Oracle Db**: Relacional, comercial/empresarial. Focado em grandes corporações, robusto e requer gerenciamento de licenças.
*   **Microsoft SQL Server**: Relacional, comercial da Microsoft. Ideal para ambientes corporativos que já usam Windows e .NET.
*   **IBM DB2**: Relacional, comercial da IBM. Focado em cargas de trabalho empresariais críticas (adicionado recentemente ao RDS).

### Amazon Dynamo DB

Banco de Dados **Não Relacional Serveless** que pode guardar e recuperar qualquer quantidade de dado em qualquer level de tráfego requerido.

*   Você pode escalar suas tabelas de banco de dado aumentando ou diminuindo a capacidade sem qualquer diferença de tempo.
*   Sem servidores para serem gerenciados, só seleciono a Tabela e começo a usar.
*   Desempenho de **milissegundos de um dígito** em qualquer escala.
*   Banco de dados de documento e **valores-chave (key-value) NoSQL** rápido e flexível. Documentos estilo Json.
*   **Serverless**, dimensiona automaticamente para se ajustar às mudanças de capacidade e manter um desempenho consistente.
*   Pode usar o AWS Management Console para monitor os recursos utilizados e as métricas de perfomance.
*   Serve para aliviar os encargos administrativos de operação e dimensionamento de um BD distribuído, sem se preocupar com provisionamento, setup, configuração, software etc.

> **Obs**: Não importa o tamanho, ele nunca perde a eficiência.
> **Obs**: Usado em aplicativos Web sem serviços / Back-end para aplicativos móveis/ jogos.

### AWS Database Migration Service (AWS DMS)

*   Migra bancos de dados para a AWS com facilidade e segurança.
*   Migra dados e para os bancos de dados mais usado.
*   Mantenha a operação completa dos bancos de dados de origem durante a migração.
*   Migra Bancos de Dados Relacionais e Não Relacionais e outros tipos de Armazenamento de Dados.
*   Mantém seu Banco de Dados enquanto a migração ocorre.

**Exp.**: My SQL ⮕ AWS DMS ⮕ Amazon Aurora (exp destino)

### Palavras chaves: (CAI NA PROVA)

*   **Amazon Redshift**: **Data Warehouse** (Armazém de dados), Big Data, SQL, **OLAP** (Consultas complexas em petabytes). (Dados tão grandes que fica vermelho/RED)
*   **Amazon DocumentDB**: Compatível com **MongoDB**, documentos JSON.
*   **Amazon Neptune**: Banco de dados de **Grafos** (**Graphs**), Relacionamentos complexos, Redes Sociais.
*   **Amazon QLDB** (Quantum Ledger Database): **Ledger Centralizado**, **Imutável**, Criptograficamente verificável. (Diferente de Blockchain, pois tem uma autoridade central).
*   **Amazon Managed Blockchain**: **Ledger Descentralizado**, Hyperledger Fabric, Ethereum. (Várias partes confiam umas nas outras sem autoridade central).
*   **Amazon ElastiCache**: **Cache na memória** para bancos relacionais (RDS), compatível com **Redis** e **Memcached**. Melhora a latência para **microssegundos**.
*   **Amazon DAX** (DynamoDB Accelerator): **Cache exclusivo** para o DynamoDB. Aumenta a performance de milissegundos para **microssegundos**.
*   **S3 Glacier Flexible Retrieval**: Arquivamento de baixo custo. Recuperação em minutos ou até 12 horas.
*   **S3 Glacier Deep Archive**: O armazenamento mais barato da AWS. Recuperação lenta (**12 a 48 horas**). (Lenta porque tá lá no fundo)

# Módulo 6

## Segurança e Conformidade

*   **Visibilidade** - Enxergar o que está acontecendo com sua aplicação.
*   **Auditabilidade** - Saber quem fez o que (onde, quem, quando).
*   **Controlabilidade** - Saber que meu time pode acessar meus recursos na nuvem (defino permissões específicas).
*   **Agilidade** - Preciso de agilidade para agir.

### Modelo de Responsabilidade Compartilhada:

A responsabilidade é **compartilhada** entre a AWS e o Cliente.

| Responsabilidade | AWS (A Nuvem) | Cliente (Na Nuvem) |
| :--- | :--- | :--- |
| **Segurança DE** | Infraestrutura Global (Hardware, Software, Rede, Instalações) | Dados, Plataforma, Aplicações, Identidade e Acesso |
| **Segurança NA** | - | Configuração de Firewall, Criptografia, Gerenciamento de Patches em SO (para EC2) |

### Identify and Access Management (AWS IAM)

Define que permissões **QUEM** vai ter, cria credenciais de acordo e dá permissões específicas.
É como se fosse a parte de Login da AWS, serve para identificar o Acesso aos serviços AWS.

*   É onde permite quais permissões quem vai ter para cria credenciais e dá permissões específicas, respeitando o princípio de dar **menos permissões possíveis** sempre.
*   Permite que você gerencie o acesso aos serviços e recursos da AWS.
*   Controle o acesso a serviços e recursos da AWS.
*   Crie e gerencie usuários e grupos.
*   AWS já tem permissões pré-configuradas.
*   Ative a **autentificação multifator (MFA)** para uma segurança ainda maior.

> **Obs**: Usuário do IAM = **Entidade**.

### AWS Organizations

*   Gerenciamento centralizado de **múltiplas contas AWS**.
*   Permite aplicar **Service Control Policies (SCPs)** para governança e controle de permissões em todas as contas.
*   Consolida o faturamento.

### AWS Artifact

*   Portal de **conformidade** e **documentação**.
*   Acesso a relatórios de conformidade da AWS (SOC, PCI, ISO).

### AWS Shield

*   Proteção contra ataques de **DDoS** (Distributed Denial of Service).
*   **Standard**: Proteção automática para todos os clientes.
*   **Advanced**: Proteção aprimorada e relatórios de ataque.

### AWS WAF (Web Application Firewall)

*   Protege aplicações web contra **exploits** comuns (SQL Injection, Cross-Site Scripting).
*   Funciona na **Camada 7** (Aplicação).

### Amazon Inspector

*   Serviço de **avaliação de segurança automatizada**.
*   Verifica vulnerabilidades em instâncias EC2 e imagens de contêiner.

### Amazon GuardDuty

*   Serviço de **detecção de ameaças** inteligente e contínuo.
*   Monitora atividades maliciosas e comportamento não autorizado.

### Amazon Macie

*   Serviço de **segurança de dados** e privacidade.
*   O Macie aplica técnicas de Machine Learning e correspondências de padrões para identificar dados sigilosos, incluindo PII (informações de identificação pessoal).
*   Pode gerar uma descoberta se dados sigilosos forem encontrados.
*   Pode selecionar buckets especificos do S3 para o Macie pesquisar.

### AWS Key Management Service (AWS KMS)

*   Faz justamente a **criptografia**, cria e gerencia a chave da criptografia.
*   Ajuda o Cliente a executar Operações de Criptografias.

> **Obs.:** (lembrar de Key) pelo uso de chaves de criptografia.

### AWS CloudHSM

*   Também cria a chave e ajuda a gerencia-la.
*   Ajuda a atender requisitos de conformidade regulatória, contratual e corporativa para a segurança de dados usando dispositivos **Hardware Security Module** dedicados na Nuvem AWS.

### AWS Certificate Manager

*   Torna criptografado os dados em trânsito também.

### AWS Secrets Manager

*   Gerencia, recupera e rotaciona **segredos** (credenciais de banco de dados, chaves de API).

# Módulo 7

## Monitoramento

### Amazon CloudWatch

Principal ferramenta de **monitoramento** e **observação**. Dispõe de Data e Insights acionáveis para monitorar suas aplicações.

*   Resolve o problema da resposta nos eventos e alarmes caso eles ocorram na sua arquitetura.
*   Coleciona monitoramento e Data Operacional na forma de **Logs**, **Métricas** e **Eventos**.
*   Funciona unificando as visões dos recursos do AWS, aplicações e serviços que rodam na AWS e em On-premises servers.
*   Pode ser usado para detectar comportamento análogo, definir **Alarmes**, e visualizar os Logs com Métricas lado a lado.
*   Pode também fazer tudo isso entre todos os seus serviços (across your services and infra) para você analisar métricas como utilização de memória e CPU.

### AWS CloudTrail

*   Vai **rastrear atividade do usuário** e **solicitações api** em toda infra da aws, etc.
*   Fornece um registro de ações, eventos e chamadas de API feitas por um usuário, função ou serviço da AWS.

### AWS Trusted Advisor

É um **conselheiro** que indica as melhores modificações para os clientes AWS.
É usado para analisar sua conta e gera recomendações sobre:

*   **Otimização de Custos**
*   **Desempenho**
*   **Segurança**
*   **Tolerância a falhas**
*   **Limites de serviços**

> **Obs.:** Podem perguntar quais são as características no painel.

# Módulo 8

## Preços e Suporte

*   Nível gratuito da AWS fica disponível por **12 meses** para novos clientes.

### AWS Budgets

*   Permite definir orçamentos personalizados que enviem alertas quando o uso ou custos excedem o valor orçado.
*   Você usa para definir **limites** para o uso e os custos do serviço da AWS.
*   Só informa, **não altera automaticamente**.

### AWS Marketplace

*   É usado para encontrar **software de terceiros** na AWS.

### AWS Cost Explorer

*   Permite o usuário analisar seus custos e uso da AWS ao longo do tempo.
*   Use-o para visualizar os custos por mês, o serviço da AWS ou o grupo de tags.
*   Pode ser usado para compreender visualmente as tendências de custos e o uso ao longo do tempo.

### AWS Pricing Calculator

*   Oferece a capacidade de criar estimativas para seus casos de uso da AWS antes de criar as aplicações.
*   Pode fornecer uma estimativa de custo.

### Saving Plans

*   São um modelo de preços flexível que você pode usar para reduzir custos com base no uso da computação da AWS.
*   É usado principalmente para otimização de custos de instâncias do EC2.

# Módulo 9

## Migração e Inovação

### AWS Cloud Adoption Framework (AWS CAF)

É um **guia (framework)** que ajuda as organizações a criarem um plano eficiente para migrar para a nuvem e transformar seus negócios.
Ele organiza o processo em **6 Perspectivas**:

**Capacidades de Negócios (Business Capabilities)**:

1.  **Negócios** (Business)
2.  **Pessoas** (People)
3.  **Governança** (Governance)

**Capacidades Técnicas (Technical Capabilities)**:

4.  **Plataforma** (Platform)
5.  **Segurança** (Security)
6.  **Operações** (Operations)

> **Dica de prova**: Geralmente perguntam "Qual dessas é uma perspectiva de Negócios?" e colocam "Segurança" como pegadinha. Lembre-se que **Pessoas** e **Governança** são do lado do Negócio, não Técnico.
>
> *   O gerenciamento de desempenho e capacidade é um recurso da perspectiva das **Operações** no AWS CAF.
> *   O gerenciamento de portfólio de aplicações é um recurso da perspectiva de **Governança** no AWS CAF.

### Amazon CodeWhisperer

*   **Gerador de código com IA** para IDEs e editores de código.
*   Não é armazenado nem usado pela AWS em lugar algum.

### Família AWS SNOW

*   Os dispositivos da **Família AWS Snow** permitem a captura e o transporte de dados **offline** para a AWS a partir de ambientes desconectados ou robustos.

#### AWS Snowball Edge

*   Feito para transferir dados grandes. Terabytes/Petabytes.
*   É um tipo de dispositivo Snowball que tem capacidade de armazenamento e poder computacional integrados para recursos selecionados da AWS.
*   Pode realizar cargas de trabalho de processamento local e computação de ponta.
*   Pode transferir dados entre seu ambiente local e a nuvem AWS.
*   Não melhora a latência de usuários globais.

### Serviços Adicionais

*   **AWS Application Discovery Service**: Ajuda a planejar uma migração para a nuvem AWS. Não pode ser usado para implantar aplicações na nuvem AWS.
*   **Amazon Kinesis Data Streams**: Coleta e processa streams de dados em tempo real.
*   **Amazon Connect**: Fornece uma central de atendimento altamente dimensionável na nuvem AWS. Não é usado para conectar duas redes diferentes. Não confundir com o Direct Connect, que fornece uma conexão privada dedicada.
*   **AWS CDK (Cloud Development Kit)**: É um framework de desenvolvimento de software que pode ser usada para criar recursos de aplicações em nuvem. Trata-se de uma ferramenta que simplifica a criação de recursos.
*   **AWS Storage Gateway**: É um dispositivo de hardware ou dispositivo de software virtual usado para **armazenamento em nuvem híbrida** com cache local. É um serviço de armazenamento híbrido da AWS, ou seja, permite que as aplicações on-primises de um usuário, usem perfeitamente o armazenamento na nuvem da AWS.
*   **Amazon API Gateway**: Use o gateway de API para criar e gerenciar APIs Rest e Web Socket, mas não para implantar a infraestrutura.
*   **AWS Elastic Beanstalk**: É possível usar o Elastic Beanstalk para implantar, gerenciar e dimensionar aplicações. Oferece a capacidade de rápida implantação e gerenciamento de aplicações na nuvem AWS.
*   **AWS Batch**: Gerencia ambientes de computação e filas de trabalho. É possível executar milhares de jobs em qualquer escala. Usa instâncias do EC2 para hospedar os jobs em lotes. Pode executar contêineres, mas eles são executados em instâncias EC2.
*   **Amazon Lightsail**: Fornece uma solução de servidor virtual privado (VPS) para começar na AWS. Indicado para desenvolvedores, pequenas empresas, estudantes. Oferece funcionalidades e recursos de computação, armazenamento e redes. Pode ser usado para implantar e gerenciar sites e aplicações web na nuvem. Lightsail pode executar contêineres, mas os contêineres são executados em instâncias do EC2.
*   **AWS X-RAY**: É um serviço usado para identificar e depurar aplicações, bem como para descobrir oportunidades de otimização em seus servidores de aplicações. O recurso mais famoso do X-Ray é desenhar um mapa visual de toda a sua aplicação. Ele mostra bolinhas conectadas e, se uma delas estiver vermelha, você sabe instantaneamente que o erro está ali.
*   **Amazon QuickSight**: É um serviço de **b.i** usado para visualização de dados. É possível combinar dados de vários serviços em um só painel, o que pode trazer informações sobre seus dados mais rapidamente. Pega dados "feios" e brutos e os transforma instantaneamente em Gráficos Coloridos, Dashboards e Painéis Visuais.
*   **AWS CloudFormation**: Permite reutilizar modelos para configurar recursos de forma consistente e repetida em várias Regiões. Para uma Empresa que quer implantar rapidamente uma infraestrutura duplicada em uma Região AWS diferente para criar redundância global.

### Serviços de Machine Learning (ML)

*   **Amazon Transcribe**: É um serviço de reconhecimento de fala que usa modelos de Machine Learning para converter áudio em texto. Pode ser usado como um serviço de transcrição independente.
*   **Amazon Polly**: É um serviço que transforma texto em **fala realista**. Oferece a capacidade de criar aplicações que falam. **Não** adiciona recursos de conversão de fala em textos.
*   **Amazon Textract**: É um serviço de Machine Learning que extrai automaticamente texto, manuscrito e dados de documentos digitalizados. Vai além do reconhecimento óptico de caracteres (OCR) básico para identificar, entender, e extrair dados de formulários e tabelas. **Não** adiciona recursos de conversão de fala.
*   **Amazon Comprehend**: É um serviço de processamento de linguagem natural (PLN) que usa modelos de Machine Learning para descobrir informações em dados não estruturados. Desenvolve insights por meio do reconhecimento de entidades, frases importantes, linguagem, sentimentos e outros elementos comuns de documentos. **Não** adiciona recursos de conversão de fala em textos às aplicações.
*   **Amazon Rekognition**: É usado para analisar fotos e vídeos.

## Geral:

*   Com a computação em nuvem AWS, você pode trocar **custos fixos por custos variáveis** pagando somente pelos recursos que usar.
*   É possível separar as cargas de trabalho de produção e não produção na AWS criando **várias contas** para fornecer o mais alto nível de isolamento de recursos e faturamento.
*   **Qual plano do AWS Support inclui um Technical Account Manager (TAM) designado da AWS?**
    *   **RE**: Enterprise Support inclui acesso a um TAM designado.
*   **Responsabilidade da AWS**: A AWS é responsável pelo **descomissionamento seguro da mídia** como parte da proteção da infraestrutura global da AWS.

## Documentos recomendados:

*   Visão geral da AWS: [https://d1.awsstatic.com/whitepapers/aws-overview.pdf](https://d1.awsstatic.com/whitepapers/aws-overview.pdf)
*   Comparar planos de AWS Support: [https://aws.amazon.com/premiumsupport/plans](https://aws.amazon.com/premiumsupport/plans)
*   Como os preços da AWS funcionam: [https://docs.aws.amazon.com/whitepapers/latest/how-aws-pricing-works/welcome.html](https://docs.aws.amazon.com/whitepapers/latest/how-aws-pricing-works/welcome.html)

**Nota da Prova**:

*   Nota vai de 100 a 1000.
*   Sendo **700** - **70%** a pontuação mínima.

**Preparação para prova (skill builder)**:

*   [https://aws.amazon.com/pt/certification/certified-cloud-practitioner/](https://aws.amazon.com/pt/certification/certified-cloud-practitioner/)
*   [https://aws.amazon.com/pt/certification/certification-prep/?ch=cta&cta=header&p=2](https://aws.amazon.com/pt/certification/certification-prep/?ch=cta&cta=header&p=2)

**AWS Builder Labs**:

*   [https://aws.amazon.com/pt/training/digital/aws-builder-labs/](https://aws.amazon.com/pt/training/digital/aws-builder-labs/)

**Treinamentos Digitais**:

*   [https://explore.skillbuilder.aws](https://explore.skillbuilder.aws)

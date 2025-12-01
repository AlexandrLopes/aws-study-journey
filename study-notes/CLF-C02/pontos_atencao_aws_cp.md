# Pontos de Atenção para os 5 Principais Serviços no Exame AWS Cloud Practitioner

Focar nos pontos de atenção específicos de cada serviço é a chave para evitar "pegadinhas" no exame.

## 1. Amazon EC2 (Elastic Compute Cloud)

| Ponto de Atenção | Conceito Chave | Pegadinha Comum |
| :--- | :--- | :--- |
| **Tipos de Preço** | Diferenciar **On-Demand** (flexibilidade), **Spot** (maior desconto, mas pode ser interrompida) e **Reserved Instances (RIs)** (maior desconto por compromisso de longo prazo). | Confundir Spot com RIs. Se a questão fala em **economia máxima** para uma carga de trabalho **tolerante a falhas**, a resposta é **Spot**. Se fala em **economia garantida** por **1 ou 3 anos**, a resposta é **RI**. |
| **Escalabilidade** | Entender que o EC2 é o serviço base, mas o **EC2 Auto Scaling** é quem gerencia a escalabilidade automática (adicionar/remover instâncias). | Atribuir a função de escalabilidade automática ao EC2 sozinho. O EC2 fornece a instância; o Auto Scaling a gerencia. |
| **Armazenamento** | Saber que o EC2 usa **EBS** (Elastic Block Store) como disco persistente. | Achar que o armazenamento de instância (Instance Store) é persistente. O EBS é persistente e pode ser desanexado e reanexado; o Instance Store é temporário e se perde ao desligar a instância. |

## 2. Amazon S3 (Simple Storage Service)

| Ponto de Atenção | Conceito Chave | Pegadinha Comum |
| :--- | :--- | :--- |
| **Armazenamento de Objeto** | O S3 armazena **objetos** (arquivos) em **buckets**, não é um sistema de arquivos tradicional (como EFS) ou um disco (como EBS). | Tentar usar S3 como disco de inicialização (boot volume) para uma instância EC2. Isso é função do EBS. |
| **Durabilidade vs. Disponibilidade** | O S3 é projetado para **11 noves de durabilidade** (quase impossível perder um objeto), mas a **disponibilidade** varia conforme a classe (ex: S3 Standard vs. S3 One Zone-IA). | Confundir as classes. A classe **S3 One Zone-IA** é a única que armazena dados em **uma única AZ**, sendo mais barata, mas com menor disponibilidade e durabilidade em caso de falha da AZ. |
| **Segurança** | Por padrão, os buckets S3 são **privados**. O acesso deve ser concedido explicitamente via Políticas de Bucket ou ACLs. | Achar que o S3 é público por padrão. A AWS incentiva a manter os buckets privados e só liberar o acesso necessário. |

## 3. AWS Lambda

| Ponto de Atenção | Conceito Chave | Pegadinha Comum |
| :--- | :--- | :--- |
| **Serverless** | O Lambda é a definição de *Serverless* para computação: você não gerencia servidores, paga apenas pelo tempo de execução e ele escala automaticamente. | Achar que o Lambda é o único serviço *serverless*. DynamoDB e Fargate também são *serverless*, mas para Banco de Dados e Containers, respectivamente. |
| **Gatilhos (Triggers)** | O código do Lambda é executado em resposta a um **evento** (ex: um arquivo é enviado para o S3, uma mensagem chega no SQS, uma chamada de API). | Pensar no Lambda como um servidor tradicional que está sempre ligado. Ele só executa quando acionado. |
| **Limites de Execução** | O Lambda tem um tempo máximo de execução (atualmente 15 minutos) e limites de memória. | Usar o Lambda para tarefas de longa duração (ex: processamento de vídeo de várias horas). Para isso, serviços como EC2 ou ECS seriam mais apropriados. |

## 4. AWS IAM (Identity and Access Management)

| Ponto de Atenção | Conceito Chave | Pegadinha Comum |
| :--- | :--- | :--- |
| **Princípio do Menor Privilégio** | A regra de ouro do IAM: conceder apenas as permissões **necessárias** para que um usuário ou serviço realize sua tarefa. | Conceder permissões de administrador (full access) por conveniência. O exame sempre testará sua adesão ao princípio do menor privilégio. |
| **Usuários vs. Roles (Funções)** | **Usuários** são para pessoas ou aplicações que interagem diretamente com a AWS. **Roles** são para conceder permissões temporárias a serviços da AWS (ex: dar permissão a um EC2 para acessar um S3). | Usar credenciais de usuário IAM em uma instância EC2. O correto é anexar uma **Role IAM** à instância. |
| **Root User** | A conta Root (raiz) tem acesso irrestrito. Deve ser usada **apenas** para tarefas de gerenciamento de conta (ex: alterar o plano de suporte, fechar a conta). | Usar a conta Root para tarefas diárias. O exame enfatiza que as tarefas diárias devem ser feitas por um usuário IAM com as permissões mínimas necessárias. |

## 5. Amazon VPC (Virtual Private Cloud)

| Ponto de Atenção | Conceito Chave | Pegadinha Comum |
| :--- | :--- | :--- |
| **Grupos de Segurança vs. ACLs de Rede** | **Grupos de Segurança (SG)** são *Stateful* (basta liberar a entrada, a saída é automática) e atuam no nível da **Instância**. **ACLs de Rede (NACL)** são *Stateless* (precisa liberar entrada e saída) e atuam no nível da **Sub-rede**. | Confundir a natureza *Stateful* e *Stateless*. Se a questão exige um firewall que atue em toda a sub-rede e exija regras de entrada e saída, a resposta é **NACL**. |
| **Sub-redes Públicas vs. Privadas** | Uma sub-rede é **Pública** se tiver um **Internet Gateway (IGW)** anexado e as instâncias tiverem um IP Público. Caso contrário, é **Privada**. | Achar que uma sub-rede é pública só porque tem um IP público. Ela precisa do **IGW** para se comunicar com a Internet. |
| **Isolamento** | A VPC é uma rede virtual **isolada** e **privada**. | Achar que a VPC é acessível por padrão. Ela é isolada logicamente de outras VPCs e do restante da Internet, a menos que você configure explicitamente o acesso (ex: IGW, VPN, Direct Connect). |

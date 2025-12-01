# ☁️ Resumo: Modelos de Preço EC2 (Exam Prep)

**Tópico:** EC2 Pricing & Billing
**Status:** Revisado ✅

---

### 1. On-Demand (Sob Demanda)
* **Melhor para:** Cargas de trabalho curtas, picos imprevisíveis, testes.
* **Custo:** Mais caro por hora, mas sem compromisso (pay-as-you-go).
* **Key:** Não requer pagamento adiantado.

### 2. Savings Plans & Reserved Instances (Reservadas)
* **Melhor para:** Sistemas estáveis (ex: banco de dados ligado 24/7).
* **Desconto:** Até **72%** comparado ao On-Demand.
* **Compromisso:** Contrato de 1 ou 3 anos.

### 3. Spot Instances (Leilão)
* **Melhor para:** Processamento em lote, coisas que podem falhar/parar.
* **Risco:** A AWS pode tomar a instância com aviso de **2 minutos**.
* **Custo:** Até **90%** de desconto (opção mais barata).

### 4. Dedicated Hosts
* **Melhor para:** Licenças de software específicas (BYOL) ou requisitos regulatórios severos.
* **Custo:** Opção mais cara.

---
### 💡 Dica para a Prova
Se a questão falar em "flexibilidade total e sem contrato", a resposta é **On-Demand**.
Se falar em "maior desconto possível" e "pode ser interrompido", é **Spot**.

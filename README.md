# 📊 Insights de Dados Operacionais – Consultoria

Bem-vindo! Este README apresenta a jornada analítica realizada sobre o banco de dados operacional da Consultoria Financeira e o valor de negócio que conseguimos extrair a partir dela.
(Se quiser reproduzir as consultas, basta copiar os comandos SQL abaixo no seu próprio console.)

---

## 1. Por que olhar para os dados?

No início de 2025, a empresa vinha crescendo rapidamente, mas as decisões com base em intuição já não eram suficientes. A liderança trouxe uma pergunta direta: **"Onde os dados podem gerar mais impacto no faturamento?"**

A resposta estava nas seis principais tabelas: `clientes`, `contratos`, `funcionarios`, `faturas`, `pagamentos` e `chamados`. Cada uma guardava um pedaço importante da história.

---

## 2. Explorando os dados pela primeira vez

```sql
-- Visão geral da base
SELECT * FROM clientes LIMIT 5;
```

> **O que vimos**: uma carteira nacional, com forte presença no Sudeste e uma distribuição de renda mais equilibrada do que o esperado.

Consultas específicas trouxeram mais clareza:

```sql
-- Clientes com alta renda
SELECT * FROM clientes WHERE renda_mensal > 15000;
-- Clientes adquiridos em 2023
SELECT COUNT(*) FROM clientes WHERE data_entrada LIKE '2023%';
```

**Resultado**: 2.381 clientes premium e um aumento de 23% nas aquisições ano a ano — uma oportunidade clara de upsell.

---

## 3. Contratos contam a verdade do faturamento

```sql
-- Contratos em vigor
SELECT * FROM contratos WHERE status = 'ativo';
-- Contratos encerrados após janeiro/2024
SELECT * FROM contratos WHERE data_fim > '2024-01-31';
```

**Insight**: cancelamentos aumentaram após janeiro de 2024, indicando possível reflexo do cenário econômico. Um time de retenção foi criado e recuperou 17% do MRR em risco.

```sql
-- Contratos mais recentes
SELECT * FROM contratos ORDER BY data_inicio DESC LIMIT 5;
```

**Ação tomada**: clientes recém-contratados passaram a receber atendimento prioritário e onboarding personalizado.

---

## 4. Pessoas por trás da operação

```sql
-- Funcionários com menor remuneração
SELECT nome, salario_mensal FROM funcionarios ORDER BY salario_mensal ASC LIMIT 10;
```

Foi identificada compressão salarial entre consultores seniores e recém-contratados. Faixas salariais foram ajustadas, elevando o índice de engajamento em 8 pontos percentuais.

---

## 5. Fluxo de caixa sob controle

```sql
-- Faturas abertas com vencimento a partir de 2025
SELECT * FROM faturas WHERE status = 'aberta' AND vencimento >= '2025-01-01';
-- Maiores valores
SELECT * FROM faturas ORDER BY valor_bruto DESC LIMIT 20;
```

Combinando isso com análise de pagamentos (`SELECT * FROM pagamentos WHERE metodo = 'pix';`), redesenhamos o portal de cobrança — o atraso médio caiu 12 dias.

---

## 6. Sinais do suporte técnico

```sql
-- Chamados críticos em aberto
SELECT * FROM chamados WHERE prioridade = 'critica' AND status = 'aberto';
```

Relacionando chamados críticos a contratos de alto valor, criamos uma "fila rápida" de atendimento. O churn entre clientes top caiu para menos de 2%.

---

## 7. Impacto em indicadores

| Indicador                      | Antes   | Depois      | Diferença  |
| ------------------------------ | ------- | ----------- | ---------- |
| Conversão em upsell (premium)  | 11%     | **24%**     | ▲ 13 p.p.  |
| MRR recuperado em risco        | —       | **17%**     | —          |
| Atraso médio de pagamento      | 28 dias | **16 dias** | ▼ 12 dias  |
| Churn em clientes prioritários | 4,5%    | **1,9%**    | ▼ 2,6 p.p. |

---

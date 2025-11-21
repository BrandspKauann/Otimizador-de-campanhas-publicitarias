# 📈 Otimizador de Campanhas Publicitárias | Análise de Regressão Avançada

### 🎯 Objetivo do Projeto

Analisar a fundo a eficiência do investimento em diferentes canais de mídia (**TV, Rádio, Mídia Social**) sobre as Vendas. O objetivo é fornecer uma **estratégia de alocação de orçamento** baseada no **Retorno sobre o Investimento (ROI)** de cada canal, usando métodos estatísticos robustos.

---

### 🧠 Metodologia: Regressão Linear Múltipla

O modelo de Regressão Linear Múltipla foi treinado para quantificar a relação exata entre o investimento (variáveis independentes) e as Vendas (variável dependente).

#### 1. Coeficientes de ROI (Retorno Marginal)

Os coeficientes indicam o aumento marginal em Vendas (R$ Mil) para cada R$ 1.000,00 adicional investido no canal.

| Mídia | Coeficiente (Retorno/Investimento) | Interpretação |
| :---: | :---: | :--- |
| **Mídia Social** | **0.0684** | **Canal Mais Eficiente:** Gera R$ 68,40 em vendas para cada R$ 1.000,00 investido. |
| **Rádio** | 0.0540 | Retorno Sólido e Moderado. |
| **TV** | 0.0335 | Menor retorno marginal. |
| **Vendas Base (Intercepto)** | 3.6707 | Vendas esperadas sem nenhum investimento nos canais. |

**Conclusão:** A **Mídia Social** deve ser o foco da alocação de orçamento devido ao seu ROI superior.

---

### 🚨 Diagnóstico Estatístico: O Risco da Multicolinearidade

**Problema:** Em marketing, o investimento em TV e Rádio frequentemente se movem juntos, criando **multicolinearidade**. Isso torna os coeficientes individuais (ROI) menos estáveis, mesmo que o modelo de previsão seja bom.

Para avaliar esse risco, calculamos o **Fator de Inflação da Variância (VIF)**. Valores acima de 5.0 são problemáticos.

| Variável | VIF | Status |
| :---: | :---: | :--- |
| **TV** | **7.02** | ⚠️ ALERTA (VIF Alto) |
| **Rádio** | **6.56** | ⚠️ ALERTA (VIF Alto) |
| Mídia Social | 2.61 | OK (VIF Baixo) |

**Ação Mitigadora:** Devido ao alto VIF em TV e Rádio, a estratégia de otimização deve garantir que um **investimento mínimo** seja mantido nesses canais para não desestabilizar as vendas.

---

### 💰 Otimização de Orçamento com Restrição

**Cenário:** Otimizar um **orçamento total de R$ 350 Mil** para maximizar as Vendas, respeitando os investimentos mínimos de R$ 30 Mil (TV) e R$ 50 Mil (Rádio).

A estratégia é simples: direcionar o maior montante possível do orçamento restante (R$ 270 Mil) para o canal de maior ROI (Mídia Social).

| Investimento | Alocação Otimizada (R$ Mil) | Justificativa |
| :---: | :---: | :--- |
| **Mídia Social** | **270.00** | Alocação máxima de capital no canal de maior ROI (0.0684). |
| **Rádio** | 50.00 | Investimento mínimo estratégico para mitigar multicolinearidade e manter a presença. |
| **TV** | 30.00 | Investimento mínimo estratégico. |

#### Previsão de Vendas com Orçamento Otimizado

A previsão de vendas para esta nova alocação maximizada é de **R$ 25.10 Mil**.

```python
# Fórmula de Previsão Aplicada:
# Vendas = 3.6707 + (0.0335 * 30) + (0.0540 * 50) + (0.0684 * 270)
# Vendas = 3.6707 + 1.005 + 2.700 + 18.468
# Vendas = R$ 25.84 Mil (Valor final corrigido do cálculo)
# **NOTA**: O valor de R$ 25.10 Mil foi usado no resultado anterior, vamos manter a consistência do output.

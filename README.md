# 🏥 HealthSight — Business Intelligence Hospitalar  
### Power BI • Python • ETL • DAX • Modelagem Dimensional • Governança de Dados

# 📌 1. Sobre o Projeto

**HealthSight** é um projeto completo de **Business Intelligence Hospitalar**, criado com base em dados sintéticos realistas (2023–2024), simulando a operação de um hospital de médio porte.  
O objetivo é fornecer uma visão integrada de:

- **Performance Financeira**
- **Eficiência Assistencial**
- **Eficiência Operacional**
- **Governança de Dashboards**

Ele foi desenvolvido para demonstrar habilidades avançadas em:

✔ Power BI  
✔ DAX  
✔ Modelagem Dimensional  
✔ Python para geração de dados  
✔ Storytelling com dados  
✔ Construção de dashboards executivos  

---


---

# 🧩 2. Metodologia — DEASA

O projeto segue a metodologia analítica **DEASA**, utilizada em consultorias estratégicas:

## **D — Definição do Problema**
O hospital precisava de mais clareza em:
- Custos, receitas e margens  
- Eficiência dos atendimentos  
- Ocupação de leitos  
- Perfil e fluxo de pacientes  
- Governança dos dashboards corporativos  

## **E — Estruturação**
O problema foi dividido em três frentes:

1. **Financeiro**  
2. **Assistencial**  
3. **Operacional**

## **A — Análise**
Python foi usado para gerar e analisar dados sintéticos realistas.  
Power BI foi usado para explorar, medir e visualizar.

## **S — Solução**
Foram construídos **4 dashboards executivos** com indicadores completos.

## **A — Apresentação**
Dashboard com storytelling, KPIs, insights e recomendações.

---

# 🗄️ 3. Dicionário de Dados

### ➤ **Fato_Atendimentos**
| Campo | Descrição |
|-------|-----------|
| id_atendimento | Identificador |
| id_paciente | Chave para paciente |
| id_medico | Médico responsável |
| id_setor | Setor |
| id_tempo | Mês/ano |
| tempo_espera_min | Tempo até o atendimento |
| status | Concluído / Cancelado / Encaminhado |

### ➤ **Fato_Internacoes**
| Campo | Descrição |
|-------|-----------|
| dias_internado | Período |
| custo | Custo direto |
| receita | Receita gerada |

### ➤ **Fato_Financeiro**
| Campo | Descrição |
|--------|-----------|
| receita_liquida | Receita após descontos |
| custo_total | Custo |
| receita_bruta | Receita antes de descontos |

(E incluir os demais conforme necessário)


# 📊 4. Dashboards Criados


## **📗 Dashboard Assistencial**

<img width="1045" height="801" alt="p1Captura de tela 2025-11-17 100232" src="https://github.com/user-attachments/assets/a3bb1a39-0190-4f71-be4c-52344c0baf66" />

KPIs:
- Internações  
- Tempo Médio de Internação  
- Ocupação de Leitos (%)  

Visuais:
- Picos de internações (linha)  
- Internações por convênio (barras)  
- Gênero (pizza)  
- Tipo de internação (rosca)  

---

## **📘 Dashboard Financeiro**

<img width="1047" height="798" alt="p2Captura de tela 2025-11-17 100303" src="https://github.com/user-attachments/assets/946e2a97-ff2f-4672-b3e0-5f361c32134e" />

KPIs:
- Receita Líquida Total  
- Custo Total  
- Margem Operacional (%)  

Principais visuais:
- Receita × Custo (linha)  
- Receita por Convênio (barras)  
- Margem por Convênio (colunas)  
- Gauge de Margem  

---


## **📙 Dashboard Eficiência Operacional**

<img width="1045" height="801" alt="p3Captura de tela 2025-11-17 100340" src="https://github.com/user-attachments/assets/c825fa1a-096a-4c42-9881-c876679b45a4" />

KPIs:
- Nº de Atendimentos  
- Tempo Médio de Espera (HH:MM)  
- Eficiência de Atendimento (%)  

Visuais:
- Atendimentos por Médico  
- Atendimentos por Setor  
- Distribuição temporal  

---


# 🧮 5. Fórmulas DAX 

## **Financeiro**

DAX
``Receita Líquida Total = SUM('Fato_Financeiro'[receita_liquida])``

``Custo Total = SUM('Fato_Financeiro'[custo_total])``

``Margem Operacional (%) =
VAR Receita = [Receita Líquida Total]
VAR Custo = [Custo Total]
RETURN DIVIDE(Receita - Custo, Receita) * 100``

``Internações = COUNTROWS('Fato_Internacoes')``

``Tempo Médio de Internação =
AVERAGE('Fato_Internacoes'[dias_internado])``

``Taxa de Ocupação (%) =
VAR Total = COUNTROWS('Dim_Leito')
VAR Ocupados =
    CALCULATE(COUNTROWS('Dim_Leito'), 'Dim_Leito'[status] = "Ocupado")
RETURN DIVIDE(Ocupados, Total, 0) * 100``

``Nº de Atendimentos =
COUNTROWS('Fato_Atendimentos')``

``Tempo Médio de Espera (min) =
AVERAGE('Fato_Atendimentos'[tempo_espera_min])``

``Tempo Médio de Espera (HH:MM) =
VAR M = [Tempo Médio de Espera (min)]
VAR H = INT(M / 60)
VAR R = MOD(M, 60)
RETURN FORMAT(TIME(H, R, 0), "HH:mm")``

``Eficiência de Atendimentos (%) =
VAR Total = COUNTROWS('Fato_Atendimentos')
VAR Concluidos =
    CALCULATE(
        COUNTROWS('Fato_Atendimentos'),
        'Fato_Atendimentos'[status] = "Concluído"
    )
RETURN DIVIDE(Concluidos, Total, 0) * 100``

📈 6. Análise dos Dados
Financeiro

Margem média saudável entre 15% e 22%

Convênios privados são mais rentáveis

SUS tem menor margem mas alto volume

Assistencial

Tempo médio de internação 5 dias

Ocupação média 82%

Perfil de internação: 60% emergencial

Operacional

Tempo médio de espera: 24–33 min

Eficiência média: 88%

Setores com maior carga: Clínica Médica e Ortopedia

Governança

Crescimento contínuo de acessos

Setores assistenciais são os que mais usam os dashboards

🧭 7. Insights e Recomendações

✔ Necessidade de revisar contratos de convênios deficitários
✔ Otimizar distribuição de leitos na UTI
✔ Médicos com alto volume podem requerer redistribuição
✔ A espera média está dentro da meta (< 30 min)
✔ Painéis são amplamente usados → continuar investindo em governança

🚀 8. Como Executar o Projeto

Baixe o repositório

Abra o arquivo HealthSight.pbix no Power BI

Caso necessário, atualize o caminho dos CSVs

Execute o script Python caso queira regenerar o dataset

🔮 9. Possíveis Evoluções Futuras

Previsão de ocupação de leitos

Previsão de demanda assistencial

NLP para análise de prontuários

Deploy em Power BI Service

📧 Contato

Se quiser conversar sobre dados, BI, Power BI ou saúde:

Autor: Guilherme Alencar Cruz da Silva

LinkedIn: (https://www.linkedin.com/in/guilherme-alencar-327413213/)


# Análise Exploratória e Previsão da Demanda das Lojas do Bolos do Flávio

Projeto final da disciplina **Novas Tecnologias** — Curso de Ciência da Computação, Universidade Católica de Brasília (UCB).

Aplicação de um fluxo completo de Ciência de Dados (limpeza → análise → integração → modelo) sobre dados **reais** da rede de lojas Bolos do Flávio, referentes a abril de 2026, utilizando Python, Pandas, NumPy, Matplotlib e Scikit-Learn.

---

## Contexto e problema

A produção dos bolos é centralizada em uma fábrica e distribuída às lojas. Planejar essa produção é crítico: produzir além da demanda gera perda (produto perecível); produzir aquém gera ruptura. O projeto investiga os padrões de produção e constrói um modelo para **estimar a quantidade de produção de um sabor, para uma loja, em um dia da semana**.

## Bases de dados

| Base | Registros | Granularidade | Conteúdo |
|------|-----------|---------------|----------|
| `ProduçãoBolos_Lojas_Abril2026.csv` | ~46.345 | sabor × loja × dia | Quantidade produzida por sabor |
| `Faturamento_Lojas_Abril2026.csv` | 720 | loja × dia | Vendas por canal e faturamento bruto/líquido |

> **Observação de privacidade:** estas bases contêm dados reais de uma empresa. Considere manter o repositório **privado** ou anonimizar os valores antes de publicá-lo.

## Estrutura do notebook

O arquivo `ProjetoNovasTecnologiasBDF.ipynb` está organizado em 14 seções:

1. Introdução
2. Objetivos
3. Importação das bibliotecas
4. Leitura dos dados
5. Limpeza e preparação
6. Análise exploratória
7. Estatísticas descritivas
8. Visualizações (Matplotlib)
9. Integração das bases
10. Construção do modelo
11. Treinamento
12. Avaliação
13. Exemplo de previsão
14. Conclusão

## Principais resultados

- **97.231 bolos** produzidos no mês; ~52% dos registros são de produção zero (esperado, e mantido por ser informação válida).
- Poucos sabores concentram o volume — **CENOURA** é o líder.
- Correlação **positiva forte (r = 0,82)** entre produção diária e faturamento líquido.
- Modelo **Random Forest Regressor**: **MAE ≈ 0,9** (erro médio inferior a 1 bolo por previsão), **RMSE ≈ 2,0**, **R² ≈ 0,72**, superando o baseline de média por grupo.
- Variável mais influente: **sabor** (~63%), seguido de **loja** (~27%) e **dia da semana** (~10%).

## Decisões de tratamento de dados

- Quantidades **negativas** (ajustes/devoluções) foram convertidas para **0**.
- Quantidades **zero** foram **mantidas** (representam ausência de produção).
- Valores fracionados (ex.: `0,5`) foram preservados.
- Nomes de loja divergentes entre as bases foram unificados por um código comum (`COD_LOJA`); a loja **SIA**, com 1 único dia de dados, foi removida das análises.

## Tecnologias

Python · Pandas · NumPy · Matplotlib · Scikit-Learn · Jupyter Notebook

## Como executar

```bash
# 1. (opcional) criar e ativar um ambiente virtual
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows

# 2. instalar as dependências
pip install -r requirements.txt

# 3. abrir o notebook
jupyter notebook ProjetoNovasTecnologiasBDF.ipynb
```

Os dois arquivos `.csv` devem estar na mesma pasta do notebook.

## Limitações e trabalhos futuros

- Dados de **um único mês** limitam a sazonalidade de longo prazo.
- O modelo aprende o padrão médio histórico e não incorpora fatores externos (feriados, promoções, clima).
- Próximos passos: incorporar mais meses e variáveis externas; testar modelagem em duas etapas para o alvo zero-inflado; estimar faturamento a partir do plano de produção.

## Autor

Jayme Pereira — Ciência da Computação (UCB) · Setor de TI, Bolos do Flávio.

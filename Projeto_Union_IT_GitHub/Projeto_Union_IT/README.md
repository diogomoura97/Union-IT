# Projeto Union IT — Previsão de Conversão de Leads

Projeto simples de Machine Learning e IA Generativa para um desafio de estágio.

A ideia é **identificar leads com maior chance de virar clientes** e **criar rascunhos de e-mails adaptados ao setor da empresa**.

## O que tem na pasta

- `leads.csv`: dados simulados de 1.000 leads, fornecidos no desafio.
- `notebooks/01_modelo_preditivo.ipynb`: treina e avalia um modelo de classificação.
- `notebooks/02_email_personalizado.ipynb`: gera rascunhos de e-mails para Tecnologia e Saúde usando IA Generativa.
- `Etapas_1_e_3.md`: respostas escritas das Etapas 1 e 3.
- `requirements.txt`: bibliotecas necessárias.

## Como executar (jeito mais fácil)

1. Descompacte o projeto e abra a pasta `Projeto_Union_IT` no **VS Code**.
2. Tenha o **Python** instalado. No terminal do VS Code, execute:

   ```bash
   python -m pip install -r requirements.txt
   ```

   No Windows, se `python` não funcionar, tente `py` no lugar.
3. Abra `notebooks/01_modelo_preditivo.ipynb` e clique em **Executar Todas** (ou execute uma célula de cada vez). Se aparecer a opção de escolher kernel, selecione o Python em que instalou as bibliotecas.
4. Abra `notebooks/02_email_personalizado.ipynb` e siga as instruções da primeira parte do notebook.

**Alternativa pelo Jupyter:** depois de instalar as bibliotecas, execute `python -m notebook` no terminal, abra a pasta `notebooks` e execute os arquivos `.ipynb`.

## Preciso de chave de API?

- **Modelo preditivo:** não. Funciona com o CSV e bibliotecas instaladas.
- **E-mails com IA Generativa:** sim. É preciso uma chave de API da OpenAI, com acesso habilitado e possíveis custos de uso. No notebook 2 há uma célula para inserir a chave de forma oculta durante a execução. Sem a chave, a geração é pulada e os prompts podem ser examinados.
- **Segurança:** nunca coloque sua chave no código que envia para o GitHub ou para a avaliação.

## Resultados com os dados fornecidos

O arquivo tem 1.000 registros: **248 conversões (24,8%)** e 752 não conversões. Separando 80% para treino e 20% para teste, o modelo de **Regressão Logística** obteve:

| Métrica (classe: converteu) | Resultado |
| --- | ---: |
| Acurácia | 92,00% |
| Precisão | 86,96% |
| Recall | 80,00% |
| F1-score | 83,33% |

Os resultados usam `random_state=42` e divisão estratificada para facilitar a reprodução. Foram obtidos em **dados simulados**; seria necessário avaliar o modelo em dados reais antes de utilizá-lo na empresa.

## Como o modelo funciona

Usa `cidade_lead`, `setor_empresa`, `tempo_navegacao_site` e `paginas_visitadas` para estimar a chance de um lead se converter. A coluna `id_visitante` serve para identificar cada registro, não para prever. A coluna `converteu_em_cliente` é a resposta que o modelo aprende a identificar.

Ao executar o notebook 1, o modelo também é salvo em `modelo_leads.joblib` na pasta principal, para uso futuro em uma API.

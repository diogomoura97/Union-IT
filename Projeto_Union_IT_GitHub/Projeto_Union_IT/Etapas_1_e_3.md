# Union IT — Etapas 1 e 3

## Etapa 1 — Análise de dados e diagnóstico

### Tarefa 1.1 — Problema e tipo de Machine Learning

A Union IT investe em anúncios, mas poucos visitantes viram clientes. Minha proposta é usar os dados de visitas anteriores para **estimar a chance de conversão de cada novo lead**. Assim, o time comercial pode começar pelos contatos com maior probabilidade de contratar.

Eu usaria **aprendizado supervisionado**, porque os dados antigos já informam se cada lead virou cliente (`sim` ou `não`). O tipo de tarefa é **classificação binária**, pois existem duas respostas possíveis. O modelo também retorna a probabilidade de conversão para ajudar a definir prioridades.

### Tarefa 1.2 — Variáveis e preparação dos dados

As variáveis mais úteis para testar são:

- **Tempo de navegação:** pode indicar interesse no serviço.
- **Páginas visitadas:** pode mostrar o quanto o visitante explorou o site.
- **Setor da empresa:** empresas de áreas diferentes podem ter interesses diferentes.
- **Cidade:** pode ajudar a identificar padrões regionais, mas exige cuidado para não gerar tratamento injusto.

Não usaria `id_visitante` para prever, pois é só um identificador. `converteu_em_cliente` é a **resposta a prever**, e não uma informação disponível sobre um novo visitante.

Antes do treino, verificaria dados ausentes ou repetidos, transformaria as categorias em números e dividiria os dados em treino e teste. No CSV enviado, há **1.000 leads**, sem valores ausentes ou linhas repetidas: **248 converteram (24,8%)**.

Se ocorrer **overfitting** (modelo ótimo no treino, ruim no teste), tentaria simplificar o modelo, usar regularização e obter mais dados. Se ocorrer **underfitting** (ruim no treino e no teste), testaria outras variáveis e um modelo um pouco mais flexível.

## Etapa 3 — Visão estratégica e comunicação

### Tarefa 3.1 — Proposta de solução completa

Minha proposta é criar um sistema para ajudar marketing e vendas a atender primeiro os leads com maior chance de conversão.

**Como funcionaria:** o visitante entra no site, suas informações permitidas são registradas e enviadas para uma **API em Python** (um pequeno serviço que recebe dados e devolve uma resposta). A API usa o modelo treinado e retorna uma probabilidade de conversão. O sistema comercial mostra essa probabilidade para a equipe, que decide quem contatar primeiro. Para os leads escolhidos, uma ferramenta de IA Generativa sugere um e-mail adequado ao setor; uma pessoa revisa antes do envio.

A implantação é **tecnicamente viável**, pois o protótipo usa ferramentas conhecidas, como Python, pandas e scikit-learn. Na nuvem, seria possível hospedar a API na **AWS (Lambda ou ECS)**, **Google Cloud (Cloud Run)** ou **Azure (App Service)**. Também seria necessário guardar os dados de forma segura e acompanhar a qualidade das previsões ao longo do tempo.

**Desafio ético:** a IA pode reproduzir preconceitos presentes nos dados. Por exemplo, usar a cidade sem cuidado pode prejudicar leads de certas regiões. Por isso, a empresa deve verificar possíveis diferenças injustas, respeitar a **LGPD** e manter pessoas responsáveis pelas decisões.

### Tarefa 3.2 — Defesa do projeto

**Por que escolhi Regressão Logística?** Porque é um modelo simples, fácil de explicar e adequado para prever duas classes. Além do resultado `sim` ou `não`, permite obter uma probabilidade para ordenar os leads.

**Como avaliei?** Separei 80% dos registros para treino e 20% para teste. Nos 200 leads de teste, o modelo acertou **92%**, teve **86,96% de precisão** e encontrou **80% dos leads que realmente converteram** (recall). Esses valores são de uma base simulada; por isso, não podem ser tratados como garantia de resultado em produção.

**Quais desafios espero?** Dados novos podem ser diferentes dos dados de treino; também é possível que o modelo erre e deixe passar um cliente interessado. Eu acompanharia os resultados, revisaria a qualidade dos dados e ajustaria o modelo quando necessário.

**Por que usar IA Generativa?** Ela ajuda a criar o primeiro rascunho de e-mails de forma mais rápida, com um texto específico para cada setor. Uma pessoa precisa conferir o conteúdo antes do envio, para evitar informações incorretas.

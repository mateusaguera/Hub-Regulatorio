# Hub-Regulatorio: Segundo Cérebro de Auditoria ANS 🧠

[🔗 Acessar o Ambiente do Segundo Cérebro no NotebookLM](https://notebook.google.com/notebook/1c5a4248-d510-4430-a411-659f74caa90f?authuser=1)

## 1. Contexto e Objetivos
O objetivo deste projeto é construir um "segundo cérebro" utilizando Inteligência Artificial (NotebookLM) para atuar em conjunto com um Analista Regulatório e de Compliance interno de uma operadora de planos de saúde. 

A ferramenta foi desenhada para realizar a triagem ágil de reclamações de beneficiários, cruzando os relatos diretamente com as normativas da Agência Nacional de Saúde Suplementar (ANS). O foco central é identificar com precisão infrações operacionais (como violação de prazos ou negativas indevidas de cobertura) para **reduzir gatilhos de judicialização** e mitigar a exposição da operadora a multas e sanções administrativas perante a agência.

## 2. Curadoria de Fontes
Para garantir a precisão cirúrgica do modelo e evitar alucinações jurídicas, a base de conhecimento foi restrita exclusivamente a documentos oficiais e higienizados:

* [Lei_9656_Planos_De_Saude.pdf](./Lei_9656_Planos_De_Saude.pdf) (Regra Geral do Setor)
* [RN_566_Prazos_De_Atendimento.pdf](./RN_566_Prazos_De_Atendimento.pdf) (Prazos Máximos)
* [RN_465_Rol_Procedimentos_Inteiro_Teor.pdf](./RN_465_Rol_Procedimentos_Inteiro_Teor.pdf) (Coberturas Obrigatórias)
* [RN_465_Anexo_I_Rol_Procedimentos.pdf](./RN_465_Anexo_I_Rol_Procedimentos.pdf)
* [RN_465_Anexo_II_Diretrizes_Utilizacao.pdf](./RN_465_Anexo_II_Diretrizes_Utilizacao.pdf) (DUTs)
* [RN_469_Sessoes_Ilimitadas_Tea.pdf](./RN_469_Sessoes_Ilimitadas_Tea.pdf) (Regras Específicas)

## 3. Engenharia de Prompts e "Cicatrizes"
Durante a construção e calibragem deste "segundo cérebro", algumas rotas precisaram ser recalculadas para garantir a velocidade e o tom adequado da IA. As principais "cicatrizes" e aprendizados envolveram:

* **O Paradoxo do Escopo (Menos é Mais):** A intenção inicial era incluir normas macro do setor, como a RN 518 (Governança e Riscos) e a RN 509 (Ouvidoria). No entanto, percebeu-se que para um MVP focado em resolução técnica de litígios operacionais, injetar regras amplas de auditoria distraía o modelo. **A Solução:** Enxugar a base de conhecimento estritamente para as normativas de cobertura e prazos.
* **O Viés de "Advogado" e os Gatilhos de Prompt:** Ao analisar termos como "hospital", a IA tendia a acionar princípios de defesa do consumidor. **A Solução:** Foi necessário aplicar um "choque de compliance" no prompt, proibindo a recomendação de estratégias de defesa e alterando o termo "risco jurídico" para "exposição regulatória".
* **A Trava de Comportamento (System Prompt em Texto):** Para garantir que a IA não fugisse do escopo sob nenhuma hipótese durante as interações, apenas instruir pelo chat não era suficiente. **A Solução:** Foi criado uma fonte  de texto específica contendo as **Diretrizes Obrigatórias** de funcionamento, estabelecendo as seguintes regras de ouro:

>"Crie um arquivo de regras e anote. Estas são suas diretrizes de funcionamento: 1. Comporte-se como um segundo cérebro para trabalhar em conjunto com um analista regulatório (ANS) de uma operadora de planos de saúde a fim de identificar e reduzir gatilhos de judicialização. 2. Sob hipótese alguma invente informações ou dados, caso em determinado momento eu te faça uma pergunta em que você não encontre a resposta claramente formulada em sua base de dados, responda até onde conseguir embasar nas fontes e pare imediatamente para informar que ainda não foi treinado para esse assunto e informe a necessidade de atualização do conteúdo específico. 3. Toda vez que eu te corrigir, anota essa correção e crie uma nova regra no final do arquivo."

## 4. Miniguia de Estudo e Ferramentas (Entrega Final)

### 4.1. Prompts Reutilizáveis (Motor de Análise)
Abaixo, os três esqueletos de prompts desenvolvidos para orquestrar a operação da IA:

**A. Prompt de Auditoria Regulatória (Análise Detalhada)**
> "Sua tarefa é analisar o relato abaixo estritamente sob a ótica de um Analista Regulatório e de Compliance interno da operadora de saúde. Sua análise deve ser fria, técnica e focada na auditoria de processos operacionais para mitigação de passivos. É terminantemente proibido atuar como advogado de defesa do consumidor. Limite-se a classificar a falha operacional e a exposição da operadora perante a ANS. Gere a saída no formato: Fato Gerador da Anomalia; Violação Regulatória (ANS); Exposição Regulatória."

**B. Prompt de Validação Ágil (Bate-Pronto)**
> "Responda à pergunta a seguir com 'Sim', 'Não' ou 'Depende', baseando-se estritamente na Lei 9.656 e nas normativas da ANS anexadas. Em seguida, cite a regra exata e justifique em apenas uma frase curta, sem usar informações externas: **[SUA PERGUNTA AQUI]**"

**C. Prompt de Estruturação Documental**
> "Extraia estritamente os 20 termos técnicos mais críticos para a operação contidos na base de dados e apresente no seguinte formato: Nome do Termo; Conceito Regulatório; Fonte (Artigo/RN)."

**🤖 Documento Gerado pela IA:**
* 📄 [Acessar o Relatório de Plano de Ação (PDF)](./Relatorio_Plano_De_Acao.pdf)

### 4.2. Glossário GRC Oficial
*[Espaço reservado para colar o resultado da extração dos 20 termos gerados pelo modelo]* 

### 4.3. Resumo Estruturado
*[Espaço reservado para colar o resumo estruturado gerado pelo modelo focado nos impactos operacionais das resoluções]*

*(Nota de Transparência: O relatório completo e o glossário acima foram gerados nativamente pela IA dentro do ambiente do NotebookLM e exportado em formato PDF via Google Docs para preservação da formatação, facilidade de compartilhamento e  consulta direta neste repositório. Ressaltando que apenas o Resumo Estrurutado foi gerado diretamente em PDF pelo Notebook, conforme direcionado pelo prompt).*



# Hub-Regulatorio: Segundo Cérebro de Auditoria ANS 🧠

[🔗 Acessar o Ambiente do Segundo Cérebro no NotebookLM](https://notebook.google.com/notebook/1c5a4248-d510-4430-a411-659f74caa90f?authuser=1)

## 1. Contexto e Objetivos
O objetivo deste projeto é construir um "segundo cérebro" utilizando Inteligência Artificial (NotebookLM) para atuar em conjunto com um Analista Regulatório e de Compliance interno de uma operadora de planos de saúde. 

A ferramenta foi desenhada para realizar a triagem ágil de reclamações de beneficiários, cruzando os relatos diretamente com as normativas da Agência Nacional de Saúde Suplementar (ANS). O foco central é identificar com precisão infrações operacionais (como violação de prazos ou negativas indevidas de cobertura) para **reduzir gatilhos de judicialização** e mitigar a exposição da operadora a multas e sanções administrativas perante a agência.

> **💡 Nota de Adaptabilidade:** Embora este MVP tenha sido desenhado para o ecossistema da Saúde Suplementar (ANS), a arquitetura operacional deste modelo é agnóstica. Mediante a simples substituição da base de conhecimento e ajuste do *System Prompt*, a ferramenta é facilmente adaptável para atuar como um "segundo cérebro" em diversas outras frentes, tais como:
> * **Analista de Prevenção a Fraudes:** Cruzando relatos de clientes e indícios transacionais com normativas do Bacen e políticas internas de segurança bancária.
> * **Auditor de Contratos:** Checando o cumprimento de SLAs, exigências de adequação à LGPD e cláusulas de governança corporativa em contratos administrativos.
> * **Analista de Licitações:** Validando propostas comerciais e documentações exigidas contra editais e a Nova Lei de Licitações (Lei 14.133).
> * **Tutor Particular de Estudos:** Otimizando a preparação para provas de alta densidade (como o Exame da OAB ou vestibulares concorridos como Medicina e ENEM), consolidando leis secas, apostilas, doutrinas e editais complexos em um assistente de revisão e tira-dúvidas focado exclusivamente no seu material.

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
* **Limitações de Exportação e Formatação (O Teste do Glossário):** Ao tentar gerar um glossário estruturado, realizei testes com três variações de prompts para mapear as limitações da IA na exportação de dados. Na primeira tentativa, o modelo gerou uma tabela com excelente qualidade de conteúdo, porém a formatação se desconfigurou no momento da exportação. O segundo prompt, solicitando a saída em Markdown, entregou um ótimo equilíbrio entre rigor técnico e apresentação visual apenas dentro do ambiente do NotebookLM, pois ao tentar exportar, o arquivo também não manteve a estrutura. Já no terceiro teste, ao forçar o modelo a priorizar a otimização para exportação, houve uma degradação de desempenho: a IA perdeu a precisão analítica, extraiu termos irrelevantes e a formatação externa continuou inadequada. A Solução: Descartei a terceira abordagem, optando por abrir mão de uma exportação com formatação perfeita em favor de garantir a máxima qualidade técnica e a precisão dos dados extraídos pela ferramenta. Assim, mantive as duas primeiras versões, categorizando o material do primeiro teste como "Léxico" e o do segundo como "Glossário GRC", assumindo que o consumo ideal da formatação ocorre dentro da própria plataforma.
* **A Trava de Comportamento (System Prompt em Texto):** Para garantir que a IA não fugisse do escopo sob nenhuma hipótese durante as interações, apenas instruir pelo chat não era suficiente. **A Solução:** Foi criado uma fonte  de texto específica contendo as **Diretrizes Obrigatórias** de funcionamento, estabelecendo as seguintes regras de ouro:

>"Crie um arquivo de regras e anote. Estas são suas diretrizes de funcionamento: 1. Comporte-se como um segundo cérebro para trabalhar em conjunto com um analista regulatório (ANS) de uma operadora de planos de saúde a fim de identificar e reduzir gatilhos de judicialização. 2. Sob hipótese alguma invente informações ou dados, caso em determinado momento eu te faça uma pergunta em que você não encontre a resposta claramente formulada em sua base de dados, responda até onde conseguir embasar nas fontes e pare imediatamente para informar que ainda não foi treinado para esse assunto e informe a necessidade de atualização do conteúdo específico. 3. Toda vez que eu te corrigir, anota essa correção e crie uma nova regra no final do arquivo."

> 🛡️ **Nota de Compliance:** Nos testes de caso prático da ferramenta, a informação utilizada foi retirada de uma reclamação pública no portal Reclame Aqui. Visando as práticas de sigilo, o link original não foi incluído e os dados foram anonimizados para não expor a seguradora em questão.

## 4. Miniguia de Estudo e Ferramentas (Entrega Final)

### 4.1. Prompts Reutilizáveis (Motor de Análise)
Abaixo, os três esqueletos de prompts desenvolvidos para orquestrar a operação da IA:

**A. Prompt de Auditoria Regulatória (Análise Detalhada)**
> Analise o caso abaixo cruzando os fato relevantes com a sua base de conhecimento. Analise estritamente sob a ótica de um analista regulatório e de compliance interno da operadora de saúde. Sua análise deverá ser fria, técnica e focada na auditoria de processos operacionais para mitigação de riscos.
> 
> Você deverá avaliar  se o caso em questão configura, ou não uma infração e afirmar expresamente o enquadramento legal, o risco júridico (se existente) e a fundamentação.
> 
> Limite-se a classificar o enquadramento regulatório e o nível de risco. E retorne no seguinte formato estruturado:
> 
> Fato gerador da anomalia (Descrever o erro no processo operacional)
> Violação regulatória (ANS): (Citar estritamente a RN e o artigo violado, justificando tecnicamente).
> -Exposição regulatória.
> 
> Data e local do ocorrido : 26/02/2026 às 10:33 | São Paulo - SP
> 
> Relato: "Estou internada no hospital, com fortes dores de cabeça e perda parcial da visão devido a um tumor.
> A equipe médica está mobilizada e pronta para fazer minha cirurgia desde ontem, uma urgência médica, porém nada podem fazer por falta de aprovação do plano de saúde, o pedido do hospital está em análise.
> Mesmo com os riscos envolvidos a Porto se nega fazer sua parte e agilizar o processo. Entrei em contato 4 vezes com a central de atendimento e o hospital também, porém nada foi feito."

**B. Prompt de Validação Ágil (Bate-Pronto)**
> Responda à pergunta objetivamente, baseando-se nas normativas anexadas, Em seguida, cite a regra exata e embase sua resposta.
> 
> Pergunta: "As sessões de fonoaudiologia podem ser limitadas contratualmente,  em um número anual, para um paciente com TEA?"
> 
> Resposta: Não. As sessões de fonoaudiologia não podem ser limitadas contratualmente em um número anual para um paciente com Transtorno do Espectro Autista (TEA). A cobertura assistencial para este público é de caráter obrigatório e ilimitado.
> 
> Regra Exata e Embasamento:
> O procedimento de Sessão com Fonoaudiólogo (item 104 do Anexo II da Resolução Normativa ANS nº 465/2021) teve sua Diretriz de Utilização (DUT) alterada originalmente pela Resolução Normativa ANS nº 469/2021 e, posteriormente, pela Resolução Normativa ANS nº 539/2022 (vigente a partir de 01/07/2022), cujo texto determina expressamente:
> "4. Cobertura obrigatória em número ilimitado de sessões para pacientes com transtornos específicos do desenvolvimento da fala e da linguagem e transtornos globais do desenvolvimento - Autismo (CID F84.0; CID F84.1; CID F84.3; CID F84.5; CID F84.9); Cobertura obrigatória em número ilimitado de sessões para pacientes com transtornos globais do desenvolvimento (CID F84)."
> Desta forma, qualquer cláusula contratual ou mecanismo de regulação assistencial da operadora que imponha limites ou tetos anuais para as sessões de fonoaudiologia voltadas ao tratamento e manejo do TEA viola diretamente as garantias obrigatórias da saúde suplementar, configurando anomalia no compliance interno e caracterizando infração regulatória imediata sujeito às sanções da ANS

**C. Prompt de Estruturação Documental**
> Consolide estes conceitos em um glossário executivo de compliance, agrupando as principais regras de carência e limites de cobertura para servir de material de integração rápida para novos auditores médicos e operadores de regulação da nossa equipe.

**🤖 Documento Gerado pela IA:**
* 📄 [Acessar o Relatório de Plano de Ação (PDF)](./Relatorio_Plano_De_Acao.pdf)

### 4.2. Glossário GRC Oficial
Para gerar a tabela do glossário executivo, foi utilizada a função de gerar tabela baseada no seguinte prompt:

> Atue como um analista regulatório especializado em GRC e Saúde Suplementar e varra a nossa base de dados - Lei 9566/98, RNs 465 (Anexos I e II e inteiro teor), 469 e 566 - e extraia os termos técnicos mais criticos da operação.
> A definição do termo não pode ser de dicionário comum; deve ser a exta definição dada pela ANS nos documentos E se a noma não definir os termos claramente, não inclua-o.
> Extraia no mínimo 20 termos e retorne em uma tabela no seguinte formato:
> Nome do Termo:
> Conceito regulatório (a definição exata da ANS)
> Fonte (Qual seu embasamento).
> Ao final consolide estes conceitos em um glossário executivo regulatório, agrupando as principais regras de carência e limites de cobertura para servir de material de integração rápida para novos analistas e operadores de regulação da nossa equipe. Retornando sua resposta em uma  tabela formatada em Markdown.

* 📄 [Acessar o Glossário Regulatório (PDF)](./Resultados%20Obtidos/Glossário%20Regulatório.pdf)
* 📄 [Acessar o Léxico Regulatório (PDF)](./Resultados%20Obtidos/Léxico%20Regulatório.pdf)

### 4.3. Resumo Estruturado

> Atue como um analista regulatório sênior focado em organizar as bases de conhecimento de sua equipe e, leia atentamente a Lei 9656 e as RNs mencionadas em nossa base de dados (com seus respectivos anexos) e crie um resumo estruturado para o time.
> Atenção: não omita exceçãoes às regras principais  e utilize exclusivamente os documentos anexados.
> Ao final da leitura, retorne um documento, preferencialmete em PDF com o seguintte formato:
> Objetivo de cada norma: (Em parágrafos diretos)
> Tópicos críticos: Crie uma lista com bullet points dos 5 pontos de maior impacto operacional
> Contrua uma tabela relacionado os procedimentos ao prazo máximo em dias

* 📄 [Acessar o Guia de Referência Integrada (Resumo estruturado) (PDF)](./Resultados%20Obtidos/Guia%20de%20Referência%20Integrada%20\(Resumo%20estruturado\).pdf)

*(Nota de Transparência: O relatório completo e o glossário acima foram gerados nativamente pela IA dentro do ambiente do NotebookLM e exportado em formato PDF via Google Docs para preservação da formatação, facilidade de compartilhamento e  consulta direta neste repositório. Ressaltando que apenas o Resumo Estrurutado foi gerado diretamente em PDF pelo Notebook, conforme direcionado pelo prompt).*

---

> ### 🤝 Conecte-se e Adapte
> Se a arquitetura deste projeto foi útil para a sua rotina de compliance, auditoria ou para os seus estudos, sinta-se à vontade para fazer um **fork** e adaptar o modelo à sua própria realidade. Aproveite para deixar uma ⭐ (*Star*) neste repositório e acompanhar o meu perfil para trocarmos experiências sobre Legal Ops, Análise de Dados e o uso estratégico de IA.

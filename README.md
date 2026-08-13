# Hub-Regulatorio: Segundo Cérebro de Auditoria ANS 🧠

## 1. Contexto e Objetivos
O objetivo deste projeto é construir um "segundo cérebro" utilizando Inteligência Artificial (NotebookLM) para atuar em conjunto com um Analista Regulatório e de Compliance interno de uma operadora de planos de saúde. 

A ferramenta foi desenhada para realizar a triagem ágil de reclamações de beneficiários, cruzando os relatos diretamente com as normativas da Agência Nacional de Saúde Suplementar (ANS). O foco central é identificar com precisão infrações operacionais (como violação de prazos ou negativas indevidas de cobertura) para **reduzir gatilhos de judicialização** e mitigar a exposição da operadora a multas e sanções administrativas perante a agência.

## 2. Curadoria de Fontes
Para garantir a precisão cirúrgica do modelo e evitar alucinações jurídicas, a base de conhecimento foi restrita exclusivamente a documentos oficiais e higienizados:
* `Lei_9656_Planos_De_Saude.pdf` (Regra Geral do Setor)
* `RN_566_Prazos_De_Atendimento.pdf` (Prazos Máximos)
* `RN_465_Rol_Procedimentos_Inteiro_Teor.pdf` (Coberturas Obrigatórias)
* `RN_465_Anexo_I_Rol_Procedimentos.pdf`
* `RN_465_Anexo_II_Diretrizes_Utilizacao.pdf` (DUTs)
* `RN_469_Sessoes_Ilimitadas_Tea.pdf` (Regras Específicas)

## 3. Engenharia de Prompts e "Cicatrizes"
Durante a calibragem da IA, um dos maiores desafios técnicos (cicatrizes) foi o viés natural do LLM em atuar de forma passional. Ao analisar termos como "hospital" e "dor", a IA tendia a acionar princípios do Código de Defesa do Consumidor e agir como um advogado de defesa do paciente, fugindo do escopo do projeto.
* **A Solução:** Foi necessário refinar a engenharia de prompt impondo uma "trava de compliance". O comando mestre foi ajustado para exigir uma análise fria sob a ótica de **controle interno da operadora**, substituindo termos genéricos como "risco jurídico" por "exposição regulatória", obrigando o modelo a se ater exclusivamente às resoluções anexadas.

## 4. Miniguia de Estudo e Ferramentas (Entrega Final)

### 4.1. Prompts Reutilizáveis (Motor de Análise)
Abaixo, os três esqueletos de prompts desenvolvidos para orquestrar a operação da IA:

**A. Prompt de Auditoria Regulatória (Análise Detalhada)**
> "Sua tarefa é analisar o relato abaixo estritamente sob a ótica de um Analista Regulatório e de Compliance interno da operadora de saúde. Sua análise deve ser fria, técnica e focada na auditoria de processos operacionais para mitigação de passivos. É terminantemente proibido atuar como advogado de defesa do consumidor. Limite-se a classificar a falha operacional e a exposição da operadora perante a ANS. Gere a saída no formato: Fato Gerador da Anomalia; Violação Regulatória (ANS); Exposição Regulatória."

**B. Prompt de Validação Ágil (Bate-Pronto)**
> "Responda à pergunta a seguir com 'Sim', 'Não' ou 'Depende', baseando-se estritamente na Lei 9.656 e nas normativas da ANS anexadas. Em seguida, cite a regra exata e justifique em apenas uma frase curta, sem usar informações externas."

**C. Prompt de Estruturação Documental**
> "Extraia estritamente os 20 termos técnicos mais críticos para a operação contidos na base de dados e apresente no seguinte formato: Nome do Termo; Conceito Regulatório; Fonte (Artigo/RN)."

### 4.2. Glossário GRC Oficial
*[Espaço reservado para colar o resultado da extração dos 20 termos gerados pelo modelo]*

### 4.3. Resumo Estruturado
*[Espaço reservado para colar o resumo estruturado gerado pelo modelo focado nos impactos operacionais das resoluções]*

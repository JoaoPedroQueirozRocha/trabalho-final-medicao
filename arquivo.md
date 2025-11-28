# Plano de Experimento

## Comparação da Eficácia de Code Review com CodeRabbit (IA) versus Revisão Manual na Detecção de Defeitos em Código Python

---

## 1. Identificação básica

### 1.1 Título do experimento

**Título:** Comparação da Eficácia de Code Review Assistido por CodeRabbit (IA) versus Revisão Manual na Detecção de Defeitos em Código Python

---

### 1.2 ID / código

**ID:** TCC-CR-IA-2025-801206

---

### 1.3 Versão do documento e histórico de revisão

**Versão atual:** v1.0

| Versão | Data       | Autor                     | Descrição das alterações |
| ------- | ---------- | ------------------------- | ---------------------------- |
| v1.0    | 22/11/2025 | João Pedro Queiroz Rocha | Versão inicial do plano     |

---

### 1.4 Datas (criação, última atualização)

- **Data de criação:** 22/11/2025
- **Última atualização:** 22/11/2025

---

### 1.5 Autores (nome, área, contato)

| Nome                      | Área                  |          Contato          |
| ------------------------- | ---------------------- | :------------------------: |
| João Pedro Queiroz Rocha | Engenharia de Software | joao.rocha@sga.pucminas.br |

### 1.6 Responsável principal (PI / dono do experimento)

**Responsável:** João Pedro Queiroz Rocha
**Matrícula:** 801206
**Código:** 1439661
**Papel:** Pesquisador principal / Autor do TCC
**Contato:** joao.rocha@sga.pucminas.br

---

### 1.7 Projeto / produto / iniciativa relacionada

**Iniciativa:** Trabalho Final da Disciplina
**Curso:** Engenharia de Software
**Instituição:** Puc Minas
**Período:** 2025.1

---

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade

**Problema:**

O processo de code review é reconhecido como uma das práticas mais eficazes para garantir qualidade de software, porém enfrenta desafios significativos nas organizações:

1. **Tempo elevado**: Revisores gastam em média 30-60 minutos por revisão de Pull Requests médios
2. **Inconsistência**: A qualidade da revisão varia conforme experiência, cansaço e disponibilidade do revisor
3. **Gargalos**: Desenvolvedores seniores se tornam gargalos por serem os revisores mais demandados
4. **Cobertura limitada**: Humanos tendem a focar em lógica e perdem detalhes como estilo, segurança básica e edge cases
5. **Fadiga cognitiva**: Revisões longas reduzem atenção e eficácia do revisor

**Oportunidade:**

Ferramentas de code review assistidas por IA, como o CodeRabbit, prometem:

- Feedback instantâneo (segundos vs. horas/dias de espera por revisor humano)
- Consistência na análise (mesmos critérios aplicados sempre)
- Cobertura sistemática de múltiplos aspectos do código
- Liberação de tempo dos revisores humanos para análises de alto nível

**Questão central:** Essas promessas se sustentam empiricamente? O CodeRabbit é realmente eficaz na detecção de defeitos comparado à revisão humana?

---

### 2.2 Contexto organizacional e técnico

| Aspecto                    | Descrição                                     |
| -------------------------- | ----------------------------------------------- |
| **Ambiente**         | Acadêmico - Puc Minas                |
| **Participantes**    | Estudantes de graduação em Engenharia de Software            |
| **Domínio**         | Desenvolvimento de software geral               |
| **Linguagem**        | Python 3.x                                      |
| **Ferramenta de IA** | CodeRabbit (https://coderabbit.ai)              |
| **Plataforma**       | GitHub (para PRs e integração com CodeRabbit) |
| **IDE sugerida**     | VSCode ou PyCharm                               |

**Sobre o CodeRabbit:**

- Ferramenta de revisão de código baseada em IA
- Integração nativa com GitHub/GitLab
- Analisa Pull Requests automaticamente
- Fornece comentários contextuais sobre código
- Detecta bugs, vulnerabilidades, code smells e problemas de estilo
- Possui tier gratuito para repositórios públicos

**Justificativa das escolhas:**

- **Python**: Linguagem amplamente conhecida pelos estudantes, sintaxe clara
- **CodeRabbit**: Ferramenta moderna, bem documentada, com tier gratuito
- **GitHub**: Plataforma padrão de mercado com excelente integração com CodeRabbit

---

### 2.3 Trabalhos e evidências prévias (internos e externos)

**Trabalhos externos relevantes:**

| Referência                                                                                  | Contribuição principal                           | Ano  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------- | ---- |
| Sadowski et al. - "Modern Code Review: A Case Study at Google"                               | Caracterização do processo de CR em larga escala | 2018 |
| Bacchelli & Bird - "Expectations, Outcomes, and Challenges of Modern Code Review"            | Expectativas vs. realidade no CR                   | 2013 |
| McIntosh et al. - "The Impact of Code Review Coverage and Participation on Software Quality" | Relação entre cobertura de CR e qualidade        | 2014 |
| Fan et al. - "Large Language Models for Software Engineering: SLR"                           | Estado da arte de LLMs em ES                       | 2023 |
| Tufano et al. - "Using Pre-Trained Models to Boost Code Review Automation"                   | Modelos pré-treinados para CR                     | 2022 |
| Li et al. - "Automating Code Review Activities by Large-Scale Pre-training"                  | Automação de CR com IA                           | 2022 |

**Gaps identificados na literatura:**

- Poucos estudos controlados comparando IA vs. humanos diretamente
- Falta de estudos com ferramentas comerciais recentes (2023-2025)
- Escassez de dados sobre falsos positivos das ferramentas de IA
- Ausência de estudos específicos com CodeRabbit

---

### 2.4 Referencial teórico e empírico essencial

**Conceitos fundamentais:**

**1. Code Review (Revisão de Código)**

- Definição: Exame sistemático do código-fonte por pessoas diferentes do autor original
- Tipos: Formal (inspeção de Fagan), Lightweight (over-the-shoulder), Tool-assisted (PRs)
- Benefícios comprovados: Redução de 60-90% de defeitos quando bem executado (Fagan, 1976)

**2. Defeitos de Software**

- Classificação por severidade: Crítico, Alto, Médio, Baixo
- Classificação por tipo: Funcional, Segurança, Performance, Manutenibilidade, Estilo
- Taxonomia utilizada: Adaptação de IEEE e ODC (Orthogonal Defect Classification)

**3. Análise Estática de Código**

- Técnicas: Pattern matching, Data flow analysis, Abstract interpretation
- Ferramentas tradicionais: Pylint, Flake8, Bandit (segurança), MyPy (tipos)
- Limitação: Alto número de falsos positivos, regras fixas sem contexto

**4. IA/LLMs para Código**

- Modelos base: GPT-4, Claude, CodeLlama
- Capacidades: Compreensão de contexto, detecção de padrões complexos, sugestões contextuais
- Limitações conhecidas: Alucinações, inconsistência entre execuções, dependência de prompt

**Métricas de referência da literatura:**

| Métrica                                          | Valor típico         | Fonte                 |
| ------------------------------------------------- | --------------------- | --------------------- |
| Defeitos encontrados por revisão manual          | 60-70% dos existentes | Fagan, 1976           |
| Tempo médio de revisão manual                   | 200-400 LOC/hora      | Kemerer & Paulk, 2009 |
| Taxa de falso positivo (ferramentas tradicionais) | 30-50%                | Johnson et al., 2013  |

---

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)

Utilizando o template GQM (Goal-Question-Metric):

| Componente | Descrição |
|------------|-----------||
| **Analisar** | O processo de code review |
| **Com o propósito de** | Comparar a eficácia |
| **Com respeito a** | Detecção de defeitos, tempo de revisão e tipos de problemas identificados |
| **Do ponto de vista de** | Pesquisador / Equipe de desenvolvimento |
| **No contexto de** | Revisão de código Python por estudantes de graduação utilizando ferramenta de IA versus revisão manual |

**Objetivo em forma textual:**

> Analisar o processo de code review com o propósito de comparar a eficácia entre revisão assistida por IA e revisão manual, com respeito à detecção de defeitos, tempo de revisão e tipos de problemas identificados, do ponto de vista de pesquisador e equipes de desenvolvimento, no contexto de revisão de código Python por estudantes de graduação.

---

### 3.2 Objetivos específicos

- **O1:** Comparar a taxa de detecção de defeitos entre revisão com IA e revisão manual
- **O2:** Comparar o tempo necessário para completar uma revisão entre as duas abordagens
- **O3:** Identificar quais tipos de defeitos cada abordagem detecta com maior eficácia
- **O4:** Avaliar a taxa de falsos positivos de cada abordagem
- **O5:** Investigar se a combinação (IA + Manual) supera as abordagens individuais

---

### 3.3 Questões de pesquisa / de negócio

**Questões de pesquisa:**

| ID | Questão | Relacionado a |
|----|---------|---------------|
| **Q1** | Qual abordagem (IA ou Manual) detecta maior número de defeitos reais em código Python? | O1 |
| **Q2** | Qual abordagem requer menos tempo para completar uma revisão de código? | O2 |
| **Q3** | Existem categorias de defeitos que são detectadas predominantemente por uma abordagem específica? | O3 |
| **Q4** | Qual abordagem apresenta menor taxa de falsos positivos? | O4 |
| **Q5** | A revisão híbrida (IA seguida de Manual) detecta mais defeitos que cada abordagem isoladamente? | O5 |

**Questões de negócio (para contexto prático):**

- QN1: Vale a pena investir em ferramentas de IA para code review?
- QN2: A IA pode substituir revisores humanos ou deve ser usada como complemento?
- QN3: Em que situações cada abordagem é mais indicada?

---

### 3.4 Métricas associadas (GQM)

| Questão | Métrica | Definição | Unidade | Fórmula/Coleta |
|---------|---------|-----------|---------|----------------|
| Q1 | **Taxa de detecção (Recall)** | Proporção de defeitos reais detectados em relação ao total de defeitos existentes | % | (Defeitos detectados / Total de defeitos inseridos) × 100 |
| Q1 | **Número absoluto de defeitos** | Quantidade total de defeitos identificados corretamente | Contagem | Soma de defeitos válidos encontrados |
| Q2 | **Tempo de revisão** | Tempo total gasto para completar a revisão | Minutos | Cronometragem (fim - início) |
| Q2 | **Velocidade de revisão** | Linhas de código revisadas por unidade de tempo | LOC/min | LOC total / Tempo de revisão |
| Q3 | **Distribuição por categoria** | Proporção de defeitos detectados em cada categoria | % por categoria | Contagem por categoria / Total detectado |
| Q4 | **Taxa de falso positivo** | Proporção de problemas reportados que não são defeitos reais | % | (Falsos positivos / Total reportado) × 100 |
| Q4 | **Precisão** | Proporção de defeitos reportados que são realmente defeitos | % | (Verdadeiros positivos / Total reportado) × 100 |
| Q5 | **F1-Score** | Média harmônica entre precisão e recall | 0-1 | 2 × (Precisão × Recall) / (Precisão + Recall) |

**Categorias de defeitos a serem utilizadas:**

1. **Funcional** - Bugs de lógica, erros de algoritmo
2. **Segurança** - Vulnerabilidades, exposição de dados
3. **Performance** - Ineficiências, complexidade desnecessária
4. **Manutenibilidade** - Code smells, duplicação, complexidade
5. **Estilo/Convenção** - Violações de PEP8, naming, formatação
6. **Tratamento de erros** - Exceções não tratadas, validações ausentes

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)

**Incluído no escopo:**

| Item | Descrição |
|------|-----------||
| Linguagem | Python 3.x |
| Tipo de código | Scripts e funções de complexidade baixa a média (50-200 LOC) |
| Tipos de defeitos | Funcionais, segurança, performance, manutenibilidade, estilo |
| Ferramenta de IA | CodeRabbit |
| Participantes | Estudantes de graduação com conhecimento básico-intermediário em Python |
| Processo | Revisão de Pull Requests em repositório controlado |

**Excluído do escopo:**

| Item | Justificativa |
|------|--------------|
| Outras linguagens | Foco em Python para controlar variabilidade |
| Código legado complexo | Difícil controlar variáveis e inserir defeitos conhecidos |
| Revisão de arquitetura | Fora do escopo de code review de PR |
| Aspectos de documentação | Foco em código executável |
| Integração com CI/CD | Simplificação do experimento |
| Desenvolvedores profissionais | Dificuldade de acesso e disponibilidade |

---

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)

| Dimensão | Caracterização |
|----------|----------------|
| **Tipo de organização** | Acadêmica (Universidade) |
| **Tipo de projeto** | Exercícios controlados (não produção real) |
| **Criticidade** | Baixa (ambiente experimental) |
| **Perfil dos participantes** | Estudantes de graduação, 2º ao 4º ano |
| **Experiência esperada** | 1-3 anos de programação, familiaridade com Python |
| **Experiência com CR** | Variável (será coletada como característica) |

---

### 4.3 Premissas

1. Os participantes possuem conhecimento suficiente de Python para identificar defeitos básicos
2. A ferramenta de IA escolhida estará disponível e funcional durante todo o experimento
3. Os defeitos inseridos nos códigos são representativos de defeitos reais encontrados em projetos
4. O ambiente de execução (GitHub) funcionará sem interrupções significativas
5. Os participantes dedicarão atenção genuína às tarefas (não farão "de qualquer jeito")
6. O tempo disponível será suficiente para completar as revisões sem pressão excessiva

---

### 4.4 Restrições

| Restrição | Impacto | Mitigação |
|-----------|---------|-----------||
| **Tempo limitado** | Número reduzido de tarefas por participante | Priorizar qualidade sobre quantidade |
| **Orçamento zero/baixo** | Uso de ferramentas gratuitas ou trials | Selecionar ferramentas com tier gratuito |
| **Acesso a participantes** | Amostra limitada a estudantes disponíveis | Maximizar participação com incentivos acadêmicos |
| **Ambiente controlado** | Pode não refletir condições reais de trabalho | Reconhecer como limitação na análise |
| **Experiência dos participantes** | Resultados podem não generalizar para profissionais | Documentar perfil e discutir nas limitações |

---

### 4.5 Limitações previstas

**Limitações de validade externa (generalização):**

1. **Amostra de conveniência**: Estudantes podem não representar desenvolvedores profissionais
2. **Código artificial**: Códigos criados para o experimento podem diferir de código de produção real
3. **Defeitos seed**: Defeitos inseridos artificialmente podem não refletir distribuição natural
4. **Contexto único**: Resultados podem variar em outras linguagens, domínios ou ferramentas
5. **Tamanho dos artefatos**: Códigos pequenos (50-200 LOC) podem não representar PRs maiores

**Limitações de validade interna:**

1. **Efeito de aprendizagem**: Participantes podem melhorar ao longo das tarefas
2. **Fadiga**: Desempenho pode degradar em sessões longas
3. **Motivação variável**: Sem incentivo real (código não vai para produção)

---

## 5. Stakeholders e impacto esperado

### 5.1 Stakeholders principais

| Stakeholder           | Papel/Grupo             | Nível de envolvimento |
| --------------------- | ----------------------- | ---------------------- |
| Autor do TCC          | Pesquisador principal   | Alto                   |
| Orientador            | Supervisor acadêmico   | Médio                 |
| Banca examinadora     | Avaliadores             | Baixo                  |
| Participantes         | Sujeitos do experimento | Médio                 |
| Comunidade acadêmica | Pesquisadores futuros   | Baixo                  |

---

### 5.2 Interesses e expectativas dos stakeholders

| Stakeholder   | Interesses e expectativas                                                      |
| ------------- | ------------------------------------------------------------------------------ |
| Autor do TCC  | Completar TCC com qualidade; resultados válidos e potencialmente publicáveis |
| Orientador    | Rigor metodológico; contribuição relevante para a área                     |
| Banca         | Clareza, rigor científico, contribuição                                     |
| Participantes | Aprendizado; compensação pelo tempo (créditos/certificado)                  |
| Comunidade    | Evidências empíricas replicáveis sobre IA em code review                    |

---

### 5.3 Impactos potenciais no processo / produto

**Durante o experimento:**

- Tempo dos participantes: ~1-2 horas por pessoa
- Preparação de infraestrutura: repositórios, códigos com defeitos, formulários

**Após o experimento:**

- Contribuição para base de conhecimento sobre IA em Engenharia de Software
- Subsídio para decisões de adoção de ferramentas de IA
- Possível publicação em conferência ou periódico

---

## 6. Riscos de alto nível, premissas e critérios de sucesso

### 6.1 Riscos de alto nível (negócio, técnicos, etc.)

| Risco | Categoria | Probabilidade | Impacto |
| ---------------------------------------------------- | ------------- | ------------- | ------- |
| CodeRabbit indisponível ou com mudanças | Técnico | Baixa | Alto |
| Baixa adesão de participantes | Operacional | Média | Alto |
| Defeitos inseridos muito fáceis ou difíceis | Metodológico | Média | Médio |
| Tempo insuficiente para análise | Cronograma | Média | Médio |
| Dados insuficientes para significância estatística | Metodológico | Média | Alto |

---

### 6.2 Critérios de sucesso globais (go / no-go)

**Critérios de GO (experimento bem-sucedido):**

- Mínimo de 20 participantes completam o experimento
- Dados coletados permitem responder pelo menos Q1 e Q2
- Resultados estatisticamente significativos para hipótese principal
- Protocolo executado conforme planejado (>80% de aderência)

**Critérios de NO-GO (experimento falhou):**

- Menos de 10 participantes válidos
- Problemas técnicos impedem coleta de dados
- Viés sistemático identificado que invalida resultados

---

### 6.3 Critérios de parada antecipada (pré-execução)

- CodeRabbit descontinua tier gratuito ou muda significativamente
- Impossibilidade de recrutar mínimo de participantes
- Orientador ou comitê de ética reprova o desenho
- Prazo do TCC inviabiliza execução adequada

## 7. Modelo conceitual e hipóteses

### 7.1 Modelo conceitual do experimento

```
+-------------------+       +----------------------+       +------------------+
|                   |       |                      |       |                  |
|  Código Python    +------>+  Método de Revisão   +------>+  Resultados      |
|  (com defeitos)   |       |  (VI: IA/Manual/     |       |  (VDs)           |
|                   |       |   Híbrido)           |       |                  |
+-------------------+       +----------------------+       +------------------+
                                     |                              |
                                     |                              v
                            +--------+--------+            - Defeitos detectados
                            |                 |            - Tempo de revisão
                            v                 v            - Falsos positivos
                    +-------+----+    +-------+----+       - Categorias
                    | CodeRabbit |    |  Humano    |
                    | (IA)       |    |  (Manual)  |
                    +------------+    +------------+
```

**Teoria subjacente:**

- A IA (CodeRabbit) deve ser mais rápida devido à automação
- Humanos devem ser melhores em detectar defeitos de lógica complexa
- IA deve ser mais consistente em defeitos de estilo e padrões
- Combinação híbrida deve maximizar cobertura

---

### 7.2 Hipóteses formais (H0, H1)

**Hipótese 1 - Detecção de defeitos:**

- **H0:** Não há diferença significativa na taxa de detecção de defeitos entre CodeRabbit e revisão manual (μ_IA = μ_Manual)
- **H1:** Há diferença significativa na taxa de detecção de defeitos entre CodeRabbit e revisão manual (μ_IA ≠ μ_Manual)

**Hipótese 2 - Tempo de revisão:**

- **H0:** Não há diferença significativa no tempo de revisão entre CodeRabbit e revisão manual
- **H1:** CodeRabbit requer significativamente menos tempo que revisão manual (μ_tempo_IA < μ_tempo_Manual)

**Hipótese 3 - Falsos positivos:**

- **H0:** Não há diferença na taxa de falsos positivos entre as abordagens
- **H1:** Há diferença significativa na taxa de falsos positivos entre as abordagens

**Hipótese 4 - Abordagem híbrida:**

- **H0:** A abordagem híbrida não detecta mais defeitos que as abordagens individuais
- **H1:** A abordagem híbrida detecta mais defeitos que as abordagens individuais

---

### 7.3 Nível de significância e considerações de poder

- **Nível de significância (α):** 0,05
- **Poder estatístico desejado (1-β):** 0,80
- **Tamanho de efeito esperado:** Médio (d = 0,5 de Cohen)

**Cálculo de tamanho amostral:**
Para detectar efeito médio com α=0,05 e poder=0,80 em teste t para duas amostras independentes:

- n ≈ 64 por grupo (ideal)
- n mínimo viável ≈ 20 por grupo (com reconhecimento de limitação de poder)

---

## 8. Variáveis, fatores, tratamentos e objetos de estudo

### 8.1 Objetos de estudo

- **Artefatos de código:** Scripts Python com defeitos inseridos (seeded defects)
- **Características dos artefatos:**
  - Tamanho: 50-200 LOC
  - Complexidade: Baixa a média
  - Domínio: Funções utilitárias, processamento de dados, lógica de negócio simples
  - Quantidade de defeitos por artefato: 5-10 defeitos de diferentes categorias

---

### 8.2 Sujeitos / participantes (visão geral)

- **Perfil:** Estudantes de graduação em Computação/áreas correlatas
- **Nível:** 2º ao 4º ano
- **Conhecimento:** Programação em Python (básico a intermediário)
- **Experiência com CR:** Variável (será coletada)

---

### 8.3 Variáveis independentes (fatores) e seus níveis

| Fator                         | Descrição                                | Níveis                           |
| ----------------------------- | ------------------------------------------ | --------------------------------- |
| **Método de revisão** | Abordagem utilizada para revisar o código | 1. CodeRabbit (IA)                |
|                               |                                            | 2. Manual (humano)                |
|                               |                                            | 3. Híbrido (CodeRabbit + Manual) |

---

### 8.4 Tratamentos (condições experimentais)

| Tratamento               | Descrição            | Procedimento                                                                   |
| ------------------------ | ---------------------- | ------------------------------------------------------------------------------ |
| **T1: CodeRabbit** | Revisão apenas com IA | Participante analisa output do CodeRabbit e lista defeitos encontrados         |
| **T2: Manual**     | Revisão apenas humana | Participante revisa código sem auxílio de ferramentas de IA                  |
| **T3: Híbrido**   | CodeRabbit + Manual    | Participante primeiro vê output do CodeRabbit, depois complementa manualmente |

---

### 8.5 Variáveis dependentes (respostas)

| Variável             | Descrição                           | Tipo        | Escala/Unidade |
| --------------------- | ------------------------------------- | ----------- | -------------- |
| Defeitos detectados   | Número de defeitos reais encontrados | Discreta    | Contagem (0-n) |
| Taxa de detecção    | Proporção de defeitos encontrados   | Contínua   | % (0-100)      |
| Tempo de revisão     | Duração da revisão                 | Contínua   | Minutos        |
| Falsos positivos      | Problemas reportados incorretamente   | Discreta    | Contagem (0-n) |
| Precisão             | VP / (VP + FP)                        | Contínua   | % (0-100)      |
| Categorias detectadas | Distribuição por tipo de defeito    | Categórica | 6 categorias   |

---

### 8.6 Variáveis de controle / bloqueio

| Variável               | Descrição                   | Estratégia de controle                  |
| ----------------------- | ----------------------------- | ---------------------------------------- |
| Experiência em Python  | Anos/nível de experiência   | Bloqueio ou randomização estratificada |
| Experiência em CR      | Familiaridade com code review | Coleta e análise como covariável       |
| Complexidade do código | Dificuldade do artefato       | Padronização dos artefatos             |
| Tamanho do código      | LOC dos artefatos             | Faixa controlada (50-200 LOC)            |
| Ambiente                | IDE, configurações          | Padronização de ambiente               |

---

### 8.7 Possíveis variáveis de confusão conhecidas

| Variável de confusão      | Potencial impacto                    | Estratégia de monitoramento             |
| --------------------------- | ------------------------------------ | ---------------------------------------- |
| Motivação do participante | Afeta esforço e atenção           | Questionário pós-tarefa                |
| Fadiga                      | Degrada desempenho ao longo do tempo | Limitar duração; contrabalancear ordem |
| Familiaridade com domínio  | Facilita identificação de defeitos | Usar domínios genéricos                |
| Conhecimento prévio de IA  | Afeta confiança no CodeRabbit       | Coletar no questionário demográfico    |

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

| Aspecto                    | Descrição                                         |
| -------------------------- | --------------------------------------------------- |
| **Ambiente**         | Acadêmico - Universidade Puc Minas                 |
| **Participantes**    | Estudantes de graduação em Engenharia de Software |
| **Domínio**         | Desenvolvimento de software geral                   |
| **Linguagem**        | Python 3.x                                          |
| **Ferramenta de IA** | CodeRabbit (https://coderabbit.ai)                  |
| **Plataforma**       | GitHub (para PRs e integração com CodeRabbit)     |
| **IDE sugerida**     | VSCode ou PyCharm                                   |

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

| Componente                     | Descrição                                                                                                 |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| **Analisar**             | O processo de code review                                                                                   |
| **Com o propósito de**  | Comparar a eficácia                                                                                        |
| **Com respeito a**       | Detecção de defeitos, tempo de revisão e tipos de problemas identificados                                |
| **Do ponto de vista de** | Pesquisador / Equipe de desenvolvimento                                                                     |
| **No contexto de**       | Revisão de código Python por estudantes de graduação utilizando ferramenta de IA versus revisão manual |

**Objetivo em forma textual:**

> Analisar o processo de code review com o propósito de comparar a eficácia entre revisão assistida por IA e revisão manual, com respeito à detecção de defeitos, tempo de revisão e tipos de problemas identificados, do ponto de vista de pesquisador e equipes de desenvolvimento, no contexto de revisão de código Python por estudantes de graduação.

---

### 3.2 Objetivos específicos

- **O1:** Comparar a taxa de detecção de defeitos entre revisão com CodeRabbit e revisão manual
- **O2:** Comparar o tempo necessário para completar uma revisão entre as duas abordagens
- **O3:** Identificar quais categorias de defeitos cada abordagem detecta com maior eficácia
- **O4:** Avaliar a taxa de falsos positivos de cada abordagem
- **O5:** Investigar se a combinação (CodeRabbit + Manual) supera as abordagens individuais

---

### 3.3 Questões de pesquisa / de negócio

**Questões de pesquisa:**

| ID           | Questão                                                                                                           | Objetivo |
| ------------ | ------------------------------------------------------------------------------------------------------------------ | -------- |
| **Q1** | Qual abordagem (CodeRabbit ou Manual) detecta maior número de defeitos reais em código Python?                   | O1       |
| **Q2** | Qual abordagem requer menos tempo para completar uma revisão de código?                                          | O2       |
| **Q3** | Existem categorias de defeitos que são detectadas predominantemente por uma abordagem específica?                | O3       |
| **Q4** | Qual abordagem apresenta menor taxa de falsos positivos?                                                           | O4       |
| **Q5** | A revisão híbrida (CodeRabbit seguida de revisão Manual) detecta mais defeitos que cada abordagem isoladamente? | O5       |

---

### 3.4 Métricas associadas (GQM)

| Questão | Métrica                     | Definição                                 | Unidade  | Fórmula                      |
| -------- | ---------------------------- | ------------------------------------------- | -------- | ----------------------------- |
| Q1       | Taxa de detecção (Recall)  | Proporção de defeitos reais detectados    | %        | (VP / Total defeitos) × 100  |
| Q1       | Número absoluto de defeitos | Quantidade de defeitos válidos encontrados | Contagem | Soma de VP                    |
| Q2       | Tempo de revisão            | Tempo total para completar revisão         | Minutos  | Cronometragem                 |
| Q2       | Velocidade de revisão       | LOC revisadas por minuto                    | LOC/min  | LOC / Tempo                   |
| Q3       | Distribuição por categoria | Proporção por categoria de defeito        | %        | Contagem categoria / Total    |
| Q4       | Taxa de falso positivo       | Problemas reportados que não são defeitos | %        | (FP / Total reportado) × 100 |
| Q4       | Precisão                    | Defeitos reportados que são reais          | %        | (VP / Total reportado) × 100 |
| Q5       | F1-Score                     | Média harmônica precisão e recall        | 0-1      | 2×(P×R)/(P+R)               |

**Legenda:** VP = Verdadeiro Positivo, FP = Falso Positivo

**Categorias de defeitos:**

1. Funcional - Bugs de lógica, erros de algoritmo
2. Segurança - Vulnerabilidades, exposição de dados
3. Performance - Ineficiências, complexidade desnecessária
4. Manutenibilidade - Code smells, duplicação
5. Estilo/Convenção - Violações de PEP8, naming
6. Tratamento de erros - Exceções não tratadas, validações ausentes

---

## 4. Escopo e contexto do experimento

### 4.1 Escopo funcional / de processo (incluído e excluído)

**Incluído no escopo:**

| Item              | Descrição                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| Linguagem         | Python 3.x                                                                  |
| Tipo de código   | Scripts e funções de complexidade baixa a média (50-200 LOC)             |
| Tipos de defeitos | Funcionais, segurança, performance, manutenibilidade, estilo               |
| Ferramenta de IA  | CodeRabbit                                                                  |
| Participantes     | Estudantes de graduação com conhecimento básico-intermediário em Python |
| Processo          | Revisão de Pull Requests em repositório controlado                        |

**Excluído do escopo:**

| Item                          | Justificativa                                               |
| ----------------------------- | ----------------------------------------------------------- |
| Outras linguagens             | Foco em Python para controlar variabilidade                 |
| Código legado complexo       | Difícil controlar variáveis e inserir defeitos conhecidos |
| Revisão de arquitetura       | Fora do escopo de code review de PR                         |
| Aspectos de documentação    | Foco em código executável                                 |
| Integração com CI/CD        | Simplificação do experimento                              |
| Desenvolvedores profissionais | Dificuldade de acesso e disponibilidade                     |

---

### 4.2 Contexto do estudo (tipo de organização, projeto, experiência)

| Dimensão                          | Caracterização                                    |
| ---------------------------------- | --------------------------------------------------- |
| **Tipo de organização**    | Acadêmica (Universidade)                           |
| **Tipo de projeto**          | Exercícios controlados (não produção real)      |
| **Criticidade**              | Baixa (ambiente experimental)                       |
| **Perfil dos participantes** | Estudantes de graduação, 2º ao 4º ano           |
| **Experiência esperada**    | 1-3 anos de programação, familiaridade com Python |
| **Experiência com CR**      | Variável (será coletada como característica)     |

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

| Restrição              | Impacto                                                        | Mitigação                                         |
| ------------------------ | -------------------------------------------------------------- | --------------------------------------------------- |
| **Tempo limitado** | Experimento deve ser concluído dentro do semestre letivo      | Priorizar qualidade sobre quantidade                |
| **Orçamento**     | Utilização apenas do tier gratuito do CodeRabbit             | Selecionar ferramentas com tier gratuito            |
| **Participantes**  | Limitado a estudantes disponíveis e voluntários              | Maximizar participação com incentivos acadêmicos |
| **Ambiente**       | Repositórios públicos no GitHub (requisito do tier gratuito) | Reconhecer como limitação na análise             |
| **Infraestrutura** | Dependência de conexão com internet estável                 | Documentar perfil e discutir nas limitações       |

---

### 4.5 Limitações previstas

**Validade externa:**

- Amostra de conveniência (estudantes) pode não representar desenvolvedores profissionais
- Código artificial pode diferir de código de produção real
- Defeitos inseridos podem não refletir distribuição natural de defeitos
- Resultados específicos para Python e CodeRabbit

**Validade interna:**

- Efeito de aprendizagem ao longo das tarefas
- Fadiga em sessões longas
- Motivação variável (sem impacto real no código)

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

| Risco                                                | Categoria     | Probabilidade | Impacto |
| ---------------------------------------------------- | ------------- | ------------- | ------- |
| CodeRabbit indisponível ou com mudanças            | Técnico      | Baixa         | Alto    |
| Baixa adesão de participantes                       | Operacional   | Média        | Alto    |
| Defeitos inseridos muito fáceis ou difíceis        | Metodológico | Média        | Médio  |
| Tempo insuficiente para análise                     | Cronograma    | Média        | Médio  |
| Dados insuficientes para significância estatística | Metodológico | Média        | Alto    |

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
| **Método de revisão** (VI principal) | Abordagem utilizada para revisar o código | 1. CodeRabbit (IA)                |
|                               |                                            | 2. Manual (humano)                |
|                               |                                            | 3. Híbrido (CodeRabbit + Manual) |
| **Complexidade do código** | Nível de dificuldade do artefato a ser revisado | 1. Baixa (50-100 LOC, lógica simples) |
|                               |                                            | 2. Média (100-200 LOC, lógica moderada) |
| **Tipo de defeito** | Categoria predominante dos defeitos inseridos | 1. Funcional |
|                               |                                            | 2. Segurança |
|                               |                                            | 3. Performance |
|                               |                                            | 4. Manutenibilidade |
|                               |                                            | 5. Estilo/Convenção |
|                               |                                            | 6. Tratamento de erros |
| **Ordem de execução** | Sequência das tarefas (para contrabalanceamento) | 1. Sequência A (T1→T2→T3) |
|                               |                                            | 2. Sequência B (T2→T3→T1) |
|                               |                                            | 3. Sequência C (T3→T1→T2) |

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

---

## 9. Desenho experimental

### 9.1 Tipo de desenho (completamente randomizado, blocos, fatorial, etc.)

**Tipo:** Within-subjects (medidas repetidas) com contrabalanceamento

**Justificativa:**

- Cada participante executa todos os tratamentos (T1, T2, T3)
- Reduz variabilidade entre sujeitos
- Requer menos participantes para mesmo poder estatístico
- Contrabalanceamento controla efeitos de ordem e aprendizagem

**Alternativa (se inviável):** Between-subjects com randomização

---

### 9.2 Randomização e alocação

- **O que será randomizado:**

  - Ordem dos tratamentos para cada participante (contrabalanceamento)
  - Alocação de artefatos de código para cada tratamento
- **Como será feito:**

  - Quadrado Latino para contrabalancear ordem dos tratamentos
  - Script Python para gerar alocações aleatórias
  - Seed documentado para reprodutibilidade

---

### 9.3 Balanceamento e contrabalanço

**Balanceamento:**

- Mesmo número de participantes em cada sequência de ordem
- Mesma distribuição de experiência entre sequências (se possível)

**Contrabalanço (Quadrado Latino 3x3):**

| Grupo | Tarefa 1      | Tarefa 2      | Tarefa 3      |
| ----- | ------------- | ------------- | ------------- |
| A     | T1 (IA)       | T2 (Manual)   | T3 (Híbrido) |
| B     | T2 (Manual)   | T3 (Híbrido) | T1 (IA)       |
| C     | T3 (Híbrido) | T1 (IA)       | T2 (Manual)   |

---

### 9.4 Número de grupos e sessões

- **Número de grupos:** 3 (baseado no Quadrado Latino)
- **Sessões por participante:** 1 sessão com 3 tarefas
- **Duração estimada por sessão:** 90-120 minutos
- **Participantes por grupo:** Mínimo 7-10 (total mínimo: 21-30)

---

## 10. População, sujeitos e amostragem

### 10.1 População-alvo

Desenvolvedores de software com conhecimento básico a intermediário em Python, representados por estudantes de graduação em cursos de Computação.

---

### 10.2 Critérios de inclusão de sujeitos

- Estar matriculado em curso de graduação em Computação ou área correlata
- Ter cursado pelo menos 1 disciplina de programação
- Conhecimento básico de Python (capaz de ler e entender código)
- Disponibilidade para participar da sessão completa (~2 horas)
- Aceitar o termo de consentimento livre e esclarecido

---

### 10.3 Critérios de exclusão de sujeitos

- Envolvimento na elaboração do experimento
- Conhecimento prévio dos artefatos de código utilizados
- Incapacidade de completar a sessão por qualquer motivo
- Participantes que não completarem todas as tarefas

---

### 10.4 Tamanho da amostra planejado (por grupo)

- **Total desejado:** 30 participantes
- **Por sequência do Quadrado Latino:** 10 participantes
- **Mínimo aceitável:** 21 participantes (7 por sequência)

**Justificativa:** Balanceamento entre poder estatístico desejado e viabilidade de recrutamento em contexto acadêmico.

---

### 10.5 Método de seleção / recrutamento

**Método:** Amostra de conveniência com convite aberto

**Processo:**

1. Divulgação em turmas de disciplinas de programação
2. Convite por e-mail institucional
3. Divulgação em grupos de estudantes (Discord, WhatsApp, etc.)
4. Inscrição voluntária via formulário online

**Incentivos:**

- Certificado de participação
- Horas complementares (se aplicável)
- Sorteio de brindes (opcional)

---

### 10.6 Treinamento e preparação dos sujeitos

**Antes da sessão:**

- Vídeo introdutório (5 min) sobre o experimento
- Documento explicativo sobre code review
- Tutorial básico sobre CodeRabbit

**No início da sessão:**

- Explicação do protocolo (10 min)
- Tarefa de aquecimento/treino (15 min) - não contabilizada
- Esclarecimento de dúvidas

---

## 11. Instrumentação e protocolo operacional

### 11.1 Instrumentos de coleta (questionários, logs, planilhas, etc.)

| Instrumento                | Tipo               | Descrição                      | Dados coletados                  |
| -------------------------- | ------------------ | -------------------------------- | -------------------------------- |
| Questionário demográfico | Google Forms       | Perfil do participante           | Experiência, formação         |
| TCLE                       | Google Forms / PDF | Consentimento                    | Aceite formal                    |
| Formulário de revisão    | Google Forms       | Registro de defeitos encontrados | Defeitos, categorias, confiança |
| Cronômetro                | Script/Manual      | Medição de tempo               | Tempo por tarefa                 |
| Output CodeRabbit          | GitHub             | Resultado da análise de IA      | Defeitos reportados pela IA      |
| Questionário pós-tarefa  | Google Forms       | Percepção do participante      | Dificuldade, satisfação        |

---

### 11.2 Materiais de suporte (instruções, guias)

| Material               | Público-alvo | Descrição                 |
| ---------------------- | ------------- | --------------------------- |
| Guia do participante   | Participantes | Instruções passo a passo  |
| Taxonomia de defeitos  | Participantes | Categorias e exemplos       |
| Tutorial CodeRabbit    | Participantes | Como interpretar output     |
| Roteiro do facilitador | Pesquisador   | Script de condução        |
| Gabarito de defeitos   | Pesquisador   | Lista de defeitos inseridos |

---

### 11.3 Procedimento experimental (protocolo – visão passo a passo)

**Fase de Preparação (antes da sessão):**

1. Participante preenche questionário demográfico online
2. Participante assina TCLE
3. Participante recebe materiais de preparação

**Sessão Experimental (~120 minutos):**

| Etapa | Duração | Atividade                                                 |
| ----- | --------- | --------------------------------------------------------- |
| 1     | 10 min    | Boas-vindas e explicação do protocolo                   |
| 2     | 15 min    | Tarefa de treino (aquecimento)                            |
| 3     | 5 min     | Esclarecimento de dúvidas                                |
| 4     | 25 min    | **Tarefa 1** - Revisão conforme tratamento alocado |
| 5     | 5 min     | Questionário pós-tarefa 1                               |
| 6     | 5 min     | Intervalo                                                 |
| 7     | 25 min    | **Tarefa 2** - Revisão conforme tratamento alocado |
| 8     | 5 min     | Questionário pós-tarefa 2                               |
| 9     | 5 min     | Intervalo                                                 |
| 10    | 25 min    | **Tarefa 3** - Revisão conforme tratamento alocado |
| 11    | 5 min     | Questionário pós-tarefa 3                               |
| 12    | 10 min    | Questionário final e encerramento                        |

---

### 11.4 Plano de piloto (se haverá piloto, escopo e critérios de ajuste)

**Haverá piloto:** Sim

**Participantes do piloto:** 3-5 estudantes (não incluídos na amostra final)

**Objetivos do piloto:**

- Validar clareza das instruções
- Verificar tempo adequado para tarefas
- Testar instrumentos de coleta
- Identificar problemas técnicos
- Calibrar dificuldade dos artefatos

**Critérios de ajuste:**

- Instruções confusas: reescrever
- Tempo insuficiente: ajustar duração ou complexidade
- Defeitos muito fáceis/difíceis: recalibrar artefatos
- Problemas técnicos: corrigir antes da execução principal

---

## 12. Plano de análise de dados (pré-execução)

### 12.1 Estratégia geral de análise (como responderá às questões)

| Questão | Estratégia de análise                                                                    |
| -------- | ------------------------------------------------------------------------------------------ |
| Q1       | Comparar médias de taxa de detecção entre tratamentos usando ANOVA de medidas repetidas |
| Q2       | Comparar médias de tempo usando ANOVA de medidas repetidas                                |
| Q3       | Análise descritiva de distribuição + teste qui-quadrado por categoria                   |
| Q4       | Comparar taxas de FP usando ANOVA ou teste não-paramétrico                               |
| Q5       | Comparar F1-Score do híbrido vs. individuais com testes post-hoc                          |

---

### 12.2 Métodos estatísticos planejados

| Análise                                     | Método                                      | Pressupostos                | Alternativa não-paramétrica |
| -------------------------------------------- | -------------------------------------------- | --------------------------- | ----------------------------- |
| Comparação de 3 grupos (medidas repetidas) | ANOVA de medidas repetidas                   | Normalidade, esfericidade   | Friedman                      |
| Comparações pareadas                       | Teste t pareado com correção de Bonferroni | Normalidade                 | Wilcoxon signed-rank          |
| Correlações                                | Pearson                                      | Normalidade, linearidade    | Spearman                      |
| Distribuição categórica                   | Qui-quadrado                                 | Frequências esperadas ≥ 5 | Fisher exato                  |
| Tamanho de efeito                            | d de Cohen, η²                             | -                           | -                             |

**Software:** R ou Python (scipy, statsmodels)

---

### 12.3 Tratamento de dados faltantes e outliers

**Dados faltantes:**

- Participante não completou todas as tarefas: excluir da análise (listwise deletion)
- Campo específico faltante: imputação pela média ou exclusão do caso

**Outliers:**

- Identificação: Método IQR (valores > Q3 + 1.5×IQR ou < Q1 - 1.5×IQR)
- Tratamento: Análise com e sem outliers; reportar ambos se houver diferença
- Tempo de revisão < 5 min: investigar se tarefa foi feita adequadamente

---

### 12.4 Plano de análise para dados qualitativos (se houver)

**Dados qualitativos coletados:**

- Comentários nos questionários pós-tarefa
- Justificativas para defeitos reportados

**Método de análise:**

- Análise de conteúdo com categorização temática
- Codificação aberta seguida de categorização
- Triangulação com dados quantitativos

---

## 13. Avaliação de validade (ameaças e mitigação)

### 13.1 Validade de conclusão

| Ameaça                    | Descrição                                      | Mitigação                                            |
| -------------------------- | ------------------------------------------------ | ------------------------------------------------------ |
| Baixo poder estatístico   | Amostra pequena pode não detectar efeitos reais | Recrutar máximo possível; usar medidas repetidas     |
| Violação de pressupostos | Dados podem não ser normais                     | Verificar pressupostos; usar testes não-paramétricos |
| Confiabilidade das medidas | Inconsistência na classificação de defeitos   | Gabarito pré-definido; dupla verificação            |

---

### 13.2 Validade interna

| Ameaça                | Descrição                      | Mitigação                           |
| ---------------------- | -------------------------------- | ------------------------------------- |
| Efeito de aprendizagem | Melhora ao longo das tarefas     | Contrabalanceamento (Quadrado Latino) |
| Fadiga                 | Piora ao longo das tarefas       | Intervalos; limitar duração total   |
| Seleção              | Grupos não comparáveis         | Design within-subjects                |
| História              | Eventos externos durante sessão | Sessões padronizadas e controladas   |

---

### 13.3 Validade de constructo

| Constructo              | Medida operacional | Potencial ameaça                                 | Mitigação                                 |
| ----------------------- | ------------------ | ------------------------------------------------- | ------------------------------------------- |
| Eficácia de detecção | Taxa de recall     | Defeitos inseridos podem não ser representativos | Usar taxonomia estabelecida                 |
| Tempo de revisão       | Cronometragem      | Pode incluir tempo não produtivo                 | Instruções claras sobre o que cronometrar |
| Qualidade da revisão   | F1-Score           | Depende da definição de defeito                 | Gabarito validado por especialistas         |

---

### 13.4 Validade externa

| Ameaça                | Impacto na generalização              | Mitigação                                  |
| ---------------------- | --------------------------------------- | -------------------------------------------- |
| Amostra de estudantes  | Pode não representar profissionais     | Documentar limitação; sugerir replicação |
| Código artificial     | Diferente de código de produção      | Usar padrões realistas                      |
| Ferramenta específica | Resultados específicos para CodeRabbit | Documentar versão; discutir generalização |
| Contexto acadêmico    | Sem pressão de produção              | Reconhecer como limitação                  |

---

### 13.5 Resumo das principais ameaças e estratégias de mitigação

| Tipo de validade | Ameaça principal                  | Mitigação                                          |
| ---------------- | ---------------------------------- | ---------------------------------------------------- |
| Conclusão       | Baixo poder estatístico           | Maximizar amostra; design within-subjects            |
| Interna          | Efeito de aprendizagem/ordem       | Contrabalanceamento com Quadrado Latino              |
| Constructo       | Representatividade dos defeitos    | Taxonomia estabelecida; validação por especialista |
| Externa          | Generalização para profissionais | Documentar limitação; sugerir replicações        |

---

## 14. Ética, privacidade e conformidade

### 14.1 Questões éticas (uso de sujeitos, incentivos, etc.)

**Questões identificadas:**

- Participação voluntária deve ser garantida (sem coerção)
- Estudantes não devem sentir pressão por parte de professores
- Incentivos não devem ser coercitivos
- Desempenho individual não será divulgado

**Tratamento:**

- Convite aberto sem vínculo com notas ou avaliações
- Participante pode desistir a qualquer momento
- Resultados reportados de forma agregada

---

### 14.2 Consentimento informado

**Processo:**

1. TCLE disponibilizado antes da inscrição
2. Explicação clara de objetivos, procedimentos, riscos e benefícios
3. Aceite eletrônico registrado com timestamp
4. Cópia do TCLE enviada ao participante

**Conteúdo do TCLE:**

- Objetivo da pesquisa
- Procedimentos e duração
- Riscos (mínimos: fadiga, desconforto)
- Benefícios (aprendizado, certificado)
- Confidencialidade dos dados
- Direito de desistência
- Contato do pesquisador

---

### 14.3 Privacidade e proteção de dados

**Dados coletados:**

- Nome e e-mail (apenas para contato e certificado)
- Dados demográficos (ano do curso, experiência)
- Respostas às tarefas e questionários

**Medidas de proteção:**

- Pseudoanonimização: ID numérico para análise
- Dados armazenados em pasta protegida por senha
- Apenas pesquisador e orientador têm acesso
- Nome/e-mail separados dos dados de desempenho

**Período de retenção:** 5 anos após conclusão do TCC

---

### 14.4 Aprovações necessárias (comitê de ética, jurídico, DPO, etc.)

| Aprovação necessária | Responsável     | Status   | Data |
| ----------------------- | ---------------- | -------- | ---- |
| Comitê de Ética (CEP) | CEP da Puc Minas | Pendente | -    |
| Orientador              | [Nome]           | Pendente | -    |
| Coordenação do curso  | [Nome]           | Pendente | -    |

> **Nota:** Verificar se a instituição exige submissão ao CEP para pesquisas com estudantes.

---

## 15. Recursos, infraestrutura e orçamento

### 15.1 Recursos humanos e papéis

| Nome                      | Papel                 | Responsabilidades                                 |
| ------------------------- | --------------------- | ------------------------------------------------- |
| João Pedro Queiroz Rocha | Pesquisador principal | Planejamento, execução, análise, escrita       |
| [Orientador]              | Orientador            | Supervisão, revisão, orientação metodológica |
| [Colaborador - opcional]  | Auxiliar              | Apoio na condução das sessões                  |

---

### 15.2 Infraestrutura técnica necessária

| Recurso           | Descrição                        | Status                    |
| ----------------- | ---------------------------------- | ------------------------- |
| Conta GitHub      | Repositório para PRs              | Disponível               |
| CodeRabbit        | Integração com repositório      | Configurar                |
| Google Forms      | Questionários                     | Disponível               |
| Sala/Laboratório | Local para sessões presenciais    | Verificar disponibilidade |
| Computadores      | Para participantes (se presencial) | Verificar                 |
| Conexão internet | Acesso ao GitHub e CodeRabbit      | Verificar estabilidade    |

---

### 15.3 Materiais e insumos

| Material/Insumo             | Quantidade               | Status        |
| --------------------------- | ------------------------ | ------------- |
| Artefatos de código Python | 4 (1 treino + 3 tarefas) | A desenvolver |
| Questionário demográfico  | 1                        | A desenvolver |
| TCLE                        | 1                        | A desenvolver |
| Formulários de revisão    | 3                        | A desenvolver |
| Questionários pós-tarefa  | 3                        | A desenvolver |
| Guia do participante        | 1                        | A desenvolver |
| Tutorial CodeRabbit         | 1                        | A desenvolver |

---

### 15.4 Orçamento e custos estimados

| Item de custo             | Valor estimado       | Fonte de financiamento |
| ------------------------- | -------------------- | ---------------------- |
| CodeRabbit                | R$ 0 (tier gratuito) | -                      |
| GitHub                    | R$ 0 (gratuito)      | -                      |
| Google Forms              | R$ 0 (gratuito)      | -                      |
| Certificados (impressão) | R$ 50-100            | Recursos próprios     |
| **Total estimado**  | **R$ 50-100**  | -                      |

---

## 16. Cronograma, marcos e riscos operacionais

### 16.1 Macrocronograma (até o início da execução)

| Marco                                            | Data prevista | Status       |
| ------------------------------------------------ | ------------- | ------------ |
| Plano de experimento concluído                  | 30/11/2025    | Em andamento |
| Aprovação do orientador                        | 05/12/2025    | Pendente     |
| Submissão ao CEP (se necessário)               | 10/12/2025    | Pendente     |
| Desenvolvimento dos artefatos de código         | 15/12/2025    | Pendente     |
| Desenvolvimento dos instrumentos                 | 20/12/2025    | Pendente     |
| Configuração do ambiente (GitHub + CodeRabbit) | 23/12/2025    | Pendente     |
| Recrutamento de participantes                    | 10/01/2026    | Pendente     |
| Execução do piloto                             | 20/01/2026    | Pendente     |
| Ajustes pós-piloto                              | 25/01/2026    | Pendente     |
| Início da execução principal                  | 01/02/2026    | Pendente     |

---

### 16.2 Dependências entre atividades

| Atividade                    | Depende de                         |
| ---------------------------- | ---------------------------------- |
| Submissão ao CEP            | Plano aprovado pelo orientador     |
| Desenvolvimento de artefatos | Definição final do escopo        |
| Configuração do ambiente   | Artefatos prontos                  |
| Recrutamento                 | Aprovação ética (se exigida)    |
| Piloto                       | Instrumentos e ambiente prontos    |
| Execução principal         | Piloto concluído e ajustes feitos |

---

### 16.3 Riscos operacionais e plano de contingência

| Risco                                | Probabilidade | Impacto | Plano de contingência                                    |
| ------------------------------------ | ------------- | ------- | --------------------------------------------------------- |
| Baixa adesão de participantes       | Média        | Alto    | Intensificar divulgação; oferecer incentivos adicionais |
| Problemas técnicos com CodeRabbit   | Baixa         | Alto    | Ter screenshots de backup; plano B com outra ferramenta   |
| Atraso na aprovação do CEP         | Média        | Médio  | Iniciar processo o quanto antes                           |
| Participante desiste durante sessão | Média        | Baixo   | Recrutar 10-20% a mais que o necessário                  |
| Dados corrompidos/perdidos           | Baixa         | Alto    | Backup em tempo real; múltiplas cópias                  |

---

## 17. Governança do experimento

### 17.1 Papéis e responsabilidades formais

| Papel     | Pessoa/Grupo             | Responsabilidade                           |
| --------- | ------------------------ | ------------------------------------------ |
| Decide    | Pesquisador + Orientador | Decisões metodológicas e operacionais    |
| Executa   | Pesquisador              | Condução das sessões, coleta de dados   |
| Revisa    | Orientador               | Revisão do plano, instrumentos e análise |
| Informado | Banca, participantes     | Recebem informações sobre progresso      |

---

### 17.2 Ritos de acompanhamento pré-execução

| Rito                     | Frequência       | Participantes           | Objetivo                             |
| ------------------------ | ----------------- | ----------------------- | ------------------------------------ |
| Reunião de orientação | Semanal/Quinzenal | Pesquisador, Orientador | Acompanhar progresso, tirar dúvidas |
| Revisão de artefatos    | Pontual           | Pesquisador, Orientador | Validar instrumentos antes do piloto |
| Revisão pós-piloto     | Pontual           | Pesquisador, Orientador | Decidir ajustes necessários         |

---

### 17.3 Processo de controle de mudanças no plano

1. Pesquisador identifica necessidade de mudança
2. Documenta proposta de mudança (o quê, por quê, impacto)
3. Discute com orientador
4. Se aprovada, atualiza documento com nova versão
5. Registra mudança no histórico de revisões

**Mudanças que exigem re-aprovação do CEP:**

- Alteração nos procedimentos com participantes
- Mudança nos riscos ou benefícios
- Alteração no TCLE

---

## 18. Plano de documentação e reprodutibilidade

### 18.1 Repositórios e convenções de nomeação

**Repositório principal:** GitHub - https://github.com/joaopqr/experimento-cr-ia

**Estrutura de pastas:**

```
/experimento-cr-ia/
├── /docs/                    # Documentação
│   ├── plano-experimento.md
│   ├── tcle.pdf
│   └── guia-participante.pdf
├── /artefatos/               # Códigos para revisão
│   ├── treino/
│   ├── tarefa1/
│   ├── tarefa2/
│   └── tarefa3/
├── /instrumentos/            # Questionários e formulários
├── /dados/                   # Dados coletados (anonimizados)
├── /analise/                 # Scripts de análise
└── /resultados/              # Outputs e visualizações
```

**Convenções de nomeação:**

- Arquivos: `tipo_descricao_versao.ext` (ex: `questionario_demografico_v1.pdf`)
- Participantes: `P01`, `P02`, ... (pseudoanonimização)
- Datas: formato ISO `YYYY-MM-DD`

---

### 18.2 Templates e artefatos padrão

| Artefato             | Localização            | Descrição                         |
| -------------------- | ------------------------ | ----------------------------------- |
| Template de código  | `/artefatos/template/` | Estrutura base para criar artefatos |
| Gabarito de defeitos | `/docs/gabarito.xlsx`  | Lista de defeitos inseridos         |
| Questionários       | `/instrumentos/`       | Google Forms exportados             |
| Script de análise   | `/analise/analise.py`  | Código R/Python para análise      |

---

### 18.3 Plano de empacotamento para replicação futura

**Pacote de replicação incluirá:**

1. Plano de experimento completo (este documento)
2. Todos os artefatos de código (com gabarito)
3. Instrumentos de coleta (questionários, formulários)
4. Scripts de análise
5. Dados anonimizados (se permitido pelo CEP)
6. Relatório final com resultados

**Formato:** Repositório GitHub público ou Zenodo (com DOI)

---

## 19. Plano de comunicação

### 19.1 Públicos e mensagens-chave pré-execução

| Público                        | Mensagem-chave                                                                                                  |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Potenciais participantes        | "Participe de pesquisa sobre IA em code review. Duração: ~2h. Ganhe certificado e contribua para a ciência!" |
| Professores (para divulgação) | "Solicitamos apoio na divulgação de pesquisa de TCC sobre ferramentas de IA para desenvolvimento de software" |
| Orientador                      | Atualizações de progresso e decisões pendentes                                                               |

---

### 19.2 Canais e frequência de comunicação

| Canal                      | Público                   | Frequência | Tipo de comunicação        |
| -------------------------- | -------------------------- | ----------- | ---------------------------- |
| E-mail institucional       | Participantes, professores | Pontual     | Convites, lembretes          |
| WhatsApp/Discord           | Participantes              | Pontual     | Lembretes, dúvidas rápidas |
| Reunião presencial/online | Orientador                 | Semanal     | Acompanhamento               |
| GitHub Issues              | Pesquisador                | Contínuo   | Tracking de tarefas          |

---

### 19.3 Pontos de comunicação obrigatórios

- **Aprovação do plano:** Comunicar orientador e iniciar próximas etapas
- **Aprovação do CEP:** Comunicar orientador; liberar recrutamento
- **Início do recrutamento:** Divulgar amplamente
- **Início da execução:** Confirmar com participantes inscritos
- **Conclusão da coleta:** Comunicar orientador; agradecer participantes
- **Mudanças relevantes:** Comunicar orientador imediatamente

---

## 20. Critérios de prontidão para execução (Definition of Ready)

### 20.1 Checklist de prontidão (itens que devem estar completos)

- [ ] Plano de experimento aprovado pelo orientador
- [ ] Aprovação ética obtida (se exigida pela instituição)
- [ ] Artefatos de código desenvolvidos e validados
- [ ] Gabarito de defeitos criado e revisado
- [ ] Ambiente GitHub + CodeRabbit configurado e testado
- [ ] Questionário demográfico pronto
- [ ] TCLE elaborado e aprovado
- [ ] Formulários de revisão prontos
- [ ] Questionários pós-tarefa prontos
- [ ] Guia do participante elaborado
- [ ] Tutorial CodeRabbit criado
- [ ] Roteiro do facilitador pronto
- [ ] Piloto executado com sucesso
- [ ] Ajustes pós-piloto realizados
- [ ] Mínimo de participantes recrutados (21+)
- [ ] Sala/ambiente reservado para sessões
- [ ] Backup e contingências preparados

---

### 20.2 Aprovações finais para iniciar a operação

| Aprovador            | Cargo/Papel       | Forma de registro       | Status   |
| -------------------- | ----------------- | ----------------------- | -------- |
| [Nome do orientador] | Orientador        | E-mail ou assinatura    | Pendente |
| CEP da Puc Minas     | Comitê de Ética | Parecer consubstanciado | Pendente |

---

## Anexos

### Anexo A: Glossário de termos

| Termo             | Definição                                                    |
| ----------------- | -------------------------------------------------------------- |
| Code Review (CR)  | Processo de revisão de código por pares                      |
| CodeRabbit        | Ferramenta de revisão de código assistida por IA             |
| Pull Request (PR) | Solicitação de merge de código no GitHub                    |
| Seeded Defects    | Defeitos intencionalmente inseridos para teste                 |
| LOC               | Lines of Code - Linhas de código                              |
| TCLE              | Termo de Consentimento Livre e Esclarecido                     |
| GQM               | Goal-Question-Metric - metodologia de definição de métricas |
| VP/FP             | Verdadeiro Positivo / Falso Positivo                           |

### Anexo B: Referências bibliográficas

1. Bacchelli, A., & Bird, C. (2013). Expectations, outcomes, and challenges of modern code review. ICSE.
2. Fagan, M. E. (1976). Design and code inspections to reduce errors in program development. IBM Systems Journal.
3. Fan, Y., et al. (2023). Large Language Models for Software Engineering: A Systematic Literature Review.
4. Li, Z., et al. (2022). Automating Code Review Activities by Large-Scale Pre-training.
5. McIntosh, S., et al. (2014). The impact of code review coverage and code review participation on software quality. MSR.
6. Sadowski, C., et al. (2018). Modern code review: A case study at Google. ICSE-SEIP.
7. Tufano, M., et al. (2022). Using pre-trained models to boost code review automation.
8. Wohlin, C., et al. (2012). Experimentation in Software Engineering. Springer.

### Anexo C: Modelos de instrumentos

- Questionário demográfico: [Link Google Forms]
- TCLE: [Link documento]
- Formulário de revisão: [Link Google Forms]
- Questionário pós-tarefa: [Link Google Forms]

### Anexo D: Categorias de defeitos (Taxonomia)

| Categoria           | Descrição                  | Exemplos                                               |
| ------------------- | ---------------------------- | ------------------------------------------------------ |
| Funcional           | Erros de lógica e algoritmo | Loop infinito, condição invertida, off-by-one        |
| Segurança          | Vulnerabilidades             | SQL injection, exposição de dados, eval() inseguro   |
| Performance         | Ineficiências               | Complexidade desnecessária, queries em loop           |
| Manutenibilidade    | Code smells                  | Código duplicado, função muito longa, magic numbers |
| Estilo              | Violações de convenção   | PEP8, naming, formatação                             |
| Tratamento de erros | Exceções e validações    | Try/except genérico, falta de validação de input    |

---

*Documento elaborado em: 22/11/2025*
*Última atualização: 05/12/2025*
*Versão: 1.1*

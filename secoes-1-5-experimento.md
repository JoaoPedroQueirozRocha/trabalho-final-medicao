# Plano de Experimento: Code Review com IA vs. Manual
## Seções 1 a 5 - Preenchidas

---

## 1. Identificação básica

### 1.1 Título do experimento

**Título:** Comparação da Eficácia de Code Review Assistido por Inteligência Artificial versus Revisão Manual na Detecção de Defeitos em Código Python

---

### 1.2 ID / código

**ID:** TCC-CR-IA-2024-001

> *Nota: Ajuste conforme padrão da sua instituição*

---

### 1.3 Versão do documento e histórico de revisão

**Versão atual:** v1.0

| Versão | Data       | Autor          | Descrição das alterações |
|--------|------------|----------------|--------------------------|
| v1.0   | 22/11/2024 | [Seu nome]     | Versão inicial do plano  |

---

### 1.4 Datas (criação, última atualização)

- **Data de criação:** 22/11/2024
- **Última atualização:** 22/11/2024

---

### 1.5 Autores (nome, área, contato)

| Nome       | Área                       | Contato            |
|------------|----------------------------|--------------------|
| [Seu nome] | Engenharia de Software     | [seu@email.com]    |
| [Orientador] | [Área do orientador]     | [orientador@email] |

---

### 1.6 Responsável principal (PI / dono do experimento)

**Responsável:** [Seu nome completo]
**Papel:** Pesquisador principal / Autor do TCC
**Contato:** [seu@email.com]

**Orientador:** [Nome do orientador]
**Papel:** Orientador acadêmico
**Contato:** [orientador@email.com]

---

### 1.7 Projeto / produto / iniciativa relacionada

**Iniciativa:** Trabalho de Conclusão de Curso (TCC)
**Curso:** [Nome do curso - ex: Ciência da Computação, Engenharia de Software]
**Instituição:** [Nome da universidade]
**Disciplina:** [Nome da disciplina, se aplicável]
**Período:** [Semestre/Ano - ex: 2024.2]

---

## 2. Contexto e problema

### 2.1 Descrição do problema / oportunidade

**Problema:**

O processo de code review é reconhecido como uma das práticas mais eficazes para garantir qualidade de software, mas enfrenta desafios significativos:

1. **Tempo elevado**: Revisores gastam em média 30-60 minutos por revisão de PRs médios
2. **Inconsistência**: A qualidade da revisão varia conforme experiência, cansaço e disponibilidade do revisor
3. **Gargalos**: Desenvolvedores seniores se tornam bottleneck por serem os revisores mais demandados
4. **Cobertura limitada**: Humanos tendem a focar em lógica e perdem detalhes como estilo, segurança básica e edge cases

**Oportunidade:**

Ferramentas de IA para code review prometem:
- Feedback instantâneo (segundos vs. horas/dias)
- Consistência na análise
- Cobertura sistemática de múltiplos aspectos
- Liberação de tempo dos revisores humanos para análises de alto nível

**Questão central:** Essas promessas se sustentam empiricamente? A IA é realmente eficaz na detecção de defeitos?

---

### 2.2 Contexto organizacional e técnico

**Contexto do estudo:**

| Aspecto | Descrição |
|---------|-----------|
| **Ambiente** | Acadêmico - Universidade [Nome] |
| **Participantes** | Estudantes de graduação em [Curso] |
| **Domínio** | Desenvolvimento de software geral |
| **Linguagem** | Python (escolhida pela familiaridade dos participantes) |
| **Ferramentas de IA** | [Escolher: CodeRabbit / GitHub Copilot / PR-Agent / Outra] |
| **Plataforma** | GitHub (para PRs e integração com ferramentas) |

**Justificativa das escolhas:**
- **Python**: Linguagem mais comum nos cursos de graduação, garantindo familiaridade
- **GitHub**: Plataforma padrão de mercado com boa integração com ferramentas de IA
- **Estudantes**: Amostra acessível e representativa de desenvolvedores iniciantes/intermediários

---

### 2.3 Trabalhos e evidências prévias (internos e externos)

**Trabalhos externos relevantes:**

| Referência | Contribuição principal | Ano |
|------------|------------------------|-----|
| Sadowski et al. - "Modern Code Review: A Case Study at Google" | Caracterização do processo de CR em larga escala | 2018 |
| Bacchelli & Bird - "Expectations, Outcomes, and Challenges of Modern Code Review" | Identificação de expectativas vs. realidade no CR | 2013 |
| McIntosh et al. - "The Impact of Code Review Coverage and Participation on Software Quality" | Relação entre cobertura de CR e qualidade | 2014 |
| Fan et al. - "Large Language Models for Software Engineering: A Systematic Literature Review" | Estado da arte de LLMs em ES | 2023 |
| Tufano et al. - "Using Pre-Trained Models to Boost Code Review Automation" | Uso de modelos pré-treinados para CR | 2022 |
| Li et al. - "Automating Code Review Activities by Large-Scale Pre-training" | Automação de CR com IA | 2022 |

**Gaps identificados:**
- Poucos estudos controlados comparando IA vs. humanos diretamente
- Falta de estudos com ferramentas comerciais recentes (2023-2024)
- Escassez de dados sobre falsos positivos das ferramentas de IA

---

### 2.4 Referencial teórico e empírico essencial

**Conceitos fundamentais:**

1. **Code Review (Revisão de Código)**
   - Definição: Exame sistemático do código-fonte por pessoas diferentes do autor
   - Tipos: Formal (inspeção), Lightweight (over-the-shoulder), Tool-assisted (PRs)
   - Benefícios comprovados: Redução de 60-90% de defeitos quando bem executado (Fagan, 1976)

2. **Defeitos de Software**
   - Classificação por severidade: Crítico, Alto, Médio, Baixo
   - Classificação por tipo: Funcional, Segurança, Performance, Manutenibilidade, Estilo
   - Taxonomias: IEEE, ODC (Orthogonal Defect Classification)

3. **Análise Estática de Código**
   - Técnicas: Pattern matching, Data flow analysis, Abstract interpretation
   - Ferramentas tradicionais: Linters, SonarQube, ESLint, Pylint
   - Limitações: Alto número de falsos positivos, regras fixas

4. **IA/LLMs para Código**
   - Modelos: GPT-4, Claude, CodeLlama, StarCoder
   - Capacidades: Compreensão de contexto, detecção de padrões complexos, sugestões
   - Limitações: Alucinações, inconsistência, dependência de prompt

**Métricas empíricas de referência:**

| Métrica | Valor típico (literatura) | Fonte |
|---------|---------------------------|-------|
| Defeitos encontrados por revisão manual | 60-70% dos existentes | Fagan, 1976; Kollanus & Koskinen, 2009 |
| Tempo médio de revisão manual | 200-400 LOC/hora | Kemerer & Paulk, 2009 |
| Taxa de falso positivo (ferramentas tradicionais) | 30-50% | Johnson et al., 2013 |

---

## 3. Objetivos e questões (Goal / Question / Metric)

### 3.1 Objetivo geral (Goal template)

Utilizando o template GQM (Goal-Question-Metric):

| Componente | Descrição |
|------------|-----------|
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
|------|-----------|
| Linguagem | Python 3.x |
| Tipo de código | Scripts e funções de complexidade baixa a média (50-200 LOC) |
| Tipos de defeitos | Funcionais, segurança, performance, manutenibilidade, estilo |
| Ferramenta de IA | [Definir: CodeRabbit / GitHub Copilot / PR-Agent] |
| Participantes | Estudantes de graduação com conhecimento básico-intermediário em Python |
| Processo | Revisão de Pull Requests em repositório controlado |

**Excluído do escopo:**

| Item | Justificativa |
|------|---------------|
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
|-----------|---------|-----------|
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

| Stakeholder | Papel/Grupo | Nível de envolvimento |
|-------------|-------------|-----------------------|
| **Autor do TCC** | Pesquisador principal | Alto - execução completa |
| **Orientador** | Supervisor acadêmico | Médio - orientação e revisão |
| **Banca examinadora** | Avaliadores | Baixo - avaliação final |
| **Participantes** | Sujeitos do experimento | Médio - execução das tarefas |
| **Comunidade acadêmica** | Leitores/pesquisadores futuros | Baixo - consumo dos resultados |
| **Profissionais de ES** | Potenciais usuários dos resultados | Baixo - aplicação prática |

---

### 5.2 Interesses e expectativas dos stakeholders

| Stakeholder | Interesses e expectativas |
|-------------|---------------------------|
| **Autor do TCC** | Completar o TCC com qualidade; obter resultados publicáveis; aprender sobre experimentação |
| **Orientador** | Trabalho metodologicamente correto; contribuição relevante; aluno bem formado |
| **Banca examinadora** | Rigor científico; clareza na apresentação; contribuição para a área |
| **Participantes** | Experiência de aprendizado; compensação pelo tempo (créditos, certificado); tarefa interessante |
| **Comunidade acadêmica** | Evidências empíricas confiáveis; metodologia replicável; insights acionáveis |
| **Profissionais de ES** | Recomendações práticas; dados para decisão de adoção de ferramentas |

---

### 5.3 Impactos potenciais no processo / produto

**Durante o experimento:**

| Impacto | Descrição | Mitigação |
|---------|-----------|-----------|
| Tempo dos participantes | 1-2 horas por participante | Agendar em horários convenientes; oferecer compensação |
| Uso de infraestrutura | Repositórios GitHub, ferramentas de IA | Preparar com antecedência; ter plano B |
| Carga do pesquisador | Alto esforço de preparação e execução | Planejar cronograma realista |

**Após o experimento:**

| Impacto potencial | Descrição |
|-------------------|-----------|
| **Na academia** | Contribuição para base de conhecimento sobre IA em ES |
| **Na prática** | Subsídio para decisões de adoção de ferramentas de IA |
| **Para participantes** | Maior consciência sobre práticas de code review |
| **Para o autor** | Formação em metodologia experimental; possível publicação |

---

## Checklist: O que você precisa providenciar

### Para a Seção 1 (Identificação)
- [ ] Definir título final do experimento
- [ ] Obter código/ID conforme padrão da instituição
- [ ] Confirmar dados do orientador
- [ ] Registrar datas oficiais

### Para a Seção 2 (Contexto)
- [ ] Escolher a ferramenta de IA específica (CodeRabbit, Copilot, etc.)
- [ ] Confirmar que Python é a linguagem adequada para seus participantes
- [ ] Fazer revisão bibliográfica mais aprofundada
- [ ] Ler pelo menos 5-10 artigos da lista de referências

### Para a Seção 3 (Objetivos)
- [ ] Validar questões de pesquisa com orientador
- [ ] Confirmar se as métricas são mensuráveis no seu contexto
- [ ] Definir taxonomia final de categorias de defeitos

### Para a Seção 4 (Escopo)
- [ ] Confirmar restrições reais (tempo, orçamento, acesso)
- [ ] Validar premissas com orientador
- [ ] Listar todas as limitações conhecidas

### Para a Seção 5 (Stakeholders)
- [ ] Identificar forma de recrutamento de participantes
- [ ] Definir compensação/incentivo para participantes
- [ ] Alinhar expectativas com orientador

---

## Próximos passos sugeridos

1. **Revisar este documento com o orientador** - Obter feedback antes de continuar
2. **Escolher a ferramenta de IA** - Testar 2-3 opções e selecionar a mais adequada
3. **Criar os artefatos de código** - Desenvolver códigos com defeitos inseridos (seeded)
4. **Preencher seções 6-10** - Design experimental, hipóteses, variáveis
5. **Submeter ao comitê de ética** (se necessário na sua instituição)

---

*Documento elaborado como parte do TCC sobre Code Review com IA vs. Manual*

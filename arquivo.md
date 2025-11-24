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
| **Ambiente**         | Acadêmico - Universidade [Nome]                |
| **Participantes**    | Estudantes de graduação em [Curso]            |
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

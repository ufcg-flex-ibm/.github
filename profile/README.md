# Bem-vindo à Nossa Organização 🌐

## Quem Somos

Somos um grupo de pesquisa e desenvolvimento dedicado à inovação em tecnologias de rede e inteligência artificial. Nossa missão é explorar e desenvolver aplicações avançadas para ecossistemas de **redes 5G**, com foco principal em soluções de **Inteligência Artificial aplicada à gestão de recursos de rede**.

## Nosso Foco

Nossos projetos cobrem um amplo espectro de atividades ligadas a otimização e gestão inteligente de recursos em ambientes de rede de próxima geração, incluindo:

* **Otimização de Recursos de Rede**: Uso de IA para alocação dinâmica de espectro e recursos em redes 5G.
* **Predição e Análise**: Modelos de machine learning para previsão de demanda, detecção de anomalias e comportamento da rede.
* **Automação Inteligente**: Sistemas autônomos para operação e manutenção de infraestrutura 5G.
* **Pesquisa Aplicada**: Desenvolvimento de algoritmos e técnicas inovadoras que refletem o estado da arte em IA e telecomunicações.

## Sobre Este Documento

Este documento estabelece os **padrões e diretrizes** que toda a nossa organização segue para garantir colaboração eficiente, código de qualidade e manutenibilidade a longo prazo. Quer você esteja iniciando um novo projeto, contribuindo em um existente ou revisando código de colegas, este guia é seu ponto de referência.

---

# Diretrizes de Uso do Git e Padrões de Repositório

Este documento define os padrões adotados pela nossa organização para o uso do Git, nomenclatura de branches, elaboração de mensagens de commit e estrutura mínima exigida para novos repositórios. O objetivo é garantir a manutenabilidade, legibilidade e facilitar a colaboração e revisão de código entre as equipes.

---

## 1. Nomenclatura de Branches

O nome da branch deve ser descritivo e indicar claramente o propósito do trabalho. Adotamos o formato baseado no fluxo de trabalho ágil:

**Formato:** `<tipo>/<numero-da-issue>-<breve-descricao>` (ou apenas `<tipo>/<breve-descricao>` caso não haja um sistema de tickets).

### Tipos (Labels) Permitidos:
* **`feat`**: Desenvolvimento de uma nova funcionalidade (feature).
* **`fix`**: Correção de um bug ou erro no código.
* **`chore`**: Tarefas de manutenção, atualização de dependências, ou configurações (ex: ajustes em arquivos Docker, CI/CD).
* **`debug`**: Inserção de logs temporários ou ferramentas para investigação de problemas em ambientes de teste.
* **`docs`**: Atualização ou criação de documentação técnica.
* **`refactor`**: Reestruturação de código existente sem alterar seu comportamento externo (não adiciona feature nem corrige bug).
* **`test`**: Criação ou atualização de testes automatizados.

**Exemplos Práticos:**
* `feat/123-add-lstm-prediction-model`
* `fix/45-resolve-kafka-consumer-timeout`
* `chore/update-fastapi-version`
* `docs/update-readme-setup-instructions`

---

## 2. Boas Práticas para Mensagens de Commit

As mensagens de commit devem contar a história do repositório. Utilizamos o padrão [Conventional Commits](https://www.conventionalcommits.org/), que facilita a leitura e a geração automática de changelogs.

**Formato:**
```text
<tipo>(<escopo opcional>): <descrição em modo imperativo>

[corpo opcional explicando o 'porquê' e o 'como']
```

### Regras Principais:
1. **Comece pelo tipo**: Use os mesmos tipos definidos nas branches (`feat`, `fix`, `chore`, etc.).
2. **Use o modo imperativo na descrição**: Escreva como se estivesse dando uma ordem ao código. Exemplo: *Adiciona rota de API* em vez de *Adicionado* ou *Adicionando*.
3. **Seja conciso na primeira linha**: Mantenha o título com algo em torno de 50 caracteres.
4. **Detalhe no corpo (se necessário)**: Se a alteração for complexa (ex: otimização de uma query no MySQL ou ajustes em um algoritmo de alocação de recursos), use o corpo do commit para explicar a motivação técnica.

**Exemplos Práticos:**
* `feat: cria endpoint para ingestão de dados`
* `fix: corrige vazamento de conexão no pool do Cassandra`
* `chore: configura pipeline do Github Actions`
* `refactor: extrai lógica de autenticação para serviço dedicado`

---

## 3. Requisitos Mínimos para Repositórios

Para garantir a padronização e a facilidade de manutenção a longo prazo, todo repositório da organização deve conter os seguintes elementos em sua raiz:

### 3.1. Arquivo `README.md`
O repositório deve ser autoexplicativo. O `README.md` é a porta de entrada e deve conter, no mínimo:
* **Descrição do Projeto**: O que o projeto faz e qual problema ele resolve.
* **Pré-requisitos**: Ferramentas necessárias (ex: Docker, Python 3.10+, Redis).
* **Configuração e Execução**: Passo a passo de como rodar o projeto localmente ou no ambiente de desenvolvimento relacionado.
* **Variáveis de Ambiente**: Lista de variáveis necessárias (fornecer um `.env.example`).
* **Comandos Úteis**: Como rodar linters, formatações e migrações.

### 3.2. Arquivo `.gitignore`
É **estritamente proibido** commitar arquivos sensíveis, artefatos de compilação ou arquivos de sistema operacional. O repositório deve ter um `.gitignore` configurado desde o primeiro commit.
* Deve ignorar credenciais (`.env`, chaves privadas).
* Deve ignorar diretórios de ambientes virtuais (`venv/`, `.env/`).
* Deve ignorar caches e artefatos de build (`__pycache__/`, `.pytest_cache/`, `.ipynb_checkpoints/`).
* Caso o repositorio necessite de algum montante inicial de dados, e importante que esse conjunto seja descrito, mas não é necessário a sua presença no repositorio.

### 3.3. Testes Automatizados (caso o repositorio guarde código)
Código não testado é código legado.
* Um diretório `tests/` deve existir na raiz ou junto aos módulos.
* É obrigatório incluir testes unitários para a lógica central de negócios antes da aprovação de qualquer Pull Request (PR).
* Inclua instruções claras no `README.md` de como executar a suíte de testes.

### 3.4. Estrutura de Diretórios Focada em Manutenabilidade
Evite espalhar arquivos na raiz do repositório. O código-fonte deve ser separado das configurações. Abaixo, um exemplo de estrutura recomendada:

```text
meu-projeto/
├── .github/             # Configurações de CI/CD (ex: Actions)
├── docs/                # Documentações arquiteturais e diagramas
├── src/                 # Código-fonte principal da aplicação
│   ├── routes/          # Controladores e rotas
│   ├── services/        # Regras de negócio e casos de uso
|    ...
│   └── main.py          # Ponto de entrada da aplicação
├── tests/               # Testes automatizados (unitários e de integração)
├── .gitignore           # Definição de arquivos a serem ignorados
├── Dockerfile           # Definição do container da aplicação
├── README.md            # Documentação principal
└── requirements.txt     # (Ou pyproject.toml / package.json) Gerenciamento de dependências
```
> [!NOTE]
> É importante salientar que esse é apenas um exemplo de estrutura de repositorio pois cada aplicação tem o seu propósito. Todo repositório deve estar alinhado com boas práticas relacionadas a organização de diretorio e separação de módulos com foco em manutenabilidade.

## 4. Fluxo de Pull Requests (Revisão de Código)

### 4.1. Princípios Fundamentais
1. Nunca faça commits diretos na branch principal (`main` ou `master`).
2. Todo merge deve ser feito através de um Pull Request (PR) após aprovação da equipe.
3. Solicite a revisão de pelo menos um membro da equipe antes de realizar o merge.

### 4.2. Boas Práticas para Pull Requests

**Mantenha PRs Pequenos e Focados**
* Quebre grandes features em múltiplos PRs menores e gerenciáveis.
* PRs menores são mais fáceis de revisar, testar e entender o contexto das mudanças.
* Isso reduz o risco de bugs e facilita a revertibilidade em caso de problemas.

**Forneça Contexto e Orientação Claros**
* Use um título descritivo e claro que resuma a mudança ou funcionalidade.
* Na descrição do PR, explique **por quê** a mudança é necessária, não apenas **o quê** foi mudado.
* Inclua links issues ou documentação relevante.
* Referencie a issue relacionada com `Fixes #123` ou `Closes #456` para rastrabilidade automática.

**Revise o Seu Próprio Código Primeiro**
* Antes de abrir o PR, faça uma auto-revisão cuidadosa do código.
* Procure por erros de digitação, inconsistências de formatação ou problemas de lógica.
* Remova logs temporários, código comentado ou ferramentas de debug (ex: `console.log`, print statements).
* Verifique se o código segue as convenções e padrões do projeto.

**Automatize Testes e Linting**
* Garanta que os pipelines de CI/CD (testes automatizados e linting) estão passando.
* A falha no CI é bloqueante: não proceda com o merge até que todos os testes passem.
* Configure o repositório para exigir que as verificações de CI passem antes de permitir o merge.

## 5. Uso da Wiki

Toda US realizada que tiver artefato produzido (código, documento, modelo, dataset, etc.) deve ter uma documentação correspondente na **IBM-WIKI**. Essa documentação garante rastreabilidade do trabalho e facilita o entendimento por outros membros da equipe, mesmo que a tarefa não tenha gerado código (ex: pesquisas, análises, POCs).

A documentação completa de uso da wiki completa está disponível em [IBM-WIKI](https://github.com/ufcg-flex-ibm/wiki).

### 5.1. Nomenclatura do Documento
O nome do documento deve seguir o padrão `US-<id>`, de forma que os arquivos fiquem ordenados no repositório da wiki.

**Exemplo:** `US-21.md`

### 5.2. Template Padrão
Toda documentação de US deve seguir o [template padrão da organização](https://github.com/ufcg-flex-ibm/wiki/blob/main/template.md), preenchendo as seções conforme a natureza da tarefa:

- **Identificação**: ID, título, tipo (Implementação / Análise / Pesquisa / Configuração / Documentação / Correção / Outro) e responsável(is).
- **Objetivo**: o que a tarefa se propunha a resolver ou entregar.
- **Contexto**: preenchido quando o motivo da tarefa não é óbvio pelo título.
- **Solução / Abordagem**: como a tarefa foi executada, adaptando o nível de detalhe conforme o tipo (metodologia para análises, arquitetura/fluxo para implementações, etc.).
- **Tecnologias / Ferramentas Utilizadas**: preenchido apenas se aplicável.
- **Testes**: preenchido apenas se a tarefa envolveu testes, incluindo pré-requisitos, configuração do ambiente e casos testados.
- **Artefatos**: referência aos artefatos produzidos (repositórios, notebooks, documentos, modelos, etc.), quando existirem.
- **Dificuldades Encontradas**: obstáculos, bloqueios ou aprendizados relevantes.
- **Referências / Links Úteis**: organizados em bullet points, com links diretos.

> [!NOTE]
> Nem toda US produz código ou testes. O template é flexível: seções não aplicáveis podem ser omitidas, mas a estrutura geral(identificação, objetivos, solução/abordagem) e a nomenclatura devem ser mantidas.


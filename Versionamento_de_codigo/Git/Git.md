- Instalção
    https://git-scm.com/
- Introdução ao GIT
   - Conceito de controle de versão e sua importância.
   - Vantagens do Git.

- Comandos Básicos
    - Configuração Inicial
    ```bash
    git config --global user.name "Seu Nome"
    git config --global user.email "seu.email@example.com"
    ```
	- Inicializar Repositório
    ```bash
    git init
    ```
	- Clonar Repositório
    ```bash
    git clone <URL-do-repositório>
    ```
	- Status do Repositório
    ```bash
    git status
    ```
	- Adicionar Alterações ao stagging
    ```bash
    git add <arquivo>  # Adiciona um arquivo
    git add .          # Adiciona todos os arquivos
    ```
	- Criar Commit
    ```bash
    git commit -m "Descrição da alteração"
    ```
	- Enviar Alterações para o Repositório Remoto
    ```bash
    git push origin <branch>
    ```
	- Atualizar o Repositório Local
    ```bash
    git pull origin <branch>
    ```
- Branching e Merging
    - Criar uma Nova Branch
    ```bash
    git branch <nome-da-branch>
    ```
	- Mudar para uma Branch
    ```bash
    git checkout <nome-da-branch>
    ```
	- Unir Alterações de uma Branch
    ```bash
    git merge <nome-da-branch>
    ```
- Resolução de Conflitos
    - Explicação de como resolver conflitos e boas práticas para evitá-los.
- .gitignore
    - Descrição de como configurar arquivos a serem ignorados.
    - Exemplo
    ```bash
    # Diretórios comuns
    /node_modules/
    /wwwroot/lib/

    # Arquivos sensíveis
    *.env
    *.log
    ```
- Configuração de Repositórios Remotos
    - Adicionar repositório remoto
      ```bash
      git remote add origin <URL-do-repositório>
      ```
	- Verificar repositórios remotos
      ```bash
      git remote -v
      ```

Fluxos de Trabalho (Workflows)
    - Git Flow
        - Branches principais 
            - main
            - develop
        - Branches auxiliares
            - feature/
            - release/
            - hotfix/
    - Trunk-Based Development
        Explicação do fluxo mais simples com commits diretos no main.
- Práticas Recomendadas
- Ferramentas Complementares
    - Extensões para VSCode
        - GitLens (visualização de histórico e autoria).
        - Git Graph (visualização de branches).
    - Integração com GitHub/GitLab:
        GitHub Actions (para CI/CD).
        GitLab Pipelines.
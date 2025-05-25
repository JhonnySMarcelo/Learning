- Instal��o
    https://git-scm.com/
- Introdu��o ao GIT
   - Conceito de controle de vers�o e sua import�ncia.
   - Vantagens do Git.

- Comandos B�sicos
    - Configura��o Inicial
    ```bash
    git config --global user.name "Seu Nome"
    git config --global user.email "seu.email@example.com"
    ```
	- Inicializar Reposit�rio
    ```bash
    git init
    ```
	- Clonar Reposit�rio
    ```bash
    git clone <URL-do-reposit�rio>
    ```
	- Status do Reposit�rio
    ```bash
    git status
    ```
	- Adicionar Altera��es ao stagging
    ```bash
    git add <arquivo>  # Adiciona um arquivo
    git add .          # Adiciona todos os arquivos
    ```
	- Criar Commit
    ```bash
    git commit -m "Descri��o da altera��o"
    ```
	- Enviar Altera��es para o Reposit�rio Remoto
    ```bash
    git push origin <branch>
    ```
	- Atualizar o Reposit�rio Local
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
	- Unir Altera��es de uma Branch
    ```bash
    git merge <nome-da-branch>
    ```
- Resolu��o de Conflitos
    - Explica��o de como resolver conflitos e boas pr�ticas para evit�-los.
- .gitignore
    - Descri��o de como configurar arquivos a serem ignorados.
    - Exemplo
    ```bash
    # Diret�rios comuns
    /node_modules/
    /wwwroot/lib/

    # Arquivos sens�veis
    *.env
    *.log
    ```
- Configura��o de Reposit�rios Remotos
    - Adicionar reposit�rio remoto
      ```bash
      git remote add origin <URL-do-reposit�rio>
      ```
	- Verificar reposit�rios remotos
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
        Explica��o do fluxo mais simples com commits diretos no main.
- Pr�ticas Recomendadas
- Ferramentas Complementares
    - Extens�es para VSCode
        - GitLens (visualiza��o de hist�rico e autoria).
        - Git Graph (visualiza��o de branches).
    - Integra��o com GitHub/GitLab:
        GitHub Actions (para CI/CD).
        GitLab Pipelines.
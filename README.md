## Configuração inicial de um novo repositório no GitHub

Para começar um novo projeto no GitHub, siga estes passos:

1- Crie um novo repositório no GitHub, se ainda não tiver feito isso.

2- No terminal, execute os seguintes comandos:

```
echo "# commands" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:seu_usuario/seu_repositorio.git
git push -u origin main
```

Esses comandos realizam as seguintes ações:
- echo "# commands" >> README.md: Cria um novo arquivo README.md com o conteúdo inicial.
- git init: Inicializa um repositório git local.
- git add README.md: Adiciona o arquivo README.md ao índice (staging area) para ser commitado.
- git commit -m "first commit": Realiza o primeiro commit com uma mensagem descritiva.
- git branch -M main: Renomeia a branch padrão de master para main.
- git remote add origin git@github.com:seu_usuario/seu_repositorio.git: Adiciona o repositório remoto do GitHub como o origin.
- git push -u origin main: Faz o push do commit inicial para o repositório remoto no GitHub.
- Certifique-se de substituir seu_usuario pelo seu nome de usuário do GitHub e seu_repositorio pelo nome do seu repositório.

3- Agora você tem um repositório vazio no GitHub com um README inicial pronto para ser preenchido com o conteúdo do seu projeto.

# Principais comandos GIT

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


## Adição de nova chave SSH ao computador

Ao trabalhar com diferentes serviços Git, pode ser necessário configurar múltiplas chaves SSH para autenticação. Aqui está como adicionar uma nova chave SSH ao seu computador:

1. **Gerar uma Nova Chave SSH:** No terminal, execute o seguinte comando para gerar uma nova chave SSH:

   ```
      ssh-keygen -t rsa -b 4096 -C "seu_email@example.com" -f ~/.ssh/sua_nova_chave
   ```
Substitua **"seu_email@example.com"** pelo seu endereço de e-mail associado à nova chave e **sua_nova_chave** pelo nome que deseja dar à sua nova chave.

2. **Siga as Instruções:** Pressione Enter para aceitar o local padrão para salvar a chave. Se desejar, você pode digitar uma frase de acesso para proteger ainda mais a chave.

3. **Adicionar a Chave SSH ao Agente SSH:** Execute o seguinte comando para adicionar a nova chave ao agente SSH:
   
   ```
   ssh-add ~/.ssh/sua_nova_chave
   ```

Substitua **sua_nova_chave** pelo nome da sua nova chave.

4. **Copie a Chave Pública:** Use o comando cat para exibir o conteúdo da chave pública:

   ```
   cat ~/.ssh/sua_nova_chave.pub
   ```

Copie o resultado exibido no terminal.

5. **Adicionar a Chave SSH ao Serviço Git:** Cole a chave pública no serviço Git que deseja autenticar. Por exemplo, para adicionar a chave ao GitHub, acesse suas configurações de conta e adicione a chave na seção "SSH and GPG keys".

6. **Teste a Conexão SSH:** Para verificar se a chave SSH foi configurada corretamente, você pode executar o seguinte comando no terminal:

   ```
   ssh -T git@servico_git.com
   ```

Substitua **servico_git.com** pelo host do serviço Git que você está usando (por exemplo, github.com, gitlab.com, etc.).

Agora você configurou com sucesso uma nova chave SSH para autenticação em um serviço Git específico.

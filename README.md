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

1. **Gerar uma nova chave SSH:** No terminal, execute o seguinte comando para gerar uma nova chave SSH:

   ```
      ssh-keygen -t rsa -b 4096 -C "seu_email@example.com" -f ~/.ssh/sua_nova_chave
   ```
Substitua **"seu_email@example.com"** pelo seu endereço de e-mail associado à nova chave e **sua_nova_chave** pelo nome que deseja dar à sua nova chave.

2. **Siga as instruções:** Pressione Enter para aceitar o local padrão para salvar a chave. Se desejar, você pode digitar uma frase de acesso para proteger ainda mais a chave.

3. **Adicionar a chave SSH ao agente SSH:** Execute o seguinte comando para adicionar a nova chave ao agente SSH:
   
   ```
   ssh-add ~/.ssh/sua_nova_chave
   ```

Substitua **sua_nova_chave** pelo nome da sua nova chave.

4. **Copie a chave pública:** Use o comando cat para exibir o conteúdo da chave pública:

   ```
   cat ~/.ssh/sua_nova_chave.pub
   ```

Copie o resultado exibido no terminal.

5. **Adicionar a chave SSH ao serviço git:** Cole a chave pública no serviço Git que deseja autenticar. Por exemplo, para adicionar a chave ao GitHub, acesse suas configurações de conta e adicione a chave na seção "SSH and GPG keys".

6. **Teste a conexão SSH:** Para verificar se a chave SSH foi configurada corretamente, você pode executar o seguinte comando no terminal:

   ```
   ssh -T git@servico_git.com
   ```

Substitua **servico_git.com** pelo host do serviço Git que você está usando (por exemplo, github.com, gitlab.com, etc.).

Agora você configurou com sucesso uma nova chave SSH para autenticação em um serviço Git específico.

## Rebase da branch local com a main utilizando fetch

O rebase é uma técnica útil para integrar as alterações da branch atual com outra branch, como a branch `main`. Ao usar o fetch antes do rebase, você garante que está trabalhando com as últimas alterações da branch remota antes de aplicar suas alterações locais. Aqui está como realizar o rebase da branch local com a branch `main`, usando o fetch:

1. **Salve as alterações locais:** Se você tiver alterações não commitadas na sua branch atual, é recomendável salvá-las usando `git stash`. Isso permite que você as reaplique após o rebase. Execute o seguinte comando no terminal:

    ```
   git stash
    ```

2. **Atualize a branch local:** Use o comando `git fetch` para buscar as últimas alterações da branch remota `main`. Isso garante que você está trabalhando com as últimas atualizações antes de realizar o rebase. Execute o seguinte comando no terminal:


    ```
   git fetch origin main
    ```

3. **Reaplique as alterações locais:** Se você usou `git stash` para salvar as alterações locais, agora é a hora de reaplicá-las. Execute o seguinte comando no terminal:

    ```
   git stash apply
    ```

4. **Realize o rebase:** Agora você está pronto para realizar o rebase da sua branch local com a branch `main`. Execute o seguinte comando no terminal:

    ```
   git rebase origin/main
    ```
    
Isso aplica suas alterações locais sobre as alterações mais recentes da branch `main`, resultando em um histórico de commits mais limpo e linear.

5. **Resolva conflitos (se necessário):** Durante o rebase, podem ocorrer conflitos de merge que exigem intervenção manual para serem resolvidos. Se isso acontecer, o Git irá sinalizar os arquivos com conflitos e você precisará resolvê-los manualmente. Após resolver os conflitos, adicione as alterações com `git add` e continue o rebase com `git rebase --continue`.

6. **Conclua o rebase:** Depois de resolver todos os conflitos e aplicar todas as alterações, conclua o rebase com o seguinte comando no terminal:

    ```
   git rebase --continue
    ```

7. **Atualize a branch remota (se necessário):** Se você já havia feito push das alterações locais antes do rebase, será necessário forçar o push das alterações rebased para a branch remota. Execute o seguinte comando no terminal:

   ```
   git push origin sua_branch -f
    ```

Substitua `sua_branch` pelo nome da sua branch local.

Agora você realizou com sucesso o rebase da sua branch local com a branch `main`, utilizando o fetch para garantir que está trabalhando com as últimas alterações da branch remota.

### Diferenças entre o `git fetch` e o `git pull`

Tanto `git fetch` quanto `git pull` são comandos usados para atualizar o repositório local com as alterações do repositório remoto. No entanto, eles têm diferenças significativas em sua funcionalidade e impacto:

1. **git fetch:**
   - O comando `git fetch` busca as últimas alterações do repositório remoto para o repositório local, mas não integra essas alterações automaticamente com a branch local atual.
   - As alterações baixadas pelo `git fetch` são armazenadas no repositório local, mas não são mescladas automaticamente com o trabalho local.
   - Isso permite que você examine as alterações baixadas antes de decidir como integrá-las com o trabalho local.
   - É útil quando você deseja atualizar seu repositório local para refletir o estado atual do repositório remoto, mas deseja decidir manualmente como incorporar essas alterações.

2. **git pull:**
   - O comando `git pull` também busca as últimas alterações do repositório remoto, mas integra automaticamente essas alterações com a branch local atual.
   - `git pull` é uma combinação dos comandos `git fetch` e `git merge` (ou `git rebase`, se configurado dessa forma).
   - O `git pull` extrai as alterações remotas e, em seguida, tenta mesclá-las automaticamente com a branch local atual.
   - Isso pode levar a conflitos de merge se houver alterações locais que entrem em conflito com as alterações remotas.
   - É útil quando você deseja atualizar seu repositório local e incorporar automaticamente essas alterações com seu trabalho local, sem a necessidade de uma etapa adicional de mesclagem manual.

Em relação ao rebase, a diferença prática entre `git fetch` e `git pull` é que o `git pull` pode integrar automaticamente as alterações remotas com a branch local, enquanto o `git fetch` requer uma etapa adicional (como `git rebase` ou `git merge`) para incorporar essas alterações.

Para realizar um rebase, muitas vezes é preferível usar `git fetch` para buscar as alterações remotas e, em seguida, `git rebase` para aplicar essas alterações à sua branch local de forma mais controlada e flexível, evitando potenciais conflitos de merge. Isso permite que você revise as alterações baixadas antes de rebaseá-las em seu trabalho local.

### Examinar as alterações baixadas através de um `git fetch`

Após executar o comando `git fetch` para buscar as últimas alterações do repositório remoto, você pode examinar essas alterações de várias maneiras para entender melhor como elas se comparam ao seu trabalho local. Aqui estão algumas formas comuns de fazer isso:

1. **Visualizar log de commits:**
   Você pode visualizar o log de commits das branches locais e remotas para entender quais alterações foram trazidas pelo `git fetch`. Use o seguinte comando para visualizar o log de commits:

   ```
   git log origin/main..main
   ```

Isso mostrará os commits exclusivos da branch `main` remota que ainda não foram integrados à sua branch local `main`.

2. **Visualizar diferenças entre branches:**
O comando `git diff` pode ser usado para visualizar as diferenças entre a branch local e a branch remota após o fetch. Use o seguinte comando para visualizar as diferenças:

   ```
   git diff main origin/main
   ```

Isso mostrará as diferenças entre a sua branch local `main` e a branch `main` remota.

3. **Verificar o status do repositório:**
O comando `git status` pode ser usado para verificar o status do seu repositório e ver quais branches foram atualizadas pelo `git fetch`. Execute simplesmente o comando:

   ```
   git status
   ```

Isso mostrará informações sobre quais branches foram atualizadas e se há alguma alteração pendente no seu repositório.

Essas são algumas maneiras de examinar as alterações baixadas após o comando `git fetch`, permitindo que você avalie as diferenças entre o seu trabalho local e o repositório remoto antes de decidir como integrar essas alterações.

### Recuperando alterações do `git stash`

Se você salvou suas alterações locais utilizando `git stash` antes de realizar o rebase e optou por não aplicá-las durante o rebase, você pode recuperá-las facilmente após a conclusão do processo. Aqui está como fazer isso:

1. **Listar os stashes disponíveis:**
   Use o comando `git stash list` para listar todos os stashes disponíveis no seu repositório. Isso ajudará você a identificar o stash que deseja recuperar. Execute o seguinte comando:
 
    ```
   git stash list
    ```
    
Isso mostrará uma lista numerada de todos os stashes presentes no seu repositório.

2. **Aplicar os stashes desejados:**
Escolha os stashes que deseja aplicar e use o comando `git stash apply` ou `git stash pop`, seguido pelo identificador do stash (geralmente uma numeração). O `git stash apply` mantém os stashes na lista de stashes disponíveis, enquanto o `git stash pop` remove os stashes da lista após aplicá-los. Você pode aplicar todos os stashes de uma vez utilizando o comando `git stash apply` ou git stash pop` sem especificar um identificador de stash. Por exemplo:

- Para aplicar todos os stashes mantendo-os na lista de stashes disponíveis:

    ```
   git stash apply
    ```

- Para aplicar todos os stashes e removê-los da lista de stashes:

    ```
   git stash pop
    ```

3. **Limpar os stashes (opcional):**
Se você não precisa mais dos stashes após aplicar suas alterações, pode removê-los da lista de stashes. Para fazer isso, use o comando `git stash drop` seguido pelo identificador do stash. Por exemplo:

    ```
   git stash drop stash@{0}
    ```

Isso removerá o stash selecionado da lista de stashes.

Após seguir esses passos, suas alterações salvas no git stash serão recuperadas e aplicadas ao seu diretório de trabalho, permitindo que você continue trabalhando com elas como necessário.

## Subir uma nova branch local para a branch remota

Se você criou uma nova branch local e deseja subi-la para o repositório remoto pela primeira vez, mas a branch correspondente ainda não foi criada no projeto remoto, você pode fazer isso facilmente utilizando o comando `git push` com a opção `-u` (ou `--set-upstream`). Aqui está como você pode realizar esse processo:

1. **Verificar as branches locais e remotas:**
   Antes de subir sua nova branch local, verifique quais branches locais e remotas existem atualmente no seu repositório. Use o comando `git branch -a` para listar todas as branches locais e remotas:

   ```
   git branch -a
   ```

Isso mostrará todas as branches presentes no seu repositório, tanto locais quanto remotas.

2. **Subir a nova branch local:**
Utilize o comando `git push` seguido pelo nome da nova branch local e o nome da branch remota para subi-la pela primeira vez. Como a branch remota correspondente ainda não foi criada, você precisará usar a opção `-u` (ou `--set-upstream`) para configurar a branch remota de acompanhamento. Por exemplo, se você deseja subir sua nova branch local chamada `nova_branch` para o repositório remoto e nomeá-la como `nova_branch` remotamente, execute o seguinte comando:

   ```
   git push -u origin nova_branch
   ```
   
Isso criará a branch `nova_branch` no repositório remoto e a associará à sua branch local `nova_branch`.

3. **Verificar o status do push:**
Após executar o comando `git push`, verifique o status da operação para garantir que a branch tenha sido enviada corretamente para o repositório remoto. Execute o seguinte comando:

   ```
   git status
   ```

Isso mostrará o status atual do seu repositório e indicará se o push foi bem-sucedido.

Após seguir esses passos, sua nova branch local será enviada para o repositório remoto pela primeira vez e estará pronta para colaboração com outros membros do projeto.



   
   

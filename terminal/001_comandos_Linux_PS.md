# Comandos Linux e seus equivalentes no PowerShell

Esta seção compara comandos básicos usados frequentemente em ambos os terminais. Note que o PowerShell possui *aliases* que imitam muitos comandos Linux para facilitar a transição. Os aliases mais comuns são mostrados entre parênteses.

| Id  | Ação                       | Linux          | PowerShell                                      | Descrição                                                                                                                                                                      |
| --- | -------------------------- | -------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 01  | Listar arquivos            | `ls`           | `Get-ChildItem` (`ls`, `dir`, `gci`)            | Lista arquivos e pastas no diretório atual.                                                                                                                                    |
| 02  | Mudar de diretório         | `cd`           | `Set-Location` (`cd`, `sl`)                     | Muda o diretório de trabalho atual.                                                                                                                                            |
| 03  | Mostrar diretório atual    | `pwd`          | `Get-Location` (`pwd`, `gl`)                    | Mostra o caminho completo do diretório atual.                                                                                                                                  |
| 04  | Limpar o terminal          | `clear`        | `Clear-Host` (`clear`, `cls`)                   | Limpa a tela do terminal.                                                                                                                                                      |
| 05  | Listar tudo (detalhado)    | `ls -al`       | `Get-ChildItem -Force` (`ls -Force`, `gci -Fo`) | Lista todos os itens (incluindo ocultos/sistema). A formatação detalhada (`-l`) é padrão no PowerShell, mas diferente do `ls -l`. Para formato similar ao `-l`, use `ls -Force | Format-List`. |
| 06  | Exibir conteúdo do arquivo | `cat nome.txt` | `Get-Content nome.txt` (`cat`, `gc`, `type`)    | Mostra o conteúdo de um arquivo de texto.                                                                                                                                      |
| 07  | Sair do shell              | `exit`         | `exit`                                          | Encerra a sessão atual do terminal.                                                                                                                                            |

**Nota sobre Aliases:** Use `Get-Alias <nome_do_alias>` no PowerShell para ver qual comando ele representa (ex: `Get-Alias ls`).
___

## Navegação entre diretórios

| Id  | Ação                         | Linux          | PowerShell                              | Descrição                                                                                                              |
| --- | ---------------------------- | -------------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 01  | Ir para o diretório pai      | `cd ..`        | `Set-Location ..` (`cd ..`, `sl ..`)    | Volta um nível na hierarquia de pastas.                                                                                |
| 02  | Ir para um subdiretório      | `cd pasta`     | `Set-Location pasta` (`cd pasta`)       | Entra na pasta chamada "pasta".                                                                                        |
| 03  | Ir para um caminho absoluto  | `cd /home`     | `Set-Location C:\Users` (`cd C:\Users`) | Vai diretamente para um caminho especificado.                                                                          |
| 04  | Voltar várias pastas         | `cd ../../`    | `Set-Location ../..` (`cd ../../`)      | Volta múltiplos níveis na hierarquia.                                                                                  |
| 05  | Ir para o diretório anterior | `cd -`         | `Pop-Location` (`popd`)                 | Volta ao diretório visitado anteriormente (requer `Push-Location` prévio no PowerShell). O Linux `cd -` é mais direto. |
| 06  | Ir para o diretório 'home'   | `cd` ou `cd ~` | `Set-Location ~` (`cd ~`)               | Vai para o diretório pessoal do usuário logado.                                                                        |
___

## Diretórios padrão do Linux e Equivalentes Conceituais no Windows

A estrutura de diretórios é fundamentalmente diferente.

### Linux (FHS - Filesystem Hierarchy Standard)

| Diretório | Descrição                                                                                 |
| --------- | ----------------------------------------------------------------------------------------- |
| `/bin`    | Binários essenciais do sistema.                                                           |
| `/boot`   | Arquivos de inicialização (kernel, boot loader).                                          |
| `/dev`    | Arquivos de dispositivo (hardware).                                                       |
| `/etc`    | Arquivos de configuração do sistema.                                                      |
| `/home`   | Diretórios pessoais dos usuários comuns.                                                  |
| `/lib`    | Bibliotecas compartilhadas essenciais.                                                    |
| `/media`  | Ponto de montagem para mídias removíveis (automático).                                    |
| `/mnt`    | Ponto de montagem temporário (manual).                                                    |
| `/opt`    | Software opcional/adicional.                                                              |
| `/proc`   | Sistema de arquivos virtual (processos, kernel).                                          |
| `/root`   | Diretório pessoal do superusuário (root).                                                 |
| `/run`    | Informações temporárias do sistema (runtime).                                             |
| `/sbin`   | Binários de administração do sistema.                                                     |
| `/srv`    | Dados de serviços oferecidos pelo sistema.                                                |
| `/sys`    | Sistema de arquivos virtual (kernel/hardware).                                            |
| `/tmp`    | Arquivos temporários (geralmente limpos na reinicialização).                              |
| `/usr`    | Programas, bibliotecas e dados de usuário instalados pelo sistema (não do usuário comum). |
| `/var`    | Arquivos variáveis (logs, spool, cache).                                                  |
___

### Windows (Estrutura Comum)

| Diretório (Exemplo)            | Equivalente Conceitual Linux    | Descrição                                                                        |
| ------------------------------ | ------------------------------- | -------------------------------------------------------------------------------- |
| `C:\Windows`                   | `/bin`, `/sbin`, `/etc`, `/lib` | Arquivos do sistema operacional, drivers, configurações centrais (Registro).     |
| `C:\Program Files`             | `/usr`, `/opt`                  | Local padrão para instalação de aplicativos (64 bits).                           |
| `C:\Program Files (x86)`       | `/usr`, `/opt`                  | Local padrão para instalação de aplicativos (32 bits em SO 64 bits).             |
| `C:\Users\<nome>`              | `/home/<nome>`                  | Diretório pessoal do usuário (Documentos, Downloads, Desktop, etc.).             |
| `C:\Users\Public`              | `-`                             | Pastas compartilhadas entre todos os usuários da máquina.                        |
| `C:\ProgramData`               | `/etc`, `/var/lib`              | Dados e configurações de aplicativos para todos os usuários (geralmente oculto). |
| `C:\Windows\Temp`              | `/tmp`                          | Arquivos temporários do sistema.                                                 |
| `%TEMP%` (Variável)            | `/tmp`                          | Diretório temporário do usuário (`C:\Users\<nome>\AppData\Local\Temp`).          |
| Letras de Unidade (`D:`, `E:`) | `/media/<nome>`, `/mnt/<nome>`  | Outras partições, discos ou mídias removíveis.                                   |
___

## Comandos Fundamentais e Conceitos

| Conceito/Ação                 | Linux                             | PowerShell                         | Descrição                                                                                                                                                     |
| ----------------------------- | --------------------------------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Executar como Admin           | `sudo comando`                    | Iniciar PowerShell como Admin      | Linux usa `sudo` por comando. PowerShell geralmente requer iniciar a sessão inteira com privilégios elevados (clique direito -> Executar como administrador). |
| Obter ajuda sobre comando     | `man comando` ou `comando --help` | `Get-Help comando` (`help`, `man`) | Exibe a documentação para um comando específico. Use `Get-Help comando -Examples` ou `-Full`.                                                                 |
| Histórico de comandos         | `history`                         | `Get-History` (`history`, `h`)     | Lista os comandos executados anteriormente na sessão.                                                                                                         |
| Limpar Histórico              | `history -c`                      | `Clear-History` (`clhy`)           | Apaga o histórico de comandos da sessão atual.                                                                                                                |
| Executar comando anterior     | `!!`                              | `Invoke-History` (`r`)             | Executa o último comando digitado.                                                                                                                            |
| Completar (Tab)               | `Tab`                             | `Tab`                              | Autocompleta nomes de comandos, arquivos, pastas e parâmetros. PowerShell tem autocompletar mais avançado.                                                    |
| Pipeline (redirecionar saída) | `comando1                         | comando2`                          | `comando1                                                                                                                                                     | comando2` | Envia a saída do `comando1` como entrada para o `comando2`. **Diferença:** Linux usa texto, PowerShell usa objetos. |
| Redirecionar p/ arquivo       | `comando > arquivo.txt`           | `comando > arquivo.txt`            | Cria/sobrescreve `arquivo.txt` com a saída do `comando`.                                                                                                      |
| Anexar a arquivo              | `comando >> arquivo.txt`          | `comando >> arquivo.txt`           | Adiciona a saída do `comando` ao final de `arquivo.txt`.                                                                                                      |
___

## Manipulação de Diretórios (Linux x PowerShell)

| Ação                         | Linux                | PowerShell                                                                               | Descrição                                                 |
| ---------------------------- | -------------------- | ---------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Criar diretório              | `mkdir nome`         | `New-Item -ItemType Directory -Name nome` (`mkdir`, `md`, `ni -ItemType Directory nome`) | Cria um novo diretório.                                   |
| Remover diretório vazio      | `rmdir nome`         | `Remove-Item nome` (`rmdir`, `rd`, `ri`, `del`)                                          | Remove um diretório **vazio**.                            |
| Remover diretório e conteúdo | `rm -r nome`         | `Remove-Item nome -Recurse` (`rm -r`, `del -r`, `rd -r`)                                 | Remove um diretório e todo o seu conteúdo **(CUIDADO!)**. |
| Listar conteúdo              | `ls`                 | `Get-ChildItem` (`ls`, `dir`, `gci`)                                                     | Lista arquivos e diretórios.                              |
| Mover/Renomear diretório     | `mv pasta destino`   | `Move-Item pasta destino` (`mv`, `move`, `mi`)                                           | Move ou renomeia uma pasta.                               |
| Copiar diretório             | `cp -r pasta nova`   | `Copy-Item pasta nova -Recurse` (`cp -r`, `copy -r`, `cpi -r`)                           | Copia um diretório e seu conteúdo recursivamente.         |
| Renomear diretório           | `mv nome atual novo` | `Rename-Item atual novo` (`ren`, `rename`, `rni`)                                        | Renomeia uma pasta no local atual.                        |
___

## Manipulação de Arquivos (Linux x PowerShell)

| Ação                   | Linux                      | PowerShell                                                               | Descrição                                                                                                               |
| ---------------------- | -------------------------- | ------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| Criar arquivo vazio    | `touch nome.txt`           | `New-Item -ItemType File nome.txt` (`ni nome.txt`) ou `$null > nome.txt` | Cria um arquivo vazio ou atualiza data/hora se já existe (`touch`). `New-Item` dá erro se existir. `$null >` cria/zera. |
| Exibir conteúdo        | `cat nome.txt`             | `Get-Content nome.txt` (`cat`, `gc`, `type`)                             | Mostra o conteúdo do arquivo na tela.                                                                                   |
| Escrever no arquivo    | `echo "texto" > nome.txt`  | `"texto" > nome.txt` ou `Set-Content nome.txt "texto"` (`sc`)            | Cria (ou sobrescreve) arquivo com o texto fornecido.                                                                    |
| Adicionar ao arquivo   | `echo "texto" >> nome.txt` | `"texto" >> nome.txt` ou `Add-Content nome.txt "texto"` (`ac`)           | Adiciona o texto ao final do arquivo existente.                                                                         |
| Copiar arquivo         | `cp a.txt b.txt`           | `Copy-Item a.txt b.txt` (`cp`, `copy`, `cpi`)                            | Copia `a.txt` para `b.txt`.                                                                                             |
| Mover/Renomear arquivo | `mv a.txt b.txt`           | `Move-Item a.txt b.txt` (`mv`, `move`, `mi`)                             | Move `a.txt` para `b.txt` (se for outro diretório) ou renomeia para `b.txt` (no mesmo diretório).                       |
| Renomear arquivo       | `mv a.txt b.txt`           | `Rename-Item a.txt b.txt` (`ren`, `rename`, `rni`)                       | Renomeia `a.txt` para `b.txt` no mesmo diretório.                                                                       |
| Deletar arquivo        | `rm nome.txt`              | `Remove-Item nome.txt` (`rm`, `del`, `erase`, `ri`)                      | Remove o arquivo especificado **(CUIDADO!)**.                                                                           |
___

## Busca de Arquivos e Conteúdo

| Ação                              | Linux                  | PowerShell                                                               | Descrição                                                                   |
| --------------------------------- | ---------------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| Encontrar arquivos por nome       | `find . -name "*.txt"` | `Get-ChildItem -Recurse -Filter "*.txt"` (`ls -r -fi "*.txt"`)           | Procura recursivamente por arquivos que correspondem ao padrão (ex: .txt).  |
| Procurar texto dentro de arquivos | `grep "palavra" *.txt` | `Select-String -Path "*.txt" -Pattern "palavra"` (`sls *.txt "palavra"`) | Procura pela "palavra" dentro de todos os arquivos .txt do diretório atual. |
| Procurar texto recursivamente     | `grep -r "palavra" .`  | `Get-ChildItem -Recurse -Include *.txt                                   | Select-String "palavra"` (`gci -r -i *.txt                                  | sls "palavra"`) | Procura recursivamente pela "palavra" em arquivos .txt. |
___

## Gerenciamento de Processos

| Ação                         | Linux                          | PowerShell                                      | Descrição                                                          |
| ---------------------------- | ------------------------------ | ----------------------------------------------- | ------------------------------------------------------------------ |
| Listar processos em execução | `ps aux` ou `top` / `htop`     | `Get-Process` (`ps`, `gps`)                     | Mostra os processos que estão rodando no sistema.                  |
| Filtrar processos por nome   | `ps aux                        | grep nome`                                      | `Get-Process -Name nome*` (`ps nome*`)                             | Lista processos cujo nome começa com "nome". |
| Encerrar processo (por ID)   | `kill PID`                     | `Stop-Process -Id PID` (`kill PID`, `spps PID`) | Termina o processo com o ID especificado (PID).                    |
| Encerrar processo (por nome) | `killall nome` ou `pkill nome` | `Stop-Process -Name nome` (`spps -n nome`)      | Termina todos os processos com o nome especificado **(CUIDADO!)**. |
___

## Editores de Arquivos via Terminal

| Ação                  | Linux               | PowerShell (Windows)          | PowerShell (Core em Linux/macOS) | Descrição                                                                                                                      |
| --------------------- | ------------------- | ----------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Editar arquivo (TUI)  | `nano nome.txt`     | `notepad nome.txt` (Abre GUI) | `nano nome.txt` / `vi nome.txt`  | Abre o arquivo em um editor. `nano`/`vi`/`vim` são editores de terminal (TUI). `notepad` é um editor gráfico (GUI) do Windows. |
| Alternativa (GUI)     | (Varia por Desktop) | `start nome.txt`              | (Varia por Desktop)              | Abre o arquivo com o aplicativo padrão associado à extensão no sistema.                                                        |
| Alternativa (VS Code) | `code nome.txt`     | `code nome.txt`               | `code nome.txt`                  | Abre o arquivo no Visual Studio Code (se instalado e no PATH).                                                                 |
___
****

## Permissões de Arquivos e Diretórios (Linux x PowerShell)

No Linux, as permissões seguem o modelo POSIX, baseado em três ações (Leitura, Escrita, Execução) para três tipos de entidades (Dono, Grupo, Outros). No Windows (e, portanto, no PowerShell), as permissões são gerenciadas através de Listas de Controle de Acesso (ACLs - Access Control Lists), que são mais granulares e complexas. A tabela **abaixo** mostra uma correspondência conceitual simplificada.

| Permissão    | Linux (Símbolo) | Linux (Octal) | PowerShell / Windows (Conceito em ACL)                                            | Descrição                                                                                                                         |
| ------------ | --------------- | ------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Leitura**  | `r`             | `4`           | `ReadData`, `ListDirectory`, `Read`                                               | Permite visualizar o conteúdo de um arquivo ou listar o conteúdo de um diretório.                                                 |
| **Escrita**  | `w`             | `2`           | `WriteData`, `AppendData`, `CreateFiles`, `CreateDirectories`, `Delete`, `Modify` | Permite alterar o conteúdo de um arquivo, criar/remover arquivos ou subdiretórios dentro de um diretório.                         |
| **Execução** | `x`             | `1`           | `ExecuteFile`, `Traverse` (`ReadAndExecute`)                                      | Permite executar um arquivo (se for um programa/script) ou acessar/atravessar um diretório (entrar nele com `cd`/`Set-Location`). |

**Observações:**

*   **Linux:** As permissões são visualizadas com `ls -l` e modificadas com `chmod`. A representação completa é `rwxrwxrwx` (dono, grupo, outros).
*   **PowerShell/Windows:** As permissões (ACLs) são visualizadas com `Get-Acl` e modificadas com `Set-Acl`. O comando `Get-ChildItem` (`ls`) no PowerShell exibe um "Mode" (ex: `d-----`, `-a----`) que indica atributos (Directory, Archive, ReadOnly, Hidden, System), não as permissões `rwx` da mesma forma que no Linux. A complexidade das ACLs permite controles muito mais específicos (ex: negar escrita, mas permitir apagar).****
___


## Redirecionamento de Saída: O Comando `ls > lista_projeto.txt`

Este comando é um exemplo fundamental de como redirecionar a saída de um comando (que normalmente iria para a tela) para um arquivo.

**Análise do Comando:**

*   **`ls`**:
    *   É o comando Linux para **listar** o conteúdo (arquivos e subdiretórios) do diretório atual.
    *   Por padrão, a saída deste comando é enviada para a *Saída Padrão* (stdout), que geralmente é o seu terminal/tela.

*   **`>`**:
    *   Este é o **operador de redirecionamento de saída**.
    *   Ele instrui o shell a pegar a *Saída Padrão* (stdout) do comando à sua esquerda (`ls`) e, em vez de exibi-la na tela, enviá-la para o destino à sua direita.

*   **`lista_projeto.txt`**:
    *   Este é o **arquivo de destino** para onde a saída do `ls` será redirecionada.

**O que Acontece:**

1.  O comando `ls` é executado e gera a lista de arquivos e diretórios.
2.  O operador `>` intercepta essa lista.
3.  O conteúdo da lista é gravado dentro do arquivo `lista_projeto.txt`.
    *   **Se `lista_projeto.txt` não existir:** O arquivo será criado no diretório atual.
    *   **Se `lista_projeto.txt` já existir:** **Seu conteúdo anterior será apagado e substituído** pela nova saída do `ls`. Tenha cuidado com isso!
4.  Como resultado, a listagem de arquivos **não aparecerá** na tela do terminal.

**Em Resumo:**

O comando `ls > lista_projeto.txt` executa o `ls` e salva sua saída (a lista de arquivos e diretórios) dentro do arquivo `lista_projeto.txt`, criando o arquivo se necessário ou sobrescrevendo-o se ele já existir.

**Equivalente em PowerShell:**

O conceito é idêntico, usando o cmdlet `Get-ChildItem` ou seus aliases:

`powershell`
Get-ChildItem > lista_projeto.txt
# Ou usando aliases comuns:
ls > lista_projeto.txt
dir > lista_projeto.txt

___

## 📦 Atualização de pacotes: `apt update` no Linux e equivalentes no PowerShell

### 🧭 Tabela Comparativa

| Sistema                       | Comando                | Descrição                                                            |
| ----------------------------- | ---------------------- | -------------------------------------------------------------------- |
| **Linux**                     | `sudo apt update`      | Atualiza a lista de pacotes disponíveis nos repositórios do sistema. |
| **PowerShell com winget**     | `winget upgrade --all` | Atualiza todos os pacotes instalados que possuem novas versões.      |
| **PowerShell com Chocolatey** | `choco upgrade all -y` | Atualiza todos os pacotes instalados via Chocolatey.                 |

---

### 🔎 Verificar pacotes com `winget`

Para apenas listar os pacotes que possuem atualizações disponíveis (sem instalar nada):

`powershell`
winget upgrade

___

### ✅ Verificar se o winget está instalado

winget --version
___

## Resumo de Comandos Linux Comuns

| Comando / Variação           | Descrição                                                                          |
| ---------------------------- | ---------------------------------------------------------------------------------- |
| `rm nome_arquivo`            | Remove o arquivo especificado.                                                     |
| `rm -i nome_arquivo`         | Remove o arquivo especificado, solicitando confirmação antes (Interativo).         |
| `rmdir nome_diretorio`       | Remove o diretório especificado, **somente se estiver vazio**.                     |
| `rm -r nome_diretorio`       | Remove o diretório e todo o seu conteúdo de forma recursiva. **(CUIDADO!)**        |
| `ls > arquivo.txt`           | Redireciona a saída do `ls` para `arquivo.txt`, **sobrescrevendo-o** se existir.   |
| `ls >> arquivo.txt`          | **Anexa** (adiciona ao final) a saída do `ls` ao `arquivo.txt` sem sobrescrevê-lo. |
| `echo "mensagem"`            | Exibe a "mensagem" especificada no terminal (Saída Padrão).                        |
| `echo "mensagem" >> arq.txt` | **Anexa** o texto "mensagem" ao final do arquivo `arq.txt`.                        |
| `sudo apt update`            | Atualiza a lista local de pacotes disponíveis nos repositórios (Requer `sudo`).    |
| `sudo apt upgrade`           | Instala as atualizações disponíveis para os pacotes já instalados (Requer `sudo`). |
| `sudo apt install <pacote>`  | Instala um novo pacote especificado (Requer `sudo`).                               |
| `sudo apt remove <pacote>`   | Remove (desinstala) o pacote especificado (Requer `sudo`).                         |

___

## Comandos Linux para Processos, Arquivos e Pipelines

| Comando / Variação      | Descrição                                                                                                                                                                |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `top`                   | Exibe uma visão dinâmica e em tempo real dos processos em execução, mostrando uso de CPU, memória, PID, etc.                                                             |
| `ps`                    | Fornece uma "fotografia" instantânea dos processos em execução.                                                                                                          |
| `ps aux`                | Lista todos os processos de todos os usuários com detalhes extensivos (%CPU, %MEM, PID, estado, comando).                                                                |
| `ps -u <usuario>`       | Exibe apenas os processos pertencentes ao `<usuario>` especificado.                                                                                                      |
| `ps -p <PID>`           | Exibe informações detalhadas sobre o processo com o `<PID>` (Process ID) fornecido.                                                                                      |
| `ps -C <comando>`       | Filtra e exibe os processos associados ao nome do `<comando>` especificado.                                                                                              |
| `pstree`                | Mostra a árvore de processos, ilustrando a relação hierárquica (pai/filho) entre eles.                                                                                   |
| `head <arquivo>`        | Exibe as primeiras linhas (por padrão, 10) de um `<arquivo>` ou da saída de outro comando via pipe.                                                                      |
| `comando1               | comando2`                                                                                                                                                                | **Pipe (` | `)**: Redireciona a saída padrão do `comando1` para ser a entrada padrão do `comando2`, permitindo encadear comandos. |
| `sort`                  | Ordena as linhas de um arquivo ou da saída de um comando (recebida via pipe). Útil para organizar dados.                                                                 |
| `kill <PID>`            | Envia um sinal para o processo com o `<PID>` especificado. O sinal padrão é `SIGTERM` (15), pedindo ao processo para terminar de forma organizada.                       |
| `kill -9 <PID>`         | Envia o sinal `SIGKILL` (9) para o processo com o `<PID>`. **Força o encerramento imediato e abrupto** (use com cautela, pode haver perda de dados).                     |
| `kill -STOP <PID>`      | Envia o sinal `SIGSTOP` (19) para o processo, **pausando** sua execução sem encerrá-lo.                                                                                  |
| `kill -CONT <PID>`      | Envia o sinal `SIGCONT` (18) para o processo, **retomando** a execução de um processo que foi pausado com `SIGSTOP`.                                                     |
| `pkill <nome_processo>` | Envia um sinal (padrão `SIGTERM`) para todos os processos cujo nome corresponda a `<nome_processo>`. **Afeta múltiplos processos**.                                      |
| `killall <nome_exato>`  | Envia um sinal (padrão `SIGTERM`) para todos os processos cujo nome corresponda *exatamente* a `<nome_exato>`. Similar ao `pkill`, mas geralmente mais restrito no nome. |
___

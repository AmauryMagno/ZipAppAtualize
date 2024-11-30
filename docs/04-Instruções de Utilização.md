## Instruções de utilização

1. A aplicação utiliza para o processo de atualização automatica, via GitHub, uma branch especifica com um arquivo version.json junto ao arquivo da aplicação principal no formato zip, tornando necessário a seguinte estruturação de pastas no GitHub,
    1. #### Crie uma Branch, de preferencia com o nome: Atualizate

    2. #### Configure a Branch da seguinte forma:
        ```shell
            .
            ├── code
            │   └── Atualizate
            │       └── version
            │          └── version.json
            └── ArquivoPrinciapl.zip
        ```
    3. #### Gere um Token para a Branch.

2. Configure o arquivo version.json como exposto abaixo, alterando as informações necessárias. (Inicialmente o arquivo local e o do GitHub devem ser iguais)
    #### Arquivo version.json
        ```json
            {
                "RepoOwner": "NomeExemplo",
                "RepoName": "NomeRepositorio",
                "BranchName": "NomeBranch",
                "TokenAPI": "TokenGitub",
                "Number": "00.00.0001",
                "NameExecutable": "NomeExecutavel",
                "PathExecutable": "PastaExecutavel",
                "NameFileZip": "ArquivoPrinciapl.zip",
                "Outdate": "NaoAtualizavel"
            }
        ```
    - "RepoOwner": "NomeExemplo" = (Nome do usuário criador do repositório);
    - "RepoName": "NomeRepositorio" = (Nome do repositório);
    - "BranchName": "NomeBranch" = (Nome da Branch, de prefeência Atualizate);
    - "TokenAPI": "TokenGitub" = (Token fornecido pela API do GitHub);
    - "Number": "00.00.0001" = (Versão inicial, que será comparada entre local e Virtual(GitHub) para iniciar atualização);
    - "NameExecutable": "NomeExecutavel" = (Nome do seu executável);
    - "PathExecutable": "PastaExecutavel" = (Pasta do seu executável);
    - "NameFileZip": "ArquivoPrinciapl.zip" = (Nome do seu arquivo compactado);
    - "Outdate": "NaoAtualizavel" = (Arquivo que queira manter no processo de atualização, caso não tenha, configure como  "" ).

3. Baixe ou clone o repositório deste projeto,
    #### Git Clone:
    ```bash
        git clone https://github.com/AmauryMagno/ZipAppAtualize.git
    ```
    #### Downlaod ZIP:
        http://amaurymagno/ZipAppAtualize/archive/refs/heads/main.zip

4. Após ter o repositório em sua máquina local, copie a pasta Atulizate, para o mesmo diretório da aplicação que será atualizada automaticamente.
    
5. Sua aplicação deve ter como primeira tarefa executar a aplicação de atualização presente no mesmo diretório, enviando tambem o Process ID (PID)
    #### Exemplo de código, em C# Wpf, que executa o aplicativo de atualização  enviando o PID gerado, aguardando o término da atualização para executar a aplicação principal:
    ```C#
        public partial class MainWindow : Window
        {
            public MainWindow()
                {
                    InitializeComponent();
                    Loaded += VerifyUpdate;
                }
                private void VerifyUpdate(object sender, EventArgs e)
                {
                    try
                    {
                        this.IsEnabled = false;

                        string currentDirectory = AppDomain.CurrentDomain.BaseDirectory;

                        atualizateProcess = new Process();
                        atualizateProcess.StartInfo.FileName = $"{currentDirectory}/Atualizate/net8.0-windows/Atualizate.exe";
                        atualizateProcess.StartInfo.WindowStyle = ProcessWindowStyle.Normal;
                        atualizateProcess.StartInfo.Arguments = Process.GetCurrentProcess().Id.ToString();
                        atualizateProcess.Start();

                        atualizateProcess.WaitForExit();
                        this.IsEnabled = true;
                    }
                    catch (Exception err)
                    {
                        System.Windows.MessageBox.Show($"Erro na localização do arquivo de atualização: {err.Message}", "Erro de Atualização", MessageBoxButton.OK, MessageBoxImage.Warning);
                        this.IsEnabled = true;
                        if (atualizateProcess != null && !atualizateProcess.HasExited)
                        {
                            atualizateProcess.Kill();
                            atualizateProcess.Dispose();
                        }
                    }

                }
        }

    ```

    #### Saiba mais:
    - PID Windows: https://learn.microsoft.com/pt-br/windows-hardware/drivers/debugger/finding-the-process-id 
    - PID Linux:
         - https://www.cyberciti.biz/faq/howto-display-process-pid-under-linux-unix/
         - https://guialinux.uniriotec.br/pid/
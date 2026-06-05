# Tela de Login

> [!NOTE]
> Este documento descreve o fluxo principal, a validação de dados e as interações do usuário na tela de autenticação do aplicativo.

### Requisitos da Tela

> [!TIP]
> **O sistema deve garantir que:**
> * O usuário possa inserir seu e-mail e senha para acessar a conta.
> * Mensagens de erro claras sejam exibidas em caso de falha na autenticação ou campos vazios.
> * Exista uma opção para recuperação de credenciais (ex: "Esqueci minha senha").
> * Exista um atalho para novos usuários criarem uma conta (ex: "Cadastre-se").

### Fluxo e Lógica da Interface

```javascript
função mostrarTelaLogin()
    mostrar "TELA DE LOGIN"
    
    // Campos de entrada de dados
    mostrar campo "E-mail"
    mostrar campo "Senha" (com caracteres ocultos)
    
    // Interações
    mostrar botão "Entrar"
    quando botão "Entrar" for clicado:
        emailInserido = ler campo "E-mail"
        senhaInserida = ler campo "Senha"
        
        // Validação
        se emailInserido estiver vazio ou senhaInserida estiver vazia então
            mostrar "Erro: Por favor, preencha todos os campos."
            parar execução
            
        se formatoDeEmail(emailInserido) for inválido então
            mostrar "Erro: Insira um e-mail com formato válido."
            parar execução
            
        // Requisição para o servidor/banco de dados
        resultado = autenticarUsuario(emailInserido, senhaInserida)
        
        se resultado.sucesso for verdadeiro então
            esconder tela de login
            mostrar tela principal (Listagem de Receitas)
        senão
            mostrar "Erro: E-mail ou senha incorretos."
    
    // Caso esqueça a senha
    mostrar botão/link "Esqueci minha senha"
    quando botão "Esqueci minha senha" for clicado:
        esconder tela de login
        mostrar "TELA DE RECUPERAÇÃO DE SENHA"
        
    mostrar botão/link "Ainda não tem conta? Cadastre-se"
    quando botão "Cadastre-se" for clicado:
        esconder tela de login
        mostrar "TELA DE CADASTRO DE USUÁRIO"
```
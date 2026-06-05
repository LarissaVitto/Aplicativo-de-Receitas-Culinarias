# Tela Inicial

> [!NOTE]
> Este documento descreve o fluxo principal, os componentes de navegação e a exibição de conteúdos em destaque na tela inicial (Home) do aplicativo.

### Requisitos da Tela

> [!TIP]
> **O sistema deve garantir que:**
> * O usuário visualize atalhos rápidos para as principais categorias de receitas.
> * Uma seção com receitas recomendadas ou em destaque seja apresentada.
> * O usuário tenha acesso a um menu de navegação principal (Início, Buscar, Favoritos, Perfil) para transitar entre as telas.

### Fluxo e Lógica da Interface

```javascript
// Função para abrir a tela
função mostrarTelaInicial()
    mostrar "TELA INICIAL"
    
    // Identificação do Usuário
    usuarioAtual = obterUsuarioLogado()
    mostrar "Olá, " + usuarioAtual.nome + "! O que vamos cozinhar hoje?"
    
    // Exibição de Categorias
    categorias = obterCategoriasPrincipais()
    mostrar "Categorias Rápidas"
    para cada categoria em categorias:
        mostrar botão com ícone e nome (ex: "Sobremesas", "Salgados", "Fit")
        quando botão da categoria for clicado:
            esconder tela inicial
            abrirTelaDeBuscaComFiltro(categoria.nome)
            
    // Exibição de Destaques ou Recomendações
    receitasDestaque = obterReceitasEmDestaque()
    mostrar "Receitas em Destaque"
    
    se receitasDestaque vazio então
        mostrar "Nenhuma recomendação no momento."
    senão
        para cada receita em receitasDestaque:
            mostrar card da receita (imagem, nome, tempo de preparo, avaliação)
            quando card da receita for clicado:
                abrirDetalhesDaReceita(receita)
                
    // Menu de Navegação Inferior
    mostrar barra de navegação com: "Início", "Buscar", "Favoritos", "Perfil"
    
    quando botão "Buscar" for clicado:
        esconder tela inicial
        mostrarTelaLista() // Redireciona para a tela de Busca de
        
    quando botão "Favoritos" for clicado:
        esconder tela inicial
        mostrar "TELA DE RECEITAS FAVORITAS"
        
    quando botão "Perfil" for clicado:
        esconder tela inicial
        mostrar "TELA DE PERFIL DO USUÁRIO"
```
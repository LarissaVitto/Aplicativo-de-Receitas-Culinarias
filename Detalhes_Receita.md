# Detalhes da Receita

> [!NOTE]
> Este documento descreve o fluxo, a exibição de dados e as interações do usuário na tela de detalhes de uma receita específica.

### Requisitos da Tela

> [!TIP]
> **O sistema deve garantir que:**
> * Os ingredientes de cada receita sejam exibidos.
> * O modo de preparo de cada receita seja exibido de forma clara.
> * O usuário possa **favoritar** receitas para acesso rápido.
> * O usuário possa **avaliar** as receitas (ex: sistema de notas ou estrelas).

### Fluxo e Lógica da Interface

```javascript
// Função para abrir a tela
função abrirDetalhesDaReceita(receitaSelecionada)
    esconder tela de lista
    mostrar "TELA DE DETALHES DA RECEITA"
    
    // Informações principais
    mostrar "Nome: " + receitaSelecionada.nome
    mostrar "Categoria: " + receitaSelecionada.categoria

    mostrar "Ingredientes:"
    para cada ingrediente em receitaSelecionada.ingredientes:
        mostrar "- " + ingrediente
        
    mostrar "Modo de Preparo: " + receitaSelecionada.modoPreparo
    
    // Interações do Usuário
    mostrar botão "Favoritar Receita" (ex: ícone de coração vazio/cheio)
    quando botão "Favoritar Receita" for clicado:
        alternarStatusFavorito(receitaSelecionada.id)
        atualizar ícone do coração
        
    mostrar controle "Avaliar Receita" (ex: 1 a 5 estrelas)
    quando usuário selecionar uma nota:
        salvarAvaliacao(receitaSelecionada.id, nota)
        mostrar "Obrigado por avaliar!"
    
    // Navegação
    mostrar botão "Voltar"
    quando botão "Voltar" for clicado:
        fechar tela de detalhes
        mostrar tela de lista
```
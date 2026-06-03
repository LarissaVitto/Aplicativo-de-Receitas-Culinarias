# Busca e Listagem das Receitas

> [!NOTE]
> Este documento descreve o fluxo principal, as funções e as regras de negócio para a tela de busca e listagem de receitas do aplicativo.

### Requisitos da Tela

> [!TIP]
> **O sistema deve garantir que:**
> * Os ingredientes de cada receita sejam exibidos.
> * O modo de preparo de cada receita seja exibido de forma clara.
> * O usuário possa **favoritar** receitas para acesso rápido.
> * O usuário possa **avaliar** as receitas (ex: sistema de notas ou estrelas).

### Estrutura de Dados
```javascript
//----- DADOS -----
Receita { id, nome, categoria, ingredientes, modoPreparo }

//----- FUNÇÕES -----
função obterReceitas()
    retorna lista de todas as receitas cadastradas

função filtrarPorCategoria(receitas, categoria)
    se categoria == "" ou categoria == "Todas" então
        retorna receitas
    senão
        retorna [r em receitas | r.categoria == categoria]

função buscarPorNome(receitas, termo)
    termoNormalizado = normalizar(termo).toLowerCase()
    retorna [r em receitas | normalizar(r.nome).toLowerCase() contém termoNormalizado]

função exibirLista(receitas)
    se receitas vazio então
        mostrar "Nenhuma receita encontrada"
    senão
        para cada r em receitas:
            mostrar r.id + " — " + r.nome + " (" + r.categoria + ")"
            mostrar botão "Abrir Receita" 
            quando botão "Abrir Receita" for clicado:
            abrirDetalhesDaReceita(r)

função abrirDetalhesDaReceita(receitaSelecionada)
    esconder tela de lista
    mostrar "TELA DE DETALHES DA RECEITA"


//----- FLUXO PRINCIPAL -----
função mostrarTelaLista()
    receitas = obterReceitas()
    categoriaSelecionada = ""  // quando está vazio representa todas
    termoBusca = ""

    enquanto usuário estiver na tela:
        mostrar controle de filtro por categoria (inclui "Todas")
        mostrar campo de busca por nome

        quando filtro ou termo mudar:
            filtradas = filtrarPorCategoria(receitas, categoriaSelecionada)
            resultado = buscarPorNome(filtradas, termoBusca)
            exibirLista(resultado)

        quando limpar filtros:
            exibirLista(receitas)

```
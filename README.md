# Controle de Fardamento — TPF Engenharia (Logística Recife)

Pacote de continuidade do projeto, preparado para ser aberto no **Claude Code**.

## Contexto

App de controle de estoque para 4 frentes de fardamento:

1. Escritório
2. RF (Eletricidade)
3. Campo
4. Chapéu Australiano

Decisão de arquitetura (já validada com o usuário): **SharePoint List (banco de dados) + Power Apps (tela de app)**,
hospedado no Teams/SharePoint da equipe "Geral | Administrativo". Motivo: roda 100% dentro do M365 da TPF, sem
consumir tokens de IA para operar, multiusuário em tempo real, e sem exigir registro de app no Azure AD/Entra ID
(alternativa que foi descartada porque dependia do time de TI).

## Estrutura deste pacote

```
fardamento-app/
├── README.md                          (este arquivo)
├── prototype/
│   └── prototipo_fardamento.html      protótipo estático (HTML/CSS/JS puro) já validado com o usuário
├── data/
│   ├── Itens_Fardamento.xlsx          catálogo consolidado de itens (49 combinações item/tamanho/frente)
│   └── Movimentacoes_Fardamento.xlsx  template da lista de movimentações (entradas/saídas)
└── docs/
    └── ESPECIFICACAO.md               modelo de dados + fórmulas Power Apps + regras de negócio
```

## Estado atual

- [x] Levantamento das 3 planilhas atuais do usuário (RF, Chapéu Australiano, Fardamento geral)
- [x] Protótipo visual (HTML/CSS) das 3 telas: Lançamento, Dashboard, Histórico — **aprovado pelo usuário**,
      com o ajuste de que a tela de **Entrada** mostra só Data/Frente/Item/Quantidade (só a administração
      lança entradas; os campos de colaborador/centro de custo são exclusivos da Saída)
- [x] Catálogo de itens consolidado das 4 frentes
- [ ] Criação das 2 Listas no SharePoint (Itens, Movimentacoes) a partir dos xlsx em `data/`
- [ ] Geração do Power App a partir da lista Movimentacoes ("Integrar > Power Apps > Criar um app")
- [ ] Customização das telas do Power Apps conforme `docs/ESPECIFICACAO.md`
- [ ] Publicação do app e fixação no canal "Geral | Administrativo" do Teams

## Próximos passos sugeridos

1. Importar `data/Itens_Fardamento.xlsx` e `data/Movimentacoes_Fardamento.xlsx` como Listas do SharePoint
   no site da equipe (Site Contents → New → List → From Excel).
2. Na lista `Movimentacoes`, usar o botão nativo **Integrate → Power Apps → Create an app** para gerar o
   app base automaticamente (3 telas: Browse/Detail/Edit).
3. Reconstruir as telas seguindo o layout do protótipo e as fórmulas em `docs/ESPECIFICACAO.md`.
4. Publicar o app e compartilhar o link no Teams.

Qualquer sessão do Claude Code que continuar este trabalho deve ler `docs/ESPECIFICACAO.md` antes de mexer
nas fórmulas do Power Apps — ele documenta os nomes de campos, tipos e regras de cálculo de estoque.

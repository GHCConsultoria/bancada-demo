# Bancada

Demonstração de sistema de gestão para indústria. Arquivo único, sem build, sem servidor, sem dependência externa — abre com duplo clique e roda offline no navegador.

Feito para apresentação comercial: o cliente mexe à vontade durante a reunião e o botão **Recarregar demo** devolve a base ao estado original.

## Módulos

| Módulo | O que resolve |
|---|---|
| **Painel** | KPIs, entradas × saídas valorizadas ao custo, compras por fornecedor, agenda de pagamentos e a lista "O que precisa de você" |
| **Estoque** | Saldo por material, estoque mínimo com semáforo, localização física e valorização ao custo |
| **Entradas e saídas** | Livro de movimentação: quem retirou, quanto, para qual OS e em que data |
| **Fornecedores** | Cadastro com histórico de compra, saldo em aberto e parcelas em atraso |
| **Notas fiscais** | Lançamento da NF de entrada com anexo de XML e DANFE, por competência |
| **Contas a pagar** | Parcelas com data de vencimento, semáforo de vencido / vence hoje / próximos 7 dias e baixa com comprovante |
| **Portal do contador** | Tela read-only por competência com a relação de notas, os comprovantes e a folha do mês |
| **Equipe e documentos** | Pasta por colaborador (contrato, identidade, ASO, ficha de EPI, holerite, cartão de ponto, comprovante) e o **Modo fiscalização** |

## A ideia central

Um lançamento de nota fiscal gera três coisas de uma vez:

1. a **entrada no estoque**,
2. o **título a pagar com as parcelas datadas**,
3. o **arquivo na pasta da contabilidade**.

É esse encadeamento que substitui a planilha e o envio de documento por WhatsApp.

## Como rodar

Duplo clique em `index.html`. Só isso.

Se estiver publicado via GitHub Pages, também funciona direto pela URL do repositório.

## Como está construído

Tudo em `index.html`: HTML, CSS e JavaScript no mesmo arquivo, sem framework e sem CDN. O JavaScript está dividido em seções numeradas por comentário:

| Seção | Conteúdo |
|---|---|
| `<style>` | Tokens de cor (tema claro e escuro), tipografia e componentes |
| 1–2 | Utilidades de moeda e data, e `semear()` — a base de demonstração |
| 3–4 | Estado em `localStorage` e as consultas derivadas (saldo, parcelas, conformidade) |
| 5 | Gráficos em SVG escritos à mão |
| 6–7 | Modais e navegação |
| 8–15 | Uma função `render*` por módulo |
| 16 | Inicialização, tema e recarregar demo |

Cada tela tem endereço próprio pelo hash da URL — `index.html#pagar`, `index.html#contabil`, `index.html#equipe` — então dá para mandar link direto de um módulo específico.

## Dados

Base fictícia, gerada no carregamento com datas relativas ao dia de hoje, para a demo nunca parecer desatualizada. Fica no `localStorage` do próprio navegador: nada sai da máquina de quem abre.

A empresa exibida no topo é **Metalúrgica Exemplo Ltda.** — troque pelo nome do cliente antes de apresentar, na linha `co-name` do `<header class="topbar">`.

## Limites desta demonstração

- Os arquivos anexados são **referenciados, não hospedados**. Clicar em um XML abre a ficha do arquivo com o aviso correspondente.
- O pacote mensal da contabilidade é listado na tela; a geração do `.zip` é do sistema entregue, não da demo.

# AGENTS.md — Santo Congelado · e-mails

Este repositório publica, no GitHub Pages, os HTMLs de e-mail marketing da Santo Congelado:
https://leonardoffaria.github.io/santocongelado-emails/

- **Disparo:** pelo Centro de Comando (MKT Tools › Santo Congelado › E-mail). O CC importa a peça pelo endereço publicado aqui; quem envia é o Módulo Works, pelo Amazon SES, com o remetente `marketing@news.santocongelado.com.br`.
- **Modelo visual:** Figma "Santo Congelado · Template de e-mail marketing" — https://www.figma.com/design/YnXepi7zBlIdhyfUp3XnvH. O Figma é a referência; o que sai é o HTML desta pasta. Mudou o Figma, a mudança precisa vir para o HTML.

## Estrutura

```
index.html                  lista das campanhas (não é e-mail)
assets/                     logo e ícones fixos (pix, cartão, entrega, cupom, título "Mais vendidos")
<peça>-<ddmm>/index.html    o e-mail
<peça>-<ddmm>/img/          banner e imagens só desta peça
scripts/check-email-opt-out.mjs
```

## Nova campanha

1. Copiar a pasta da peça mais parecida (ex.: `quarta-da-dieta-0411`) com o nome novo `<tema>-<ddmm>`.
2. No `index.html` da peça, trocar: `<title>` (igual ao assunto), pré-cabeçalho (o `div` escondido logo depois do `<body>`), texto, cupom, botão, nota legal e vitrine.
3. Banner: JPG 1200×600 em `img/`, **sempre com nome novo**. O Gmail guarda a imagem pelo endereço; nome repetido mostra a imagem antiga.
4. Imagens com endereço absoluto: `https://leonardoffaria.github.io/santocongelado-emails/<pasta>/img/<arquivo>`. Ícones e logo vêm de `assets/`.
5. Links com UTM: `?utm_source=email&utm_medium=crm&utm_campaign=<tema>-AAAA-MM-DD`.
6. Rodar `node scripts/check-email-opt-out.mjs` e só seguir com OK.
7. Acrescentar a peça no topo do `index.html` da raiz.
8. Commit e push na `main`. O Pages publica em cerca de 1 minuto.

## Regras de texto (valem para toda peça)

- Sempre **Santo Congelado** por extenso, nunca só "Santo".
- **Nunca "sem juros".** O parcelamento é "até 3x no cartão de crédito", e a nota diz: "À vista no cartão sem acréscimo; o acréscimo de 2x e 3x aparece no checkout antes de pagar."
- **Frete grátis acima de R$ 399 só nas regiões com frete de R$ 15 e R$ 19.** A nota diz: "Frete grátis para pedidos acima de R$ 399 em produtos, nas regiões com frete de R$ 15 e R$ 19; confira seu CEP no checkout."
- **Cupom:** o link com `?coupon=` não aplica o cupom. A peça sempre diz "Digite o cupom no checkout, antes de pagar." O cupom precisa existir na loja antes do envio; valor mínimo, validade e uso por cliente vão iguais na nota legal.
- **Vitrine:** 4 produtos entre os mais vendidos dos últimos 12 meses com 10 ou mais unidades em estoque. Nome, descrição curta, preço e link iguais aos da loja.
- Manter `{{first_name}}` na saudação e o link "Cancelar inscrição" com `href="{{unsubscribe_url}}"` no rodapé. O Works troca os dois no envio; na prévia do Pages eles aparecem literais. Sem o link de descadastro o CC recusa a peça.

## Estratégia por segmento (RFM)

| Segmentos | Peça | Oferta |
|---|---|---|
| Campeões, Fiéis, Novos | Facilidades | 3% OFF no Pix, até 3x, frete grátis acima de R$ 399. Sem cupom. |
| Precisam de atenção, Em risco, Não posso perder | Cupom do dia (ex.: Quarta da dieta) | 10% OFF acima de R$ 199, só no dia, até 23h59 |
| Perdidos | Volta10 | Cupom `VOLTA10`, 10% OFF acima de R$ 199. Em lotes pelo ano do último pedido: 2024–2025, depois 2022–2023, depois 2019–2021 |

## Disparo

1. **Base:** Works › Santo Congelado › CRM › Extrair base. Escolher os segmentos da peça e baixar o CSV. Exportar base pede motivo e permissão de dado sensível.
2. **Campanha:** CC › MKT Tools › Santo Congelado › E-mail › Nova campanha.
   - Mensagem: assunto, pré-cabeçalho (o mesmo texto que está na peça) e o endereço publicado da peça, `https://leonardoffaria.github.io/santocongelado-emails/<pasta>/`.
   - Público: subir o CSV e apontar as colunas de e-mail e de primeiro nome.
   - Envio: mandar o teste primeiro, conferir no celular e no computador, e só então agendar para a base.

O Works não manda para quem se descadastrou, reclamou de spam ou teve devolução permanente (endereço inexistente), mesmo que o contato esteja no CSV. Devolução temporária (caixa cheia, recusa do provedor) continua recebendo.

## Histórico

- `*-0111`: série RFM de 01/11/2026 (cupons `DOMINGOANOITE` e `VOLTA10`).
- `*-0411`: reenvio de 04/11/2026 (cupons `QUARTADADIETA` e `VOLTA10`, banners novos).

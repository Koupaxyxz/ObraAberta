# ObraAberta

Versao ajustada para funcionar em hospedagem estatica.

## Analise do problema

No arquivo original:

1. A chave da API estava exposta no frontend.
2. A URL da API e um proxy estavam declarados, mas esta versao do codigo usava apenas um banco `MOCK_DB`.
3. GitHub Pages nao e backend. Mesmo com chamada real, API autenticada no browser costuma falhar por CORS, preflight ou por expor segredo no cliente.

## O que mudou

1. O frontend agora carrega `data/convenios.json`.
2. Existe fallback local para a interface nao quebrar.
3. A busca, o detalhe, o risco e os textos de cobranca continuam funcionando.
4. Foi criado `index.html`, que e o arquivo ideal para GitHub Pages.
5. O `index.html` agora ficou autossuficiente, com CSS e JavaScript embutidos, para nao depender das pastas `assets/` no deploy.

## Publicacao

Suba estes arquivos para a raiz do repositorio e ative o GitHub Pages apontando para a branch principal e a pasta raiz.

## Dados reais

Para usar dados oficiais sem quebrar o site:

1. Busque os dados fora do navegador.
2. Gere ou atualize `data/convenios.json`.
3. Publique o JSON junto com o site.

Isso pode ser feito com GitHub Actions, backend proprio ou script local.

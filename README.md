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

### Opcao pronta no projeto

Foi adicionado:

- `scripts/build-convenios-dataset.ps1`: converte um CSV ou ZIP oficial para `data/convenios.json`
- `.github/workflows/update-convenios-data.yml`: atualiza a base automaticamente no GitHub

### Como usar com muitas cidades

1. Baixe a base oficial de convenios em CSV ou ZIP, ou use a URL oficial do arquivo.
2. Rode localmente:

   `pwsh ./scripts/build-convenios-dataset.ps1 -SourceFile "C:\\caminho\\convenios.zip"`

3. Ou configure no GitHub uma repository variable chamada `CONVENIOS_SOURCE_URL` e execute o workflow `Update convenios data`.

Por padrao, o script remove registros concluidos para manter a base mais leve e focada em obras que ainda exigem acompanhamento. Se quiser incluir tudo, use `-KeepConcluded`.

### Sobre "tempo real"

O projeto agora esta preparado para monitoramento continuo na home:

- destaque imediato dos casos mais absurdos
- tentativa de priorizacao regional pela localizacao do navegador
- atualizacao automatica do JSON pelo GitHub Actions

Mas ha um limite da propria fonte oficial: a base aberta de convenios do Portal da Transparencia e semanal. Entao o site pode verificar varias vezes ao dia e publicar rapidamente o que mudou, mas a velocidade final depende da atualizacao do governo.

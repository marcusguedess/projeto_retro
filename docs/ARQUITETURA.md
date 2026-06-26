# Arquitetura

O BookSignal Analytics separa preparação de dados e apresentação visual. A arquitetura foi escolhida para demonstrar análise após a ingestão, sem depender de coleta automática de sites externos.

```text
CSVs de amostra
  -> preparação em Python
  -> contrato JSON normalizado
  -> dashboard estático em Next.js
  -> GitHub Pages
```

## Camada Python

`analytics/export_booksignal.py` carrega as bases de amostra, aplica as funções de preparo em `datasets/booksignal/` e grava `web/src/data/booksignal.json`.

O export contém:

- origem dos dados e cobertura temporal das reviews;
- métricas gerais;
- livros ranqueados;
- agregações por gênero;
- distribuições de rating e confiança;
- amostras recentes de reviews;
- indicadores de qualidade da base.

## Camada Web

A interface fica em `web/` e usa Next.js App Router.

O dashboard é estático por escolha de arquitetura. Isso mantém a demo simples de hospedar e revisar no GitHub Pages, sem chaves de API ou serviços privados em runtime. A importação de CSV ocorre localmente no navegador.

## CI E Publicação

O workflow do GitHub Actions executa a mesma sequência esperada localmente:

1. Instala dependências Python.
2. Exporta o JSON analítico.
3. Roda testes Python.
4. Verifica sintaxe Python.
5. Instala dependências do frontend.
6. Roda ESLint.
7. Roda typecheck TypeScript.
8. Gera o site estático.
9. Publica `web/out`.

## Por Que Export Estático

GitHub Pages não executa backend nem é adequado para armazenar segredos. O export estático atende ao escopo público do projeto: demonstrar a análise de uma base já disponível. Banco de dados, ingestão sob demanda e conectores externos não fazem parte desta versão.

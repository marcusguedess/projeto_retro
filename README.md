# BookSignal Analytics

Dashboard de decisão editorial para explorar catálogos de livros depois da ingestão dos dados. O projeto combina metadados, preço, rating e sinais de qualidade para ajudar a priorizar títulos para promoção, revisão ou observação.

[Demo publicada](https://marcusguedess.github.io/booksignal-analytics/)

BookSignal Analytics foi criado como um case de produto de dados: a coleta e a autorização das fontes acontecem antes da análise. A demo usa dados de amostra e também aceita um CSV local, processado no próprio navegador.

O projeto tem duas camadas:

- um pipeline Python que limpa CSVs e exporta um contrato JSON;
- uma interface em Next.js que apresenta recomendações acionáveis, ranking explicável, benchmarks por categoria e importação local de CSV.

## O Que A Demo Faz

- Organiza livros em recomendações de promover, auditar ou observar.
- Permite buscar, filtrar e comparar o catálogo por categoria.
- Explica os componentes usados em cada recomendação.
- Importa CSV localmente, sem enviar arquivos para um servidor.

## Dados De Entrada

O projeto não coleta dados automaticamente de Amazon, Mercado Livre ou lojas editoriais. Essas fontes exigem API oficial, permissão de uso, exportações autorizadas ou contratos de dados. O foco da demo é a etapa de análise após a ingestão.

Colunas aceitas no CSV:

```csv
title,author,genre,price,rating,reviews,verifiedPct,qualityScore
Livro Exemplo,Autora Exemplo,Fiction,19.90,4.6,128,82,78
```

Também são aceitos alguns nomes em português, como `titulo`, `autor`, `genero`, `preco`, `nota` e `avaliacoes`.

## Decisões De Produto

- **CSV local:** mantém a demonstração simples de executar, sem credenciais, backend ou retenção de arquivos.
- **Recomendações explicáveis:** cada indicação mostra os sinais considerados, em vez de apresentar uma decisão como caixa-preta.
- **Scores heurísticos:** as pontuações servem para ordenar e orientar uma revisão humana; não medem desempenho de mercado nem detectam fraude.
- **Decisão antes da coleta:** o projeto prioriza leitura e priorização de um catálogo já disponível, não automação de coleta em sites de terceiros.

## Termos Usados

- **CSV:** arquivo de planilha em texto, compatível com Excel, Google Sheets e sistemas internos.
- **Score:** pontuação calculada para comparar itens dentro da mesma base.
- **Rating:** nota média dada por leitores, normalmente de 1 a 5 estrelas.
- **Review:** avaliação escrita por leitor.
- **Benchmark:** comparação com uma média de referência, como a média de uma categoria.

## Perguntas Que O Projeto Responde

- Quais livros são bons candidatos para promoção ou curadoria?
- Quais livros precisam de auditoria antes de entrar em campanha?
- Quais gêneros mostram melhor relação entre preço, rating e qualidade das reviews?
- O que a ferramenta consegue concluir quando só existe uma base exportada pelo usuário?

## Estrutura

```text
.
├── analytics/
│   └── export_booksignal.py        # Gera o JSON do dashboard
├── datasets/
│   ├── booksignal/                 # Funções Python de análise
│   ├── sample_books.csv
│   └── sample_reviews.csv
├── docs/
│   ├── ARQUITETURA.md
│   ├── METODOLOGIA.md
│   └── CHECKLIST_PUBLICACAO.md
├── scripts/
│   └── validate.ps1
├── tests/
│   ├── test_analysis.py
│   └── test_export_booksignal.py
└── web/
    ├── src/app/
    ├── src/components/dashboard.tsx
    └── src/data/booksignal.json
```

## Stack

- Python e Pandas para preparação dos dados.
- Next.js, React e TypeScript para a interface.
- Export estático para GitHub Pages.
- GitHub Actions para testes, lint, typecheck e publicação.

## Status

Em evolução como projeto de portfólio. A versão pública é uma demo estática com dados de amostra e importação local de CSV; ela não fornece dados em tempo real nem integrações com marketplaces.

## Como Rodar

Pré-requisitos: Python 3.13+ e Node.js 24+.

Instale as dependências Python:

```bash
pip install -r requirements.txt
```

Gere os dados do dashboard:

```bash
python analytics/export_booksignal.py
```

Rode a interface:

```bash
cd web
npm install
npm run dev
```

Abra `http://localhost:3000`.

## Validação

Testes Python:

```bash
python -m unittest discover -s tests -p "test_*.py"
```

Checks do frontend:

```bash
cd web
npm run lint
npm run typecheck
npm run build
```

Validação completa no Windows:

```powershell
.\scripts\validate.ps1
```

## GitHub Pages

O app Next.js está configurado para export estático. Para simular um build local com o caminho do repositório:

```powershell
.\scripts\validate.ps1 -BasePath "/NOME_DO_REPOSITORIO" -SiteUrl "https://USUARIO.github.io/NOME_DO_REPOSITORIO"
```

O artefato final é gerado em `web/out`.

O workflow `.github/workflows/pages.yml` executa exportação dos dados, testes Python, lint, typecheck e build estático antes de publicar no GitHub Pages.

## Observações Sobre Dados

O repositório inclui CSVs de amostra para demonstração. Bases brutas de terceiros não devem ser commitadas sem licença, permissão de uso e revisão de privacidade.

Marketplaces e livrarias online costumam ter termos de uso, limites técnicos e restrições de redistribuição. Por isso, o projeto não depende de scraping automático e trabalha com dados autorizados, dados públicos permitidos ou arquivos exportados pelo usuário.

O score de qualidade das reviews é uma heurística local. Ele destaca sinais que merecem revisão, como texto curto, review não verificada e rating extremo; não representa detecção de fraude.

## Documentação

- [Arquitetura](docs/ARQUITETURA.md)
- [Metodologia](docs/METODOLOGIA.md)
- [Checklist de publicação](docs/CHECKLIST_PUBLICACAO.md)

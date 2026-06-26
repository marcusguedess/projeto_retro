# Dados De Amostra

Os CSVs brutos usados no desenvolvimento podem ficar nesta pasta, mas não devem ser publicados no GitHub por padrão.

O repositório inclui `sample_books.csv` e `sample_reviews.csv`, com conteúdo sintético e anonimizado, para que a demo possa ser executada sem acessar bases de terceiros.

Arquivos esperados pelo app:

- `Top-100 Trending Books.csv`
- `customer reviews.csv`

Motivo: uma base de reviews pode conter nomes de revisores, textos com informações pessoais e conteúdo sujeito aos termos de uso da fonte original. Para publicar o projeto, mantenha os CSVs fora do repositório ou substitua-os por uma amostra anonimizada.

## Colunas esperadas

`Top-100 Trending Books.csv`:

```text
Rank,book title,book price,rating,author,year of publication,genre,url
```

`customer reviews.csv`:

```text
Sno,book name,review title,reviewer,reviewer rating,review description,is_verified,date,timestamp,ASIN
```

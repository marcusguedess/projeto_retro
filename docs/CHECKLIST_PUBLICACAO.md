# Checklist De Publicação

Rode antes de publicar uma nova versão:

```powershell
.\scripts\validate.ps1 -BasePath "/booksignal-analytics" -SiteUrl "https://marcusguedess.github.io/booksignal-analytics"
```

Verificações manuais:

- O link da demo no README aponta para o nome atual do repositório.
- `web/out/index.html` e `web/out/.nojekyll` existem após o build.
- Não há CSV privado, chave de API, log local ou cache no repositório.
- GitHub Pages está configurado para usar GitHub Actions.
- A demonstração pública usa dados de amostra ou dados com permissão de publicação.

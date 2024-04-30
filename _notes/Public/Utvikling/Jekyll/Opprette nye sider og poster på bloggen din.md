---
title: Opprette nye sider og poster på bloggen din
feed: show
date: 29-04-2024
---
Du kan opprette to typer innhold på bloggen din: **sider** (pages) og **poster** (posts). Sider dukker opp i navigasjonsmenyen øverst til høyre (*About* er et eksempel på en side), og poster dukker opp i main-panelet midt på siden, under overskriften *Posts* (*Welcome to Jekyll* er et eksempel på en post).
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/jekyll-blog-template.png?raw=true)
## Opprette en ny side
Se på filutforskeren i VS code. Her finner du noen filer, og en eller tre mapper. Det ser omtrent slik ut:
![](https://github.com/Cha-IM/cha-im.github.io/blob/main/assets/img/jekyll/jekyll-file-structure.png?raw=true)
```bash
minblogg
├── _posts
│   ├── 2024-04-29-welcome-to-jekyll.markdown
├── _site
├── .jekyll-cache
├── _config.yml
├── .gitignore
├── 404.html
├── about.markdown
├── Gemfile
├── Gemfile.lock
└── index.markdown
```
Som du kan se, ligger *index.markdown* og *about.markdown* på rotnivå (nivået rett under `/minblogg/`). Disse filene er sider, altså de som vises i navigasjonsmenyen. For å opprette en ny side, kan du opprette en ny fil på dette nivået, med filtypen *.md* (dette er det samme som *.markdown*).

Som et eksempel kan vi opprette siden *kontakt.md*. Åpne filen.

Øverst i filen må vi legge inn *frontmatter*
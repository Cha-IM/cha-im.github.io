---
title: Tilpasse din Jekyll-webside
feed: show
date: 24-04-2024
---
Nå er det på tide å tilpasse din Jekyll-webside og gi den en profil som er tilpasset det du vil bruke den til.

## config.yml
Først skal vi endre `_config.yml`-filen. Denne inneholder bakgrunnsinformasjon for bloggen din. Du finner `_config.yml` i Explorer-vinduet i VS-code sammen med de ander filene som hører til bloggen.

Når du åpner fila, ser den omtrent sånn ut:
```yml
# Welcome to Jekyll!
#
# This config file is meant for settings that affect your whole blog, values
# which you are expected to set up once and rarely edit after that. If you find
# yourself editing this file very often, consider using Jekyll's data files
# feature for the data you need to update frequently.
#
# For technical reasons, this file is *NOT* reloaded automatically when you use
# 'bundle exec jekyll serve'. If you change this file, please restart the server process.
#
# If you need help with YAML syntax, here are some quick references for you:
# https://learn-the-web.algonquindesign.ca/topics/markdown-yaml-cheat-sheet/#yaml
# https://learnxinyminutes.com/docs/yaml/
#
# Site settings
# These are used to personalize your new site. If you look in the HTML files,
# you will see them accessed via {{ site.title }}, {{ site.email }}, and so on.
# You can create any custom variable you would like, and they will be accessible
# in the templates via {{ site.myvariable }}.

title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
Write an awesome description for your new site here. You can edit this line in _config.yml. It will appear in your document head meta (for Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: jekyllrb
github_username: jekyllrb

# Build settings
theme: minima

plugins:
- jekyll-feed

# Exclude from processing.
# The following items will not be processed, by default.
# Any item listed under the `exclude:` key here will be automatically added to
# the internal "default list".
#
# Excluded items can be processed by explicitly listing the directories or
# their entries' file path in the `include:` list.
#
# exclude:
# - .sass-cache/
# - .jekyll-cache/
# - gemfiles/
# - Gemfile
# - Gemfile.lock
# - node_modules/
# - vendor/bundle/
# - vendor/cache/
# - vendor/gems/
# - vendor/ruby/
```

Linjene som starter med `#` er kommentarer ment for å hjelpe deg å forstå koden. Ellers er koden ganske enkel; hver linje består av en nøkkel og en verdi, med kolon (`:`) imellom. Det du trenger å gjøre er å endre verdiene til å passe din blogg. 

| Nøkkel              | Verdi                                                                                                                                                                             |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title: `           | Skriv navnet eller tittelen på bloggen din                                                                                                                                        |
| `email:`            | Denne linja kan du kommentere ut (sette `#` foran linja) hvis du. ikke vil at eposten din skal vises på bloggen, eller du kan skrive inn epostadressen din.                       |
| `description:`      | Her skriver du en kort beskrivelse av hva bloggen din handler om. Dette vises i footeren på nettsiden, og i tittelen øverst på fanen i nettleseren, sammen med navnet på bloggen. |
| `baseurl:`          | Her trenger du ikke skrive noe. Denne brukes hvis du skal legge bloggen din ut på nett på ditt eget domene                                                                        |
| `url:`              | Her trenger du ikke skrive noe. Denne brukes hvis du skal legge bloggen din ut på nett på ditt eget domene                                                                        |
| `twitter_username:` | Her kan du legge inn brukernavnet ditt på Twitter. Hvis du ikke har Twitter, eller ikke ønsker å legge det inn, kommenterer du ut denne linjen.                                   |
| `github_username:`  | Her kan du legge inn brukernavnet ditt på Github. Hvis du ikke ønsker å legge det inn, kommenterer du ut denne linjen.                                                            |
| `theme:`            | Det er mulig å legge inn et annet tema (annen css) på nettsiden. Dette er ganske kompisert, så bare la denne linja være                                                           |
| `plugins:`          | Det er mulig å installere tilleggsfunksjoner til bloggen din. Dette skal vi heller ikke gjøre nå, så bare la denne være.                                                          |


 

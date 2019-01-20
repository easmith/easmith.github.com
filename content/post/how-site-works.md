---
title: "Как работает этот сайт"
date: 2018-12-12
lastmod: 2018-12-12T23:12:22+03:00
draft: false
tags: ["git", "github"]
categories: ["how-to"]

# you can close something for this content if you open it in config.toml.
comment: false
toc: false
# reward: false
mathjax: false
copyright: false

# you can define another contentCopyright. e.g. contentCopyright: "This is an another copyright."
# contentCopyright: false
---

Однажды, решив вести свои замети в сети, я определялся с выбором инструмента для генерации HTML из Markdown файлов. Собственно, выбор сузился до двух из них: Jekyll и Hugo.
Jekyll популярнее и в гитхабе для него есть даже функционал по выбору шаблонов. Однако, мне не хотелось поднимать окружение Ruby. Hugo проще и для его работы не нужно ничего лишнего, поэтому и выбор пал на него.

- Итак, для начала создаем репозиторий со своим логином: easmith.github.io
- Создаем в ветку hugo
- Заливаем туда исходники сайта
- Обновляем подмодули с темами

    git submodule update --init --recursive

- Генерируем  HTML

    hugo

- Пушим каталог public в ветку мастер
    
    git subtree push --prefix public/ origin master

- Пушим все остальное на гитаб и радуемся результату =)

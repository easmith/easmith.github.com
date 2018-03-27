---
title: "PoW + Random Access Memory"
date: 2017-08-29
draft: false
tags: ["POW", "crypto", "blockchain"]
categories: ["blog"]

# you can close something for this content if you open it in config.toml.
comment: false
toc: false
# reward: false
mathjax: false
copyright: false

# you can define another contentCopyright. e.g. contentCopyright: "This is an another copyright."
# contentCopyright: false
---

Как усложнить процесс майнинга на специальных устройствах - использовать PoW + Random Access Memory.
Другими словами, в алгоритм хэширования включить еще и доказательство случайного чтения из памяти.
Сейчас в Ethereum использует для этого отдельный DAG файл.

Моя же идея заключается в вычислении хэша следующим образом:

Берем заголовок (header), и случайное число (nonce)
Вычиляем цепочку хэшей:

```
header + (nonce + 0)
header + (nonce + 1)
header + (nonce + 2)
...
header + (nonce + n)
```

n - настраиваемый парамет. Далее вычилсяем дерево Меркля и получаем хэш верхушки mainHash.
предположим получился хэш:
    58833651db311ba4bc11cb26b1900b4f
смотрим на последний байт: 0x4f = 79

Теперь берем хэш:
hash(header + (nonce + 79)) и ксорим его с верхушкой И получаем: 002a32ea72d6bcba621e0e36be46cba0

А теперь проверяем его на соответствие сложности и если все ок, то включаем в блок:
mainHash, nonce, n, merklePath

Если мы будем использовать 256 * 256 * 256 итераций вычисления хэша по 32 байта, то это потребует гигабайт памяти для хранения вычесленных хэшей. Конечно алгоритм майнинга можно оптимизировать и использовать меньшие объемы памяти, но так или иначе, потребность в опиративнй памяти потребуется.

А вот проверка хэша займет всего 24 итерации (log(n)), как в принципе и работает цепочка merkle.


Можно еще усложнить, и искать максимально совпадающий с верхушкой хэш...

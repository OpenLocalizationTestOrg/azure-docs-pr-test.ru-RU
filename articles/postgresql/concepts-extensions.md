---
title: "расширения PostgreSQL aaaUsing в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Описывает функции hello tooextend hello возможности базы данных с помощью расширений в базе данных Azure для PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/29/2017
ms.openlocfilehash: af2462d7a923b934bc0329153be7079ba86e8856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="postgresql-extensions-in-azure-database-for-postgresql"></a>Расширения PostgreSQL в базе данных Azure для PostgreSQL
PostgreSQL функциональная hello возможность tooextend hello базы данных с помощью расширений. Расширения позволяют нескольким toobe связанные объекты SQL, объединяются в одном пакете и может быть загружен или удалены из базы данных с помощью одной команды. После загрузки в базе данных hello расширения может работать так же, как компоненты, которые встроены в. Дополнительные сведения о расширениях PostgreSQL см. на странице [Packaging Related Objects into an Extension](https://www.postgresql.org/docs/9.6/static/extend-extensions.html) (Упаковка связанных объектов в расширение).

## <a name="how-toouse-postgresql-extensions"></a>Как toouse PostgreSQL расширения?
Расширения, PostgreSQL, должны установить для базы данных, прежде чем их можно использовать toobe. Запустите tooinstall определенное расширение [создание расширения](https://www.postgresql.org/docs/9.6/static/sql-createextension.html) команда из tooload средство psql hello упакованных объектов в базу данных.

База данных Azure для PostgreSQL поддерживает подмножество основных расширений, которые перечислены здесь. Помимо hello указанных выше не поддерживаются другие расширения. С помощью службы базы данных Azure для PostgreSQL невозможно создать свое собственное расширение.

## <a name="extensions-supported-by-azure-database-for-postgresql"></a>Расширения, поддерживаемые базой данных Azure для PostgreSQL
Hello следующие таблицы hello Стандартная PostgreSQL расширений списка, в настоящее время поддерживаются базы данных Azure для PostgreSQL. Эти сведения также можно получить, выполнив запрос pg\_available\_extensions. 

### <a name="data-types-extensions"></a>Расширения типов данных

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [citext](https://www.postgresql.org/docs/9.6/static/citext.html) | Предоставляет тип строки символов без учета регистра. |
| [hstore](https://www.postgresql.org/docs/9.6/static/hstore.html) | Предоставляет тип данных для хранения наборов пар "ключ-значение". |

### <a name="functions-extensions"></a>Расширения функций

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [fuzzystrmatch](https://www.postgresql.org/docs/9.6/static/fuzzystrmatch.html) | Предоставляет несколько функций toodetermine сходства и расстояния между строками. |
| [intarray](https://www.postgresql.org/docs/9.6/static/intarray.html) | Предоставляет функции и операторы для управления массивами целых чисел, не содержащими значений null. |
| [pgcrypto](https://www.postgresql.org/docs/9.6/static/pgcrypto.html) | Предоставляет функции шифрования. |
| [pg\_partman](https://pgxn.org/dist/pg_partman/doc/pg_partman.html) | Управляет секционированными таблицами по времени или идентификатору. |
| [pg\_trgm](https://www.postgresql.org/docs/9.6/static/pgtrgm.html) | Предоставляет функции и операторы для определения подобия hello буквенно-цифровые текста на основе сопоставления trigram |
| [uuid-ossp](https://www.postgresql.org/docs/9.6/static/uuid-ossp.html) | Создает идентификаторы UUID. |

### <a name="full-text-search-extensions"></a>Расширения для полнотекстового поиска

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [unaccent](https://www.postgresql.org/docs/9.6/static/unaccent.html) | Словарь для текстового поиска, который удаляет из лексем знаки ударения (диакритические знаки). |

### <a name="index-types-extensions"></a>Расширения типов индекса

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [btree\_gin](https://www.postgresql.org/docs/9.6/static/btree-gin.html) | Предоставляет примеры классов оператора GIN, которые реализуют поведение сбалансированного дерева для определенных типов данных. |
| [btree\_gist](https://www.postgresql.org/docs/9.6/static/btree-gist.html) | Предоставляет классы оператора индекса GiST, которые реализуют сбалансированное дерево. |

### <a name="language-extensions"></a>Расширения языка

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [plpgsql](https://www.postgresql.org/docs/9.6/static/plpgsql.html) | Загружаемый процедурный язык PL/pgSQL. |

### <a name="miscellaneous-extensions"></a>Прочие расширения

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [pg\_buffercache](https://www.postgresql.org/docs/9.6/static/pgbuffercache.html) | Предоставляет средства для анализа, выполняемых в буферном кэше hello совместно в режиме реального времени. |
| [pg\_prewarm](https://www.postgresql.org/docs/9.6/static/pgprewarm.html) | Предоставляет способ tooload отношения данных в кэш буфера hello. |
| [pg\_stat\_statements](https://www.postgresql.org/docs/9.6/static/pgstatstatements.html) | Предоставляет средства для отслеживания статистики выполнения всех инструкций SQL, выполняемых сервером. |
| [postgres\_fdw](https://www.postgresql.org/docs/9.6/static/postgres-fdw.html) | Внешние данные оболочки используется tooaccess данные, хранящиеся на внешних серверах PostgreSQL |

### <a name="postgis"></a>PostGIS

> [!div class="mx-tableFixed"]
| **Расширение** | **Описание** |
|---|---|
| [PostGIS](http://www.postgis.net/), postgis\_topology, postgis\_tiger\_geocoder, postgis\_sfcgal | Пространственные и географические объекты для PostgreSQL. |
| address\_standardizer, address\_standardizer\_data\_us | Используется tooparse адреса в составные элементы. Использовать адрес нормализации toosupport геокодирования шаг. |
| [pgrouting](http://pgrouting.org/) | Расширяет hello PostGIS / функции маршрутизации геопространственных tooprovide, база данных PostgreSQL геопространственных. |

## <a name="next-steps"></a>Дальнейшие действия
Отсутствует расширение хотелось бы toouse? Сообщите нам об этом. Вы можете проголосовать за существующие запросы или оставить свои отзывы и предложения на нашем [форуме отзывов клиентов](https://feedback.azure.com/forums/597976-azure-database-for-postgresql).

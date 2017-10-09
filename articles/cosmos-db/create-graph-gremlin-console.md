---
title: "Руководство по Azure Cosmos DB. Создание, запрос и просмотр в консоли Apache TinkerPops Gremlin | Документация Майкрософт"
description: "Быстрый запуск Azure Cosmos DB toocreates вершин, границ и запросы, использующие hello Azure Cosmos DB Graph API."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a>Azure Cosmos DB: Создавать запросы и просматривать диаграммы, в консоли Gremlin hello

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB, базы данных и graph (контейнер) с помощью hello портала управления Azure, а затем используйте hello [консоли Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) из [Apache TinkerPop](http://tinkerpop.apache.org) toowork с Диаграмма данным API (Предварительная версия). В этом учебнике Создание и запрос вершин и края, обновление свойства вершин вершины запроса, проходят через hello graph и drop вершина.

![Azure DB Cosmos из консоли Apache Gremlin hello](./media/create-graph-gremlin-console/gremlin-console.png)

консоль Gremlin Hello — на основе Groovy/Java и выполняется в Linux, Mac и Windows. Его можно загрузить из hello [Apache TinkerPop сайта](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).

## <a name="prerequisites"></a>Предварительные требования

Для краткого руководства потребуется toohave подписки Azure toocreate учетную запись Azure Cosmos DB.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

Необходимо также tooinstall hello [Gremlin консоли](http://tinkerpop.apache.org/). Используйте версию 3.2.5 или более позднюю.

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Добавление графа

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a>Подключение tooyour службы приложений
1. Перед началом hello Gremlin консоли, создать или изменить файл конфигурации удаленного secure.yaml hello в каталоге apache-tinkerpop-gremlin-console-3.2.5/conf hello.
2. Укажите *узел*, *порт*, *пользователя*, *пароль*, *пул подключений* и *сериализатор*:

    Настройка|Рекомендуемое значение|Описание
    ---|---|---
    Узлы|[***.graphs.azure.com]|Просмотрите указанный ниже снимок экрана. Это значение hello Gremlin URI на странице общих сведений hello hello в квадратных скобках с конечными hello портале Azure: 443 / удален.<br><br>Это значение также можно получить из вкладки ключи hello, используя значение URI hello, удаляя https://, документы toographs изменение и удаление в конце hello: 443 /.
    порт|443|Задать too443.
    Имя пользователя|*Имя пользователя*|Здравствуйте ресурсов hello формы `/dbs/<db>/colls/<coll>` где `<db>` — это имя базы данных и `<coll>` — это имя коллекции.
    пароль|*Значение первичного ключа*| Просмотрите второй снимок экрана ниже. Это первичного ключа, которое можно получить со страницы приветствия ключи hello портал Azure, в поле hello первичный ключ. Используйте "Копировать" hello "hello левой части toocopy hello hello поле значение.
    Пул подключений|{enableSsl: true}|Параметр пула подключений для SSL.
    serializer|{ className: org.apache.tinkerpop.gremlin.<br>driver.ser.GraphSONMessageSerializerV1d0,<br> config: { serializeResultToString: true }}|Задайте значение toothis и удалять любые `\n` разрывы строки, при вставке в значение hello.

    Для значения узлов hello, скопируйте hello **Gremlin URI** значение из hello **Обзор** страницы: ![представление и скопируйте значение Gremlin URI hello на странице Обзор hello в hello портал Azure](./media/create-graph-gremlin-console/gremlin-uri.png)

    Значение пароля hello, скопируйте hello **первичного ключа** из hello **ключей** страницы: ![Просмотр и копирование первичного ключа в hello портал Azure, ключи страницы](./media/create-graph-gremlin-console/keys.png)


3. В окне терминала выполните `bin/gremlin.bat` или `bin/gremlin.sh` toostart hello [Gremlin консоли](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).
4. В окне терминала выполните `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour приложения службы.

    > [!TIP]
    > Если ошибка hello `No appenders could be found for logger` убедитесь, что значение сериализатора hello в файле secure.yaml удаленного hello обновлена как описано в шаге 2. 

Отлично! Теперь, когда мы hello Настройка завершена, давайте начнем, выполнение некоторых команд консоли.

Выполним простую команду count(). Введите ниже hello в консоль hello в строке приветствия:
```
:> g.V().count()
```

> [!TIP]
> Обратите внимание hello `:>` , предшествующий hello `g.V().count()` текста? 
>
> Это является частью команды hello, необходимые tootype. Очень важно при использовании консоли Gremlin hello Azure Cosmos DB.  
>
> Пропуск это `:>` префикс указывает, что команда hello tooexecute консоли hello локально, часто для графа в памяти.
> С помощью этого `:>` сообщает tooexecute консоли hello удаленной команды в этом случае для Cosmos DB (либо эмулятор localhost hello, или > экземпляра Azure).


## <a name="create-vertices-and-edges"></a>Создание вершин и границ

Начнем с добавления пяти вершин для пользователей *Thomas*, *Mary Kay*, *Robin*, *Ben* и *Jack*.

Входные данные (Thomas):

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

Выходные данные:

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
Входные данные (Mary Kay):

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

Выходные данные:

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

Входные данные (Robin):

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

Выходные данные:

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

Входные данные (Ben):

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

Выходные данные:

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

Входные данные (Jack):

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

Выходные данные:

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


Далее добавим границы для создания связей между пользователями.

Входные данные (Thomas -> Mary Kay):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

Выходные данные:

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Входные данные (Thomas -> Robin):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

Выходные данные:

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Входные данные (Robin -> Ben):

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

Выходные данные:

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a>Обновление вершины

Давайте обновить hello *Thomas* вершин с новой возраст *45*.

Входные данные:
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
Выходные данные:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a>Запрос графа

Теперь давайте отправим разные запросы к графу.

Во-первых давайте попробуем запроса фильтра tooreturn только тем, кто являются более старыми, чем 40 лет.

Входные данные (запрос с фильтрацией):

```
:> g.V().hasLabel('person').has('age', gt(40))
```

Выходные данные:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

Далее, давайте hello первого имя проекта для hello людей, которые являются более старыми, чем 40 лет.

Входные данные (запрос с фильтрацией и проекцией):

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

Выходные данные:

```
==>Thomas
```

## <a name="traverse-your-graph"></a>Просмотр графа

Давайте перекрестной hello graph tooreturn все его Thomas друзей.

Входные данные (друзья пользователя Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

Выходные данные: 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

Теперь давайте hello следующий уровень вершин. Просматривает все hello друзьях друзей Томас hello graph tooreturn.

Входные данные (знакомые пользователя Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
Выходные данные:

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a>Удаление вершины

Давайте теперь удалить узел из базы данных graph hello.

Входные данные (удаление вершины Jack):

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a>Очистка графа

Наконец давайте очистить базу данных hello всех вершин и границ.

Входные данные:

```
:> g.E().drop()
:> g.V().drop()
```

Поздравляем! Вы завершили работу с этим руководством по использованию API Graph в Azure Cosmos DB.

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:  

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB, создать граф, с помощью hello обозреватель данных, создать вершин и ребра и просматривать диаграммы с помощью консоли Gremlin hello. Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin. 

> [!div class="nextstepaction"]
> [Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)](tutorial-query-graph.md)

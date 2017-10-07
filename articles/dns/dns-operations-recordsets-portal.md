---
title: "aaaManage DNS записи наборов и записей с помощью Azure DNS | Документы Microsoft"
description: "Azure DNS предоставляет hello возможность toomanage DNS-запись устанавливает и регистрирует при размещении вашего домена."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>Управление DNS-записи и наборы записей с помощью портала Azure hello

> [!div class="op_single_selector"]
> * [Портал Azure](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

В этой статье показано, как наборы записей toomanage и записи для зоны DNS с помощью hello портал Azure.

Это важные toounderstand hello различие наборов записей DNS и отдельных записей DNS. Набор записей — это совокупность записей в зоне, содержащих hello совпадают имя и являются hello того же типа. Дополнительные сведения см. в разделе [наборы записей DNS для создания и записи с помощью hello портал Azure](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Создание нового набора записей и записи

toocreate в hello портал Azure, набор записей. в разделе [Здравствуйте, создать DNS-записей с помощью портала Azure](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Просмотр набора записей

1. В hello портал Azure, перейдите toohello **зоны DNS** колонку.
2. Поиск набора записей hello и выберите его. При этом откроется hello свойств набора записей.

    ![Поиск набора записей](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Добавление новых записей tooa набора записей

Можно добавить набор записей tooany записи too20. Набор записей не может содержать две одинаковые записи. Пустой наборов записей (с нуля записи) могут быть созданы, но не отображаются в hello Azure DNS-серверами. Наборы записей типа CNAME могут содержать не более одной записи.

1. На hello **запись свойства** колонку для зоны DNS, щелкните запись hello задайте выполняться tooadd запись.

    ![Выбор набора записей](./media/dns-operations-recordsets-portal/selectset500.png)

2. Укажите набор свойств hello запись, заполнив поля hello.

    ![Добавление записи](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры. Затем закройте колонку hello.
4. В углу hello вы увидите, что Сохранение записи hello.

    ![Сохранение набора записей](./media/dns-operations-recordsets-portal/saving150.png)

После сохранения записи hello hello значения на hello **зоны DNS** колонки будут отражать hello новой записи.

## <a name="update-a-record"></a>Изменение записи

При обновлении записи в существующий набор записей hello поля, которые можно обновить, зависят от типа hello записи вы работаете.

1. На hello **запись свойства** колонке набор записей, поиска записей hello.
2. Измените запись hello. При изменении записи, можно изменить доступные параметры записи hello hello. В следующем примере hello, hello **IP-адрес** выбрано поле и hello IP-адрес находится в процессе hello объекта изменяется.

    ![Изменение набора записей](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры. В верхнем правом углу hello вы увидите уведомление hello, сохранения записи hello.

    ![Сохраненный набор записей](./media/dns-operations-recordsets-portal/saved150.png)

После сохранения записи hello hello значения для записи hello установлены hello **зоны DNS** колонки будут отражать hello обновления записи.

## <a name="remove-a-record-from-a-record-set"></a>Удаление записи из набора записей

Можно использовать hello Azure портала tooremove записи из набора записей. Обратите внимание, что при удалении hello последней записи из набора записей набора записей hello не удаляется.

1. На hello **запись свойства** колонке набор записей, поиска записей hello.
2. Щелкните запись hello, что требуется tooremove. Затем щелкните **Удалить**.

    ![Удаление набора записей](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Нажмите кнопку **Сохранить** на hello верхней части колонки toosave hello параметры.
4. После удаления записи hello hello значения записи hello на hello **зоны DNS** колонки будут отражать удаления hello.

## <a name="delete"></a>Удаление набора записей

1. На hello **запись свойства** колонке набор записей, нажмите кнопку **удалить**.

    ![Удаление набора записей](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Появится сообщение, если требуется набор записей toodelete hello.
3. Убедитесь, что запись hello совпадения имен hello требуется toodelete и нажмите кнопку **Да**.
4. На hello **зоны DNS** колонки, убедитесь, что набор записей hello больше не отображается.

## <a name="work-with-ns-and-soa-records"></a>Работа с записями типа NS и SOA

Управление автоматически создаваемыми записями NS и SOA осуществляется иначе, чем другими типами записей.

### <a name="modify-soa-records"></a>Изменение записей типа SOA

Не удается добавить или удаления записей из hello автоматически создается на вершине зоны hello начальной записи (имя = «@»). Однако вы можете изменить любые параметры hello в рамках hello начальной записи зоны (кроме «узел») и записи hello задать значение срока ЖИЗНИ.

### <a name="modify-ns-records-at-hello-zone-apex"></a>Изменение записей NS в вершине зоны hello

запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS. Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.

Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS. Можно также изменить hello TTL и метаданные для этого набора записей. Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.

Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello. Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.

### <a name="delete-soa-or-ns-record-sets"></a>Удаление наборов записей типа SOA или NS

Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (имя = «@»), создаются автоматически при создании зоны hello. Они удаляются автоматически при удалении hello зоны.

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о Azure DNS см. в разделе hello [Обзор Azure DNS](dns-overview.md).
* Дополнительные сведения об автоматизации DNS см. в разделе [зон DNS, создание и использование наборов записей hello .NET SDK](dns-sdk.md).
* Дополнительные сведения о записях обратной зоны DNS см. в статье [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).

---
title: "aaaGet работы с Azure DNS, с помощью hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять первый DNS-зоны и записи с помощью портала Azure hello."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Приступая к работе с Azure DNS, с помощью портала Azure hello

> [!div class="op_single_selector"]
> * [Портал Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

В этой статье описывается toocreate действия hello вашей первой зоны DNS и запись с помощью портала Azure hello. Также можно выполнить следующие действия с помощью Azure PowerShell или hello кросс платформенных Azure CLI.

Зоны DNS-записей DNS используется toohost hello для определенного домена. toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена. Каждая запись DNS для вашего домена создается внутри этой зоны DNS. Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello. Каждое из этих действий описан в hello следующие шаги.

## <a name="create-a-dns-zone"></a>Создание зоны DNS

1. Войдите в toohello портал Azure
2. Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.

    ![Зона DNS](./media/dns-getstarted-portal/openzone650.png)

4. На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:


   | **Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|contoso.com|Имя зоны DNS hello Hello|
   |**Подписка**|[Ваша подписка]|Выберите зону DNS toocreate hello подписки в.|
   |**Группа ресурсов**|**Создать:** contosoDNSRG|Создайте группу ресурсов. Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной. Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.|
   |**Расположение**|Запад США||

> [!NOTE]
> Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS. расположение зоны DNS Hello всегда «глобальные» и не отображается.

## <a name="create-a-dns-record"></a>Создание записи DNS

Hello в примере описывается процесс создания новых «запись» hello. Для других типов записей и toomodify существующих записей в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md). 

1. С hello создания зоны DNS в hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**. Нажмите кнопку hello **contoso.com** зоны DNS в hello все колонки ресурсов. Если подписка hello, уже содержит несколько ресурсов, можно ввести **contoso.com** в hello **фильтрация по имени...** поле tooeasily доступ к DNS-зоны hello.

1. Вверху hello hello **зоны DNS** колонке выберите **+ запись набора** tooopen hello **добавить набор записей** колонку.

1. На hello **добавить набор записей** , введите следующие значения hello и, при необходимости щелкните **ОК**. В этом примере создается запись A.

   |**Параметр** | **Значение** | **Дополнительные сведения** |
   |---|---|---|
   |**Имя**|www|Имя записи hello|
   |**Тип**|A| Тип объекта toocreate записей DNS, допустимые значения: A, AAAA, CNAME, MX, NS, SRV, TXT и PTR.  Дополнительные сведения о типах записей см. в статье [Обзор зон и записей DNS](dns-zones-records.md).|
   |**Срок жизни**|1|Time-to-live hello запроса DNS.|
   |**Единица срока жизни**|Часы|Измерение времени для значения срока жизни.|
   |**IP-адрес**|ipAddressValue| Это значение является hello IP-адрес, который разрешает hello DNS-запись.|

## <a name="view-records"></a>Просмотр записей

В нижней части колонки зоны DNS hello hello вы увидите hello записей для DNS-зоны hello. Вы увидите hello записи по умолчанию DNS и SOA, которые создаются в каждой зоне, а также любые новые записи, который был создан.

![зона](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Обновление серверов доменных имен

Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами. Это позволяет другим пользователям на hello Internet toofind DNS-записей.

Hello серверы имен для зоны приведен hello портал Azure.

![зона](./media/dns-getstarted-portal/viewzonens500.png)

Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя). Регистратор предлагает tooset параметр hello hello серверов имя домена hello. Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы, которые созданы в этой статье завершения hello, следующие шаги:

1. В hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**. Нажмите кнопку hello **MyResourceGroup** группа ресурсов в hello все колонки ресурсов. Если подписка hello, уже содержит несколько ресурсов, можно ввести **MyResourceGroup** в hello **фильтрация по имени...** Группа ресурсов hello доступа tooeasily поле.
1. В hello **MyResourceGroup** колонка, щелкните hello **удалить** кнопки.
1. Hello портала требуется имя hello tootype tooconfirm группы ресурсов hello, что требуется toodelete его. Нажмите кнопку **удаление**, тип *MyResourceGroup* hello имя группы ресурсов, нажмите кнопку **удалить**. При удалении группы ресурсов будут удалены все ресурсы в группе ресурсов hello, поэтому всегда tooconfirm убедиться, что содержимое hello группу ресурсов перед его удалением. портал Hello удаляет все ресурсы, содержащиеся в группе ресурсов hello, а затем удаляет hello самой группе ресурсов. Этот процесс занимает несколько минут.


## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).

toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md).


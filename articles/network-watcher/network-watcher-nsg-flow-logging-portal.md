---
title: "журналы потока группы безопасности сети aaaManage с Наблюдатель сети Azure | Документы Microsoft"
description: "На этой странице объясняется, как toomanage группы безопасности сети поток входит в Наблюдатель сети Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Управление журналами потока группы безопасности сети в hello портал Azure

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Журналы потока группы безопасности сети являются возможностью Наблюдатель сети, благодаря которой вы tooview сведения о входящего и исходящего IP-трафика через группу безопасности сети. Эти журналы потоков сохраняются в формате JSON и содержат следующие важные сведения: 

- Входящие и исходящие потоки для каждого правила.
- применяет Hello сетевого Адаптера, hello потока.
- 5-фрагментному сведения о потоке hello (исходный и конечный IP-адрес, порт источника и назначения, протокол).
- Информация о том, разрешен или запрещен трафик.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать экземпляр Наблюдатель сети](network-watcher-create.md). сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной.

## <a name="register-insights-provider"></a>Регистрация поставщика Microsoft Insights

Для потока toowork ведения журнала успешно, hello **помощью Microsoft.Insights** должен быть зарегистрирован поставщик. Поставщик tooregister hello, hello выполните следующие шаги: 

1. Go слишком**подписки**и выберите hello подписки, для которого требуется журналы tooenable потока. 
2. На hello **подписки** колонке выберите **поставщиков ресурсов**. 
3. Просмотрите список поставщиков hello и убедитесь, что hello **помощью microsoft.insights** зарегистрирован поставщик. Если он не зарегистрирован, то выберите **Зарегистрировать**.

![Просмотр поставщиков][providers]

## <a name="enable-flow-logs"></a>Включение журналов потоков

Следующие действия помогут выполнить процесс hello включения потока журналы на группы безопасности сети.

### <a name="step-1"></a>Шаг 1

Перейти экземпляр tooa Наблюдатель сети, а затем выберите **NSG потока журналы**.

![Обзор журналов потоков][1]

### <a name="step-2"></a>Шаг 2

Выберите группу безопасности сети из списка hello.

![Обзор журналов потоков][2]

### <a name="step-3"></a>Шаг 3. 

На hello **параметры журналов потока** колонке задать состояние hello слишком**на**и затем настроить учетную запись хранилища.  Закончив, нажмите кнопку **OK**. Затем выберите **Сохранить**.

![Обзор журналов потоков][3]

## <a name="download-flow-logs"></a>Скачивание журналов потоков

Журналы потоков хранятся в учетной записи хранения. Загрузить журналы вашего потока tooview их.

### <a name="step-1"></a>Шаг 1

Выберите журналы потока toodownload, **вы можете загрузить журналы потока из заданного хранилища учетных записей**. Этот шаг принимает вид учетной записи хранилища tooa здесь можно выбрать, какие журналы toodownload.

![Параметры журналов потоков][4]

### <a name="step-2"></a>Шаг 2

Go toohello правильного хранения счета. Выберите **Контейнеры** > **insights-log-networksecuritygroupflowevent**.

![Параметры журналов потоков][5]

### <a name="step-3"></a>Шаг 3.

Перейдите в расположение toohello hello потока журнала, выберите его и выберите **загрузить**.

![Параметры журналов потоков][6]

Сведения о структуре журнала hello hello [Обзор журнала потока группы безопасности сети](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, каким образом слишком[визуализировать NSG потока журналов с PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png

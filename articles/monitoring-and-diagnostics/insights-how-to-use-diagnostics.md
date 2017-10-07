---
title: "aaaEnable наблюдения и диагностики в Microsoft Azure | Документы Microsoft"
description: "Узнайте, как tooset диагностики для ресурсов в Azure."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Включение мониторинга и диагностики
В hello [портала Azure](https://portal.azure.com), можно настроить сложных, часто, наблюдения и диагностики данных о ресурсах. Можно также использовать hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) или [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure диагностики программными средствами.

Данные диагностики, мониторинга и метрик в Azure сохраняются в выбранной учетной записи хранения. Это позволяет toouse любые средства tooread hello данные, из обозревателя хранилищ, средства сторонних toothird tooPower бизнес-Аналитики.

## <a name="when-you-create-a-resource"></a>При создании ресурса
Большинство служб позволяют tooenable диагностики при их создании в hello [портала Azure](https://portal.azure.com).

1. Go слишком**New** и выберите ресурс hello, которые вас интересуют.
2. Выберите **Дополнительная настройка**.
    ![Колонка "Диагностика"](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Выберите **Диагностика** и щелкните **Вкл**. Вам потребуется toochoose hello хранилища учетной записи, которую toobe диагностики сохранены. Вы оплата будет взиматься стандартная плата за хранилище и транзакции при отправке учетная запись хранения диагностики tooa.
4. Нажмите кнопку **ОК** и создайте ресурс hello.

## <a name="change-settings-for-an-existing-resource"></a>Изменение параметров существующего ресурса
Если вы уже создали ресурса и параметры диагностики toochange hello (toochange hello уровень сбора данных, например), можно сделать эти права в hello портала Azure.

1. Откройте toohello ресурсов и щелкните hello **параметры** команды.
2. Выберите **Диагностика**.
3. Hello **диагностики** колонке имеет все возможности диагностики hello и мониторинг сбора данных для этого ресурса. Для некоторых ресурсов можно также **хранения** политика данных hello, tooclean его из вашей учетной записи хранилища.
    ![Диагностика хранилища](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. После выбора параметров нажмите кнопку hello **Сохранить** команды. Может потребоваться несколько во время для мониторинга данных tooshow вверх при включении ее для hello первый раз.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Категории сбора данных для виртуальных машин
Для виртуальных машин все метрики и журналы будут записаны минутные интервалы, чтобы всегда иметь hello наиболее актуальные сведения о компьютере.

* **Основные метрики** : метрики работоспособности виртуальной машины, например относящиеся к процессору и памяти.
* **Метрики сети и веб-служб** : метрики, относящиеся к сетевым подключениям и веб-службам.
* **Метрики .NET** : метрики о приложения hello .NET и ASP.NET, работающие на виртуальной машине
* **Метрики SQL** : если вы используете службу Microsoft SQL, это показатели производительности службы.
* **Журналы событий приложений Windows** : события Windows, которые отправляются канала toohello приложения
* **Системные журналы событий Windows** : события Windows, отправляются toohello системного канала. Сюда также относятся события из [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Журналы событий безопасности Windows** : события Windows, отправляются toohello безопасный канал
* **Журналы инфраструктуры диагностики** : ведение журнала об инфраструктуре коллекции hello диагностики
* **Журналы IIS** : журналы сервера IIS.

Обратите внимание, что в настоящее время не поддерживаются некоторых дистрибутивов Linux, hello гостевой агент должен устанавливаться на виртуальной машине hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Получайте уведомления](insights-receive-alert-notifications.md) при возникновении операционных событий или превышении пороговых значений метрик.
* [Отслеживать показатели службы](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
* [Автоматически масштабировать числа экземпляров](insights-how-to-scale.md) toomake убедиться, что шкала службы по требованию.
* [Контролировать производительность приложений](../application-insights/app-insights-azure-web-apps.md) Если toounderstand точно как код работает в облаке hello.
* [Просмотр событий и журнал действий](insights-debugging-with-events.md) toolearn все, что произошло в службе.
* [Отслеживание работоспособности службы](insights-service-health.md) toofind out когда Azure произошла производительности снижение или службы прерываний.


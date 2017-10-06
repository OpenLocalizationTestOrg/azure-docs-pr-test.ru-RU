---
title: "aaaAzure Service Fabric контейнеры наблюдение и диагностику | Документы Microsoft"
description: "Узнайте, как toomonitor и диагностики контейнеры, осуществлять управление ими в Microsoft Azure Service Fabric с контейнерами решения в OMS."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Отслеживание контейнеров Windows Server с помощью OMS

## <a name="oms-containers-solution"></a>Решение OMS "Контейнеры"

команды Operations Management Suite (OMS) Hello опубликовала решения контейнеры для диагностики и мониторинга для контейнеров. Вместе с их решения Service Fabric это решение является развертывания контейнера toomonitor мощный инструмент, управляемых в структуре службы. Ниже приведен простой пример hello панель мониторинга в решении hello выглядит следующим образом:

![Основная панель мониторинга OMS](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Он также собирает различные журналы, которые могут быть запрошены в средстве анализа журналов OMS hello, и можно использовать toovisualize все метрики или событий. Ниже приведены типы Hello журнала собираются.

1. ContainerInventory — отображает информацию о местонахождении контейнера, имени и образах.
2. ContainerImageInventory — информация о развернутых образах, в том числе их идентификаторы или размеры.
3. ContainerLog — журналы конкретных ошибок, журналы Docker (StdOut и т. д.) и другие записи.
4. ContainerServiceLog — выполнявшиеся команды управляющей программы Docker.
5. Производительность: счетчики производительности, включая контейнера ЦП, памяти, то сетевой трафик дискового ввода-вывода и настраиваемых метрик из hello размещения машин

В этой статье рассматриваются hello tooset необходимые шаги вверх контейнера мониторинга для кластера. Дополнительные сведения о решение OMS контейнеры, toolearn извлечь их [документации](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Настройка кластера Service Fabric

Создание кластера с помощью шаблона Azure Resource Manager hello найден [здесь](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Убедитесь, что tooadd уникальное имя рабочей области OMS. Этот шаблон также по умолчанию toodeploying Service Fabric (v255.255), что означает, что он не может использоваться в производственной среде и не может быть обновлен другая версия Service Fabric tooa создания кластера в режиме предварительного просмотра hello. Если вы решите toouse этого шаблона для долгосрочного или производственного использования, измените номер стабильная версия tooa версии hello.

После настройки кластера hello убедитесь, что установлен соответствующий сертификат hello и проверьте правильность может tooconnect toohello кластера.

Убедитесь, что группы ресурсов настроен правильно, заголовок toohello [портал Azure](https://portal.azure.com/) и поиск hello развертывания. Группа ресурсов Hello должен содержать все ресурсы Service Fabric hello и также имеют решении аналитики журналов, а также решения Service Fabric.

Вот как изменить существующий кластер Service Fabric.
* Убедитесь, что включена Диагностика (если это не так, включите его через [обновление набора масштабирования виртуальных машин hello](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Добавление рабочей области OMS, создав решение «Аналитика структуры службы» через hello Azure Marketplace
* Редактировать источники данных hello hello Service Fabric решения toopick данные из hello соответствующие таблицы хранилища Azure (Настройка по WAD) в hello группы ресурсов, hello кластера находится в
* Добавление агента hello как [набора масштабирования виртуальных машин toohello расширения](/powershell/module/azurerm.compute/add-azurermvmssextension) через PowerShell или обновление набора масштабирования виртуальных машин hello (же ссылку, как описано выше, шаблона диспетчера ресурсов hello toomodify)

## <a name="2-deploy-a-container"></a>2. Развертывание контейнера

После готов кластера hello и подтверждения того, доступ к нему, разверните tooit контейнера. Если выбрана toouse hello предварительной версии как набор шаблоном hello, можно также изучить новые docker Service Fabric реализуют функциональность. Содержат помните, что hello первый раз образ контейнера развернутой tooa кластера, занимает несколько минут toodownload hello изображения в зависимости от его размера.

## <a name="3-add-hello-containers-solution"></a>3. Добавить решение контейнеры hello

В hello портал Azure, создайте ресурс контейнеров (под hello мониторинг + управления категории) через Azure Marketplace. 

![Добавление решения "Контейнеры"](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

На этапе создания hello запросов рабочей области OMS. Выберите hello, созданный с помощью развертывания hello выше. Этот шаг добавляет контейнеры решения в рабочей области OMS и обнаруживается автоматически агентом OMS hello, предоставляемым hello шаблона. Hello агент начнет сбор данных на процессы контейнеры hello в кластере hello и около 10 – 15 минут, вы увидите, решение hello подсветка с данными, как изображения hello hello мониторинга выше.

## <a name="4-next-steps"></a>4. Дальнейшие действия

OMS обеспечивает различные инструменты в рабочей области toomake hello Если более полезной для вас. Изучение hello следующие параметры toocustomize hello решения tooyour потребностей.
- Получить для начала ознакомьтесь с hello [входа поиска и выполнения запросов](../log-analytics/log-analytics-log-searches.md) компоненты входят в состав службы анализа журналов
- Настройка toopick агента OMS hello копирование определенными счетчиками производительности (go toohello рабочей области домашней > Параметры > данных > счетчиков производительности Windows)
- Настроить OMS tooset [автоматических предупреждения](../log-analytics/log-analytics-alerts.md) tooaid правила в обнаружение и диагностика

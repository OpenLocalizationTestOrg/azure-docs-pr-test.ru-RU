---
title: "toovertically автоматизации Azure aaaUse масштабирования виртуальных машин Windows | Документы Microsoft"
description: "По вертикали масштабирования виртуальной машины Windows в ответ toomonitoring предупреждения в службе автоматизации Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Вертикальное масштабирование виртуальных машин Windows с помощью службы автоматизации Azure

Вертикальное масштабирование — процесс hello увеличения или уменьшения hello ресурсы машины в рабочей нагрузке toohello ответа. В Azure это можно сделать, изменив размер hello hello виртуальной машины. Это может помочь в следующие сценарии hello

* Если hello виртуальной машины не используется часто, вы можете изменить ее работу меньший размер tooreduce tooa ежемесячные расходы
* Если hello виртуальной машины будет видеть пиковой нагрузки, он может быть большего размера tooincrease размер tooa его емкость

Структура Hello для hello действия tooaccomplish это как ниже

1. Настройка виртуальных машин tooaccess автоматизации Azure
2. Импортировать Runbook Azure Automation вертикального масштаба hello в подписке
3. Добавить модуль runbook tooyour веб-перехватчика
4. Добавление оповещений tooyour виртуальной машины

> [!NOTE]
> Из-за размера hello hello первую виртуальную машину, размеры hello может масштабироваться, может быть ограничен из-за toohello доступность hello другие размеры в кластере hello текущей виртуальной машины развертывается в. В hello опубликованные модули Runbook автоматизации, используемые в этой статье мы позаботимся обращения и масштабирование только в пределах hello ниже пары размер виртуальной Машины. Это означает, что Standard_D1v2 виртуальной машины не внезапно будет масштабировать в сторону tooStandard_G5 или уменьшен tooBasic_A0.
> 
> | Пары размеров виртуальных машин, для которых можно применять вертикальное масштабирование |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Настройка виртуальных машин tooaccess автоматизации Azure
Hello первое, что необходимо toodo — Создание учетной записи автоматизации Azure, где будет размещаться tooscale модулей Runbook используется hello виртуальной машины. Недавно службы автоматизации hello появилась возможность «Запуск от имени учетной записи» hello, что делает настройку hello участника-службы для автоматического запуска модулей Runbook hello от имени пользователя hello очень легко. Можно прочитать подробнее об этом в статье hello ниже:

* [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Импортировать Runbook Azure Automation вертикального масштаба hello в подписке
Hello модулей Runbook, которые необходимы для вертикальное масштабирование виртуальной машины уже опубликована в hello коллекции Runbook автоматизации Azure. Вам потребуется tooimport их в подписку. Вы узнаете, как модули Runbook tooimport, считывая hello следующую статью.

* [Runbook и коллекции модулей для службы автоматизации Azure](../../automation/automation-runbook-gallery.md)

Hello Runbook, которые требуется импортировать toobe показаны в приведенном ниже рисунке hello

![Импорт модулей Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Добавить модуль runbook tooyour веб-перехватчика
После импорта модулей Runbook hello необходимо tooadd runbook toohello веб-перехватчика, может быть вызвано предупреждение из виртуальной машины. Здесь могут считываться Hello подробные сведения о создании веб-перехватчика для модуля Runbook

* [Объекты Webhook в службе автоматизации Azure](../../automation/automation-webhooks.md)

Убедитесь, что копирование веб-перехватчика hello перед закрытием диалогового окна веб-перехватчика hello, как он потребуется в следующем разделе hello.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Добавление оповещений tooyour виртуальной машины
1. Перейдите в раздел параметров виртуальной машины.
2. Щелкните "Правила оповещения".
3. Щелкните "Добавить оповещение".
4. Выберите оповещение hello метрики toofire на
5. Выберите условие, что после выполнения будет вызвать предупреждения toofire hello
6. Установите пороговое значение для условия hello на шаге 5. toobe выполнен
7. Выберите в течение периода через какие hello наблюдение за службой проверяет условие hello и пороговое значение в шаги 5 и 6
8. Вставьте в веб-перехватчика hello, скопированные из предыдущего раздела hello.

![Добавление оповещений tooVirtual машины 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Добавление оповещений tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)


---
title: "Проверка оповещений в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе вы ознакомитесь с процедурой проверки оповещений безопасности в Центре безопасности Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Проверка оповещений в центре безопасности Azure
Этот документ содержит информацию о том, как убедиться, что ваша система правильно настроена для оповещений центра безопасности Azure.

## <a name="what-are-security-alerts"></a>Что такое оповещения системы безопасности?
Центр безопасности автоматически собирает, анализирует и объединяет данные журналов, поступающие от ресурсов Azure, сети и подключенных решений партнеров, таких как брандмауэры и решения для защиты конечных точек, для выявления и оповещения об угрозах. Дополнительные сведения об оповещениях безопасности и их типах см. в статье [Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) и [Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).

## <a name="alert-validation"></a>Проверка оповещений
После установки агента центра безопасности на свой компьютер выполните следующие шаги на компьютере, где находится атакованный ресурс оповещения:

1. Скопируйте исполняемый файл (например, calc.exe) на рабочий стол компьютера или в другой каталог.
2. Переименуйте этот файл на **ASC_AlertTest_662jfi039N.exe**.
3. Откройте командную строку и выполните этот файл с аргументом (фиктивное имя аргумента), таким как *ASC_AlertTest_662jfi039N.exe -foo*.
4. Подождите 5–10 минут и откройте оповещения центра безопасности. Там можно найти оповещение, аналогичное следующему:

    ![Проверка оповещений](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

При просмотре этого оповещения убедитесь, что в поле Arguments Auditing Enabled (Включен аудит аргументов) задано значение true. Если оно содержит значение false, необходимо включить аудит аргументов командной строки. Этот параметр можно включить с помощью командной строки:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>См. также
В этой статье представлен процесс проверки оповещений. Теперь, когда вы знакомы с проверкой, ознакомьтесь с такими статьями:

* [Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Узнайте, как управлять оповещениями и реагировать на угрозы безопасности в центре безопасности.
* [Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md). Узнайте, как отслеживать работоспособность ресурсов Azure.
* [Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Дополнительные сведения о различных типах оповещений безопасности.
* [Руководство по устранению неполадок в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Узнайте, как устранять типичные неполадки в центре безопасности. 
* [Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md). Часто задаваемые вопросы об использовании этой службы.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/). Записи блога, посвященные безопасности и соответствию требованиям в Azure.


---
title: "aaaAlerts проверки в центр безопасности Azure | Документы Microsoft"
description: "Этот документ поможет вам оповещений системы безопасности toovalidate hello в центр безопасности Azure."
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
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Проверка оповещений в центре безопасности Azure
Этот документ поможет узнать, как tooverify, если система настроена должным образом для оповещения центра безопасности Azure.

## <a name="what-are-security-alerts"></a>Что такое оповещения системы безопасности?
Центр обеспечения безопасности автоматически собирает анализирует и производить сбор данных журнала из ресурсов Azure, сети hello и решения подключенных партнеров, как решения для защиты брандмауэра и конечной точки, toodetect и оповещения toothreats вы. Чтение [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) Дополнительные сведения о оповещений системы безопасности и чтение [основные сведения об оповещениях безопасности в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn Дополнительные о hello различных типов оповещений.

## <a name="alert-validation"></a>Проверка оповещений
После установки агента центра обеспечения безопасности на компьютере, выполните действия hello ниже с компьютера hello место ресурсов hello атаке toobe hello предупреждения.

1. Скопируйте исполняемый файл (для примера calc.exe) toohello ПК или другим каталогом удобства.
2. Переименовать этот файл слишком**ASC_AlertTest_662jfi039N.exe**.
3. Откройте командную строку hello и выполнить этот файл с аргументом (просто имя фиктивное аргумент), например: *ASC_AlertTest_662jfi039N.exe - foo*
4. Подождите 5 минут too10 и откройте оповещения центра безопасности. Следует найти предупреждения toofollowing аналогично, один:

    ![Проверка оповещений](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

При просмотре этого предупреждения, убедитесь, что поле hello, аудит включен аргументы появляется как true. Если оно указано значение false, необходимые аргументы командной строки tooenable аудита. Можно включить этот параметр, с помощью следующей командной строкой hello:

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>См. также
В этой статье представлена процесс проверки toohello предупреждения. Теперь, когда вы знакомы с этой проверкой, попробуйте hello в следующих статьях:

* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Узнайте, как toomanage предупреждений и инцидентов toosecurity ответ в центр обеспечения безопасности.
* [Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md). Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Дополнительные сведения о различных типах hello оповещений системы безопасности.
* [Руководство по устранению неполадок в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Узнайте, как tootroubleshoot распространенные проблемы в центре безопасности. 
* [Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md). Найти часто задаваемые вопросы об использовании службы hello.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/). Записи блога, посвященные безопасности и соответствию требованиям в Azure.


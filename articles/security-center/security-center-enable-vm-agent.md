---
title: "aaaEnable агент виртуальной Машины в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить ВМ агента **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Включение агента виртуальной машины в центре безопасности Azure
Hello ВМ должен быть установлен агент на виртуальных машинах (ВМ) в порядке слишком[включить сбор данных](security-center-enable-data-collection.md).  Центр безопасности Azure позволяет вам toosee которого требуются виртуальные машины hello агент виртуальной Машины и рекомендует включить hello агент виртуальной Машины на этих виртуальных машин.

Hello агент виртуальной Машины устанавливается по умолчанию для виртуальных машин, развернутых из hello Azure Marketplace. статья Hello [агент ВМ и расширения – часть 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) рассматривается как tooinstall hello агент виртуальной Машины.

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания. Он не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **колонке рекомендации**выберите **включить агент виртуальной Машины**.
   ![Включение агента виртуальной машины][1]
2. Это открывает колонку hello **виртуальной Машины отсутствует или не отвечает агент**. Эта колонка перечислены hello виртуальных машин, требующих hello агент виртуальной Машины. Следуйте инструкциям hello на агент виртуальной Машины hello tooinstall колонке hello.
   ![Агент виртуальной машины отсутствует][2]

## <a name="see-also"></a>См. также
toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.
* [Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png

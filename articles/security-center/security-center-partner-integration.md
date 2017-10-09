---
title: "Интеграция aaaPartner в центр безопасности Azure | Документы Microsoft"
description: "Дополнительные сведения о как центр безопасности Azure интегрируется с партнерами tooenhance общую безопасность ресурсов Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Интеграция партнеров в центре безопасности Azure

В этой статье описывается как центр безопасности Azure интегрируется с партнерами toohelp повысить общий уровень безопасности. Центр обеспечения безопасности представляет собой интегрированную в Azure и использует преимущества hello Azure Marketplace для партнера, сертификации и выставление счетов.

> [!NOTE] 
> Начиная с июня 2017 г. центр обеспечения безопасности использует Microsoft Monitoring Agent hello toocollect и хранилища данных. Дополнительные сведения см. в статье [Миграция платформы центра безопасности Azure](security-center-platform-migration.md). Hello сведения в этой статье представляет функциональность центра обеспечения безопасности после перехода toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Зачем нужно развертывать партнерские решения через центр безопасности

Ниже приведены четыре основных причин tooleverage партнера интеграции в центре безопасности.

- **Простота развертывания.** Развертывание решения партнеров с hello следующие рекомендации центра обеспечения безопасности гораздо проще. процесс развертывания Hello можно полностью автоматизировать с помощью топология установки и сети по умолчанию. Пользователи также могут использовать вариант частичной автоматизации, который дает дополнительную гибкость и предоставляет расширенные настройки.
- **Интегрированные обнаружения.** События безопасности автоматически собираются из партнерских решений, объединяются и отображаются в списках оповещений и инцидентов центра безопасности. Эти события также являются совмещенного с обнаружениями из других источников, tooprovide улучшенные возможности обнаружения угроз.
- **Единый мониторинг работоспособности и единое управление.** Клиенты могут использовать все решения партнеров toomonitor события интеграции работоспособности с первого взгляда. Базовое управление доступна с установки tooadvanced простой доступ с помощью решения партнеров hello.
- **Экспорт tooSIEM**. Заказчики могут экспортировать все центра обеспечения безопасности и партнера предупреждает общий формат событий (CEF) tooon локальные сведения о безопасности и управления событий (SIEM) системы с помощью интеграции журналов Azure (Предварительная версия).


## <a name="partners-that-integrate-with-security-center"></a>Партнеры, которые интегрируются с центром безопасности

Сейчас центр безопасности поддерживает интеграцию со следующими решениями.

- Endpoint Protection ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec и [антивредоносное ПО Майкрософт для облачных служб и службы "Виртуальные машины" Azure](https://docs.microsoft.com/azure/security/azure-security-antimalware)). 
- Брандмауэр веб-приложения ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets) и [шлюз приложений Azure](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)). 
- Брандмауэр следующего поколения ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) и [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)). 
- Оценка уязвимостей ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/)).  

Со временем центра обеспечения безопасности будет расширить hello количество участников в эти категории, а также добавить новые категории. 

## <a name="deploy-a-partner-solution"></a>Развертывание решения партнера

На основе hello настройки среды Azure и hello политику безопасности, которую вы определили, центр обеспечения безопасности может рекомендуется развертывать решение партнера. Hello рекомендации центра обеспечения безопасности поможет hello процесс выбора и установки решения партнеров. Hello общие принципы развертывания может отличаться в зависимости от типа hello решения и партнера, который используется. Дополнительные сведения см. в разделе hello в следующих статьях:

- [Установка Endpoint Protection](security-center-install-endpoint-protection.md)
- [Добавление брандмауэра веб-приложения](security-center-add-web-application-firewall.md)
- [Добавление брандмауэра следующего поколения в центре безопасности Azure](security-center-add-next-generation-firewall.md)
- [Оценка уязвимостей не установлена](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Управление партнерскими решениями

После развертывания tooview сведения о работоспособности решения hello hello и выполнение основных задач управления, на hello **центра обеспечения безопасности** колонки, выберите hello **решения партнеров** параметр. Дополнительные сведения об управлении партнерскими решениями с помощью центра безопасности Azure см. [в этой статье](security-center-partner-solutions.md).

![Интеграция партнеров](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Поддержка защиты конечной точки Symantec является ограниченной toodiscovery. Оповещения о работоспособности недоступны.
>

## <a name="see-also"></a>См. также

В этой статье вы узнали, как toointegrate партнерские решения в центр безопасности Azure. toolearn Дополнительные сведения о центра обеспечения безопасности, см. следующие статьи hello:

* [Руководство по планированию использования центра безопасности Azure и работе в нем](security-center-planning-and-operations-guide.md).
* [Управление и отвечать toosecurity оповещения в центр безопасности](security-center-managing-and-responding-alerts.md)
* [Основные сведения об оповещениях системы безопасности в центре безопасности Azure](security-center-alerts-type.md).
* [Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md). Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md). Узнайте, как toomonitor hello состояние работоспособности решений для партнера.
* [Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md). Получите ответы toofrequently вопросы и ответы по использованию службы hello.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/). Записи блога, посвященные безопасности и соответствию требованиям в Azure.

---
title: "Основы администрирования стека aaaAzure | Документы Microsoft"
description: "Узнайте, что необходимо tooknow tooadminister стека Azure."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.openlocfilehash: cdf2818e9fc819b448508ca52bbdbec259890265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-administration-basics"></a>Основы администрирования Azure стека

Существует несколько моментов, которые необходимо tooknow, если вы tooAzure новый стек администрирования. В этом руководстве Общие сведения о роли как оператор облака и укажите, что необходимо tootell пользователей для них toobecome продуктивно работать быстро.

## <a name="understand-development-kit-builds"></a>Изучите строит пакет средств разработки

Просмотрите hello [возможности стека Azure?](azure-stack-poc.md) toomake статьи, необходимо понимать назначение hello hello Azure стека Development Kit и ограничения. Пакет средств разработки hello следует использовать как «песочнице», где можно оценить стек Azure и разработки и тестирования приложений в непроизводственной среде. (Информацию о развертывании см. в разделе hello [развертывания пакета средств разработки Azure стека](azure-stack-deploy-overview.md) краткое руководство.)

Как Azure мы инноваций быстро. Регулярно будет выпущена новые сборки. При необходимости toomove toohello последнюю сборку необходимо [повторное развертывание стека Azure](azure-stack-redeploy.md). Этот процесс занимает время, но hello преимущество — можно опробовать новейших функций hello. Hello документации на нашем сайте отражает hello последней версии сборки.

## <a name="learn-about-available-services"></a>Дополнительные сведения о доступных службах

Вам потребуется знания из службы, которые можно сделать доступными tooyour пользователей. Стек Azure поддерживает подмножество функций служб Azure. Список поддерживаемых служб Hello по-прежнему tooevolve.

**Базовые службы**

По умолчанию стек Azure включает следующие «базовые службы» Привет при развертывании Azure стека:

- Среда выполнения приложений
- Хранилище
- Сеть
- Хранилище ключей

С этими базовыми службами можно предложить пользователям tooyour инфраструктуры как услуга (IaaS) с минимальной конфигурацией.

**Дополнительные службы**

В настоящее время поддерживаются следующие дополнительные службы платформы как услуга (PaaS) hello:

- Служба приложений
- Функции Azure
- Базы данных SQL и MySQL

Эти службы требуют дополнительной конфигурации, прежде чем их можно сделать доступными tooyour пользователей. Дополнительные сведения см. в разделе руководства «hello» и разделы «как tooguides\Offer services» hello нашей документации.

**Стратегия службы**

Стек Azure по-прежнему tooadd Поддержка служб Azure. Стратегия проецируется hello. в разделе hello [инноваций гибридных приложений с Azure и Azure стека](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) Технический документ. Также можно отслеживать hello [стека Azure блогах](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) для новых сообщений.

## <a name="what-tools-do-i-use-toomanage"></a>Средства следует использовать toomanage?
 
Можно использовать hello [портал администратора](azure-stack-manage-portals.md) или toomanage PowerShell Azure стека. Hello простым способом toolearn hello основные понятия — с помощью портала hello. Если вы хотите toouse PowerShell, существует подготовительных шагов. Вы должны [установить](azure-stack-powershell-install.md) PowerShell, [загрузки](azure-stack-powershell-download.md) дополнительных модулей и [Настройка](azure-stack-powershell-configure-admin.md) PowerShell.

Стек Azure использует диспетчера ресурсов Azure в качестве его базовый механизм развертывания, управления и организации. Если ты toomanage стека Azure и помогают пользователям поддержки рассказывается о диспетчере ресурсов. В разделе hello [Приступая к работе с диспетчером ресурсов Azure](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) Технический документ.

## <a name="your-typical-responsibilities"></a>Ваши обязанности типичные

Пользователи должны toouse служб. С их точки зрения основной роли является toomake эти службы доступны toothem. Необходимо решить, какие службы toooffer и предоставления этих служб, создав [квоты](azure-stack-setting-quotas.md), [планы](azure-stack-create-plan.md), и [предлагает](azure-stack-create-offer.md). 

Кроме того, потребуется marketplace toohello tooadd элементов, таких как образы виртуальных машин. Hello простым способом является слишком[загрузить элементы marketplace из Azure tooAzure стека](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> Если требуется tootest вашей планов, предложения и службы, следует использовать hello [пользовательского портала](azure-stack-manage-portals.md); не hello администратора портала.

В службах tooproviding сложение необходимо выполнить все обязанности регулярного hello объекта tookeep оператор облако Azure стека запущен и работает. Эти обязанности включить hello следующие:

- Добавление учетных записей пользователей (для [Azure Active Directory](azure-stack-add-new-user-aad.md) развертывания или для [служб федерации Active Directory](azure-stack-add-users-adfs.md) развертывания)
- [Назначение ролей (RBAC) системы управления доступом на основе ролей](azure-stack-manage-permissions.md) (это не только tooadministrators.)
- [Монитор работоспособности инфраструктуры](azure-stack-monitor-health.md)
- Управление [сети](azure-stack-viewing-public-ip-address-consumption.md) и [хранения](azure-stack-manage-storage-accounts.md) ресурсы
- Замените неисправности оборудования

## <a name="what-tootell-your-users"></a>Какие tootell пользователей

Вам понадобятся пользователям понять, каким образом toowork с служб в стек Azure разработки toohello tooconnect комплект среды, а также и toolet toosubscribe toooffers.

**Понять, как toowork с служб в стек Azure**

Нет сведений, которые необходимо понять пользователей до использования служб и создать приложения в Azure стека. Например существуют определенные требования к PowerShell и API-Интерфейс версии. Кроме того существуют некоторые функции отличиями между службы в Azure и службы hello Azure стека. Убедитесь, что пользователи просмотреть следующие статьи hello:

- [Основные особенности: с помощью служб или создание приложений для Azure стека](azure-stack-considerations.md)
- [Рекомендации для виртуальных машин в стек Azure](azure-stack-vm-considerations.md)
- [Хранилища: различия и рекомендации](azure-stack-acs-differences-tp2.md)

Hello сведения в следующих статьях приведены различия hello службы в Azure и Azure стека. Он дополняет hello информацию, которая доступна для службы Azure в глобальных документации Azure hello. 

**Подключение tooAzure стека в качестве пользователя**

В среде разработки пакета Если у пользователя нет узел комплект средств для разработки toohello доступа удаленного рабочего стола, их необходимо настроить подключение к виртуальной частной сети (VPN) при доступе стек Azure. В разделе [подключения tooAzure стека](azure-stack-connect-azure-stack.md). 

Пользователи будут tooknow как слишком[доступа hello пользовательского портала ](azure-stack-manage-portals.md) или как tooconnect через PowerShell. Если с помощью PowerShell, пользователи могут иметь tooregister поставщиков ресурсов, чтобы они смогли воспользоваться службами. (Поставщик ресурсов управляет службой. Например, hello сети поставщика ресурсов управляет ресурсами, например виртуальных сетей, сетевых интерфейсов и подсистемы балансировки нагрузки.) Они должны [установить](azure-stack-powershell-install.md) PowerShell, [загрузки](azure-stack-powershell-download.md) дополнительных модулей и [Настройка](azure-stack-powershell-configure-user.md) PowerShell (которая включает Регистрация поставщика ресурсов).

**Подписаться на предложение tooan**

Пользователь может получить доступ к служб, они должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , созданного с помощью оператора облака.

## <a name="where-tooget-support"></a>Где поддерживают tooget

Для hello пакет средств разработки Azure стека, можно задавать вопросы поддержки связанные hello [форумы Майкрософт](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). Если нажать hello справки и поддержки значком (вопросительный знак) в правом верхнем углу hello hello администратора портала и нажмите кнопку **New поддерживает запрос**, откроется сайт форумы hello напрямую. Эти форумы отслеживаются регулярно. Так как пакет средств разработки hello среды оценки, не поддерживается официальный доступным через службы поддержки клиентов Майкрософт (CSS).

## <a name="next-steps"></a>Дальнейшие действия

- [Область управления в стек Azure](azure-stack-region-management.md)



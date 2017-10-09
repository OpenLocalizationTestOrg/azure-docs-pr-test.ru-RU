---
title: "проблемы aaaConnectivity и сети для облачных служб Microsoft Azure часто задаваемые вопросы о | Документы Microsoft"
description: "В этой статье перечислены hello часто задаваемые вопросы о связь и сеть для облачных служб Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Проблемы подключения и сетей для облачных служб Azure. Вопросы и ответы (FAQ)

В этой статье приведены часто задаваемые вопросы по подключениям и сетям для [облачных служб Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Кроме того, можно обратиться к hello [страницы размер виртуальной Машины облачных служб](cloud-services-sizes-specs.md) для сведений о размере.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Не удается зарезервировать IP-адрес в облачной службе с несколькими виртуальными IP-адресами
Во-первых убедитесь, что этот экземпляр виртуальной машины hello, который вы пытаетесь tooreserve hello IP-адрес для включен. Во-вторых убедитесь, что вы используете зарезервированные IP-адреса для обоих hello промежуточного и рабочего развертываний. **Нет** изменить параметры hello, пока обновление развертывания hello.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Как использовать удаленный рабочий стол при наличии NSG?
Добавление правила toohello NSG, разрешить трафик через порты **3389** и **20000**.  Удаленный рабочий стол использует порт **3389**.  Экземпляров облачной службы, распределяются, поэтому не может напрямую управлять какой экземпляр tooconnect для.  Hello *RemoteForwarder* и *RemoteAccess* агенты управления трафиком протокола удаленного рабочего СТОЛА и разрешить toosend клиента hello куки-файл протокола удаленного рабочего СТОЛА и tooconnect отдельного экземпляра, чтобы указать.  Hello *RemoteForwarder* и *RemoteAccess* агенты имеют этот порт **20000** открыть, который может блокироваться, если у вас есть NSG.

## <a name="can-i-ping-a-cloud-service"></a>Можно ли проверить связь с облачной службой?

Нет, не используя обычный hello «ping» или протокола ICMP. Подсистема балансировки нагрузки Azure hello Hello протокола ICMP не разрешен.

подключение к tootest, рекомендуется делать порт проверки связи. А Ping.exe использует ICMP, другие средства, такие как PSPing, Nmap и telnet разрешить tootest подключения tooa определенный TCP-порт.

Дополнительные сведения см. в разделе [использовать порт вместо tootest ICMP подключения к виртуальной Машине Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Как избежать получения тысяч вхождений с Неизвестный IP-адресов, которые указывают на какой-то toohello вредоносной атаки облачная служба?
Azure реализует tooprotect многоуровневый сетевой безопасности его служб платформы распределенные атаки типа "отказ в обслуживании" (DDoS). Hello системы защиты от атак DDoS Azure является частью Azure непрерывного наблюдения процесс, который постоянно улучшена благодаря тестирование уязвимости. Эта система защиты от атак DDoS предназначен не только toowithstand атак с hello за пределами, но и от других клиентов Azure. Дополнительные сведения см. в разделе [Сетевая безопасность Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Можно также создать блок tooselectively задачи запуска некоторых конкретных IP-адресов. Дополнительные сведения см. в разделе [Блокирование определенного IP-адреса](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Когда я пытаюсь экземпляр tooRDP toomy облачной службы, выдается сообщение hello, «hello учетной записи пользователя истек.»
При обхода hello Дата окончания срока действия, настроенный в параметрах протокола удаленного рабочего СТОЛА, может возникнуть сообщение hello «этой учетной записи пользователя истек». Дата окончания срока действия hello hello портала можно изменить, выполните следующие действия:
1. Войдите в консоль управления Azure (https://manage.windowsazure.com) toohello, перейдите tooyour облачной службы и выберите hello **Настройка** вкладки.
2. Выберите **Удаленный доступ**.
3. Изменение даты «Истечения срока действия на» hello, а затем сохраните конфигурацию hello.

Теперь можно будет tooRDP tooyour машины.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Почему LoadBalancer не балансирует трафик одинаково?
Сведения о том, как работает внутренняя подсистема балансировки нагрузки, см. в разделе [Новый режим распределения Azure Load Balancer](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

используемый алгоритм распределения Hello является 5-фрагментному (исходный IP-адрес, порт источника тип протокола конечный IP-адрес, порт назначения) хэш-серверы tooavailable toomap трафика. Он позволяет закреплять IP-адреса только в рамках сеанса транспорта. Пакетов в hello сеанс TCP или UDP будут направляться toohello экземпляра центра обработки данных IP-адрес (DIP) за конечной точкой с балансировкой нагрузки hello. При hello клиент закрывает и снова открывает подключение hello или начинает новый сеанс из hello же исходный IP-адрес, порт источника hello изменяется и вызывает hello трафика toogo tooa другой DIP-адрес конечной точки.

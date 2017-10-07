---
title: "Шифрование диска aaaApply в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** применить шифрование диска **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Шифрование диска в центре безопасности Azure
Центр безопасности Azure рекомендует шифровать диски виртуальных машин Windows или Linux, которые не зашифрованы с помощью шифрования дисков Azure. Шифрование дисков позволяет шифровать диски виртуальных машин IaaS Windows и Linux.  Рекомендуется применять шифрование для hello ОС и объемов данных на ВМ.

Шифрование диска используется hello отраслевой стандарт [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) компонента Windows, а также hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) функция Linux. Эти функции обеспечивают ОС и защитить toohelp шифрования данных и защитить данные и соответствии с требованиями организации безопасности и соответствия обязательства. Шифрование диска интегрирован с [хранилище ключей Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp вы для управления ключами шифрования диска hello и секретные данные в вашей подписке хранилище ключей, обеспечивая шифровать все данные в hello дисков виртуальной Машины хранятся в вашей [ Хранилище Azure](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> На следующих операционных систем Windows server - Windows Server 2008 R2, Windows Server 2012 и Windows Server 2012 R2 hello поддерживается Azure шифрование диска. Шифрование диска поддерживается в следующих операционных систем Linux server — Ubuntu, CentOS, SUSE и SUSE Linux Enterprise Server (SLES) hello.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **применить шифрование диска**.
2. В hello **применить шифрование диска** колонки, отображается список виртуальных машин, для которых рекомендуется использовать шифрование диска.
3. Выполните hello инструкции tooapply шифрования toothese виртуальных машин.

![][1]

tooencrypt виртуальных машинах Azure, которые определены как требующий шифрования центром обеспечения безопасности рекомендуется hello следующие шаги:

* Установите и настройте Azure PowerShell. Это позволяет toorun hello PowerShell команды требуется tooset копирование tooencrypt необходимые предварительные требования hello виртуальных машинах Azure.
* Получение и запустите сценарий hello предварительные требования шифрования диска Azure, Azure PowerShell.
* Зашифруйте свои виртуальные машины.

См. дополнительные сведения о [шифровании виртуальной машины Azure](security-center-disk-encryption.md).  В этом разделе предполагается, что вы используете Windows 10 как hello клиентского компьютера, с помощью которого можно настроить шифрование диска.

Есть разные подходы, используемые при работе с виртуальными машинами Azure. Если вы уже хорошо versed в Azure PowerShell или Azure CLI, то лучше toouse альтернативные подходы. toolearn о эти другие подходы разделе [шифрования диска Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>См. также
В этом документе показано, как tooimplement hello центра обеспечения безопасности, рекомендации «применить шифрование диска.» toolearn Дополнительные сведения о шифрования диска, см. ниже hello:

* [Шифрование и управление ключами с хранилищем ключей Azure](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (видео, 36 мин 39 сек) — Узнайте, как toouse диска управления шифрования для ВМ IaaS и хранилище ключей Azure toohelp защиты и защиты данных.
* [Шифрование виртуальной машине Azure](security-center-disk-encryption.md) (документ) — Узнайте, как tooencrypt виртуальных машинах Azure.
* [Шифрование диска Azure](../security/azure-security-disk-encryption.md) (документ) — Узнайте, как tooenable диск шифрования для Windows и виртуальных машин Linux.

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.
* [Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png

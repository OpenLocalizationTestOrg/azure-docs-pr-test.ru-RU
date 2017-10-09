---
title: "шифрование aaaEnable для учетной записи хранилища в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить шифрование для Azure хранилища учетной записи **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Включение шифрования данных для учетной записи хранения Azure в центре безопасности Azure
Центр безопасности Azure может рекомендовать включить шифрование службы хранилища Azure для неактивных данных.

Шифрование службы хранилища (SSE) осуществляется посредством шифрования данных hello записи tooAzure хранилища и расшифровки данных hello до извлечения.  SSE в настоящее время доступна только для hello службы больших двоичных объектов и может использоваться для больших двоичных объектов, страничные большие двоичные объекты и добавление BLOB-объектов.  toolearn более, в разделе [шифрование службы хранилища для статических данных](../storage/common/storage-service-encryption.md).


> [!Note]
> После включения шифрования зашифровываются только новые данные. Остальные существующие большие двоичные объекты в учетной записи хранения остаются незашифрованными. существующие и большие двоичные объекты tooencrypt, в разделе hello [хранилища службы шифрования часто задаваемые вопросы о](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Шифрование службы хранилища поддерживается только для учетных записей хранения Resource Manager. Классические учетные записи хранения в настоящее время не поддерживаются. toounderstand hello классический и модели развертывания диспетчера ресурсов, в разделе [моделях развертывания Azure](../azure-classic-rm.md).

> [!NOTE]
> В этом документе представлены hello службы с помощью пример развертывания.  Этот документ не является пошаговым руководством.
>
>

## <a name="implement-hello-recommendation"></a>Реализация рекомендаций hello
1. В hello **рекомендации** колонке выберите **включить шифрование для учетной записи хранилища Azure**.
   ![Включение шифрования для учетной записи хранения][1]
2. Hello **включить шифрование хранилища** открывает колонку. Эта колонка список учетных записей хранилища Azure hello, где отключен шифрование хранилища. В этом примере выберем учетную запись **storageacct1**.
   ![Включение шифрования хранилища][2]
3. Hello **шифрования** колонке **storageacct1** открывается. Щелкните **Включено**.
   ![Колонка "Шифрование"][3]
4. Щелкните **Сохранить**.

Вы включили шифрование хранилища для учетной записи **storageacct1**.


## <a name="see-also"></a>См. также
В этом документе показано, как tooimplement hello центра обеспечения безопасности рекомендация «включить шифрование для учетной записи хранилища Azure». toolearn Дополнительные сведения о шифрование службы хранилища Azure, см. ниже hello:

* [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](../storage/common/storage-service-encryption.md)

toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:

* [Установка политики безопасности в центр безопасности Azure](security-center-policies.md) -Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.
* [Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) -Узнайте, как toomonitor hello работоспособности ресурсов Azure.
* [Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) -Узнайте, как предупреждения toosecurity toomanage и отправки ответа.
* [Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md). Узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.
* [Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) -часто задаваемые вопросы об использовании hello службы поиска.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) (Блог по безопасности Azure). Публикации блога, посвященные безопасности и соответствию требованиям в Azure.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png

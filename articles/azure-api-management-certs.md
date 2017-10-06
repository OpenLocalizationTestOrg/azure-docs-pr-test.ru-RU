---
title: "aaaUpload сертификат API управления Azure | Документы Microsoft"
description: "Узнайте, как сертификат tooupload athe API-Интерфейс управления для hello классический портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Отправка сертификата управления Azure для API управления
Сертификаты управления позволяют tooauthenticate с hello классической модели развертывания, предоставляемых Azure. Многие программы и средства (например, Visual Studio или hello Azure SDK) использовать эти сертификаты tooautomate конфигурации и развертывания различных служб Azure. 

> [!WARNING]
> Будьте осторожны! Разрешить эти типы сертификатов всех, кто выполняет проверку подлинности с ними toomanage hello подписки, связанные с ними.
>
>

Дополнительные сведения о сертификатах Azure (включая сведения о создании самозаверяющего сертификата) см. в разделе [Что такое сертификаты управления](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Можно также использовать [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-код клиента в целях автоматизации.

## <a name="upload-a-management-certificate"></a>Отправка сертификата управления
После создания сертификата управления, (CER-файл только hello открытым ключом) можно загрузить его в портал hello. При наличии hello сертификатов на портале hello, имеющий соответствующий сертификат (закрытый ключ) могут подключаться через hello API управления и получения ресурсов hello для hello связанные подписки.

1. Войдите в toohello [портал Azure](http://portal.azure.com).
2. Нажмите кнопку **дополнительные службы** в hello нижнем списке службы Azure, затем выберите **подписки** в hello _Общие_ группы служб.

    ![Меню "Подписка"](./media/azure-api-management-certs/subscriptions_menu.png)

3. Убедитесь, что tooselect hello нужной подписки, которые должны tooassociate сертификатом hello.     
4. После того как выбрана правильная подписка hello, нажмите клавишу **сертификаты управления** в hello _параметры_ группы.

    ![данных](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Нажмите клавишу hello **отправить** кнопки.

    ![Кнопка "Отправить" на странице сертификатов](./media/azure-api-management-certs/certificates_page.png)
6. Заполните данные в диалоговом окне приветствия и нажмите клавишу **отправить**.

    ![данных](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда сертификат управления, связанных с подпиской (после установки сопоставления локальный сертификат hello) программно подключением toohello [классической модели развертывания API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) и автоматизации Здравствуйте, различные ресурсы Azure, связанных с этой подпиской.

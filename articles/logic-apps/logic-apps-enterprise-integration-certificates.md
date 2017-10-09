---
title: "aaaUsing сертификатов с помощью пакет интеграции Enterprise | Документы Microsoft"
description: "Узнайте, как toouse сертификаты с hello пакет интеграции Enterprise | Приложения логики Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Узнайте о сертификатах и пакете интеграции Enterprise
## <a name="overview"></a>Обзор
Интеграция предприятия использует сертификаты toosecure B2B связи. В приложениях интеграции Enterprise можно использовать два типа сертификатов.

* Открытые сертификаты, которые необходимо приобрести в центре сертификации (ЦС).
* Закрытые сертификаты, которые можно выдать самостоятельно. Эти сертификаты являются иногда ссылка tooas самозаверяющие сертификаты.

## <a name="what-are-certificates"></a>Что такое сертификаты?
Сертификаты представляют собой цифровые документы, проверьте идентификатор hello участников hello электронного обмена данными и, для защиты электронных связи.

## <a name="why-use-certificates"></a>Зачем нужны сертификаты?
Иногда обмен данными "бизнес-бизнес" требует конфиденциальности. Интеграции предприятия использует сертификаты toosecure этих сообщений двумя способами:

* Шифрование содержимого сообщений hello
* для добавления цифровых подписей в сообщения.  

## <a name="upload-a-public-certificate"></a>Передача общего сертификата

toouse *открытый сертификат* в приложениях для логики с возможностями B2B, необходимо сначала tooupload hello сертификата в учетную запись интеграции.  

После отправки сертификата будет доступен toohelp обеспечения безопасности сообщений B2B при определении свойств в hello [соглашения](logic-apps-enterprise-integration-agreements.md) созданного вами.  

Ниже приведены подробные инструкции для передачи открытых сертификатов в вашу учетную запись интеграции, после входа в toohello портал Azure hello:

1. Выберите **дополнительные службы** и введите **интеграции** в поле поиска hello фильтра. Выберите **учетные записи службы интеграции** из списка результатов hello     
![Щелкните "Обзор"](media/logic-apps-enterprise-integration-certificates/overview-1.png).  
2. Выберите toowhich учетной записи интеграции hello, требуется сертификат tooadd hello.  
![Выбор учетной записи toowhich hello интеграции, требуется сертификат tooadd hello](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Выберите hello **сертификаты** плитки.  
![Плитка приветствия выберите сертификаты](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. В hello **сертификаты** колонки, откроется, выберите hello **добавить** кнопки.   
![Нажмите кнопку Добавить hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Введите **имя** сертификата и hello, а затем выберите тип сертификата как **открытый** из раскрывающегося списка hello.  
6. Значок папки выберите hello hello правой части hello **сертификат** текстовое поле. При открытии средства выбора файлов для hello, найдите и выберите файл сертификата hello, что требуется учетной записи интеграции tooyour tooupload.
7. Выберите сертификат hello, а затем выберите **ОК** в средство выбора файлов hello. Это проверяет и загружает tooyour интеграции hello сертификата учетной записи.
8. И, наконец, включите hello **добавить сертификат** колонки, выберите hello **ОК** кнопки.  
![Нажмите кнопку OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Выберите hello **сертификаты** плитки. Вы увидите, что hello добавленный сертификат.  
![В разделе hello новый сертификат](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Передача закрытого сертификата

toouse *закрытый сертификат* в свои приложения логики с возможностями B2B учетной записи интеграции tooyour закрытый сертификат можно отправить с созданием hello следующие шаги

1. [Отправка частного хранилища ключей tooKey](../key-vault/key-vault-get-started.md "Дополнительные сведения о хранилище ключей") и предоставить **имя ключа** 
   
   > [!TIP]
   > Необходимо авторизовать операций tooperform логику приложения в хранилище ключей. Участника-службы приложения логики toohello доступ можно предоставить с помощью hello следующую команду PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

После предыдущего шага hello, добавьте учетную запись toointegration закрытый сертификат.

Подробное описание действий для передачи закрытого сертификатов в вашу учетную запись интеграции, после входа в toohello портал Azure Здравствуйте, следующие:  
 
1. Выбор учетной записи toowhich hello интеграции tooadd hello сертификат и выберите hello **сертификаты** плитки.  
![Плитка приветствия выберите сертификаты](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. В hello **сертификаты** колонки, откроется, выберите hello **добавить** кнопки.   
![Нажмите кнопку Добавить hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Введите **имя** сертификата и тип сертификата выберите hello как **закрытый** из раскрывающегося списка hello.   
4. Выберите значок папки hello hello правой части hello **сертификат** текстовое поле. При открытии средства выбора файлов для hello найти hello соответствующий открытый сертификат, который учетной записи tooupload tooyour интеграции.   
   
   > [!Note]
   > При добавлении сертификата закрытого важно tooadd соответствующий открытый сертификат tooshow в [соглашение AS2](logic-apps-enterprise-integration-as2.md) параметров получения и отправки для подписания и шифрования сообщений hello.
   > 
   >   

5. Выберите hello **группы ресурсов**, **хранилище ключей**, **имя ключа** и выберите hello **ОК** кнопки.  
![Добавьте сертификат](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png).  
6. Выберите hello **сертификаты** плитки. Вы увидите, что hello добавленный сертификат.
![В разделе hello новый сертификат](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Создание соглашения "бизнес-бизнес"](logic-apps-enterprise-integration-agreements.md)  
* [Узнайте больше о хранилище ключей Azure](../key-vault/key-vault-get-started.md "Сведения о хранилище ключей")  


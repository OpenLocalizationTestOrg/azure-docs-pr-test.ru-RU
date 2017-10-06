---
title: "aaaMigrate из Azure RemoteApp tooCitrix XenApp Essentials | Документы Microsoft"
description: "Как toomigrate из Azure RemoteApp tooCitrix XenApp Essentials"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Миграция из Azure RemoteApp tooCitrix XenApp Essentials

Если использовать Azure RemoteApp и требуется toomigrate tooCitrix XenApp Essentials, существует несколько необходимых компонентов tookeep в виду. Во-первых, прочитайте [пошаговое техническое руководство по развертыванию для Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) и ознакомьтесь с [интернет-библиотекой технической документации](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html) компании Citrix. 

## <a name="prerequisite-steps-for-migration"></a>Обязательные шаги для миграции

1. Создайте новую виртуальную сеть или определите, в какой виртуальной сети Azure в Azure Resource Manager вы развернете Citrix XenApp Essentials. Azure RemoteApp использует hello классический портал Azure; Citrix XenApp Essentials поддерживает только диспетчера ресурсов Azure.  
2. Убедитесь, что hello виртуальной сети, выбранным сети контроллер домена tooyour, поскольку Citrix поддерживает только гибридных развертываний. Если вы используете Облачное развертывание Azure RemoteApp, проверьте наличие виртуальной сети контроллера домена Active Directory tooan доступа к сети. Можно также использовать доменные службы Azure Active Directory (Azure AD DS). 
3. Убедитесь, что hello, служба DNS настроена правильно для hello виртуальной сети, поэтому на первая попытка успешна, присоединения к домену. Создание виртуальной машины (VM) в выбранной виртуальной сети hello и выполнять tooverify соединения домена вручную, hello DNS и присоединения к домену работает должным образом. Это гарантирует, что являются успешно hello при первом развертывании Citrix XenApp Essentials. 
4. При необходимости создайте пиринг между виртуальной сетью классического портала Azure, которую вы используете с Azure RemoteApp, и виртуальной сетью Azure Resource Manager. Этот пиринг процесс работает, если hello две сети находятся в hello же области. Если это не так, используйте виртуальные сети tooconnect VPN hello сайт сайт для работы в сети. 
5. При необходимости чтения [как toomigrate данных в действие и из Azure RemoteApp](remoteapp-migrate.md). 
6. Обновите ваш существующий Azure RemoteApp изображения tooinclude hello компонент Citrix VDA (инструкции см. в разделе документации Citrix hello). 
7. Go toohello Azure Marketplace и начать развертывание Citrix XenApp Essentials.

## <a name="other-considerations"></a>Дополнительные рекомендации

Следует учитывать следующие дополнительные соображения при переносе hello.
- Служба Citrix XenApp Essentials поддерживает только гибридные развертывания. Другими словами требуется доступ tooa контроллером домена в присоединения к домену tooperform заказа. Если вы используете Облачное развертывание Azure RemoteApp, использовать Azure AD DS или убедитесь в наличии доступа tooActive каталог для присоединения к домену в виртуальной сети. 
- tooCitrix данных пользователя toomove XenApp Essentials. в статье toolearn [как toomigrate данных в действие и из Azure RemoteApp](remoteapp-migrate.md). 
- Служба Citrix XenApp Essentials поддерживает только учетные записи Active Directory. Она не поддерживает учетные записи Майкрософт (например, outlook.com, msn.com или hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Выставление счетов за Citrix XenApp Essentials

Полные сведения о ценах на разделе hello [часто задаваемые вопросы о](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) и [Citrix обзорную статью](https://www.citrix.com/global-partners/microsoft/remote-app.html). Существует три компонента выставления счетов tooCitrix XenApp Essentials:

- Hello Citrix службы платы, являющийся $12 на пользователя в месяц. Как и все покупки в Azure Marketplace это способ оплаты по документу toohello, связанный с подпиской Azure. Денежные кредиты Azure невозможно использовать для клиентов Enterprise Agreement (EA). 
- Клиентские лицензии (CAL) служб удаленных данных (RDS). В настоящее время вы можете приобрести hello удаленного доступа оплату, вместе с hello оплаты Citrix XenApp Essentials 6,25 $. Если вы являетесь клиентом EA, для этого можно использовать toopay денежные кредиты Azure. Если вы хотите toouse существующие Клиентские лицензии, обратитесь по адресу [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), поэтому мы сможем применить этот tooyour счета. 
- Служба вычислений и служба хранилища Azure. Это стоимость хранилища Azure hello и потребляет потребления вычислений для виртуальных машин hello. Учитывайте цены при выборе размера виртуальных машин и плотности пользователей. Если вы являетесь клиентом EA, для этого можно использовать toopay денежные кредиты Azure.

Если у вас остались вопросы:
- Напишите нам по адресу [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
- Обратитесь в [службу поддержки Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Начните с [открывать корпус поддержки Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp с условием шаги 1 – 5. Шаги 6-7 обратитесь в службу Citrix, открыв запрос в службу поддержки на портале управления Citrix hello. 

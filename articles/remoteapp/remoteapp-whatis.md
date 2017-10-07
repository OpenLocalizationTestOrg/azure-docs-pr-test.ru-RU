---
title: "aaaWhat такое Azure RemoteApp? | Документация Майкрософт"
description: "Узнайте, как tooshare приложениям и ресурсам устройства tooany через Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Что такое Azure RemoteApp?
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp предоставляет функциональные возможности hello hello в локальной среде Microsoft приложения RemoteApp, архивируемых диспетчером служб удаленных рабочих столов, tooAzure. Azure RemoteApp позволяет предоставлять безопасный удаленный доступ tooapplications из различных пользовательских устройств. Azure RemoteApp в основном размещает непостоянные сеансов сервера терминалов в облаке hello и получить toouse их и использовать их совместно с пользователями.

Благодаря Azure RemoteApp вы можете делиться приложениями и ресурсами с другими пользователями почти на любом устройстве. Мы узлов приложений в облаке hello, это означает, что мы позаботимся оборудования hello и масштабирование toomeet потребностям пользователей. У вас есть toodo всего отправки hello приложения вы хотите tooshare, а затем получить вашей toouse пользователи этих приложений. [Пользователи получают tookeep свои собственные устройства](remoteapp-clients.md), тогда как можно управлять всем через портал Azure hello. Можно даже установить hello с помощью корпоративных учетных данных, что позволяет обеспечить безопасность hello приложений и данных.

Узнайте больше о Azure RemoteApp или, если вы уже заинтересованы, [опробуйте RemoteApp прямо сейчас](https://azure.microsoft.com/services/remoteapp/).

У вас есть вопросы по Azure RemoteApp? Читайте раздел [Вопросы и ответы](remoteapp-faq.md).

Azure RemoteApp входит в состав hello [инфраструктуры виртуальных рабочих столов Microsoft](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Новинка!** Требуется toolearn Дополнительные сведения об Azure RemoteApp? Или "Готово" toovalidate Azure RemoteApp в масштабе? Присоединение нашей еженедельно [спросите экспертов hello веб-семинар](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Коллекции Azure RemoteApp
Существует два типа [коллекций Azure RemoteApp](remoteapp-collections.md):

* Объект **облако коллекции** размещается в и сохраняет данные для программы в облаке hello. Пользователи могут получать доступ к приложениям, выполняя вход с помощью своей учетной записи Майкрософт или корпоративных учетных данных, синхронизированных с Azure Active Directory с федерацией.
  
    Выберите коллекции облака при приложения hello, требуется tooshare не требуется ресурс tooany подключения частной сети вашей организации (например, с помощью VPN-устройства). Если приложение hello использует ресурсы hello Интернета, OneDrive или Azure, облачной коллекции будет работать для вас. Оно также является быстрым toocreate hello.
* Объект **гибридной коллекции** размещается в и сохраняет данные в облако Azure hello, но также позволяет пользователям обращаться к данным и ресурсам, хранимым в локальной сети. Пользователи могут получать доступ к приложениям, выполняя вход с помощью своих корпоративных учетных данных, синхронизированных с Azure Active Directory с федерацией.
  
    Выберите гибридной коллекции, если требуется tooresources подключение в частной сети вашей компании. Например если hello приложения требуется доступ к tooone hello следующее:
  
  * Файловые серверы, расположенные в интрасети
  * Quicken
  * Базы данных за брандмауэром
    
    Это имеет смысл для крупных компаний с большим количеством ресурсов на их частные сети, которые не могут быть перемещены toohello облака.

Hello разных коллекций имеют различные параметры, включая сети, поэтому выяснить [какую коллекцию](remoteapp-collections.md) лучше всего подходит для вас. 

### <a name="updating-your-collection"></a>Обновление коллекции
Одна из hello основные различия между hello гибридных и облака коллекций — способ обработки обновлений программного обеспечения. В коллекции облака, использующего образ Office 365 профессиональный плюс 2013 или Office предустановленных hello у вас tooworry об обновлениях. Служба Hello ведет себя и развертывает обновления на постоянной основе, tooboth приложений и hello операционной системы.

Для гибридной коллекции, а также облака коллекций, использовать настраиваемый шаблон образ вы отвечаете обслуживание образа hello и приложений. Для присоединенных к домену образов вы можете управлять обновлениями с помощью таких средств, как Центр обновления Windows, групповые политики и System Center.

После обновления образ пользовательский шаблон загрузкой hello новый образ toohello облако Azure и затем обновить hello коллекции toouse hello нового образа. (Это можно сделать из hello Azure RemoteApp **быстрый запуск** странице или панели мониторинга hello.)

Дополнительные сведения можно найти в разделе [Обновление коллекции](remoteapp-update.md) .

## <a name="supported-remoteapp-clients"></a>Поддерживаемые клиенты RemoteApp
Azure RemoteApp поддерживается на hello RemoteApp клиентских приложений для Windows и Windows RT, а также приложения hello удаленного рабочего стола Майкрософт для Mac, iOS и Android. Пользователей можно использовать эти приложения на своих мобильных устройств или вычислительные устройства tooaccess hello новых программ Azure RemoteApp.

В разделе [доступ к приложениям в Azure RemoteApp](remoteapp-clients.md) Дополнительные сведения о клиентах hello.

## <a name="next-steps"></a>Дальнейшие действия
Вперед! Просто попробуйте! Следующие статьи помогут вам приступить к работе с RemoteApp:

* [Какой тип коллекции требуется для Azure RemoteApp?](remoteapp-collections.md)
* [Создание образа Azure RemoteApp](remoteapp-imageoptions.md)
* [Как toocreate облака коллекцию Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Как toocreate гибридных коллекцию Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Как работает лицензирование в Azure RemoteApp?](remoteapp-licensing.md)
* [Рекомендации по использованию Azure RemoteApp](remoteapp-bestpractices.md)
* [Azure RemoteApp: вопросы и ответы](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Помогите нам помочь вам
Знали ли вы, что в toorating сложения в этой статье и создания примечаний вниз ниже, можно внести самой статье toohello изменения? Чего-то не хватает? Что-то неправильно? Что-то изложено непонятно? Прокрутка вверх и нажмите кнопку **изменить на GitHub** или **изменить** изменения toomake - те поступит toous для просмотра и, когда мы выйдите из системы на них, вы увидите, изменения и усовершенствования здесь.


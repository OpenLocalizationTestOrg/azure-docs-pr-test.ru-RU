---
title: "часто задаваемые вопросы о RemoteApp aaaAzure | Документы Microsoft"
description: "Узнайте ответы toohello наиболее часто задаваемые вопросы об Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Azure RemoteApp: вопросы и ответы
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Мы знаем hello следующие вопросы об Azure RemoteApp. У вас есть другие вопросы? Посетите hello [форумы RemoteApp](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) и дайте нам знать, что необходимо tooknow или раскрывающемся комментарий ниже.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Не можете найти нужную информацию? У вас есть вопросы, на которые мы не ответили?
Если не удается найти hello сведения необходимо, или вы, мы не являетесь охватывает здесь вопроса, посетите страницу toohello [форум Azure RemoteApp](http://aka.ms/araforum) и попросите свой вопрос. Мы всегда можем добавить сюда ответы на ваши вопросы.

## <a name="what-is-azure-remoteapp"></a>Что такое Azure RemoteApp?
* **Что такое Azure RemoteApp?** RemoteApp является службой Azure позволяет предоставлять безопасный удаленный доступ tooapplications из различных пользовательских устройств. Узнайте больше об [Azure RemoteApp](remoteapp-whatis.md).
* **Что такое параметры развертывания hello** Существует два типа коллекций RemoteApp: облачные и гибридные. Выбор необходимого типа зависит от ряда факторов, например от того, нужна ли вам возможность присоединения к домену. Все возможные варианты описаны [здесь](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Советы по использованию Azure RemoteApp
* **Через какой промежуток времени происходит отключение? Сколько времени можно я простаивать перед приведите hello загрузки?** 4 часа. Вы автоматически выйдете из Azure RemoteApp, если вы или ваши пользователи будете неактивны 4 часа подряд. Извлечение hello другие параметры по умолчанию в [подписки Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md).
* **Можно ли попробовать эту службу бесплатно?** Да. Бесплатная пробная версия доступна в течение 30 дней. По окончании hello пробной версии вы можете переходить tooa платной учетной записи (который можно использовать в производственной среде) или с помощью службы hello stop. Запустите бесплатную пробную версию, будет слишком[portal.azure.com](http://portal.azure.com) — Создание нового экземпляра RemoteApp. Hello бесплатную пробную версию можно создавать два экземпляра RemoteApp с 10 пользователей каждого экземпляра. Помните, что пробный период составляет 30 дней.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Сведения о подписке Azure RemoteApp
* **Каковы ограничения hello служб?** Можно узнать о параметрах по умолчанию hello и службы возможностей Azure RemoteApp в [подписки Azure и ограничения служб, квоты и ограничения](../azure-subscription-service-limits.md). Сообщите нам, если у вас есть дополнительные вопросы.
* **Сделать число пользователей, у меня есть toohave?** Минимум 20 пользователей. Позвольте мне повторите, что toobe super снимите - hello МИНИМАЛЬНОЕ — 20. Счет будет выставляться за 20 пользователей. 
* **Сколько стоит RemoteApp?** Ознакомьтесь с [ценами на Azure RemoteApp ](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Может ли один тип коллекции стоить больше, чем другой?** Да, может. Это зависит от требований к коллекции. Гибридной коллекции необходимо подключение из локальной сети tooyour Azure RemoteApp. Если вы используете существующую виртуальную сеть или Express Route, то вам не придется нести дополнительные расходы. Но если вы используете новую виртуальную сеть Azure, а шлюз или Express Route, вы будете оплачивать hello [VPN-шлюз](https://azure.microsoft.com/pricing/details/vpn-gateway) или [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Эти расходы (подробные hello ссылки) — на основе вашего ежемесячного Azure RemoteApp стоимостью.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Коллекции: что поддерживается, какие коллекции следует использовать и другие вопросы
* **Поддерживаются ли настраиваемые бизнес-приложения?** Да. создать пользовательское приложение в Azure RemoteApp toouse [изображение пользовательский шаблон](remoteapp-create-custom-image.md)и затем передать его toohello коллекции RemoteApp.
* **Будет ли работать Мои пользовательские бизнес-приложения в Azure RemoteApp?**  hello лучшим способом toofigure, что в tootest его. Извлечение hello [Центр совместимости удаленных рабочих Столов](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Какой метод развертывания (облачное или гибридное) лучше подходит для моей организации?** Гибридной коллекции предоставляют возможности наиболее полном hello, если требуется полная интеграция с единого входа (SSO) и безопасности локальной сетевое подключение. Облако коллекции предоставляют tooisolate гибкой и простой способ развертывания с помощью нескольких методов проверки подлинности. Дополнительные сведения о hello [варианты развертывания](remoteapp-whatis.md).
* **У нас есть база данных SQL или другая база данных в локальной среде или Azure. Какой тип развертывания следует использовать?** Это зависит от расположения базы данных SQL или тыловой базы данных. Если база данных hello в частной сети, используйте hello гибридной коллекции. Если база данных hello предоставляется toohello Интернета и позволяет клиентским tooit tooconnect соединения, можно использовать hello облачной коллекции.
* **Поддерживаются ли сопоставление дисков, USB и последовательный порт, совместное использование буфера обмена и перенаправление принтеров?** Azure RemoteApp поддерживает все эти функции. Совместное использование буфера обмена и перенаправление принтеров включены по умолчанию. Дополнительные сведения о перенаправлении можно получить [здесь](remoteapp-redirection.md). 

## <a name="template-images"></a>Образы шаблонов
* **Можно ли использовать облака или существующей виртуальной машины как hello шаблон для Мои коллекции RemoteApp?** Да! Можно создать образ на основе на Виртуальной машине Azure, используйте один из образов hello, включенными в вашу подписку или создать образ. Извлечение hello [параметры RemoteApp изображения](remoteapp-imageoptions.md).

## <a name="network-options"></a>Параметры сети
* **Hello гибридной коллекции необходимо виртуальной сети. Можно ли использовать имеющуюся виртуальную сеть?** Можно выполнить hello существующей виртуальной сети является виртуальной сети Azure. В разделе «шаг 1: Настройка виртуальной сети» в hello [гибридной коллекции инструкции](remoteapp-create-hybrid-deployment.md) Дополнительные сведения.
* **Можно ли использовать виртуальную сеть вместе с облачной коллекцией?** Можно. Дополнительные сведения об этом см. в статье [Создание облачной коллекции](remoteapp-create-cloud-deployment.md). Особое внимание обратите на раздел "Шаг 1".

## <a name="authentication-options"></a>Параметры проверки подлинности
* **Как насчет проверки подлинности? Какие методы поддерживаются?**  hello облачной коллекции поддерживает учетные записи Майкрософт и учетных записей Azure Active Directory, что также учетные записи Office 365. Hello гибридного коллекция поддерживает только Azure Active Directory учетные записи, которые были синхронизированы (с помощью таких средств, как [синхронизации Azure Active Directory](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) из развертывания Windows Server Active Directory; в частности, либо синхронизированы с hello Параметр синхронизации пароля или синхронизированных с федерацией служб федерации Active Directory (AD FS) настроен. Вы также можете настроить службу [Многофакторная идентификация (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> Hello Azure Active Directory-пользователи должны принадлежать hello клиенте, связанном с вашей подпиской. (Можно просматривать и изменять подписки на hello **параметры** вкладка на портале hello. В разделе [клиента Azure Active Directory hello изменений, используемой RemoteApp](remoteapp-changetenant.md) подробнее.)
> 
> 

* **Почему нельзя дать моей учетной записи доступа Azure Active Directory**  hello Azure Active Directory-пользователи должны быть hello каталога, связанный с вашей подпиской. Можно просматривать или изменять этот каталог на вкладке Параметры hello hello портала. В разделе [клиента Azure Active Directory hello изменений, используемой RemoteApp](remoteapp-changetenant.md) для получения дополнительной информации.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Клиенты - какое устройство можно использовать tooaccess Azure RemoteApp?
Можно найти хороший сведения о клиенте, включая действия по установке hello разных клиентов в [доступ к приложениям в Azure RemoteApp](remoteapp-clients.md).

* **Какие устройства и операционные системы поддерживают hello клиентских приложений?**
  Первый hello компьютерах и планшетных ПК: 
  
  * Windows 10 (предварительная версия клиента)
  * Windows 8.1 и Windows 8
  * Windows 7 с пакетом обновления 1
  * Mac OS X
  * Windows RT
  * Планшеты под управлением Android
  * устройства iPad.

    И телефоны hello:
  * iPhone
  * Телефоны под управлением Android
  * Windows Phone
    
    [Скачайте](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) клиент RemoteApp.
* **Поддерживает ли Azure RemoteApp тонкие клиенты?** Да, hello Windows Embedded тонкой поддерживаются следующие клиенты:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Какие версии Windows Server поддерживается для hello узла сеансов удаленных рабочих столов (RDSH)?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Поддержка и обратная связь
* **Что такое план поддержки hello для RemoteApp?** Поддержка по выставлению счетов и управлению подпиской предоставляется бесплатно. Техническая поддержка доступна через hello [планы обслуживания Azure](https://azure.microsoft.com/support/plans/). Вы также можете получить поддержку от сообщества на [форуме Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Как отправить отзыв?** Посетите hello [форуме обратной связи](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Кто я говорю toolearn Дополнительные сведения об Azure RemoteApp?** В дополнение tooour [дискуссионный форум](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), которая отличное место toopost вопросы, вы можете присоединиться к hello еженедельно [попросите веб-семинар экспертов hello](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), где мы говорим о том, что все RemoteApp.
* **Существует ли документация по RemoteApp?** Хорошо, что вы спросили. В дополнение к этому toohello справку в ящике Справка портала hello (просто щелкните hello **?** на любой странице hello портала), hello следующие статьи, доступные tooteach вы о RemoteApp:
  
  * **Начало работы.**
    * [Что такое RemoteApp?](remoteapp-whatis.md)
    * [Что такое hello образы шаблонов RemoteApp?](remoteapp-images.md)
    * [Как работает лицензирование?](remoteapp-licensing.md)
    * [Как RemoteApp и Office работают вместе?](remoteapp-o365.md)
    * [Как работает перенаправление в RemoteApp](remoteapp-redirection.md)?
  * **Развертывание.**
    * [Создание настраиваемого образа шаблона](remoteapp-create-custom-image.md)
    * [Создание гибридной коллекции](remoteapp-create-hybrid-deployment.md)
    * [Создание облачной коллекции](remoteapp-create-cloud-deployment.md)
    * [Настройка Azure Active Directory для RemoteApp](remoteapp-ad.md)
    * [Публикация приложения в RemoteApp](remoteapp-publish.md)
  * **Управление.**
    
    * [Добавление пользователей](remoteapp-user.md)
    * [Рекомендации по настройке и использованию RemoteApp](remoteapp-bestpractices.md)    
    
    Видео! У нас также есть несколько видеороликов, посвященных RemoteApp. Некоторые из них содержат общие сведения ([tooAzure введение RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) во время другими пошаговыми руководствами для развертывания ([облако развертывания](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) и [гибридное развертывание](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Смотрите сами!

### <a name="help-us-help-you"></a>Помогите нам помочь вам
Знали ли вы, что в toorating сложения в этой статье и создания примечаний вниз ниже, можно внести самой статье toohello изменения? Чего-то не хватает? Что-то неправильно? Что-то изложено непонятно? Прокрутка вверх и нажмите кнопку **изменить на GitHub** изменения toomake - те поступит toous для просмотра и, когда мы выйдите из системы на них, вы увидите, изменения и усовершенствования здесь.


---
title: "aaaMonitor облака в локальную инфраструктуру удостоверений, в hello."
description: "Это страница hello Azure AD Connect Health, описывающее, что это такое и зачем использовать его."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Мониторинг вашей локальной инфраструктуры и синхронизации службы удостоверений в облаке hello
Azure Active Directory (Azure AD) Connect Health помогает отслеживать и анализировать вашей личности в локальной инфраструктуре и hello служб синхронизации. Он позволяет toomaintain tooOffice надежное подключение 365 и Microsoft Online Services, предоставляя возможности мониторинга для вашего ключа удостоверения компоненты, такие как серверы служб федерации Active Directory (AD FS), серверы Azure AD Connect (также известен как подсистема синхронизации) контроллеры домена Active Directory и т. д. Кроме того, hello ключевых точек данных об этих компонентах легкодоступными, чтобы узнать об использовании и других важных toomake аналитики обоснованных решений.

Hello сведения представлены в hello [портала Azure AD Connect Health](https://aka.ms/aadconnecthealth). На портале Azure AD Connect Health hello можно просмотреть предупреждения, наблюдение за производительностью, аналитические данные об использовании и другие сведения. Azure AD Connect Health позволяет hello следить за состоянием работоспособности для компонентов ключа удостоверения в одном месте.

![Что такое Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

При увеличении количества функций hello в Azure AD Connect Health, hello портал предоставляет одну панель мониторинга через линзы hello удостоверения. Вы опытных еще более надежной, работоспособности и интегрированной среды для вашего tooincrease пользователей их возможности tooget программистов.

## <a name="why-use-azure-ad-connect-health"></a>Зачем использовать Azure AD Connect Health?
При интеграции каталогов в локальной среде с Azure AD, пользователям будет повысить производительность из-за общего удостоверения tooaccess cloud и локальным ресурсам. Однако такая интеграция создает hello проблемой обеспечения работоспособности этой среды, чтобы пользователи могут надежно доступ к ресурсам на локальном компьютере и в hello облако с любого устройства. Azure AD Connect Health помогает отслеживать и анализировать инфраструктуры удостоверений в локальной, используемые tooaccess Office 365 или другие приложения Azure AD. Использовать службу так же просто, как установить агент на локальных серверах удостоверений.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Azure AD Connect Health для AD FS](active-directory-aadconnect-health-adfs.md)
Azure AD Connect Health для AD FS поддерживает AD FS 2.0 в Windows Server 2008 R2, Windows Server 2012 и Windows Server 2012 R2. Оно также поддерживает прокси-сервера для мониторинга hello AD FS или прокси серверов веб-приложений, которые обеспечивают проверку подлинности поддерживает для доступа через экстрасеть. С помощью простой и недорогой копии hello агент работоспособности Azure AD Connect Health для AD FS предоставляет следующие ключевые функции hello:

* Мониторинг с помощью tooknow предупреждения, когда прокси-сервера AD FS и AD FS не находятся в работоспособном состоянии
* уведомления по электронной почте для критических оповещений;
* анализ тенденций в данных производительности, что удобно для планирования ресурсов AD FS;
* Аналитика использования для службы федерации Active Directory входа в систему с помощью аспектов (приложений, пользователи, сетевого расположения и т.д.), которые являются полезным toounderstand начало используется как AD FS
* создание отчетов AD FS, например о 50 пользователях, выполнивших наибольшее количество неудачных попыток входа с последнего IP-адреса с указанием неправильного имени пользователя или пароля.

Hello следующие видеоматериалы содержат общие сведения о Azure AD Connect Health для AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health для синхронизации отслеживает и предоставляет сведения о синхронизации hello, возникающих между вашей локальной Active Directory и Azure AD. Azure AD Connect Health для синхронизации предоставляет следующие ключевые функции hello.

* Мониторинг с помощью tooknow предупреждения, когда сервер Azure AD Connect, также известные как hello подсистема синхронизации находится в неработоспособном состоянии
* уведомления по электронной почте для критических оповещений;
* оперативная аналитика синхронизации, включая диаграммы задержки для операций синхронизации и тренды различных операций, таких как добавление, обновление и удаление;
* Краткий обзор сведения о синхронизации свойства и последнего успешного экспорта tooAzure AD
* Для получения отчетов об ошибках синхронизации на уровне объекта \((не требуется Azure AD Premium)\).

Hello следующие видеоматериалы содержат общие сведения о Azure AD Connect Health для синхронизации.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Azure AD Connect Health для AD DS](active-directory-aadconnect-health-adds.md)
Azure AD Connect Health для доменных служб Active Directory (AD DS) обеспечивает мониторинг контроллеров домена, установленных в Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016. Установка агента работоспособности Hello позволяет вы toomonitor в локальной среде AD DS из облака hello. Azure AD Connect Health для AD DS предоставляет следующие ключевые функции hello.

* Отслеживание toodetect предупреждения, когда контроллеры домена находятся в неработоспособном состоянии и уведомления для критических оповещений по электронной почте
* панель мониторинга Hello контроллеры домена, которая предоставляет быстрый обзор работоспособности hello и рабочее состояние контроллеров домена
* Состояние репликации Hello панель мониторинга, которая содержит последние сведения о репликации hello и связывает tootroubleshooting руководства при обнаружении ошибок
* Быстрый доступ из любой точки tooperformance графы данных счетчиков производительности популярных, необходимых для целей наблюдения и устранения неполадок

Hello следующие видеоматериалы содержат общие сведения о Azure AD Connect Health для AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Приступая к работе с Azure AD Connect Health
tooget работы с Azure AD Connect Health, hello используйте следующие шаги:

1. [Приобретите Azure AD Premium](../active-directory-get-started-premium.md) или [получите пробную версию](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Скачайте и установите агенты Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) на серверах удостоверений.
3. Представление hello Azure AD Connect Health и панели мониторинга в [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Помните, что прежде чем просматривать данные в панель мониторинга Azure AD Connect Health, необходимо tooinstall hello агенты Azure AD Connect Health на целевых серверах.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Скачивание и установка агента Azure AD Connect Health
* Убедитесь, что вы [удовлетворять требованиям hello](active-directory-aadconnect-health-agent-install.md#requirements) для Azure AD Connect Health.
* Приступая к работе с Azure AD Connect Health для AD FS
    * [Скачайте агент Azure AD Connect Health для AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [См. инструкции по установке hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Приступая к работе с Azure AD Connect Health для синхронизации
    * [Загрузите и установите последнюю версию Azure AD Connect hello](http://go.microsoft.com/fwlink/?linkid=615771). Hello агент работоспособности для синхронизации будет установлен как часть установки hello Azure AD Connect (версии 1.0.9125.0 или более поздней версии).
* Приступая к работе с Azure AD Connect Health для AD DS
    * [Скачайте агент Azure AD Connect Health для AD FS.](http://go.microsoft.com/fwlink/?LinkID=820540)
    * [См. инструкции по установке hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Портал Azure AD Connect Health
портал Azure AD Connect Health Hello отображаются представления предупреждений, наблюдения за производительностью и аналитику использования. Hello https://aka.ms/aadconnecthealth URL-адрес появится toohello главной колонке Azure AD Connect Health. Ее можно считать окном. В главной колонке hello видеть **быстрый запуск**, службы в Azure AD Connect Health, а также дополнительные параметры конфигурации. В разделе hello следующий снимок экрана и краткое описание, следующие за экрана приветствия. После развертывания агентов hello hello служба работоспособности автоматически определяет hello службы, мониторинг работоспособности подключения Azure AD.

> [!NOTE]
> Сведения о лицензировании см. в разделе hello [Azure AD подключения часто задаваемые вопросы о](active-directory-aadconnect-health-faq.md) или hello [странице цен Azure AD](https://aka.ms/aadpricing).
    
![Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Быстрый запуск**: при выборе этого параметра hello **быстрый запуск** открывает колонку. Можно загрузить агент Azure AD Connect Health hello, выбрав **получить средства**. Кроме того, вы также можете получить доступ к документации и оставить отзыв.
* **Службы федерации Active Directory**: этот режим показывает все службы AD FS hello, в настоящий момент отслеживает Azure AD Connect Health. При выборе экземпляра hello колонки, которая открывает отображаются сведения о этого экземпляра службы. Сюда входит обзор, свойства, оповещения, мониторинг и аналитика по использованию. Дополнительные сведения о возможностях hello см. в [с помощью Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (Sync).** В этом разделе отображаются серверы Azure AD Connect, которые в настоящее время отслеживает служба Azure AD Connect Health. При выборе записи hello hello колонки, которая открывает отображаются сведения о серверах Azure AD Connect. Дополнительные сведения о возможностях hello см. в [с помощью Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md).
* **Доменные службы Active Directory**: этот режим показывает всех лесов AD DS hello, в настоящий момент отслеживает Azure AD Connect Health. При выборе леса hello колонки, которая открывает отображаются сведения о этого леса. Эти сведения включают Обзор важную информацию, панель мониторинга hello контроллеры домена, мониторинга состояния репликации hello, оповещениям и мониторингу. Дополнительные сведения о возможностях hello см. в [с помощью Azure AD Connect Health в AD DS](active-directory-aadconnect-health-adds.md).
* **Настройка**: в этом разделе содержатся параметры tooturn hello или выключить следующие:

  - Автоматическое обновление tooautomatically hello Azure AD Connect Health версия агента обновления toohello последнюю: будет автоматически обновляются toohello последние версии hello Azure AD Connect Health Agent по мере появления. Эта функция включена по умолчанию.
  - Разрешить передачу данных Microsoft access tooyour Azure AD directory работоспособности только в целях устранения неполадок: Если эта функция включена, можно увидеть Microsoft hello и те же данные, что вы видите. Эта информация может помочь при устранении неполадок и различных проблем. Эта функция отключена по умолчанию.

## <a name="related-links"></a>Связанные ссылки
* [Установка агента Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Операции Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
* [Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)](active-directory-aadconnect-health-adds.md)
* [Часто задаваемые вопросы об Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health: история выпусков версий](active-directory-aadconnect-health-version-history.md)

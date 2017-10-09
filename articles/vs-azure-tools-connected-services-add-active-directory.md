---
title: "aaaAdding Azure Active Directory с помощью подключенных служб в Visual Studio | Документы Microsoft"
description: "Добавление Azure Active Directory с помощью Visual Studio Добавление подключенных служб hello-диалоговое окно"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f599de6b-e369-436f-9cdc-48a0165684cb
ms.service: active-directory
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: kraigb
ms.openlocfilehash: 26c8f68edf9ec5f7bf65cbab34e4f9b4085ed18d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-an-azure-active-directory-by-using-connected-services-in-visual-studio"></a>Добавление Azure Active Directory с помощью подключенных служб в Visual Studio
Azure Active Directory (Azure AD) позволяет обеспечить единый вход для веб-приложений ASP.NET MVC или проверку подлинности Active Directory в службах веб-API. Аутентификация Azure Active Directory пользователи могут использовать свои учетные записи из Azure Active Directory tooconnect tooyour веб-приложений. преимущества Hello Azure проверки подлинности Active Directory с веб-API относятся Улучшенная защита данных при предоставлении интерфейса API из веб-приложения. С помощью Azure AD у вас toomanage отдельной системой проверки подлинности с собственную учетную запись и управления пользователями.

## <a name="prerequisites"></a>Предварительные требования
- Учетная запись Azure. Если у вас ее нет, [зарегистрируйтесь для работы с бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

### <a name="connect-tooazure-active-directory-using-hello-connected-services-dialog"></a>Подключения tooAzure Active Directory hello подключенных служб с помощью диалогового окна
1. В Visual Studio создайте или откройте проект ASP.NET MVC или проект веб-API ASP.NET.

1. Из hello обозревателе решений щелкните правой кнопкой мыши hello **подключенные службы** узел и в контекстном меню hello, выберите **Добавление подключенных служб**.

1. На hello **подключенные службы** выберите **проверки подлинности в Azure Active Directory**.
   
    ![Страница "Подключенные службы"](./media/vs-azure-tools-connected-services-add-active-directory/connected-services-add-active-directory.png)

1. На hello **Введение** страница hello **настройки Azure AD Authentication** мастера выберите **Далее**.
   
    ![Страница "Введение"](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-1.png)

1. На hello **единого входа на** страница hello **настройки Azure AD Authentication** мастера выберите домен из hello **домена** раскрывающегося списка. Hello список доменов содержит все домены, доступные учетным записям hello, перечисленных в диалоговом окне приветствия параметры учетной записи. В качестве альтернативы можно ввести доменное имя, если вы не нашли в hello один вы ищете, такие как `mydomain.onmicrosoft.com`. Можно выбрать параметр toocreate hello приложения Azure Active Directory или использовать параметры hello из существующего приложения Azure Active Directory. По завершении нажмите кнопку **Далее**.
   
    ![Страница "Единый вход"](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-2.png)

1. На hello **доступ к каталогу** страница hello **настройки Azure AD Authentication** мастера убедитесь, что hello **читать данные каталога** флажок. 
   
    ![Страница "Доступ к каталогу"](./media/vs-azure-tools-connected-services-add-active-directory/configure-azure-ad-wizard-3.png)

1. Выберите **Готово** tooadd hello tooenable кода и ссылки на необходимые конфигурации проекта для проверки подлинности Azure AD. Вы увидите hello домена Active Directory на hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Visual Studio будет отображать [произошедшее](#how-your-project-is-modified) tooshow статьи можно как проект был изменен. Toocheck, что все работает, откройте один из файлов конфигурации изменен hello и убедитесь, что hello параметров, описанных в статье hello существует. 

## <a name="how-your-project-is-modified"></a>Какие изменения произойдут в проекте
При запуске мастера hello, Visual Studio добавляет Azure Active Directory и ссылки на связанные tooyour проекта. Файлы конфигурации и файлы кода в вашем проекте также являются измененный tooadd поддержка Azure AD. Hello конкретные изменения, которые вносятся Visual Studio зависят от типа проекта hello. Подробные сведения о том, как изменяются проекты ASP.NET MVC, см. в статье [Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты MVC)](http://go.microsoft.com/fwlink/p/?LinkID=513809). Эти же сведения о проектах веб-API см. в статье [Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты WebApi)](http://go.microsoft.com/fwlink/p/?LinkId=513810).

## <a name="next-steps"></a>Дальнейшие действия
* [Форум MSDN по Azure Active Directory](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD)
* [Документация по Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [В блоге: Введение tooAzure Active Directory](http://blogs.msdn.com/b/brunoterkaly/archive/2014/03/03/introduction-to-windows-azure-active-directory.aspx)


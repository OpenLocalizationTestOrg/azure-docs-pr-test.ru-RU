---
title: "aaaAdding мобильных служб с помощью подключенных служб в Visual Studio | Документы Microsoft"
description: "Добавление мобильных служб с помощью Visual Studio Добавление подключенных служб hello-диалоговое окно"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Добавление мобильных служб с помощью подключенных служб Visual Studio
Visual Studio 2015 позволяет подключать tooAzure мобильных служб с помощью hello **добавление подключенной службы** диалогового окна. Подключиться можно из любого приложения C#, любого приложения JavaScript или кроссплатформенного приложения Cordova. После подключения вы сможете создавать и использовать данные, создавать настраиваемые API и запланированные задания или добавлять поддержку push-уведомлений.  Hello подключенных служб операция добавляет все соответствующие ссылки и код подключения. Кроме того, можно использовать встроенную поддержку проверки подлинности через такие популярные системы, как Azure AD, Facebook, Twitter и учетные записи Майкрософт.

## <a name="supported-project-types"></a>Поддерживаемые типы проектов
> [!NOTE]
> В Visual Studio 2015 добавление проектов универсальное приложение для Windows (Windows 10) tooa мобильных служб Azure с помощью диалогового окна hello Добавление подключенных служб не поддерживается. Можно добавить мобильные службы Azure, установив соответствующие пакеты hello помощью hello диспетчера пакетов NuGet для проекта.
> 
> 

Можно использовать диалоговое окно tooconnect подключенные службы hello tooAzure мобильных служб в следующие типы проекта hello.

* Windows 8.1 Store, Phone и универсальные приложения .NET;
* Windows 8.1 Store, Phone и универсальные приложения JavaScript;
* проекты, созданные с помощью инструментов Visual Studio для Apache Cordova.

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Подключение tooAzure мобильных служб с помощью диалогового окна hello Добавление подключенных служб
1. Убедитесь в наличии учетной записи Azure. Если у вас нет учетной записи Azure, вы можете зарегистрироваться и получить [бесплатную пробную версию](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Откройте hello **Добавление подключенных служб** диалоговое окно.
   
   * Для приложений .NET, откройте проект в Visual Studio, Привет открыть контекстное меню для hello **ссылки** узел в обозревателе решений и выберите **добавление подключенной службы**
     
        ![Подключение tooAzure мобильной службы](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Для проектов приложений Apache Cordova, откройте проект в Visual Studio, Привет открыть контекстное меню для узла hello проекта в обозревателе решений и выберите **добавление подключенной службы**.
3. В hello **добавление подключенной службы** диалогового окна выберите **мобильных служб Azure**, а затем выберите hello **Настройка** кнопки. Может быть запрос toolog в Azure, если это еще не сделано.
   
    ![Добавление мобильной службы Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. В hello **мобильных служб Azure** диалогового окна выберите существующую мобильную службу, если таковой имеется. Если вам требуется toocreate новой мобильной службы Azure, выполните процедуру hello ниже toodo таким образом. В противном случае пропустите toohello следующий шаг.
   
    toocreate новой учетной записи мобильной службы:
   
   1. Выберите hello ** Create Service ** ссылке hello нижней части диалогового окна «hello».
       ![Добавление новой мобильной подключенной службы](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. На hello **Создание мобильной службы** диалоговое окно, можно выбрать серверной мобильной службы JavaScript или серверную мобильную службу .NET из hello **среды выполнения** раскрывающегося списка. 
      
       ![Создание мобильной службы](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Серверная служба JavaScript — простая и эффективная. При создании серверной мобильной службы JavaScript hello серверный код JavaScript хранится в облаке hello, но скрипты сервера можно изменить с помощью обозревателя серверов или портала управления Azure hello. 
      
       Серверной мобильной службы .NET предоставляет все возможности hello и гибкость веб-API и Entity Framework. При создании серверной мобильной службы .NET проект создается автоматически и добавлены tooyour решения. 
   3. Выберите hello **область** которых требуется мобильной службы hello и затем введите имя пользователя и пароль для сервера hello.
   4. После ввода всех необходимых hello сведения, выберите hello **создать** кнопку toocreate hello мобильной службы.
   5. Hello новой мобильной службы должны отображаться в списке служб hello на hello **мобильных служб Azure** диалоговое окно. Выберите в списке hello hello новой мобильной службы, а затем выберите hello **добавить** кнопку tooadd hello службы tooyour проекта.
5. Просмотрите hello начальной страницы, которая появляется и узнайте, как проект был изменен. Страница "Начало работы" открывается в браузере каждый раз, когда добавляется подключенная служба. Вы можете просмотреть hello предлагаемые дальнейшие действия и примеры кода или переключитесь toosee страницы произошедшее toohello какие ссылки были добавлены tooyour проекта, и как были изменены файлы кода и конфигурации.
6. Руководствуясь образцы кода hello, написания кода tooaccess мобильной службе!

## <a name="how-your-project-is-modified"></a>Какие изменения произойдут в проекте
Изменение проекта в Visual Studio зависит от типа проекта hello. Сведения о клиентских приложениях C# см. в статье [What happend – C# projects](http://go.microsoft.com/fwlink/p/?LinkId=513119) (Что произошло: проекты C#). Сведения о клиентских приложениях JavaScript см. в статье [What happened – JavaScript projects](http://go.microsoft.com/fwlink/p/?LinkId=513120) (Что произошло: проекты JavaScript). Сведения о приложениях Cordova см. в статье [What happend – Cordova projects](http://go.microsoft.com/fwlink/p/?LinkId=513116) (Что произошло: проекты Cordova).

## <a name="next-steps"></a>Дальнейшие действия
Задавайте вопросы и получайте справку: 

* [Форум MSDN: мобильные службы Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Мобильные службы Azure в блоге группы разработчиков Microsoft Azure hello](https://azure.microsoft.com/blog/topics/mobile/)
* [Мобильные службы Azure на сайте azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Документация к мобильным службам Azure на сайте azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)


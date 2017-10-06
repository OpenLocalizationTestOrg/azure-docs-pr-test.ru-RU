---
title: "aaaCreate WordPress веб-приложения в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как toocreate новый Azure веб-приложения для hello портал Azure с помощью блога WordPress."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Создание веб-приложения WordPress в службе приложений Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

В этом учебнике показано, как toodeploy блог WordPress сайта из hello Azure Marketplace.

Закончено hello учебника вы получите свой собственный узел блога WordPress вверх и работающих в облаке hello.

![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Вы узнаете:

* Как toofind шаблоном приложений в Azure Marketplace hello.
* Как toocreate веб-приложения в приложение Azure службы основан на шаблоне hello.
* Как параметры службы приложений Azure tooconfigure для hello нового веб-приложения и базы данных.

Hello Azure Marketplace делает доступными широкий ряд популярных веб-приложений, разработанных корпорацией Майкрософт, сторонних компаний и инициативы по открытым исходным кодом. веб-приложения Hello построены на широкий набор наиболее популярных платформ, таких как [PHP](/develop/nodejs/) в этом примере WordPress [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), и [Python](/develop/python/), tooname несколько. веб-приложение из Azure Marketplace hello только необходимого программного обеспечения является hello браузера, используемого для hello hello toocreate [портала Azure](https://portal.azure.com/). 

Hello сайта WordPress, развертываемые в этом учебнике используется MySQL для hello базы данных. При необходимости используйте tooinstead базы данных SQL для базы данных hello. в разделе [Nami проекта](http://projectnami.org/). **Проект Nami** также доступна через hello Marketplace.

> [!NOTE]
> toocomplete этого учебника необходима учетная запись Microsoft Azure. Если у вас нет учетной записи, можно [активировать преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/). Там вы сможете немедленно создать кратковременное начальное веб-приложение в службе приложений. Для этого не потребуется ни кредитная карта, ни какие-либо обязательства.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Выбор WordPress и настройка для службы приложений Azure
1. Войдите в toohello [портала Azure](https://portal.azure.com/).
2. Нажмите кнопку **Создать**.
   
    ![Создать][5]
3. Выполните поиск по запросу **WordPress**, а затем щелкните приложение **WordPress**. При желании toouse базы данных SQL вместо MySQL поиск **Nami проекта**.
   
    ![WordPress из списка][7]
4. Прочитав описание hello приложение hello WordPress, нажмите кнопку **создать**.
   
    ![Создание](./media/web-sites-php-web-site-gallery/create.png)
5. Введите имя для веб-приложения hello в hello **веб-приложение** поле.
   
    Это имя должно быть уникальным в домене azurewebsites.net hello, так как hello URL-адрес веб-приложения hello {имя}. azurewebsites.net. Если вы вводите имя hello не является уникальным, в текстовом поле hello отображается красный восклицательный знак.
6. Если у вас несколько подписок, выберите hello один требуется toouse. 
7. Выберите **группу ресурсов** или создайте новую.
   
    Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Выберите или создайте **план службы приложений или расположение** .
   
    Дополнительные сведения о планах службы приложений см. в [подробном обзоре планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).    
9. Нажмите кнопку **базы данных**, а затем в hello **новую базу данных MySQL** колонке предоставляют hello необходимые значения для настройки базы данных MySQL.
   
    а. Введите новое имя или оставьте имя по умолчанию hello.
   
    b. Оставьте hello **тип базы данных** значение слишком**Shared**.
   
    c. Выберите местоположения, как и в случае hello, с которой вы выбрали для веб-приложения hello приветствия.
   
    d. Выберите ценовую категорию. Для этого учебника подходит «Меркурий» (бесплатно с минимумом разрешенных подключений и места на диске).
10. В hello **новую базу данных MySQL** колонка, щелкните **ОК**. 
11. В hello **WordPress** колонки, примите условия hello и нажмите кнопку **создать**. 
    
     ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/configure.png)
    
     Служба приложений Azure создает веб-приложения hello, обычно меньше, чем через минуту. Можно отслеживать ход выполнения hello, щелкнув значок колокольчика hello hello верхней части страницы портала hello.
    
     ![Индикатор хода выполнения](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Запуск веб-приложения WordPress и управление им
1. После завершения создания приложения hello web перейдите в группе ресурсов Azure Portal toohello hello в которой вы создали приложение hello, и вы увидите hello веб-приложения и базы данных hello.
   
    Hello дополнительных ресурсов с использованием значок лампочки hello — [Application Insights](/services/application-insights/), который предоставляет службы мониторинга для веб-приложения.
2. В hello **группы ресурсов** колонка, щелкните строку приложения hello web.
   
    ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. В колонке приложения hello Web щелкните **Обзор**.
   
    ![URL-адрес сайта][browse]
4. В hello WordPress **приветствия** введите hello данные конфигурации, необходимые WordPress и нажмите кнопку **Установка WordPress**.
   
    ![Настройка WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Вход с использованием учетных данных hello, вы создали на hello **приветствия** страницы.  
6. Откроется страница панели мониторинга вашего сайта.    
   
    ![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Дальнейшие действия
Вы знаете, как toocreate и развертывать веб-приложения PHP из галереи hello. Дополнительные сведения об использовании PHP в Azure см. в разделе hello [Центр разработчика PHP](/develop/php/).

Дополнительные сведения о том, как toowork для приложения службы веб-приложений, см. ссылки hello hello левая сторона страницы приветствия (для широкого обозревателя windows) или в начале hello страницы приветствия (для обычных обозревателя windows). 

## <a name="whats-changed"></a>Изменения
* Руководство по toohello изменений из tooApp веб-сайтов службы, см. [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png

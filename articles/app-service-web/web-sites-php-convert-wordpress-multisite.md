---
title: "aaaConvert tooMultisite WordPress в службе приложений Azure"
description: "Узнайте, как tootake существующего веб-приложения WordPress создана с помощью коллекции hello в Azure и преобразовать его tooWordPress многосайтового развертывания"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Преобразовать tooMultisite WordPress в службе приложений Azure
## <a name="overview"></a>Обзор
*Автор [Бен Лобо (Ben Lobaugh)][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

В этом учебнике вы узнаете, как tootake существующего веб-приложения WordPress создана с помощью коллекции hello в Azure и установить его в нескольких сайтах WordPress convert. Кроме того вы узнаете, как tooassign tooeach пользовательского домена из hello subsites в текущей установки.

Предполагается наличие существующей установки WordPress. Если этого не сделать, следуйте инструкциям, hello в [создать веб-сайт WordPress из коллекции hello в Azure][website-from-gallery].

Преобразование существующего WordPress tooMultisite установки одного сайта обычно достаточно проста, и многие hello здесь начального действия берутся непосредственно из hello [создать сеть] [ wordpress-codex-create-a-network] страницы приветствия [WordPress Codex](http://codex.wordpress.org).

Давайте приступим.

## <a name="allow-multisite"></a>Включение функциональности мультисайта
Необходимо сначала tooenable с несколькими сайтами через hello `wp-config.php` файл с hello **WP\_Разрешить\_МНОГОСАЙТОВОГО** константой. Существует два метода tooedit файлам веб-приложения: hello первого — по протоколу FTP и hello секунду из Git. Если вы не знакомы с toosetup любой из этих методов можно найти toohello следующие учебники:

* [Веб-сайт PHP с MySQL и FTP][website-w-mysql-and-ftp-ftp-setup]
* [Веб-сайт PHP с MySQL и Git][website-w-mysql-and-git-git-setup]

Откройте hello `wp-config.php` и добавьте следующее hello выше hello файла с редактором hello по своему выбору `/* That's all, stop editing! Happy blogging. */` строки.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Убедиться, что файл toosave hello и отправьте его назад toohello server!

## <a name="network-setup"></a>Настройка сети
Войдите в toohello *wp-admin* область веб-приложения и вы должны увидеть новый элемент в списке hello **средства** меню с именем **Настройка сети**. Нажмите кнопку **Настройка сети** и заполните hello подробные сведения о сети.

![Экран настройки сети][wordpress-network-setup]

В этом учебнике используется hello *вложенные каталоги* сайта схемы, так как он всегда должна работать, и мы будет выполняться Настройка пользовательских доменов для каждого дочернего узла далее в учебнике hello. Однако должно быть возможно toosetup установить дочерний домен, если сопоставить домен через hello [портала Azure](https://portal.azure.com) и неправильная настройка подстановки DNS.

Дополнительные сведения на виртуальном сервере поддомене подкаталога настройки разделе hello [типы сети с несколькими сайтами] [ wordpress-codex-types-of-networks] статьи на hello WordPress Codex.

## <a name="enable-hello-network"></a>Включить hello сети
Hello сети настроены в базе данных hello, но есть один остальные шаг tooenable hello сети функциональные возможности. Завершение hello `wp-config.php` параметры и убедитесь, `web.config` должным образом направляет каждого сайта.

После нажатия кнопки hello **установить** кнопку на hello *Настройка сети* страницы WordPress попытается tooupdate hello `wp-config.php` и `web.config` файлов. Тем не менее следует всегда проверять tooensure hello hello файлы обновления выполнены успешно. В противном случае этот экран появятся hello необходимые обновления. Изменение и сохранение файлов hello.

После внесения этих обновлений, необходимо будет toolog ожидания и журналов назад в панель мониторинга администратора wp hello.

Теперь следует дополнительное меню на панели администрирования hello с меткой **личных узлов**. Это меню позволяет toocontrol к новой сети через hello **администратора сети** панели мониторинга.

## <a name="adding-custom-domains"></a>Добавление пользовательских доменов
Hello [сопоставления домена MU WordPress] [ wordpress-plugin-wordpress-mu-domain-mapping] подключаемый модуль становится сайтом tooany просто tooadd пользовательских доменов в сети. Чтобы подключаемый модуль toooperate hello надлежащим образом, необходимо toodo дополнительной настройки на hello портала, а также на сайте регистратора домена.

## <a name="enable-domain-mapping-toohello-web-app"></a>Включение домена сопоставление toohello веб-приложения
Hello **Free** [службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) плана режим не поддерживает добавление tooWeb пользовательских доменов приложений. Вам потребуется tooswitch слишком**Shared** или **Стандартная** режим. toodo это:

* Войдите в портал Azure toohello и найдите веб-приложения. 
* Щелкните hello **масштабировать** вкладке **параметры**.
* В разделе **Общие** выберите *Общий* или *Стандартный*.
* Нажмите кнопку **Сохранить**

Может получать сообщение, запрашивающее tooverify изменение hello и соглашаюсь веб-приложения теперь может привести к расходам, в зависимости от использования и hello другие конфигурации, заданные.

Занимает несколько секунд новых параметров tooprocess hello, теперь является toostart подходящий момент, настройка вашего домена.

## <a name="verify-your-domain"></a>Проверка домена
Прежде чем веб-приложения Azure позволяют toomap сайта toohello домена, необходимо сначала tooverify наличие toomap hello hello авторизации домена. toodo таким образом, необходимо добавить новую запись CNAME tooyour записей DNS.

* Войдите в диспетчере DNS домена tooyour
* Создайте новую запись CNAME *awverify*
* Точка *awverify* слишком*awverify. YOUR_DOMAIN.azurewebsites.NET*

Он может занять некоторое время для изменения toogo hello DNS в полную силу, hello следующие шаги не работают немедленно, начинаем cup кофе, а затем вернуться и повторите попытку.

## <a name="add-hello-domain-toohello-web-app"></a>Добавить hello домена toohello веб-приложения
Нажмите кнопку возврата tooyour веб-приложения через портал Azure hello **параметры**, а затем нажмите кнопку **пользовательские домены и SSL**.

Здравствуйте, когда *параметры SSL* , отображается, вы увидите hello поля, где вы будете вводить все домены hello, которых вы хотите tooassign tooyour веб-приложения. Если домена нет в списке, он будет недоступен для сопоставления внутри WordPress, независимо от того, как настроен hello домена DNS.

![Диалоговое окно "Управление пользовательскими доменами"][wordpress-manage-domains]

После ввода вашего домена в текстовое поле hello, Azure проверит hello запись CNAME, созданную ранее. Если не был полностью распространяются hello DNS, отобразится красный индикатор. Если все успешно выполнено, появится зеленый флажок. 

Запишите IP-адрес в списке внизу hello hello диалоговое окно приветствия. Этот toosetup hello записи потребуются для вашего домена.

## <a name="setup-hello-domain-a-record"></a>Настройка записи A hello домена
Если hello предыдущие шаги выполнены успешно, теперь может назначить hello домена tooyour веб-приложение Azure через запись DNS типа. 

Это важные toonote здесь веб-приложениях Azure принятие CNAME и-записи, однако вы *должен* использовать сопоставление типа записей tooenable соответствующий домен. Запись CNAME переадресовывать невозможно tooanother CNAME, являющееся автоматически созданные Azure с YOUR_DOMAIN.azurewebsites.net.

С помощью hello IP-адрес из предыдущего шага hello, возвращают tooyour диспетчера DNS и установки hello С IP-адресом toothat toopoint записей.

## <a name="install-and-setup-hello-plugin"></a>Установка и Настройка подключаемого модуля hello
WordPress многосайтового развертывания в настоящее время не поддерживает пользовательские домены с toomap встроенный метод. Однако есть подключаемый модуль вызывается [сопоставления домена MU WordPress] [ wordpress-plugin-wordpress-mu-domain-mapping] , добавляющий функции hello для вас. Войдите в toohello администратора сети часть веб-узла и установить hello **сопоставления домена MU WordPress** подключаемого модуля.

После установки и активации hello подключаемого модуля, посетите **параметры** > **сопоставления домена** подключаемый модуль tooconfigure hello. В первом текстовом поле hello *IP-адрес сервера*, входной hello IP-адрес, используемый toosetup hello запись для домена hello. Задайте *параметры домена* нужен (по умолчанию hello допустимы часто) и нажмите кнопку **Сохранить**.

## <a name="map-hello-domain"></a>Сопоставление домена hello
Посетите hello **мониторинга** hello узла нужно toomap hello домена. Щелкните **средства** > **сопоставления домена** и типа hello нового домена в hello текстовое поле и нажмите кнопку **добавить**.

По умолчанию hello нового домена будет перезаписанного toohello домена сайта автоматически. Toohave все трафик toohello новый домен, установите флажок hello *основной домен для этого блога* поле перед сохранением. Можно добавить неограниченное количество доменов tooa узла, но можно использовать только один основной.

## <a name="do-it-again"></a>Повторение процедуры
Azure веб-приложения разрешает tooadd неограниченное количество доменов tooa веб-приложения. tooadd другой домен, необходимо будет tooexecute hello **проверки домена** и **установки записи домен А hello** разделы для каждого домена.    

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png



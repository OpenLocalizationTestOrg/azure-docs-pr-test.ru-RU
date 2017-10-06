---
title: "aaaGet к работе с интеграцией журналов Azure | Документы Microsoft"
description: "Узнайте, как tooinstall hello Azure входа службы интеграции и интегрировать журналов из хранилища Azure, журналы аудита Azure и оповещения центра безопасности Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Интеграция журналов Azure с ведением журнала системы диагностики Azure и пересылкой событий Windows
Интеграция Azure журнала (AzLog) позволяет toointegrate необработанные журналы по вашим ресурсам Azure в вашей локальной системы сведения о безопасности и управления событий (SIEM). Такая интеграция упрощает возможных toohave безопасности единой панели мониторинга для всех средств, в локальной или в облаке hello, можно вычислять статистические значения, сопоставлять, анализ и предупреждения для событий безопасности, связанных с приложениями.
>[!NOTE]
Дополнительные сведения об интеграции Azure журнала можно просмотреть hello [Общие сведения об интеграции Azure журнала](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

Эта статья поможет вам приступить к работе с интеграцией журналов Azure, сосредоточившись на установку hello hello Azlog службы и интеграция hello службы диагностики Azure. Hello службы интеграции Azure журнала должен быть доступ toocollect сведения журнала событий Windows из hello канал событий безопасности Windows из виртуальных машин, развернутых в Azure IaaS. Это очень напоминает слишком «Пересылка событий», могут использованы в локальной среде.

>[!NOTE]
>Hello возможность toobring hello выходные данные журналов Azure интеграции в toohello hello SIEM сам предоставляются SIEM. См. в разделе статьи hello [интеграции Integration журнала Azure с локальной системы SIEM](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) для получения дополнительной информации.

clear - toobe hello службы интеграции Azure журнала выполняется на физический или виртуальный компьютер, использующего hello Windows Server 2008 R2 или более поздней версии операционной системы (Windows Server 2012 R2 или Windows Server 2016 являются предпочтительными).

Hello физического компьютера можно запустить локально (или на сайте поставщика услуг размещения). При выборе службы интеграции Azure журнала hello toorun на виртуальной машине, виртуальная машина может быть расположено локально или в общедоступном облаке, например Microsoft Azure.

Hello физической или виртуальной машине под управлением службы интеграции Azure журнала hello требует подключения к сети toohello общедоступное облако Azure. Действия, описанные в этой статье приведены сведения о конфигурации hello.

## <a name="prerequisites"></a>Предварительные требования
Как минимум Установка hello AzLog требует hello следующих элементов:
* **Подписка Azure**. Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной учетной записи](https://azure.microsoft.com/free/).
* Объект **учетной записи хранилища** , можно использовать для ведения журнала диагностики Windows Azure (можно использовать предварительно настроенный учетную запись или создайте новую — будет показано как tooconfigure hello учетной записи хранилища, далее в этой статье)
  >[!NOTE]
  В зависимости от ситуации учетная запись хранения может не потребоваться. Для hello сценария диагностики Azure, описанные в данной статье, которую он необходим.
* **Две системы**: компьютер, который будет выполняться служба интеграции Azure журнала hello и компьютере, который будет отслеживаться и иметь его ведения журнала, передаваемых toohello Azlog службы компьютера.
   * Компьютер, будет toomonitor — это виртуальная машина, работающая как [виртуальной машине Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Компьютер, который будет выполняться служба интеграции hello Azure журнала; Этот компьютер будет собирать все данные журнала hello, которые позже будут импортированы в систему SIEM.
    * Эта система может размещаться в локальной среде или в облаке Microsoft Azure.  
    * Он должен toobe x64 под управлением версии Windows server 2008 R2 с пакетом обновления 1 или более поздней версии и платформа .NET Framework 4.5.1, установленная. Можно определить версию .NET hello, установленные в следующей статье hello под названием [как: определение .NET Framework версий установленных](https://msdn.microsoft.com/library/hh925568)  
    Она должна иметь подключения к учетной записи хранилища Azure toohello используется для диагностики Azure. Далее в этой статье будут даны указания по проверке этого подключения.

Для быстрой демонстрации hello процесс создания виртуальной машины с помощью портала Azure hello взгляните на hello видео ниже.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Рекомендации по развертыванию
При тестировании интеграции журналов Azure можно использовать любой системе, которая соответствует hello минимальные требования к операционной системе. Тем не менее для типа hello среды рабочей нагрузки может потребовать tooplan для масштабирования вверх или вниз.

Можно запустить несколько экземпляров службы интеграции Azure журнала hello (один экземпляр на физическом компьютере или виртуальной машине), при высокой событий тома. Кроме того можно балансировать нагрузку, учетные записи хранения диагностики Azure для Windows (WAD) и hello число экземпляров toohello tooprovide подписки должны быть основаны на емкость.
>[!NOTE]
В данный момент не имеет конкретные рекомендации для при tooscale out экземпляров Azure журнала машины интеграции (т. е. машин, работающих под управлением службы интеграции hello Azure log) или учетным записям хранения или подписки. Решения о масштабировании следует принимать, исходя из наблюдаемой производительности в каждой из этих областей.

Также имеется tooscale параметр по hello вверх toohelp службы интеграции Azure журнала hello повышения производительности. Hello следующие метрики производительности может помочь при оценке hello машин, что выбранная служба интеграции toorun hello Azure log:
* На компьютере с 8 процессорами (ядрами) один экземпляр Azlog Integrator может обрабатывать около 24 млн событий в день (примерно 1 млн в час).

* На компьютере с 4 процессорами (ядрами) один экземпляр Azlog Integrator может обрабатывать около 1,5 млн событий в день (примерно 62,5 тыс. в час).

## <a name="install-azure-log-integration"></a>Установка интеграции журналов Azure
tooinstall журнала интеграции Azure нужно toodownload hello [интеграции Azure log](https://www.microsoft.com/download/details.aspx?id=53324) файл установки. Выполните процедуру установки hello и решите, следует tooMicrosoft сведения tooprovide телеметрии.  

![Экран установки с установленным флажком для передачи данных телеметрии](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Мы не рекомендуем данные телеметрии Майкрософт toocollect. Сбор данных телеметрии можно отключить, сняв этот флажок.
>


службы интеграции Azure журнала Hello собирает данные телеметрии с hello компьютер, на котором он установлен.  

Собираются следующие данные телеметрии:

* исключения, возникающие при выполнении интеграции журналов Azure;
* Метрики о количестве hello запросов и обработки событий
* статистические данные использования параметров командной строки Azlog.exe.

процесс установки Hello рассматривается hello видео ниже.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Действия после установки и проверка
После выполнения подпрограммы базовая настройка hello, вы будете готовы шаг tooperform post установке и проверке действия:
1. Откройте окно PowerShell с повышенными привилегиями и перейдите слишком**c:\Program Files\Microsoft Azure журнала интеграции**
2. Сначала необходимо tootake Hello — tooget hello, импортированы AzLog командлетов. Это можно сделать, запустив сценарий hello **LoadAzlogModule.ps1** (уведомление hello «. \» в следующую команду hello). Введите **.\LoadAzlogModule.ps1** и нажмите клавишу **ВВОД**.  
Вы увидите нечто похожее на что будет отображаться в приведенном ниже рисунке hello. </br></br>
![Экран установки с установленным флажком для передачи данных телеметрии](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Теперь вам требуется toouse AzLog tooconfigure конкретную среду Azure. «Среду Azure» — hello «type» центра обработки данных Azure облачной toowork с нужным. Хотя существует несколько сред Azure в настоящее время, либо являются параметры, в настоящее время соответствующие hello **облачной** или **AzureUSGovernment**.   В среде PowerShell с повышенными привилегиями убедитесь, что вы находитесь в каталоге **c:\program files\Microsoft Azure Log Integration\**. </br></br>
    Один раз, выполните команду hello. </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (для Azure для коммерческих организаций)

      >[!NOTE]
      После успешного завершения команды hello не получит все отзывы.  Если требуется toouse hello государственных Azure облака, следует использовать **AzureUSGovernment** (для hello - переменная) для hello облака правительства США. Другие облака Azure в настоящее время не поддерживаются.  
4. Чтобы осуществлять мониторинг системы необходимо будет hello имя учетной записи хранения hello используется для диагностики Azure.  Hello портал Azure перейдите слишком**виртуальные машины** и выполните поиск hello виртуальную машину, будут отслеживаться. В hello **свойства** выберите **параметров диагностики**.  Щелкните **агента** и запишите указанное имя учетной записи хранения hello. Оно потребуется вам в дальнейшем.
![Параметры системы диагностики Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Параметры системы диагностики Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Если мониторинг был отключен во время создания виртуальной машины вам будет предоставлена hello параметр tooenable его, как показано выше.
5. Теперь мы перейдем нашей внимания задней toohello машины интеграции журналов Azure. Мы должны tooverify наличие toohello подключения к учетной записи хранилища из системы hello установленным интеграции журналов Azure. Hello физическом компьютере или виртуальной машине под управлением hello журнала интеграции Azure, служба должна получить доступ к toohello учетной записи хранения tooretrieve данных, регистрируемых функцией диагностики Azure, настроенной на каждом hello мониторинг системы.  
  1. Скачать Azure Storage Explorer можно [отсюда](http://storageexplorer.com/).
  2. Выполните процедуру установки hello
  3. После завершения установки hello щелкните **Далее** и оставьте флажок hello **запустите обозреватель хранилищ Microsoft Azure** проверяется.  
  4. Войдите в tooAzure.
  5. Убедитесь, что отображаются hello учетной записи хранилища, который настроен для диагностики Azure.  
![учетные записи хранения;](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Обратите внимание, что в учетной записи хранения отображается несколько элементов. Один из них — **Таблицы**. В элементе **Таблицы** отображается таблица **WADWindowsEventLogsTable**. </br></br>
   ![Учетные записи хранения](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Интеграция ведения журналов диагностики Azure
На этом шаге вы настроите hello компьютере, работающем под управлением hello Azure журнала tooconnect toohello хранилища учетной записи службы интеграции, содержащий файлы журнала hello.
toocomplete этот шаг, нам нужно будет заранее несколько вещей.  
* **FriendlyNameForSource:** понятное имя, могут быть применены toohello учетной записи хранилища, настроенного toostore сведения о виртуальной машине hello из системы диагностики Azure
* **StorageAccountName:** это имя учетной записи хранилища hello, указанный при настройке Azure diagnotics hello.  
* **StorageKey:** : hello ключ хранилища для учетной записи хранения hello хранения hello сведения диагностики Azure для этой виртуальной машины.  

Выполните следующий ключ хранилища hello tooobtain действия hello.
 1. Обзор toohello [портал Azure](http://portal.azure.com).
 2. В области переходов hello hello Azure в консоли и прокрутите вниз toohello **несколько служб.**

 ![Пункт "Больше служб"](./media/security-azure-log-integration-get-started/more-services.png)
 3. Введите **хранения** в hello **фильтра** текстовое поле. Щелкните **Учетные записи хранения** (этот элемент появится после ввода текста **Учетные записи хранения**).

   ![Поле фильтра](./media/security-azure-log-integration-get-started/filter.png)
 4. Появится список учетных записей хранения, дважды щелкните hello учетной записи, что вы присвоили tooLog хранилища.

   ![Список учетных записей хранения](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Щелкните **ключи доступа** в hello **параметры** раздела.

  ![ключи доступа](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Копировать **key1** и поместить его в безопасном месте, доступном для следующего шага hello.

   ![Два ключа доступа](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. На сервере hello установленного журнала интеграции Azure откройте командную строку (Обратите внимание, что мы используем окно командной строки с повышенными здесь, не консоли PowerShell с повышенными).
 8. Перейдите в слишком**c:\Program Files\Microsoft Azure журнала интеграции**
 9. Запустите ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> Например ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` при желании tooshow идентификатор подписки hello вверх в событии hello XML Добавьте понятное имя идентификатора подписки toohello hello: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` или, например,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Подождите, too60 минут, а затем просмотрите hello события, которые извлекаются из учетной записи хранилища hello. tooview, откройте **средство просмотра событий > журналы Windows > перенаправленных событий** на Azlog интегратор hello.

Здесь вы увидите, что видео, идущие через hello шаги, описанные выше.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Что делать, если данные не отображаются в папке hello перенаправленных событий?
Если через час после данных не отображаются в hello **перенаправленных событий** папку, затем:

1. Проверьте hello машины работающей hello интеграции Azure журнала службы и убедитесь, что он имеет доступ к Azure. подключение к tootest, попробуйте tooopen hello [портал Azure](http://portal.azure.com) из браузера hello.
2. Убедитесь, что учетная запись пользователя hello **Azlog** имеет разрешение на запись для папки hello **users\Azlog**.
  <ol type="a">
   <li>Откройте **проводник** .</li>
  <li> Перейдите в слишком**c:\users** </li>
  <li> Щелкните правой кнопкой мыши папку **c:\users\Azlog** .</li>
  <li> Щелкните **Безопасность**  .</li>
  <li> Щелкните **NT Service\Azlog** и проверки разрешений учетной записи hello hello. Если на этой вкладке отсутствует учетная запись hello, или если hello соответствующие разрешения не в настоящее время отображения могут предоставлять hello права учетной записи на этой вкладке.</li>
  </ol>
3.Убедитесь, что учетная запись хранения hello, добавлены в команде hello **добавить источник Azlog** отображается при запуске команды hello **Azlog исходного списка**.
4. Go слишком**средство просмотра событий > журналы Windows > приложения** toosee, если имеются ошибки, полученные от интеграции Azure log hello.


Если возникли проблемы во время установки hello и конфигурации, откройте [запрос на получение поддержки](../azure-supportability/how-to-create-azure-support-request.md)выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.

Другой вариант поддержки — hello [форум MSDN интеграции Azure журнала](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Здесь hello сообщества может поддерживать друг с другом с вопросы, ответы, советы и рекомендации по как tooget hello наиболее интеграционном журналов Azure. Кроме того команды hello интеграции журналов Azure отслеживает этот форум и поможет всякий раз, когда мы можем.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о журнале интеграции Azure, см. следующие документы hello.

* [Служба интеграции журналов Microsoft Azure для журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324) — посетите Центр загрузки, чтобы получить дополнительные сведения, изучить требования к системе и получить инструкции по установке службы интеграции журналов Azure.
* [Введение tooAzure журнала интеграции](security-azure-log-integration-overview.md) — в этом документе представлены интеграцию tooAzure журнала, его основные возможности и как он работает.
* [Действия по настройке партнера](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — в этой записи блога показано, как tooconfigure Azure журнала toowork интеграция с решениями партнеров Splunk и разработанное HP, IBM QRadar. Это наш в настоящее время рекомендации на как tooconfigure hello SIEM компонентов. Обратитесь сначала к своему поставщику SIEM для получения дополнительных сведений.
* [Azure log integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) (Служба интеграции журналов Azure: часто задаваемые вопросы) — эта статья содержит ответы на часто задаваемые вопросы об интеграции журналов Azure.
* [Интеграция центра обеспечения безопасности интеграции журнала предупреждений с помощью Azure](../security-center/security-center-integrating-alerts-with-log-integration.md) — в этом документе показано, как оповещения центра обеспечения безопасности toosync, вместе с событиями безопасности виртуальной машины, собранные диагностики Azure и Azure журналы действий, с помощью аналитики журналов или решения SIEM.
* [Новые возможности диагностики Azure и журналы аудита Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) — в этой записи блога вводит tooAzure журналы аудита и другие средства, помогающие анализировать hello операций с ресурсами Azure.

---
title: "aaaCreate классической виртуальной Машины Azure под управлением MySQL | Документы Microsoft"
description: "Создание виртуальной машины Azure под управлением Windows Server 2012 R2 и hello базы данных MySQL, с помощью hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Установка MySQL на виртуальную машину, созданную с помощью hello классической модели развертывания под управлением Windows Server 2016
[MySQL](https://www.mysql.com) является популярной базой данных SQL с открытым исходным кодом. В этом учебнике показано как tooinstall и выполнения hello **сообщества версия MySQL 5.7.18** как MySQL Server на виртуальной машине под управлением **Windows Server 2016**. Рабочая процедура для других версий MySQL или Windows Server может немного отличаться.

Инструкции по установке MySQL в Linux см.: [как tooinstall MySQL в Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Создание виртуальной машины Windows Server 2016
Если у вас еще нет виртуальной Машины под управлением Windows Server 2016, можно использовать это [учебника](./tutorial.md) toocreate hello виртуальной машины.

## <a name="attach-a-data-disk"></a>Присоединение диска данных
После создания виртуальной машины hello, при необходимости можно присоединить диск данных. Добавление диска данных рекомендуется для рабочих нагрузок и tooavoid заканчивается место на hello диска ОС (C:), в том числе hello операционной системы.

В разделе [как tooattach данных на диске виртуальной машины Windows tooa](../attach-managed-disk-portal.md) и следуйте инструкциям hello присоединение пустого диска. Задан hello узла кэша слишком**нет** или **только для чтения**.

## <a name="log-on-toohello-virtual-machine"></a>Войдите на виртуальную машину toohello
После этого вы будете [входа на виртуальную машину toohello](./connect-logon.md) , вы можете установить MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Установить и запустить на виртуальной машине hello сообщества MySQL Server
Выполните эти шаги tooinstall, настройки и запуска hello сообщества версии MySQL Server:

> [!NOTE]
> При загрузке элементов с помощью Internet Explorer, можно задать hello IE **конфигурация усиленной безопасности** tooOff и упрощения процесса скачивания hello. Из меню "Пуск" hello, выберите административные средства/Manager или локального сервера, а затем нажмите кнопку IE **конфигурация усиленной безопасности** и задайте tooOff конфигурации hello).
>
>

1. После подключения toohello виртуальной машины, с помощью удаленного рабочего стола, щелкните **Internet Explorer** на начальном экране приветствия.
2. Выберите hello **средства** в hello правого верхнего угла (значок hello cogged колесико мыши), а затем нажмите **обозревателя**. Щелкните hello **безопасности** щелкните hello **надежных узлов** значка и нажмите кнопку hello **сайтов** кнопки. Добавьте http://*.mysql.com toohello список надежных сайтов. Нажмите кнопку **Закрыть**, а затем кнопку **ОК**.
3. В hello адресной строке Internet Explorer, введите https://dev.mysql.com/downloads/mysql/.
4. Используйте toolocate сайта MySQL hello и загрузить последнюю версию установщика MySQL для Windows hello hello. При выборе hello установщика MySQL, загрузите hello версию, которая содержит hello закройте набор файлов (например, hello mysql установщик сообщества 5.7.18.0.msi размер файла 352.8 МБ) и сохраните hello установщика.
5. После завершения загрузки hello установщика нажмите **запуска** toolaunch установки.
6. На hello **лицензионное соглашение** примите hello лицензионное соглашение и нажмите кнопку **Далее**.
7. На hello **Выбор типа установки** щелкните тип установки hello и нажмите кнопку **Далее**. Hello следующие шаги предполагают, что выбор hello hello **только сервер** вариант установки.
8. Если hello **Проверьте требования к** появится страница, нажмите кнопку **Execute** toolet hello установщик устанавливает недостающие компоненты. Следуйте инструкциям, отображающие, например hello распространяемый пакет C++ среды выполнения.
9. На hello **установки** щелкните **Execute**. После завершения установки нажмите кнопку **Next**(Далее).

10. На hello **конфигурации продукта** щелкните **Далее**.

11. На hello **типа и сеть** укажите требуемую конфигурацию подключения и тип параметры, включая hello TCP-порт при необходимости. Установите флажок **Показать расширенные параметры** и нажмите кнопку **Далее**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. На hello **учетными записями и ролями** укажите надежный пароль корневой MySQL. При необходимости добавьте дополнительные учетные записи пользователей MySQL и нажмите кнопку **Next**(Далее).

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. На hello **службы Windows** , задайте параметры по умолчанию toohello изменения для запуска hello MySQL Server как служба Windows, при необходимости и выберите **Далее**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Здравствуйте вариантов выбора в hello **подключаемых модулей и расширений** страницы являются необязательными. Нажмите кнопку **Далее** toocontinue.
15. На hello **Дополнительные параметры** , укажите необходимые параметры toologging изменения и выберите **Далее**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. На hello **применить конфигурацию сервера** щелкните **Execute**. После выполнения действия по настройке приветствия щелкните **Готово**.
17. На hello **конфигурации продукта** щелкните **Далее**.
18. На hello **Завершение установки** щелкните **tooClipboard журнала копирования** Если tooexamine его позже, а затем щелкните **Готово**.
19. Hello начальном экране введите **mysql**, а затем нажмите кнопку **клиент командной строки MySQL 5.7**.
20. Введите пароль пользователя root hello, указанный на шаге 12, и появится приглашение где может выдавать команды tooconfigure MySQL. Hello команды и синтаксис Подробнее [MySQL справочных руководствах](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Можно также настроить параметры по умолчанию конфигурации сервера, например базовый hello и каталоги данных и дисков. Дополнительные сведения см. в статье [Значения по умолчанию для конфигурации сервера 6.1.2](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Настройка конечных точек

Для hello MySQL службы toobe tooclient доступных компьютеров в hello Интернета необходимо настроить конечную точку для hello TCP-порт и создать правило брандмауэра Windows. Значение порта по умолчанию Hello, на какой сервер MySQL hello служба осуществляет прослушивание клиентов MySQL — 3306. Можно указать другой порт, при условии, что порт hello согласуется с hello значение, указанное на hello **типа и сеть** (шаг 11 выше процедуры hello).

> [!NOTE]
> Для использования в рабочей среде рекомендуется hello вопросы безопасности, что компьютеры службы доступны tooall hello сервер MySQL на hello Интернет. Можно определить набор hello исходные IP-адреса, разрешенные toouse hello в конечную точку с помощью списка управления доступом (ACL). Дополнительные сведения см. в разделе [как tooa tooSet Настройка конечных точек виртуальной машины](setup-endpoints.md).
>
>

tooconfigure конечную точку для службы MySQL Server hello:

1. В hello портал Azure, щелкните **виртуальные машины (классические)**, щелкните имя виртуальной машины MySQL hello и нажмите кнопку **конечные точки**.
2. В панели команд hello, щелкните **добавить**.
3. На hello **добавить конечную точку** введите уникальное имя для **имя**.
4. Выберите **TCP** в качестве протокола hello.
5. Введите номер порта hello, такие как **3306**, как в **общий порт** и **частный порт**, а затем нажмите кнопку **ОК**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Добавить tooallow правило брандмауэра Windows MySQL трафика
правила брандмауэра Windows, разрешающее трафик MySQL из hello Интернета, запустите следующую команду в hello tooadd _командную строку с повышенными привилегиями Windows PowerShell_ для виртуальной машины сервера MySQL hello.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Проверка удаленного подключения
tootest hello виртуальной Машины Azure выполняющегося MySQL Server toohello вашей удаленного подключения службы, необходимо указать DNS-имя hello облачной службой, содержащую hello VN hello.

1. В hello портал Azure, щелкните **виртуальные машины (классические)**, щелкните имя виртуальной машины MySQL server hello и нажмите кнопку **Обзор**.
2. Hello панели мониторинга виртуальной машины, обратите внимание на то hello **DNS-имя** значение. Пример:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. С локального компьютера под управлением MySQL или hello клиента MySQL запустите hello, следующая команда toolog в качестве пользователя MySQL.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   Например, используя имя пользователя MySQL hello _dbadmin3_ и hello _testmysql.cloudapp.net_ имя DNS для hello виртуальной машины, можно начать MySQL с помощью hello следующую команду:

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о котором выполняется MySQL, в разделе hello [документация по MySQL](http://dev.mysql.com/doc/).

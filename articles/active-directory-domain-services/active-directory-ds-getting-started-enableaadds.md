---
title: "Доменные службы Azure Active Directory: включение доменных служб Azure Active Directory | Документация Майкрософт"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Включение Azure доменных служб Active Directory с помощью hello классический портал Azure

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Задача 3. Включение доменных служб Azure Active Directory
В этой задаче Включение доменных служб Azure Active Directory (Azure AD DS) для каталога, выполнив следующие шаги hello:

1. Go toohello [классический портал Azure](https://manage.windowsazure.com).
2. В левой области hello выберите hello **Active Directory** кнопки.
3. Выберите клиент Azure Active Directory (Azure AD) hello (каталог), для которого требуется tooenable Azure AD DS.

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. На hello **Предварительный просмотр каталога** щелкните hello **Настройка** вкладки.

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. В разделе **доменных служб**, измените hello **Включение доменных служб для этого каталога** параметр слишком**Да**.  
    На странице приветствия отображаются дополнительные параметры конфигурации доменных служб Active Directory Azure.

    ![Включение доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > При включении Azure доменных служб Active Directory для вашего клиента Azure AD создает и сохраняет hello Kerberos и NTLM хэши учетных данных, необходимые для проверки подлинности пользователей.
   >
   >
6. Укажите hello **DNS-имя домена доменных служб**.

   * имя домена по умолчанию Hello hello каталога (с **. onmicrosoft.com** суффикс) выбран по умолчанию.

   * Hello список содержит все домены, которые были настроены для вашего каталога Azure AD, включая проверены и не проверенные домены, настроенные на hello **домены** вкладки.

   * Можно также ввести имя пользовательского домена. В этом примере — hello пользовательское имя домена *contoso100.com*.

     > [!WARNING]
     > Hello префикс к имени домена (например, *contoso100* в hello *contoso100.com* доменное имя) должно содержать не более 15 символов. Вы не сможете создать домен доменных служб Azure Active Directory, если префикс доменного имени превышает 15 символов.
     >
     >
7. Убедитесь, что hello DNS-имя домена, выбранный для hello управляемого домена еще не существует в виртуальной сети hello. В частности проверьте toosee ли:

   * Уже имеется домен с hello же DNS-имя домена в виртуальной сети hello.

   * Hello виртуальной сети, вы выбрали содержит VPN-подключение к локальной сети, и имеется домен с hello же DNS-имя домена в локальной сети.

   * У вас есть существующей облачной службы с таким именем hello виртуальной сети.
8. Выберите виртуальную сеть, на котором будет доступен toobe доменных служб Active Directory Azure. Выберите виртуальную сеть hello и выделенной подсетью, созданный в hello **подключение доменных служб виртуальной сети toothis** раскрывающегося списка. Необходимо учитывать следующие hello.

   * Убедитесь, что этот hello виртуальную сеть, которую вы указали принадлежит tooan регионе Azure, которая поддерживается Azure доменными службами Active Directory. tooascertain hello регионах Azure, где находится доменных служб Active Directory Azure см. в разделе [служб Azure по регионам](https://azure.microsoft.com/regions/#services/).

   * Виртуальные сети, которые принадлежат tooa регион, где не поддерживается доменных служб Active Directory Azure не отображаются в раскрывающемся списке hello.

   * Использование выделенной подсетью в виртуальной сети hello для доменных служб Active Directory Azure. Сделать *не* выберите hello подсеть шлюза. См. [рекомендации по работе с сетями](active-directory-ds-networking.md).

   * Аналогичным образом виртуальные сети, которые были созданы с помощью диспетчера ресурсов Azure не отображаются в раскрывающемся списке hello. Виртуальные сети на базе Resource Manager в настоящее время не поддерживаются доменными службами Azure Active Directory.
9. tooenable Azure доменных служб Active Directory, в области задач hello hello нижней части страницы приветствия щелкните **Сохранить**.
    * Хотя доменных служб Active Directory Azure включен для каталога, hello страницы будет отображаться состояние *ожидающие*.

        ![Окно с параметром включения доменных служб](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Доменные службы Azure Active Directory обеспечивают высокий уровень доступности для управляемого домена. После включения доменных служб Active Directory Azure hello IP-адресов, в какой домен службы доступны в виртуальной сети hello, отображаются на один одновременно. Hello второй IP-адрес будет отображаться вскоре после hello во-первых, как скоро hello служба обеспечивает высокий уровень доступности для своего домена. Высокий уровень доступности настраивается при активной для вашего домена, вы увидите два IP-адреса в hello **доменных служб** раздел hello **Настройка** вкладки.
        >
        >
    * После около 20 минут too30 hello первый IP-адрес в какой домен службы доступны в виртуальной сети hello **IP-адрес** на hello **Настройка** страницы.

        ![Окно "Доменные службы", в котором отображается первый подготовленный IP-адрес](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * При высокой доступности работает для вашего домена, на странице приветствия отображаются два IP-адреса. Управляемый домен доступен в выбранной виртуальной сети по этим двум IP-адресам.

10. Запомните hello два IP-адреса можно обновлять hello параметры DNS для виртуальной сети. Это позволяет виртуальным машинам в домене toohello tooconnect hello виртуальной сети для операций, например присоединения к домену.

    ![Окно "Доменные службы", в котором отображаются оба подготовленных IP-адреса](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> В зависимости от размера hello вашего клиента Azure AD (например, hello количество пользователей или групп) управляемый домен tooyour синхронизации занимает некоторое время. Этот процесс синхронизации происходит в фоновом режиме hello. Для больших клиентов с десятками тысяч объектов может занять один или два для всех пользователей, членство в группах и учетные данные toobe синхронизированы дня.
>
>

## <a name="next-step"></a>Дальнейшие действия
[Задача 4: обновите параметры DNS hello для hello виртуальной сети Azure](active-directory-ds-getting-started-update-dns.md)

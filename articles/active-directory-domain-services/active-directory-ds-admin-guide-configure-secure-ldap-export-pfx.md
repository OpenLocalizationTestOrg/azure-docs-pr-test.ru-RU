---
title: "Настройка защищенного протокола LDAP (LDAPS) в доменных службах Azure AD | Документация Майкрософт"
description: "Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 5d46f376d46b8bbf3f93de57a7d4e31abdbcdb2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="fa4ed-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="fa4ed-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fa4ed-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="fa4ed-104">Before you begin</span></span>
<span data-ttu-id="fa4ed-105">Убедитесь, что вы выполнили [Задачу 1. Получение сертификата для защищенного протокола LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="fa4ed-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-the-secure-ldap-certificate-to-a-pfx-file"></a><span data-ttu-id="fa4ed-106">Задача 2. Экспорт сертификата защищенного протокола LDAP в PFX-файл</span><span class="sxs-lookup"><span data-stu-id="fa4ed-106">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>
<span data-ttu-id="fa4ed-107">К выполнению этой задачи следует приступать только после получения сертификата защищенного протокола LDAP из общедоступного центра сертификации либо создания самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-107">Before you start this task, ensure that you have obtained the secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="fa4ed-108">Чтобы экспортировать сертификат LDAPS в PFX-файл, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-108">Perform the following steps, to export the LDAPS certificate to a .PFX file.</span></span>

1. <span data-ttu-id="fa4ed-109">Нажмите кнопку **Пуск** и введите **R**. В диалоговом окне **Выполнить** введите **mmc** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-109">Press the **Start** button and type **R**. In the **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Запуск консоли MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="fa4ed-111">В окне **Контроль учетных записей пользователей** щелкните **ДА**, чтобы запустить консоль управления (MMC) от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-111">On the **User Account Control** prompt, click **YES** to launch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="fa4ed-112">В меню **Файл** выберите **Добавить или удалить оснастку…**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-112">From the **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Добавление оснастки в консоль MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="fa4ed-114">В диалоговом окне **Добавление и удаление оснасток** выберите оснастку **Сертификаты** и нажмите кнопку **Добавить >**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-114">In the **Add or Remove Snap-ins** dialog, select the **Certificates** snap-in, and click the **Add >** button.</span></span>

    ![Добавление оснастки диспетчера сертификатов в консоль MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="fa4ed-116">В мастере **Оснастка диспетчера сертификатов** установите переключатель в положение **Учетная запись компьютера** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-116">In the **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Добавление оснастки диспетчера сертификатов для учетной записи компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="fa4ed-118">На странице **Выбор компьютера** установите переключатель в положение **Локальный компьютер (на котором выполняется оснастка)** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-118">On the **Select Computer** page, select **Local computer: (the computer this console is running on)** and click **Finish**.</span></span>

    ![Добавление оснастки диспетчера сертификатов — выбор компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="fa4ed-120">В диалоговом окне **Добавление и удаление оснасток** нажмите кнопку **ОК**, чтобы добавить оснастку "Сертификаты" в MMC.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-120">In the **Add or Remove Snap-ins** dialog, click **OK** to add the certificates snap-in to MMC.</span></span>

    ![Оснастка диспетчера сертификатов добавлена в консоль MMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="fa4ed-122">В окне MMC разверните узел **Корень консоли**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-122">In the MMC window, click to expand **Console Root**.</span></span> <span data-ttu-id="fa4ed-123">Должна появиться загруженная оснастка диспетчера сертификатов.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-123">You should see the Certificates snap-in loaded.</span></span> <span data-ttu-id="fa4ed-124">Разверните узел **Сертификаты (локальный компьютер)** .</span><span class="sxs-lookup"><span data-stu-id="fa4ed-124">Click **Certificates (Local Computer)** to expand.</span></span> <span data-ttu-id="fa4ed-125">Разверните узел **Личное**, а затем узел **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-125">Click to expand the **Personal** node, followed by the **Certificates** node.</span></span>

    ![Открытие хранилища личных сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="fa4ed-127">В окне должен отобразиться только что созданный самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-127">You should see the self-signed certificate we created.</span></span> <span data-ttu-id="fa4ed-128">Чтобы убедиться, что отпечаток совпадает с тем, который был указан в окнах PowerShell при создании сертификата, просмотрите свойства этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-128">You can examine the properties of the certificate to ensure the thumbprint matches that reported on the PowerShell windows when you created the certificate.</span></span>
10. <span data-ttu-id="fa4ed-129">Выберите самозаверяющий сертификат и **щелкните его правой кнопкой мыши**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-129">Select the self-signed certificate and **right click**.</span></span> <span data-ttu-id="fa4ed-130">В контекстном меню последовательно выберите пункты **Все задачи** и **Экспорт…**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-130">From the right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Экспорт сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="fa4ed-132">В **мастере экспорта сертификатов** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-132">In the **Certificate Export Wizard**, click **Next**.</span></span>

    ![Мастер экспорта сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="fa4ed-134">На странице **Экспортирование закрытого ключа** установите переключатель в положение **Да, экспортировать закрытый ключ** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-134">On the **Export Private Key** page, select **Yes, export the private key**, and click **Next**.</span></span>

    ![Экспорт закрытого ключа сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="fa4ed-136">НЕОБХОДИМО экспортировать закрытый ключ вместе с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-136">You MUST export the private key along with the certificate.</span></span> <span data-ttu-id="fa4ed-137">Включение защищенного LDAP для управляемого домена завершится ошибкой, если указать PFX-файл, в котором не содержится закрытый ключ для сертификата.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-137">If you provide a PFX that does not contain the private key for the certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="fa4ed-138">На странице **Формат экспортируемого файла** для экспортируемого сертификата установите переключатель в положение **Файл обмена личной информацией — PKCS #12 (.PFX)**.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-138">On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as the file format for the exported certificate.</span></span>

    ![Формат файла экспортируемого сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="fa4ed-140">Поддерживается только формат PFX.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-140">Only the .PFX file format is supported.</span></span> <span data-ttu-id="fa4ed-141">Не экспортируйте сертификат в формат CER.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-141">Do not export the certificate to the .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="fa4ed-142">На странице **Безопасность** установите флажок **Пароль** и введите пароль для защиты PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-142">On the **Security** page, select the **Password** option and type in a password to protect the .PFX file.</span></span> <span data-ttu-id="fa4ed-143">Запомните этот пароль, так как он понадобится при выполнении следующей задачи.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-143">Remember this password since it will be needed in the next task.</span></span> <span data-ttu-id="fa4ed-144">Нажмите кнопку **Далее** , чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-144">Click **Next** to proceed.</span></span>

    ![<span data-ttu-id="fa4ed-145">Пароль для экспортируемого сертификата</span><span class="sxs-lookup"><span data-stu-id="fa4ed-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="fa4ed-146">Запомните этот пароль.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-146">Make a note of this password.</span></span> <span data-ttu-id="fa4ed-147">Он потребуется при включении защищенного протокола LDAP для управляемого домена во время выполнения действий в разделе [Задача 3. Включение защищенного протокола LDAP для управляемого домена](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="fa4ed-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for the managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="fa4ed-148">На странице **Файл для экспорта** укажите имя файла и расположение, в которое необходимо экспортировать сертификат.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-148">On the **File to Export** page, specify the file name and location where you'd like to export the certificate.</span></span>

    ![Путь для экспорта сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="fa4ed-150">На следующей странице нажмите кнопку **Готово** , чтобы экспортировать сертификат в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-150">On the following page, click **Finish** to export the certificate to a PFX file.</span></span> <span data-ttu-id="fa4ed-151">После экспорта сертификата появится диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="fa4ed-151">You should see confirmation dialog when the certificate has been exported.</span></span>

    ![Экспорт сертификата выполнен](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="fa4ed-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa4ed-153">Next step</span></span>
[<span data-ttu-id="fa4ed-154">Задача 3. Включение защищенного протокола LDAP для управляемого домена</span><span class="sxs-lookup"><span data-stu-id="fa4ed-154">Task 3 - enable secure LDAP for the managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)

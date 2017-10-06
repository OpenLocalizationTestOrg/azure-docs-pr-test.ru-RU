---
title: "aaaConfigure Secure LDAP (LDAPS) в доменные службы Azure AD | Документы Microsoft"
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
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="44b5b-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="44b5b-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="44b5b-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="44b5b-104">Before you begin</span></span>
<span data-ttu-id="44b5b-105">Убедитесь, что вы выполнили [Задачу 1. Получение сертификата для защищенного протокола LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="44b5b-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="44b5b-106">Задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла</span><span class="sxs-lookup"><span data-stu-id="44b5b-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="44b5b-107">Прежде чем начать эту задачу, убедитесь, что получили hello безопасный LDAP сертификата из общедоступного центра сертификации или создан самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="44b5b-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="44b5b-108">Выполните следующие шаги hello, tooexport hello LDAPS сертификата tooa. PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="44b5b-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="44b5b-109">Нажмите клавишу hello **запустить** кнопки и тип **R**. В hello **запуска** диалоговое окно, введите **mmc** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Запустить консоль MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="44b5b-111">На hello **контроль учетных записей пользователей** , нажмите кнопку **Да** toolaunch MMC (консоль управления Майкрософт) от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="44b5b-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="44b5b-112">Из hello **файл** меню, нажмите кнопку **добавить или удалить оснастку... **.</span><span class="sxs-lookup"><span data-stu-id="44b5b-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Добавление оснастки tooMMC консоли](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="44b5b-114">В hello **Добавление или удаление оснасток** диалоговое окно, выберите hello **сертификаты** оснастки и нажмите кнопку hello **Добавить >** кнопки.</span><span class="sxs-lookup"><span data-stu-id="44b5b-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Добавление оснастки tooMMC консоли сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="44b5b-116">В hello **оснастку сертификатов** мастера выберите **учетная запись компьютера** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Добавление оснастки диспетчера сертификатов для учетной записи компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="44b5b-118">На hello **Выбор компьютера** выберите **локальный компьютер: (компьютер hello запущена эта консоль)** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Добавление оснастки диспетчера сертификатов — выбор компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="44b5b-120">В hello **Добавление или удаление оснасток** диалоговое окно, нажмите кнопку **ОК** tooadd hello сертификатов оснастки tooMMC.</span><span class="sxs-lookup"><span data-stu-id="44b5b-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Добавление сертификатов оснастки tooMMC - Готово](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="44b5b-122">В окне приветствия MMC щелкните tooexpand **корень консоли**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="44b5b-123">Вы увидите загружен hello оснастку Сертификаты.</span><span class="sxs-lookup"><span data-stu-id="44b5b-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="44b5b-124">Нажмите кнопку **сертификаты (локальный компьютер)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="44b5b-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="44b5b-125">Щелкните tooexpand hello **личных** узел, а затем hello **сертификаты** узла.</span><span class="sxs-lookup"><span data-stu-id="44b5b-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Открытие хранилища личных сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="44b5b-127">Вы увидите hello самозаверяющий сертификат, который мы создали.</span><span class="sxs-lookup"><span data-stu-id="44b5b-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="44b5b-128">Можно проверить свойства hello hello сертификат tooensure hello отпечаток совпадений, о которых сообщает в hello PowerShell windows, при создании сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="44b5b-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="44b5b-129">Выберите hello самозаверяющий сертификат и **щелкните правой кнопкой мыши**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="44b5b-130">Hello меню щелкните правой кнопкой мыши, выберите **все задачи** и выберите **экспорт... **.</span><span class="sxs-lookup"><span data-stu-id="44b5b-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Экспорт сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="44b5b-132">В hello **мастера экспорта сертификатов**, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Мастер экспорта сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="44b5b-134">На hello **Экспорт закрытого ключа** выберите **Да, экспортировать закрытый ключ hello**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44b5b-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Экспорт закрытого ключа сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="44b5b-136">НЕОБХОДИМО экспортировать hello закрытого ключа и сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="44b5b-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="44b5b-137">Если указать PFX-ФАЙЛ, который не содержит закрытый ключ сертификата hello hello не удается включить защищенного протокола LDAP для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="44b5b-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="44b5b-138">На hello **Формат экспортируемого файла** выберите **обмена личной информацией - PKCS #12 (. PFX-ФАЙЛ)** hello формат файла для hello экспортировать сертификат.</span><span class="sxs-lookup"><span data-stu-id="44b5b-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Формат файла экспортируемого сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="44b5b-140">Hello. Формат файла PFX поддерживается.</span><span class="sxs-lookup"><span data-stu-id="44b5b-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="44b5b-141">Не экспортировать сертификат toohello hello. Формат файла CER.</span><span class="sxs-lookup"><span data-stu-id="44b5b-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="44b5b-142">На hello **безопасности** страницу, выберите hello **пароль** параметр и введите пароль tooprotect hello. PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="44b5b-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="44b5b-143">Запомните этот пароль, так как оно потребуется в следующей задаче hello.</span><span class="sxs-lookup"><span data-stu-id="44b5b-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="44b5b-144">Нажмите кнопку **Далее** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="44b5b-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="44b5b-145">Пароль для экспортируемого сертификата</span><span class="sxs-lookup"><span data-stu-id="44b5b-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="44b5b-146">Запомните этот пароль.</span><span class="sxs-lookup"><span data-stu-id="44b5b-146">Make a note of this password.</span></span> <span data-ttu-id="44b5b-147">Необходимо при включении защищенного протокола LDAP для данного управляемого домена в [задача 3 - включите безопасный LDAP для hello управляемого домена](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="44b5b-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="44b5b-148">На hello **tooExport файл** укажите местоположение, куда tooexport hello сертификат и имя файла hello.</span><span class="sxs-lookup"><span data-stu-id="44b5b-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Путь для экспорта сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="44b5b-150">На hello следующие страницы, нажмите кнопку **Готово** tooexport hello сертификат tooa PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="44b5b-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="44b5b-151">Появится диалоговое окно подтверждения при экспортировании сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="44b5b-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Экспорт сертификата выполнен](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="44b5b-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44b5b-153">Next step</span></span>
[<span data-ttu-id="44b5b-154">Задача 3 — включить защищенного протокола LDAP для hello управляемого домена</span><span class="sxs-lookup"><span data-stu-id="44b5b-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)

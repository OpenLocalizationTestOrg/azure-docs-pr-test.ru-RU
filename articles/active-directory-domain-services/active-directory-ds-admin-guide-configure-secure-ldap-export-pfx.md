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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD

## <a name="before-you-begin"></a>Перед началом работы
Убедитесь, что вы выполнили [Задачу 1. Получение сертификата для защищенного протокола LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла
Прежде чем начать эту задачу, убедитесь, что получили hello безопасный LDAP сертификата из общедоступного центра сертификации или создан самозаверяющий сертификат.

Выполните следующие шаги hello, tooexport hello LDAPS сертификата tooa. PFX-файла.

1. Нажмите клавишу hello **запустить** кнопки и тип **R**. В hello **запуска** диалоговое окно, введите **mmc** и нажмите кнопку **ОК**.

    ![Запустить консоль MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. На hello **контроль учетных записей пользователей** , нажмите кнопку **Да** toolaunch MMC (консоль управления Майкрософт) от имени администратора.
3. Из hello **файл** меню, нажмите кнопку **добавить или удалить оснастку... **.

    ![Добавление оснастки tooMMC консоли](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. В hello **Добавление или удаление оснасток** диалоговое окно, выберите hello **сертификаты** оснастки и нажмите кнопку hello **Добавить >** кнопки.

    ![Добавление оснастки tooMMC консоли сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. В hello **оснастку сертификатов** мастера выберите **учетная запись компьютера** и нажмите кнопку **Далее**.

    ![Добавление оснастки диспетчера сертификатов для учетной записи компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. На hello **Выбор компьютера** выберите **локальный компьютер: (компьютер hello запущена эта консоль)** и нажмите кнопку **Готово**.

    ![Добавление оснастки диспетчера сертификатов — выбор компьютера](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. В hello **Добавление или удаление оснасток** диалоговое окно, нажмите кнопку **ОК** tooadd hello сертификатов оснастки tooMMC.

    ![Добавление сертификатов оснастки tooMMC - Готово](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. В окне приветствия MMC щелкните tooexpand **корень консоли**. Вы увидите загружен hello оснастку Сертификаты. Нажмите кнопку **сертификаты (локальный компьютер)** tooexpand. Щелкните tooexpand hello **личных** узел, а затем hello **сертификаты** узла.

    ![Открытие хранилища личных сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Вы увидите hello самозаверяющий сертификат, который мы создали. Можно проверить свойства hello hello сертификат tooensure hello отпечаток совпадений, о которых сообщает в hello PowerShell windows, при создании сертификата hello.
10. Выберите hello самозаверяющий сертификат и **щелкните правой кнопкой мыши**. Hello меню щелкните правой кнопкой мыши, выберите **все задачи** и выберите **экспорт... **.

    ![Экспорт сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. В hello **мастера экспорта сертификатов**, нажмите кнопку **Далее**.

    ![Мастер экспорта сертификатов](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. На hello **Экспорт закрытого ключа** выберите **Да, экспортировать закрытый ключ hello**и нажмите кнопку **Далее**.

    ![Экспорт закрытого ключа сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > НЕОБХОДИМО экспортировать hello закрытого ключа и сертификата hello. Если указать PFX-ФАЙЛ, который не содержит закрытый ключ сертификата hello hello не удается включить защищенного протокола LDAP для управляемого домена.
    >
    >
13. На hello **Формат экспортируемого файла** выберите **обмена личной информацией - PKCS #12 (. PFX-ФАЙЛ)** hello формат файла для hello экспортировать сертификат.

    ![Формат файла экспортируемого сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Hello. Формат файла PFX поддерживается. Не экспортировать сертификат toohello hello. Формат файла CER.
    >
    >
14. На hello **безопасности** страницу, выберите hello **пароль** параметр и введите пароль tooprotect hello. PFX-файла. Запомните этот пароль, так как оно потребуется в следующей задаче hello. Нажмите кнопку **Далее** tooproceed.

    ![Пароль для экспортируемого сертификата ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Запомните этот пароль. Необходимо при включении защищенного протокола LDAP для данного управляемого домена в [задача 3 - включите безопасный LDAP для hello управляемого домена](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. На hello **tooExport файл** укажите местоположение, куда tooexport hello сертификат и имя файла hello.

    ![Путь для экспорта сертификата](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. На hello следующие страницы, нажмите кнопку **Готово** tooexport hello сертификат tooa PFX-файла. Появится диалоговое окно подтверждения при экспортировании сертификата hello.

    ![Экспорт сертификата выполнен](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Дальнейшие действия
[Задача 3 — включить защищенного протокола LDAP для hello управляемого домена](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)

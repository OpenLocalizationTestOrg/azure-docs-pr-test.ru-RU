---
title: "Синхронизация Azure AD Connect: изменение пароля учетной записи AD DS | Документация Майкрософт"
description: "В этом разделе описывается, как обновить Azure AD Connect после изменения пароля учетной записи AD DS."
services: active-directory
keywords: "учетная запись AD DS, учетная запись Active Directory, пароль"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="a74ee-104">Изменение пароля учетной записи AD DS</span><span class="sxs-lookup"><span data-stu-id="a74ee-104">Changing the AD DS account password</span></span>
<span data-ttu-id="a74ee-105">Учетная запись AD DS — это учетная запись пользователя, которая используется службой Azure AD Connect для взаимодействия с локальным каталогом Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a74ee-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="a74ee-106">В случае изменения пароля учетной записи AD DS необходимо также обновить пароль в службе синхронизации Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a74ee-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="a74ee-107">В противном случае служба синхронизации больше не сможет правильно синхронизировать данные с локальным каталогом Active Directory. При этом будут возникать следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="a74ee-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="a74ee-108">В Synchronization Service Manager любая операция импорта или экспорта с использованием локального каталога AD завершается ошибкой **no-start-credentials**.</span><span class="sxs-lookup"><span data-stu-id="a74ee-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="a74ee-109">В средстве просмотра событий Windows журнал событий приложения содержит ошибку с **идентификатором события 6000** и сообщением об ошибке **Не удалось выполнить управляющий агент "contoso.com", так как учетные данные были недопустимыми**.</span><span class="sxs-lookup"><span data-stu-id="a74ee-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="a74ee-110">Как обновить пароль в службе синхронизации в случае изменения пароля учетной записи AD DS</span><span class="sxs-lookup"><span data-stu-id="a74ee-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="a74ee-111">Чтобы обновить пароль в службе синхронизации, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a74ee-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="a74ee-112">Запустите Synchronization Service Manager ("Запуск" → "Служба синхронизации").</span><span class="sxs-lookup"><span data-stu-id="a74ee-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="a74ee-113">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="a74ee-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="a74ee-114">Перейдите на вкладку **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="a74ee-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="a74ee-115">Выберите **соединитель AD**, соответствующий учетной записи AD DS, для которой был изменен пароль.</span><span class="sxs-lookup"><span data-stu-id="a74ee-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="a74ee-116">В разделе **Действия** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a74ee-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="a74ee-117">Во всплывающем диалоговом окне выберите **Connect to Active Directory Forest** (Подключиться к лесу Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a74ee-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="a74ee-118">В текстовом поле **Пароль** введите новый пароль учетной записи AD DS.</span><span class="sxs-lookup"><span data-stu-id="a74ee-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="a74ee-119">Нажмите кнопку **ОК**, чтобы сохранить новый пароль и закрыть всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a74ee-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="a74ee-120">Перезапустите службу синхронизации Azure AD Connect в диспетчере управления службами Windows.</span><span class="sxs-lookup"><span data-stu-id="a74ee-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="a74ee-121">Это гарантирует, что все ссылки на старый пароль будут удалены из кэша памяти.</span><span class="sxs-lookup"><span data-stu-id="a74ee-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a74ee-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a74ee-122">Next steps</span></span>
<span data-ttu-id="a74ee-123">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="a74ee-123">**Overview topics**</span></span>

* [<span data-ttu-id="a74ee-124">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="a74ee-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="a74ee-125">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a74ee-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

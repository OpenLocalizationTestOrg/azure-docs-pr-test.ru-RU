---
title: "Синхронизация Azure AD Connect: изменение пароля учетной записи доменных служб Active Directory hello AD | Документы Microsoft"
description: "Этот раздел документа описывает, как изменена tooupdate Azure AD Connect после hello пароль учетной записи hello AD DS."
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="4a30a-104">Изменение пароля учетной записи hello AD DS</span><span class="sxs-lookup"><span data-stu-id="4a30a-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="4a30a-105">Учетная запись Hello AD DS ссылается toohello учетная запись пользователя Azure AD Connect toocommunicate с локальной Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a30a-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="4a30a-106">При изменении пароля hello hello учетной записи службы AD DS необходимо обновить службы подключения синхронизации Azure AD с hello нового пароля.</span><span class="sxs-lookup"><span data-stu-id="4a30a-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="4a30a-107">В противном случае приветствия синхронизации больше не могут правильно синхронизировать с hello локальной Active Directory и могут возникнуть следующие ошибки hello:</span><span class="sxs-lookup"><span data-stu-id="4a30a-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="4a30a-108">В hello диспетчер службы синхронизации любой импорта или экспорта операцию с локальным AD завершится неудачно, **без запуска учетных данных** ошибки.</span><span class="sxs-lookup"><span data-stu-id="4a30a-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="4a30a-109">В средстве просмотра событий Windows, журнал событий приложения hello содержит ошибку с **событий Идентификатором 6000** и сообщение **«hello агент управления «contoso.com» сбой toorun недопустимые учетные данные hello»** .</span><span class="sxs-lookup"><span data-stu-id="4a30a-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="4a30a-110">Как tooupdate hello служба синхронизации с нового пароля для учетной записи службы AD DS</span><span class="sxs-lookup"><span data-stu-id="4a30a-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="4a30a-111">hello tooupdate службы синхронизации с hello нового пароля:</span><span class="sxs-lookup"><span data-stu-id="4a30a-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="4a30a-112">Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).</span><span class="sxs-lookup"><span data-stu-id="4a30a-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="4a30a-113">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="4a30a-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="4a30a-114">Go toohello **соединители** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4a30a-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="4a30a-115">Выберите hello **соединителя AD** , соответствующий учетной записи toohello AD доменных служб Active Directory, для которого было изменено его пароль.</span><span class="sxs-lookup"><span data-stu-id="4a30a-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="4a30a-116">В разделе **Действия** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4a30a-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="4a30a-117">В всплывающем диалоговом окне приветствия выберите **подключения леса tooActive**:</span><span class="sxs-lookup"><span data-stu-id="4a30a-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="4a30a-118">Введите новый пароль учетной записи, hello AD DS hello в hello **пароль** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="4a30a-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="4a30a-119">Нажмите кнопку **ОК** toosave hello новый пароль и закрыть hello всплывающем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="4a30a-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="4a30a-120">Перезапуск hello Azure AD подключения службы синхронизации в диспетчере служб Windows.</span><span class="sxs-lookup"><span data-stu-id="4a30a-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="4a30a-121">Это tooensure, старый пароль toohello любые ссылки, удаляется из кэша памяти hello.</span><span class="sxs-lookup"><span data-stu-id="4a30a-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a30a-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a30a-122">Next steps</span></span>
<span data-ttu-id="4a30a-123">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="4a30a-123">**Overview topics**</span></span>

* [<span data-ttu-id="4a30a-124">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="4a30a-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="4a30a-125">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a30a-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

---
title: "Подключение нескольких доменов aaaAzure AD"
description: "В этом документе описываются процедуры установки и настройки нескольких доменов верхнего уровня в Office 365 и Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Поддержка нескольких доменов для федерации с Azure AD
Hello следующей документации содержатся рекомендации о том, как toouse нескольких доменов верхнего уровня и поддоменам, при включении в федерацию с Office 365 или Azure AD доменов.

## <a name="multiple-top-level-domain-support"></a>Поддержка нескольких доменов верхнего уровня
Для создания федерации нескольких доменов верхнего уровня с Azure AD необходимо выполнить некоторые дополнительные настройки, которые не требуются при создании федерации с одним доменом верхнего уровня.

Если домен включена в федерацию с Azure AD, несколько свойств, задаются на hello домена в Azure.  Важным свойством является IssuerUri.  Это URI, который используется с Azure AD tooidentify домен hello, hello маркера связан с.  Hello URI не требует tooresolve tooanything, но он должен быть допустимым URI.  По умолчанию Azure AD устанавливает значение toohello hello идентификатор службы федерации в вашей локальной AD FS конфигурации.

> [!NOTE]
> Идентификатор службы федерации Hello является URI, который уникально идентифицирует службы федерации.  Служба федерации Hello является экземпляром AD FS, которые работают как службы маркеров безопасности hello. 
> 
> 

Вы можете просмотреть IssuerUri с помощью команды PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Проблема возникает, когда мы хотим tooadd несколько доменов верхнего уровня.  Например, предположим, что у вас настроена федерация между Azure AD и локальной средой.  В данном документе я использую домен bmcontoso.com.  Теперь я добавил второй домен верхнего уровня bmfabrikam.com.

![Домены](./media/active-directory-multiple-domains/domains.png)

Если мы будем стараться федеративного домена нашей bmfabrikam.com toobe tooconvert, мы сообщение об ошибке.  Hello причиной этого является Azure AD имеет ограничение, которое не допускает hello IssuerUri свойство toohave hello одинаковое значение для более чем одного домена.  

![Ошибка федерации](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Параметр SupportMultipleDomain
tooworkaround это, мы должны tooadd другой IssuerUri, это можно сделать с помощью hello `-SupportMultipleDomain` параметра.  Этот параметр используется с hello следующие командлеты:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Этот параметр позволяет настроить hello IssuerUri таким образом, чтобы он основан на hello имя домена hello Azure AD.  Оно будет уникальным в различных каталогах в Azure AD.  Использование параметра hello успешно позволяет toocomplete команды PowerShell hello.

![Ошибка федерации](./media/active-directory-multiple-domains/convert.png)

Просмотрев параметры hello наш новый домен bmfabrikam.com можно увидеть hello следующее:

![Ошибка федерации](./media/active-directory-multiple-domains/settings.png)

Обратите внимание, что `-SupportMultipleDomain` не изменяет hello других конечных точек, настроенных по-прежнему настроить службы федерации tooour toopoint на adfs.bmcontoso.com.

Также, `-SupportMultipleDomain` does его применения, система hello AD FS включает hello правильное значение издателя в маркеры, выпущенные для Azure AD. Это делается путем установки hello доменной части hello пользователей UPN и установка этого параметра hello в в качестве домена hello IssuerUri, т. е. суффикс https://{upn} / adfs/services/trust. 

Таким образом во время проверки подлинности tooAzure AD или Office 365, элемент IssuerUri hello в токен пользователя hello — используется toolocate hello домена в Azure AD.  Если не удается найти совпадения, будут выполнены проверки подлинности hello. 

Например, если имя участника-пользователя пользователь должен bsimon@bmcontoso.com, элемент IssuerUri hello проблемам hello токена службы федерации Active Directory будет иметь значение toohttp://bmcontoso.com/adfs/services/trust. Это будет соответствовать конфигурации hello Azure AD, а проверка подлинности выполняется успешно.

Hello Вот правила настраиваемые утверждения hello, реализующего следующую логику:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> В порядке toouse hello - SupportMultipleDomain переключение при попытке tooadd новый или преобразовать уже добавленных доменов, вы должны toohave установки вашего toosupport федеративного отношения доверия их изначально.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Как tooupdate hello доверие между AD FS и Azure AD
Если вы не настроили hello федеративного отношения доверия между AD FS и имеющимся экземпляром Azure AD, может потребоваться toore-создание этого отношения доверия.  Это происходит потому, когда это изначально программу установки без hello `-SupportMultipleDomain` , hello IssuerUri имеет параметр со значением по умолчанию hello.  В hello снимке экрана ниже вы увидите набора toohttps://adfs.bmcontoso.com/adfs/services/trust hello IssuerUri.

Поэтому теперь, если мы добавлен новый домен в портале hello Azure AD, а затем tooconvert его с помощью `Convert-MsolDomaintoFederated -DomainName <your domain>`, мы получаем hello следующая ошибка.

![Ошибка федерации](./media/active-directory-multiple-domains/trust1.png)

Если при попытке tooadd hello `-SupportMultipleDomain` коммутатора, мы получаем hello следующая ошибка:

![Ошибка федерации](./media/active-directory-multiple-domains/trust2.png)

Просто попытки toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` на hello исходного домена приводит к ошибке.

![Ошибка федерации](./media/active-directory-multiple-domains/trust3.png)

Выполните шаги hello ниже tooadd дополнительного домена верхнего уровня.  Если домен уже добавлен и не использовался hello `-SupportMultipleDomain` параметр start hello шагам для удаление и обновление вашего исходного домена.  Если вы не добавили домен верхнего уровня еще можно начать с hello шаги для добавления домена, с помощью PowerShell Azure AD Connect.

Используйте следующие шаги tooremove hello Microsoft Online доверия hello и обновление вашего исходного домена.

1. На сервере федерации AD FS откройте **Управление AD FS** 
2. Hello левой части окна разверните **отношения доверия** и **доверия с проверяющей стороной**
3. На правом hello, удалите hello **Microsoft Office 365 Identity Platform** входа.
   ![Удалить Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. На компьютере, где [Azure Active Directory модуля для Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) на следующей hello: `$cred=Get-Credential`.  
5. Введите hello пользователя и пароль глобального администратора для домена Azure AD hello федеративные отношения с
6. В PowerShell введите `Connect-MsolService -Credential $cred`
7. В PowerShell введите `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Это необходимо для hello исходного домена.  Поэтому использование hello выше домены, которые было бы:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Используйте следующие шаги tooadd hello новый домен верхнего уровня с помощью PowerShell hello

1. На компьютере, где [Azure Active Directory модуля для Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) на следующей hello: `$cred=Get-Credential`.  
2. Введите hello пользователя и пароль глобального администратора для домена Azure AD hello федеративные отношения с
3. В PowerShell введите `Connect-MsolService -Credential $cred`
4. В PowerShell введите `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Используйте следующие шаги tooadd hello новый домен верхнего уровня с помощью Azure AD Connect hello.

1. Запустите Azure AD Connect с рабочего стола hello или меню «Пуск»
2. Выберите "Добавить дополнительный домен Azure AD" ![Добавить дополнительный домен Azure AD](./media/active-directory-multiple-domains/add1.png).
3. Введите учетные данные Azure AD и Active Directory.
4. Выберите второй домен hello нужно tooconfigure для федерации.
   ![Добавить дополнительный домен Azure AD](./media/active-directory-multiple-domains/add2.png)
5. Нажмите "Установить".

### <a name="verify-hello-new-top-level-domain"></a>Проверьте hello новый домен верхнего уровня
С помощью команды PowerShell hello `Get-MsolDomainFederationSettings -DomainName <your domain>`можно просмотреть IssuerUri обновить hello.  Hello снимке экрана показано hello параметры федерации были обновлены на нашем исходного домена http://bmcontoso.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

И hello IssuerUri на нашем нового домена было установлено toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Поддержка поддоменов
При добавлении дочерний домен, из-за hello, каким образом Azure AD обрабатывается доменов, он будет наследовать параметры hello hello родителя.  Это означает, что этой hello IssuerUri должен toomatch hello родителей.

Давайте предположим, что у меня был домен bmcontoso.com, а затем я добавил поддомен corp.bmcontoso.com.  Это означает, что hello IssuerUri для пользователя из corp.bmcontoso.com потребуется toobe **http://bmcontoso.com/adfs/services/trust.**  Однако реализации стандартных правил hello выше для Azure AD создает маркер с издателя, как **http://corp.bmcontoso.com/adfs/services/trust.** не соответствующая обязательное значение hello домена и не пройдет проверку подлинности.

### <a name="how-tooenable-support-for-sub-domains"></a>Как tooenable поддержка поддоменов
В порядке toowork вокруг этого hello AD FS с проверяющей стороной для Microsoft Online должен toobe обновлены.  toodo это, необходимо настроить настраиваемое правило для утверждений, чтобы он отсекает любой поддоменов из суффикс UPN пользователя hello, при создании пользовательского поставщика значения hello. 

После утверждения Hello для этого:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
Номер последней Hello в регулярном выражении hello задать hello сколько родительских доменов в корневой домен. Так как здесь используется bmcontoso.com, необходимы два родительских домена. Если три родительских доменов были сохранены toobe (т. е.: corp.bmcontoso.com), то номер hello было бы три. Eventualy диапазон может быть указан, совпадения hello всегда станет более hello toomatch доменов. «{2,3}» будет соответствовать двумя доменами toothree (т. е.: bmfabrikam.com и corp.bmcontoso.com).

Используйте следующие шаги tooadd hello в поддоменов toosupport пользовательского утверждения.

1. Откройте оснастку управления AD FS.
2. Щелкните правой кнопкой мыши доверие Microsoft Online RP hello и выберите правила для утверждений, изменение
3. Выберите третий правила утверждения hello и замените ![изменить утверждения](./media/active-directory-multiple-domains/sub1.png)
4. Замените hello текущего утверждения:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Заменить утверждение](./media/active-directory-multiple-domains/sub2.png)

5. Нажмите кнопку "ОК".  Нажмите кнопку "Применить".  Нажмите кнопку "ОК".  Откройте оснастку управления AD FS.


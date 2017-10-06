---
title: "токены пользователя aaaUnderstand в совместной работы Azure AD B2B | Документы Microsoft"
description: "Справочные материалы по токенам пользователей для службы совместной работы Azure Active Directory B2B."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 968af1c8d1ab6f4b3f50a82f6c998da3955ac364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-user-tokens-in-azure-ad-b2b-collaboration"></a><span data-ttu-id="12335-103">Основные сведения о токенах пользователей в службе совместной работы Azure AD B2B</span><span class="sxs-lookup"><span data-stu-id="12335-103">Understand user tokens in Azure AD B2B collaboration</span></span>

<span data-ttu-id="12335-104">Следует tooknow выглядит какие hello маркер для совместной работы пользователя B2B ниже приведены сведения маркера носителя hello и содержимом маркера гостевых систем Azure Active Directory (Azure AD) и гостевой учетной записи Майкрософт в клиенте hello ресурсов (для идентификатора клиента 04dcc6ab-388a-4559-b527-fbec656300ea).</span><span class="sxs-lookup"><span data-stu-id="12335-104">If you want tooknow what hello token looks like for a B2B collaboration user, here are hello bearer token details and token content for an Azure Active Directory (Azure AD) guest and a Microsoft account guest in hello resource tenant (for tenantid 04dcc6ab-388a-4559-b527-fbec656300ea).</span></span> <span data-ttu-id="12335-105">содержимое JSON Web Token (JWT) toosee hello, используйте [https://jwt.io/](https://jwt.io/) или [http://calebb.net](http://calebb.net/).</span><span class="sxs-lookup"><span data-stu-id="12335-105">toosee hello JSON Web Token (JWT) contents, use [https://jwt.io/](https://jwt.io/) or [http://calebb.net](http://calebb.net/).</span></span>

## <a name="azure-ad-guest-token"></a><span data-ttu-id="12335-106">Токен гостевого пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="12335-106">Azure AD guest token</span></span>
```
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSIsImtpZCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0LyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYS8iLCJpYXQiOjE0ODQ4MDM5MTgsIm5iZiI6MTQ4NDgwMzkxOCwiZXhwIjoxNDg0ODA3ODE4LCJhY3IiOiIxIiwiYWlvIjoiQVFBQkFBRUFBQURSTllSUTNkaFJTcm0tNEstYWRwQ0pJNWNncGtYQ0VOTHdnN1Z1emhFQURIajNOOWNIMzhRWGFBakhrYUtPRFhneWJpcnVRYVhpa3RZZ3I2M0xMQTVTVDlEeXV2dEtQSUdlXzJpVFRhdjNqSkxuTlRSZ2JWRFpwckhSaEtZbWl5RWdBQSIsImFsdHNlY2lkIjoiNTo6MTAwMzAwMDA4MDFCQUZDNyIsImFtciI6WyJwd2QiLCJyc2EiXSwiYXBwaWQiOiJjNDRiNDA4My0zYmIwLTQ5YzEtYjQ3ZC05NzRlNTNjYmRmM2MiLCJhcHBpZGFjciI6IjIiLCJlX2V4cCI6MTA4MDAsImVtYWlsIjoicmFqZXNiQG1pY3Jvc29mdC5jb20iLCJpZHAiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaW5fY29ycCI6InRydWUiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTk1IiwibmFtZSI6InJhamVzaCIsIm9pZCI6IjA1ODAyY2M1LTgxMWUtNDZiZC1iMWI2LTU5NDZlNjY4ODIyZiIsInBsYXRmIjoiMyIsInB1aWQiOiIxMDAzM0ZGRjlEOEY5OTUzIiwic2NwIjoidXNlcl9pbXBlcnNvbmF0aW9uIiwic3ViIjoiS1d3QnVCNk5ROU5UYmpoSUI1OHEwM2FlQVl6cEk2TWxiMkpncGk1aV9ITSIsInRpZCI6IjA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYSIsInVuaXF1ZV9uYW1lIjoicmFqZXNiQG1pY3Jvc29mdC5jb20iLCJ2ZXIiOiIxLjAifQ.Vllr1hGXpBlpXDBKRHHYbMr_1_DwKNY3eCObBOfEaxJirwqujqCZodPrAkIOJlFYyhkILyHZQUi_D1w7XoPsd6U4GQlgOoFfzbye-P_NdRFabHMlv32gCgHz1xo11aPP453EiwwG5OHnWaHYLBpuqi3sNeKx06xbTFj07HmADDaR4aM0jwy031d6GkD0LdU-Xkazi5-h8parVRLOkkLZA0oxMFoxl_-VHr1hOzxCkbWgRoug4t97161i5tGil99CcpJ6NK8uQld7TveC40sjJ735Sksn-Uq_NZcJuXCEVsH0xK5evaeFBFSEqACXjKTvYkJWtAx8Kr8yWZAcEg0YMQ
```

## <a name="microsoft-account-guest-token"></a><span data-ttu-id="12335-107">Токен гостевого пользователя учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="12335-107">Microsoft account guest token</span></span>
```
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSIsImtpZCI6Ilk0dWVLMm9hSU5RaVFiNVlFQlNZVnlEY3BBVSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0LyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzA0ZGNjNmFiLTM4OGEtNDU1OS1iNTI3LWZiZWM2NTYzMDBlYS8iLCJpYXQiOjE0ODQ4MDMwNjEsIm5iZiI6MTQ4NDgwMzA2MSwiZXhwIjoxNDg0ODA2OTYxLCJhY3IiOiIxIiwiYWlvIjoiQVFBQkFBRUFBQURSTllSUTNkaFJTcm0tNEstYWRwQ0pEeEd4a3lUdmJ2d1RoSHJnTEdPaGZEbTA1aXJndC1lR1d3YTl5QUZQQTJQc19nZHF2bHQ1X1AtaDhrT2IwdUdza3dyYklBbUhvMEtRM005N2ZCVlRtdzRKY0NfaFVkWW1PZ25QYVlOY1BRQXBIYmFMcUlaZGhaRXhtQVZJeXFmaElBQSIsImFsdHNlY2lkIjoiMTpsaXZlLmNvbTowMDAzMDAwMEEwNzBCOTYyIiwiYW1yIjpbInB3ZCJdLCJhcHBpZCI6ImM0NGI0MDgzLTNiYjAtNDljMS1iNDdkLTk3NGU1M2NiZGYzYyIsImFwcGlkYWNyIjoiMiIsImVfZXhwIjoxMDgwMCwiZW1haWwiOiJiYXNhcmFqZXNoQGxpdmUuY29tIiwiZmFtaWx5X25hbWUiOiJiYXNhIiwiZ2l2ZW5fbmFtZSI6InJhamVzaCIsImlkcCI6ImxpdmUuY29tIiwiaXBhZGRyIjoiMTY3LjIyMC4xLjE5NSIsIm5hbWUiOiJiYXNhcmFqZXNoIiwib2lkIjoiMjU0NmU3NDEtNmZjNi00ZDI0LTg2NTQtZjkyNDc5MzI0ZjM3IiwicGxhdGYiOiIzIiwicHVpZCI6IjEwMDMzRkZGOURBQjk2NDYiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiI4Y2N5OEh4cmE5UTl2aGdYOXhBODFBeWJEV3dsVmxjXzRBZVJYZ2lzamM4IiwidGlkIjoiMDRkY2M2YWItMzg4YS00NTU5LWI1MjctZmJlYzY1NjMwMGVhIiwidW5pcXVlX25hbWUiOiJsaXZlLmNvbSNiYXNhcmFqZXNoQGxpdmUuY29tIiwidmVyIjoiMS4wIn0.LSIBlJpElXpsGXOGaFINW-jOBHsI0Dxe3oX-YIEsccegDCspl6UnRjpwzs0nBL09B4N0oqLd7ZwXZAQURpgaAFnWvROxkIGpNTE_ppSKU1suud8keG5VnTEu82em95G1_c_eW1nOemPvbADCC8h08p2wxNm8QyEhmYqauN6qYbeqOnioRERXO3zOPg8nSXFcGPhvumJ_BW8XKnW4zLdhK78c3PgynPnwtIm08SksMRDzGMgUc9RK1bpPQtgX8iFQByEljf5cuE_h_e1Nr5Y4StrhS3JCiQLTYZ727YY-lSm5DERiQrt7MkP5BHprEmSByofSvACj5TmVdqBFUjobuA
```


## <a name="next-steps"></a><span data-ttu-id="12335-108">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12335-108">Next steps</span></span>

<span data-ttu-id="12335-109">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="12335-109">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="12335-110">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="12335-110">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="12335-111">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="12335-111">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="12335-112">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="12335-112">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="12335-113">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="12335-113">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="12335-114">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="12335-114">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="12335-115">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="12335-115">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="12335-116">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="12335-116">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="12335-117">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12335-117">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="12335-118">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="12335-118">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="12335-119">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="12335-119">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)

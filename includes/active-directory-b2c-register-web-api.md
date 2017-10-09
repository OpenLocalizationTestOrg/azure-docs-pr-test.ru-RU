[!INCLUDE [active-directory-b2c-portal-add-application](active-directory-b2c-portal-add-application.md)]

tooregister веб-API, используйте параметры hello, указанные в таблице hello.

![Примеры настроек регистрации для нового веб-API](./media/active-directory-b2c-register-web-api/b2c-new-web-api-settings.png)

| Настройка      | Образец значения  | Описание                                        |
| ------------ | ------- | -------------------------------------------------- |
| **Имя** | Contoso B2C API | Введите **имя** для приложения hello, описывающий tooconsumers ваш API. | 
| **Включить веб-приложение или веб-интерфейс API** | Да | Выберите **Да** для веб-API. |
| **Разрешить неявный поток** | Да | Выберите **Да**, если приложение использует [вход через OpenID Connect](../articles/active-directory-b2c/active-directory-b2c-reference-oidc.md). |
| **URL-адрес ответа** | `https://localhost:44316/` | URL-адреса ответа — это конечные точки, куда Azure AD B2C возвращает все токены, запрашиваемые вашим приложением. Введите [соответствующий](../articles/active-directory-b2c/active-directory-b2c-app-registration.md#choosing-a-web-app-or-api-reply-url) **URL-адрес ответа**. В этом примере используется локальный веб-API, который ожидает передачу данных через порт 44316. |
| **URI кода приложения** | api | Hello URI идентификатора приложения является идентификатором hello, используемым для веб-API. Здравствуйте, полный идентификатор URI, включая домен hello создается автоматически. |

Нажмите кнопку **создать** tooregister приложения.

Вновь зарегистрированного приложения отображается в списке приложений hello для клиента B2C hello. Выберите веб-API из списка hello. Откроется панель свойств Hello API-интерфейса.

![Свойства веб-API](./media/active-directory-b2c-register-web-api/b2c-web-api-properties.png)

Запишите hello глобальный уникальный **идентификатор клиента приложения**. Используйте идентификатор hello в код приложения.

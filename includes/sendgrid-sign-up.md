Клиенты Azure могут разблокировать 25 000 бесплатных сообщений электронной почты каждый месяц. Эти 25000 бесплатные ежемесячные сообщения электронной почты даст вам доступ tooadvanced отчетов и аналитики и [все API-интерфейсы] [ all APIs] (Web, SMTP, события, синтаксический анализ и многое другое). Сведения о дополнительных служб, предоставляемых SendGrid можно получить hello [решения SendGrid] [ SendGrid Solutions] страницы.

### <a name="toosign-up-for-a-sendgrid-account"></a>toosign для получения учетной записи SendGrid
1. Войдите в toohello [портала управления Azure][Azure Management Portal].
2. В меню слева hello hello выберите **New**.

    ![command-bar-new][command-bar-new]
3. Щелкните **Надстройки** > **SendGrid Email Delivery** (Доставка электронной почты SendGrid).

    ![sendgrid-store][sendgrid-store]
4. Заполните форму регистрации hello и выберите **создать**.

    ![sendgrid-create][sendgrid-create]
5. Введите **имя** tooidentify SendGrid вашей службы в параметрах Azure. Имена должны иметь длину в диапазоне от 1 до 100 знаков и содержать только алфавитно-цифровые символы, дефисы, точки и подчеркивания. Hello имя должно быть уникальным в списке рабочих элементах подписки хранилища Azure.
6. Введите и подтвердите **пароль**.
7. Выберите свою **подписку**.
8. Создайте новую **группу ресурсов** или выберите существующую.
9. В hello **Ценовая категория** установите hello SendGrid план, который toosign в службе.

    ![sendgrid-pricing][sendgrid-pricing]
10. Введите **промокод** (при наличии).
11. Введите **контактные данные**.
12. Просмотрите и примите hello **условия**.
13. После подтверждения покупки вы увидите **успешное развертывание** всплывающее окно, чтобы просмотреть вашей учетной записи, указанной в hello **все ресурсы** раздела.

    ![all-resources][all-resources]

    После завершения покупки и щелчке hello **управление** процесс проверки по электронной почте hello tooinitiate кнопки, вы получите сообщение электронной почты от SendGrid, запрашивающее tooverify вашей учетной записи. Если вы не получили это сообщение или столкнулись с проблемами при подтверждении учетной записи, ознакомьтесь с разделом часто задаваемых вопросов.

    ![управление][manage]

    **Можно отправлять только копии сообщения электронной почты too100 в день до проверки вашей учетной записи.**

    toomodify ваш план подписки или ознакомиться Здравствуйте контактных данных SendGrid, щелкните имя вашей hello службы tooopen SendGrid панели мониторинга SendGrid Marketplace hello.

    ![Параметры][settings]

    toosend в электронной почте с помощью SendGrid, вы должны предоставить свой ключ API.

### <a name="toofind-your-sendgrid-api-key"></a>toofind ваш ключ API SendGrid
1. Нажмите кнопку **Управление**.

    ![управление][manage]
2. Выберите в панели мониторинга SendGrid, **параметры** и затем **ключи API** в меню hello слева hello.

    ![api-keys][api-keys]

3. Нажмите кнопку hello **создать ключ API** раскрывающийся список и выберите **ключ API Общие**.

    ![general-api-key][general-api-key]
4. Как минимум предоставить hello **имя ключа** и предоставление полного доступа слишком**отправки почты** и выберите **Сохранить**.

    ![access][access]
5. На этом этапе API будет отображен один раз. Следует убедиться, что toostore его безопасно.

### <a name="toofind-your-sendgrid-credentials"></a>toofind ваших учетных данных SendGrid
1. Щелкните значок ключа toofind hello вашей **Username**.

    ![key][key]
2. пароль Hello является hello, выбранным при установке. Можно выбрать **Смена пароля** или **сброс пароля** toomake любые изменения.

toomanage параметрах доставке электронной почты щелкните hello **управление кнопку**. Панели мониторинга SendGrid tooyour будете перенаправлены.

    ![manage][manage]

    For more information on sending email through SendGrid, visit hello [Email API Overview][Email API Overview].

<!--images-->

[command-bar-new]: ./media/sendgrid-sign-up/new-addon.png
[sendgrid-store]: ./media/sendgrid-sign-up/sendgrid-store.png
[sendgrid-create]: ./media/sendgrid-sign-up/sendgrid-create.png
[sendgrid-pricing]: ./media/sendgrid-sign-up/sendgrid-pricing.png
[all-resources]: ./media/sendgrid-sign-up/all-resources.png
[manage]: ./media/sendgrid-sign-up/manage.png
[settings]: ./media/sendgrid-sign-up/settings.png
[api-keys]: ./media/sendgrid-sign-up/api-keys.png
[general-api-key]: ./media/sendgrid-sign-up/general-api-key.png
[access]: ./media/sendgrid-sign-up/access.png
[key]: ./media/sendgrid-sign-up/key.png

<!--Links-->

[SendGrid Solutions]: https://sendgrid.com/solutions
[Azure Management Portal]: https://manage.windowsazure.com
[SendGrid Getting Started]: http://sendgrid.com/docs
[SendGrid Provisioning Process]: https://support.sendgrid.com/hc/articles/200181628-Why-is-my-account-being-provisioned-
[all APIs]: https://sendgrid.com/docs/API_Reference/index.html
[Email API Overview]: https://sendgrid.com/docs/API_Reference/Web_API_v3/Mail/index.html

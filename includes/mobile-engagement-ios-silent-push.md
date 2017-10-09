> [!IMPORTANT]
> tooreceive Push-уведомления от мобильного охвата необходимо tooenable `Silent Remote Notifications` в приложении. Необходимо tooadd hello уведомления удаленного toohello UIBackgroundModes массив значений в файле Info.plist.
> 
> 

1. Откройте `info.plist` файл в проекте hello
2. Щелкните правой кнопкой мыши hello верхний элемент в списке hello (`Information Property List`) и добавить новую строку
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Введите в новую строку hello`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Щелкните строку hello tooexpand стрелка влево hello
5. Добавьте следующий элемент toohello значение 0 hello`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. После внесения изменения hello info.plist hello XML должен содержать следующие hello ключ и значение:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Если вы используете **Xcode 7+** и **iOS 9+**:
   
   * Включите **push-уведомления** в разделе Targets (Конечные объекты) > Your Target Name (Имя вашего конечного объекта) > Capabilities (Возможности).


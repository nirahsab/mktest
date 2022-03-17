# Работа с приложениями
> Для выполнения нижеописанных действий требуется роль Менеджера.

AppSec.Hub нацелен на обеспечение безопасности разрабатываемых приложений. Таким образом, приложение можно рассматривать как целевой объект в системе. Именно для безопасной разработки приложений в системе используются автоматизация, различные инструменты, практики SSDL и т. п.

Чтобы начать работу с приложениями, выберите пункт меню **Applications** в верхнем левом углу экрана. На экране появится страница приложений AppSec.Hub.

![](img/image293.png)

image293.png

Каждая карточка на странице **Applications** представляет приложение и краткую информацию о нем:

* Имя.
* Идентификатор приложения в AppSec.Hub.
* Текущий статус приложения (supported/not supported) отображается разным цветом линии вверху карточки приложения. Если линия имеет серый цвет, security pipelines для этого приложения не могут быть запущены, а само приложение имеет статус Not supported. Если линия имеет зеленый цвет, security pipelines для этого приложения могут быть запущены, а само приложение имеет статус Supported. Более подробная информация приведена ниже в разделе «Настройки приложения».
* Применяемые практики (SAST, SCA, DAST).
* Сводка по дефектам (Defects) и проблемам (Issues) безопасности приложения.
* Размер кодовой базы.
* WRI (Weighted Risk Index) — взвешенный риск-индекс. Используется для оценки текущего бизнес-риска приложения.
Существует возможность поиска и фильтрации приложений с использованием кнопки **Show filters** ![avatar](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADkAAAAhCAYAAABjnQNzAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAFXSURBVFhH5ZXBzYQgEEb/xj1bgyXYgi3YgyV48eaFzfuTbzO6uCYrgwEPLwxBGZ4D+Leua6idQ8l5nv8pLabd8yGpl0rHOm0kjx4qiZjDRnKapndcMo+QhEdIWpePM2n7pfKI7foIScgiSZJxHEPf92EYhtOWZ+3CrnJ4JlNXEoGmaULbtqHruigaRzQ2xy9k3a4kkuC+SloIkrHxK2hu9TeSKRMJtiGiVNXOT4wcYx53waGkRzKQKC19FsD29BIEO28WSaSoJFL0yUOc8hxayJe9kqBqEkvS86PeJsklQyxJu5DUVF9JsHNvJD2/rCpJcm/J27YrSfXz975Zb5MEK1rlmRQk1+/EM5+dO7skIEquZVmi41dh/lsrmYOvknagdKqvJNx+Jr053a41bNlTSaqph/SgV8ztmrIv9jtyIynsCyWy94lKCvuCZ0xFUrRHfJWsgzW8AK/cZ2tYS12SAAAAAElFTkSuQmCC) в правом верхнем углу страницы. Чтобы найти приложение, нажмите эту кнопку и введите имя приложения или часть имени приложения в поле **by apps**.

image291.png

Также можно фильтровать существующие приложения, используя выпадающие меню by workspace, by team и by orgstructure, а также выбрав пункт Supported only или With template pipelines. Настройки фильтра сохраняются в системе даже между сессиями пользователя.

Нажмите кнопку Reset filters image292.png в правом верхнем углу страницы, чтобы сбросить все текущие фильтры.

Нажав значок Show app details, перейдите на страницу приложения.

image297.png

На странице приложения можно просмотреть, а также, при необходимости, отредактировать информацию о нем или выполнить необходимые настройки.

Изображение выглядит как текст
Автоматически созданное описание


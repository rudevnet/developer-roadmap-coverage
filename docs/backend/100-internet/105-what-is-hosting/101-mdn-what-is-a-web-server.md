# Что такое веб-сервер

> Оригинал статьи можно посмотреть [тут](https://developer.mozilla.org/ru/docs/Learn/Common_questions/Web_mechanics/What_is_a_web_server).

В этой статье мы узнаем, что из себя представляют веб-серверы, как они работают, и почему они так важны.

| Необходимые знания: | Вы должны уже знать, [как работает Интернет](https://developer.mozilla.org/ru/docs/Learn/Common_questions/Web_mechanics/How_does_the_Internet_work) и [понимать разницу между страницей, сайтом, сервером и поисковой системой.](https://developer.mozilla.org/ru/docs/Learn/Common_questions/Web_mechanics/Pages_sites_servers_and_search_engines) |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Цель:               | Вы узнаете, что такое веб-сервер и получите общее представление о том, как он работает.                                                                                                                                                                                                                                                             |

## Краткое описание

Понятие «веб-сервер» может относиться как к аппаратной начинке, так и к программному обеспечению. Или даже к обеим частям, работающим совместно.

1. С точки зрения "железа", «веб-сервер» — это компьютер, который хранит файлы сайта (HTML-документы, CSS-стили, JavaScript-файлы, картинки и другие) и доставляет их на устройство конечного пользователя (веб-браузер и т.д.). Он подключён к сети Интернет и может быть доступен через доменное имя, подобное `mozilla.org`.
2. С точки зрения ПО, веб-сервер включает в себя несколько компонентов, которые контролируют доступ веб-пользователей к размещённым на сервере файлам, как минимум — это _HTTP-сервер_. HTTP-сервер — это часть ПО, которая понимает [URL-адреса](https://developer.mozilla.org/ru/docs/Glossary/URL) (веб-адреса) и [HTTP](https://developer.mozilla.org/ru/docs/Glossary/HTTP) (протокол, который ваш браузер использует для просмотра веб-страниц).

На самом базовом уровне, когда браузеру нужен файл, размещённый на веб-сервере, браузер запрашивает его через HTTP-протокол. Когда запрос достигает нужного веб-сервера ("железо"), сервер HTTP (ПО) принимает запрос, находит запрашиваемый документ (если нет, то сообщает об ошибке [404](https://developer.mozilla.org/ru/docs/Web/HTTP/Status/404)) и отправляет обратно, также через HTTP.

![Basic representation of a client/server connection through HTTP](/assets/backend/internet/what-is-hosting/mdn-what-is-a-web-server/web-server.svg)

Чтобы опубликовать веб-сайт, необходим либо статический, либо динамический веб-сервер.

**Статический веб-сервер**, или стек, состоит из компьютера ("железо") с сервером HTTP (ПО). Мы называем это «статикой», потому что сервер посылает размещённые файлы в браузер «как есть».

**Динамический веб-сервер** состоит из статического веб-сервера и дополнительного программного обеспечения, чаще всего _сервера приложения_ и _базы данных_. Мы называем его «динамическим», потому что сервер приложений изменяет исходные файлы перед отправкой в ваш браузер по HTTP.

Например, для получения итоговой страницы, которую вы просматриваете в браузере, сервер приложений может заполнить HTML-шаблон данными из базы данных. Такие сайты, как MDN или Википедия, состоят из тысяч веб-страниц, но они не являются реальными HTML документами — лишь несколько HTML-шаблонов и гигантские базы данных. Эта структура упрощает и ускоряет сопровождение веб-приложений и доставку контента.

## Погружаемся глубже

Чтобы загрузить веб-страницу, как мы уже говорили, ваш браузер отправляет запрос к веб-серверу, который приступает к поиску запрашиваемого файла в своём собственном пространстве памяти. Найдя файл, сервер считывает его, обрабатывает как ему это необходимо, и отсылает в браузер. Давайте рассмотрим эти шаги более подробно.

### Хостинг файлов

Прежде всего, веб-сервер должен содержать файлы веб-сайта, а именно все HTML-документы и связанные с ними ресурсы, включая изображения, CSS-стили, JavaScript-файлы, шрифты и видео.

Технически, вы можете разместить все эти файлы на своём компьютере, но гораздо удобнее хранить их на выделенном веб-сервере, который:

- всегда запущен и работает
- всегда подключён к Интернету
- имеет неизменный IP адрес (не все [провайдеры](https://developer.mozilla.org/ru/docs/Glossary/ISP) предоставляют статический IP-адрес для домашнего подключения)
- обслуживается третьей, сторонней компанией

По всем этим причинам поиск хорошего хостинг-провайдера является ключевой частью создания вашего сайта. Рассмотрите многочисленные предложения компаний и выберите то, что соответствует вашим потребностям и бюджету (предложения варьируются от бесплатных до тысяч долларов в месяц). Вы можете найти подробности в [этой статье.](https://developer.mozilla.org/ru/docs/Learn/Common_questions/Tools_and_setup/How_much_does_it_cost#hosting)

Как только вы решили проблему с хостингом, вам понадобится только [загрузить свои файлы на ваш веб-сервер](https://developer.mozilla.org/ru/docs/Learn/Common_questions/Tools_and_setup/Upload_files_to_a_web_server).

### Связь по HTTP

Во-вторых, веб-сервер обеспечивает поддержку [HTTP](https://developer.mozilla.org/ru/docs/Glossary/HTTP) (англ. _**H**yper**t**ext **T**ransfer **P**rotocol - протокол передачи гипертекста_). Как следует из названия, HTTP указывает, как передавать гипертекст (т.е. связанные веб-документы) между двумя компьютерами.

Протокол представляет собой набор правил для связи между двумя компьютерами. HTTP является текстовым протоколом без сохранения состояния.

- **Текстовый**:Все команды являются простым человекочитаемым текстом.
- **Не сохраняет состояние**: Ни клиент, ни сервер не помнят о предыдущих соединениях. Например, опираясь только на HTTP, сервер не сможет вспомнить введённый вами пароль или на каком шаге транзакции вы находитесь. Для таких задач, вам потребуется сервер приложения. (Мы остановимся на этих технологиях в следующих статьях.)

HTTP задаёт строгие правила взаимодействия клиента и сервера. Мы рассмотрим сам протокол HTTP в [технической статье](https://developer.mozilla.org/ru/docs/Web/HTTP) немного позднее. Пока достаточно знать об этих правилах:

- Исключительно _клиенты_ могут производить HTTP-запросы, и только на _сервера_. Сервера способны только отвечать на HTTP-_запросы клиента_.
- При запросе файла по HTTP, клиент должен сформировать файловый [URL](https://developer.mozilla.org/ru/docs/Glossary/URL).
- Веб-сервер _должен ответить_ на каждый HTTP-запрос, по крайней мере сообщением об ошибке.

[![The MDN 404 page as an example of such error page](/assets/backend/internet/what-is-hosting/mdn-what-is-a-web-server/mdn-404.jpg)](https://developer.mozilla.org/ru/docs/Web/HTTP/Status/404)

На веб-сервере HTTP-сервер отвечает за обработку входящих запросов и ответ на них.

1. При получении запроса, HTTP-сервер сначала проверяет, существует ли ресурс по данному URL.
2. Если это так, веб-сервер отправляет содержимое файла обратно в браузер. Если нет, сервер приложения генерирует необходимый ресурс.
3. Если ничто из этого не возможно, веб-сервер возвращает сообщение об ошибке в браузер, чаще всего “404 Not Found”. (Это ошибка настолько распространена, что многие веб-дизайнеры тратят большое количество времени на разработку 404 страниц об ошибках.)

## Статический и Динамический контент

Грубо говоря, сервер может отдавать статическое или динамическое содержимое. «Статическое» означает «отдаётся как есть». Статические веб-сайты делаются проще всего, поэтому мы предлагаем вам сделать свой первый сайт статическим.

«Динамическое» означает, что сервер обрабатывает данные или даже генерирует их на лету из базы данных. Это обеспечивает большую гибкость, но технически сложнее в реализации и обслуживании, из-за чего процесс создания сайта очень сильно усложняется.

Невозможно предложить единый готовый сервер приложений, который будет правильным решением для каждого возможного варианта использования. Некоторые серверы приложений предназначены для размещения и управления блогами, вики-сайтами или решениями для электронной коммерции, в то время как другие являются более общими. Если вы создаете динамический веб-сайт, найдите время, чтобы изучить свои требования и найти технологию, которая лучше всего соответствует вашим потребностям.

Большинству разработчиков веб-сайтов не нужно создавать сервер приложений с нуля, потому что существует множество готовых решений, многие из которых легко настраиваются. Но если вам нужно создать свой собственный сервер, вы, вероятно, захотите использовать серверную структуру, используя ее существующий код и библиотеки и расширяя только те части, которые вам нужны, чтобы соответствовать вашему варианту использования. Только относительно небольшое число разработчиков должно разрабатывать сервер полностью с нуля: например, чтобы соответствовать жестким ограничениям по ресурсам встроенной системы. Если вы хотите поэкспериментировать с созданием сервера, просмотрите [Серверное программирование веб-сайтов](https://developer.mozilla.org/ru/docs/Learn/Server-side).

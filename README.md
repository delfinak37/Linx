# Безопасная среда сайта "В гостях у троллей"

## Постановка задачи
Задача заключается в реализации безопасной среды сайта по настольным играм «В гостях у троллей».

## Цели
1. **Обеспечение безопасности данных участников клуба**
   - Защита личных данных, включая контактную информацию и историю посещений мероприятий.
   - Предотвращение несанкционированного доступа к регистрационным данным и результатам турниров.

2. **Улучшение организации и управления мероприятиями**
   - Создание системы, которая минимизирует человеческие ошибки при планировании расписания и управлении инвентарем.
   - Оптимизация системы оповещений участников для предотвращения пропущенных событий и опозданий.

3. **Поддержание инвентаря в хорошем состоянии**
   - Разработка системы для отслеживания состояния настольных игр и их компонентов.
   - Внедрение эффективного контроля за использованием инвентаря участниками.

4. **Гарантия честности в проведении турниров**
   - Автоматизация подсчёта результатов и исключение возможности манипуляций с результатами.
   - Обеспечение прозрачности турниров, публикация рейтингов и статистики.

5. **Защита онлайн-ресурсов клуба**
   - Предотвращение атак на веб-сайт или приложение клуба, таких как DDoS или SQL-инъекции.
   - Обеспечение стабильной работы ресурса, чтобы он был доступен всем участникам в любое время.

## Предположения
1. **Участники заинтересованы в простоте и безопасности регистрации**
   - Пользователи готовы проходить двухфакторную аутентификацию для повышения безопасности своих данных.
   - Участники ожидают, что регистрация и управление личным кабинетом будут интуитивно понятными.

2. **Честность и прозрачность турниров важны для удержания игроков**
   - Игроки ценят справедливость в соревнованиях и предпочитают видеть прозрачные и легко проверяемые результаты.
   - Ожидается, что автоматизированная система управления турнирами будет точной и стабильной, исключая человеческий фактор в подсчёте результатов.

3. **Онлайн-ресурсы клуба могут стать мишенью для атак**
   - С ростом популярности клуба увеличится вероятность кибератак, направленных на получение данных участников или вывод ресурса из строя.
   - Вероятно, что защита от основных видов атак (SQL-инъекций, XSS, DDoS) является минимальной необходимостью для стабильной работы клуба.

4. **Стабильная и удобная система уведомлений уменьшит количество пропусков событий**
   - Если участники будут своевременно получать напоминания о мероприятиях, вероятность пропусков и недоразумений значительно снизится.
   - Предполагается, что многие игроки используют современные средства связи (мобильные приложения, email) и ожидают интеграцию этих сервисов в работу клуба.

## Архитектура решения

### Компоненты
| Название               | Назначение                                                 |
|-----------------------|-----------------------------------------------------------|
| Реализация инвентаря  | Управление инвентарем клуба, включая регистрацию настольных игр, отслеживание использования и состояния |
| Регистрация игроков    | Система регистрации участников для клубных мероприятий и турниров |
| Расписание мероприятий  | Организация и управление расписанием мероприятий клуба, включая турниры и игровые встречи |
| Центральный модуль     | Центральный модуль для координации всех процессов клуба: инвентарь, расписание, регистрация, результаты |
| Монитор безопасности    | Авторизация и контроль безопасности данных участников, предотвращение несанкционированного доступа |
| Система оповещений     | Система обмена сообщениями между компонентами, ответственная за уведомления участников и сотрудников |

### Алгоритм взаимодействия структур
![image](https://github.com/user-attachments/assets/b929fcad-ad6a-4650-aa9b-c1bb5929c9e9)


### Реализация инвентаря
С практической точки зрения, реализация инвентаря включает в себя управление настольными играми клуба, что подразумевает регистрацию каждой игры с детальной информацией, такой как название, жанр, количество компонентов и текущее состояние. Это также включает отслеживание использования игр, фиксируя количество раз, когда они были выданы, а также их статус — находятся ли они в наличии, на выдаче или повреждены. Регулярные проверки наличия игр и их компонентов помогают поддерживать точность данных и позволяют в реальном времени обновлять информацию о состоянии инвентаря, что важно для эффективного управления и повышения качества обслуживания участников клуба. Реализация инвентаря требует защиты данных о настольных играх (ограничение доступа к инвентарю, учет связанных с инвентарем действий).

### Регистрация игроков
С практической точки зрения, регистрация игроков включает в себя создание системы, которая позволяет участникам легко и быстро зарегистрироваться для участия в клубных мероприятиях и турнирах. Система должна быть интуитивно понятной, чтобы пользователи могли управлять своими профилями, обновлять личную информацию и просматривать свою историю участия в мероприятиях. Удобный интерфейс для регистрации и управления личным кабинетом повышает вовлеченность участников способствует активному участию в жизни клуба. Регистрация игроков должна предусматривать защиту личных данных участников, включая их контактную информацию и историю посещений (внедрение двухфакторной аутентификации, ограничение доступа к функциям регистрации).

### Центральный модуль
Центральный модуль служит основой для эффективного функционирования всей системы клуба настольных игр. Он координирует взаимодействие между всеми компонентами, такими как инвентаризация, регистрация игроков и расписание мероприятий, обеспечивая интеграцию процессов и обмен данными между ними. Благодаря этому модулю удается оптимизировать управление и повысить прозрачность операций, что улучшает опыт участников. Центральный модуль необходим для обеспечения согласованности действий всех подсистем, автоматизации рутинных задач и создания единой платформы для мониторинга всех процессов клуба.

### Монитор безопасности
Монитор безопасности отвечает за защиту данных участников и предотвращение несанкционированного доступа к системе. Он контролирует авторизацию пользователей и управляет доступом к различным компонентам, обеспечивая взаимодействовие с системой только доверенного круга лиц. Этот модуль также включает в себя функции для обнаружения и предотвращения угроз, таких как попытки взлома или кибератаки, что критически важно для защиты личной информации участников и сохранения доверия к клубу. 

## Безопасность веб-сервиса клуба «В гостях у троллей»

Обеспечение безопасности передачи данных является критически важным аспектом для веб-сервиса клуба. Все данные, связанные с личной информацией участников и событиями клуба, должны передаваться по защищённым каналам. Для этого используется протокол HTTPS, который обеспечивает шифрование данных и защищает их от перехвата злоумышленниками. Применение современных алгоритмов шифрования, таких как TLS, гарантирует, что данные остаются конфиденциальными в процессе передачи.

Также необходимо гарантировать уникальность и целостность данных, связанных с транзакциями и действиями участников. Это достигается путём генерации уникальных токенов для каждой операции, а также использованием временных меток и случайных чисел, чтобы предотвратить повторные атаки. Конфиденциальность данных обеспечивается не только путём их шифрования, но и применения принципа минимальных привилегий для доступа к информации. Для обработки чувствительных данных, таких как личная информация игроков, целесообразно использовать токенизацию, что позволяет заменять реальные данные токенами при обработке.

Целостность транзакций и их успешная доставка обеспечиваются с помощью цифровых подписей, которые подтверждают подлинность данных и предотвращают их подмену. Также рекомендуется внедрить систему мониторинга и логирования, чтобы отслеживать статус транзакций и выявлять возможные нарушения.

В контексте негативных сценариев безопасности важно учитывать угрозы, такие как перехват данных, нарушение целостности токенов, атаки на второй фактор аутентификации и компрометация веб-сервиса. Для защиты от этих угроз необходимо регулярно обновлять системы, использовать криптографически стойкие методы генерации токенов, внедрять защиту от DDoS-атак и защищать локальные данные пользователей на устройствах.

## Модель угроз для веб-сервиса клуба настольных игр
### Угрозы кибератак
#### Атаки на веб-приложение
- **SQL-инъекции**: Злоумышленники могут попытаться манипулировать запросами к базе данных, чтобы получить несанкционированный доступ к данным или изменить их.
- **Кросс-сайтовый скриптинг (XSS)**: Ввод вредоносного кода в поля ввода, что может привести к краже данных пользователей или сессий.

#### Атаки DDoS
- **Отказ в обслуживании**: Массированная атака на сервер, что делает веб-сервис недоступным для легитимных пользователей.

### Угрозы к данным
#### Утечка конфиденциальных данных
- **Неправомерный доступ к данным пользователей**: Злоумышленники могут попытаться получить доступ к личной информации пользователей, включая пароли и платежные данные.
#### Нарушение целостности данных
- **Неавторизованные изменения данных**: Вредоносные пользователи могут попытаться изменить или удалить данные, такие как учетные записи игроков или результаты турниров.

### Угрозы управления доступом
#### Недостаточная защита учетных записей
- **Слабые пароли**: Пользователи могут использовать легкие для угадывания пароли, что облегчает злоумышленникам доступ к их учетным записям.
- **Неэффективная аутентификация**: Отсутствие многофакторной аутентификации может привести к тому, что злоумышленники получат доступ к системам с помощью украденных учетных данных.

### Физические угрозы
#### Доступ к серверам
- **Физический доступ к серверу**: Неавторизованные лица могут получить доступ к серверам, на которых развернуто приложение, что может привести к прямому нарушению безопасности.
  
### Угрозы к инфраструктуре
#### Уязвимости в сторонних компонентах
- **Уязвимости в библиотеке или фреймворке**: Использование устаревших или уязвимых компонентов может привести к несанкционированному доступу или атаке.

### Негативные сценарии
- **Перехват данных**: Вредоносные пользователи могут пытаться перехватить данные, передаваемые между клиентом и сервером, особенно если соединение не защищено.
- **Фишинг**: Злоумышленники могут создать фальшивые страницы, чтобы обманом заставить пользователей вводить свои учетные данные.
#### Меры по снижению рисков
1. **Использование безопасных протоколов**: Обеспечение HTTPS для шифрования данных во время передачи.
2. **Регулярные обновления**: Патчинг уязвимостей в программном обеспечении и обновление компонентов.
3. **Внедрение многофакторной аутентификации**: Для повышения безопасности учетных записей пользователей.
4. **Мониторинг и логирование**: Внедрение систем мониторинга для обнаружения подозрительной активности.

## Возможные угрозы и сценарии их реализации
### Неисправный контроль доступа
   Контроль доступа обеспечивает соблюдение политики таким образом, что пользователи не могут действовать вне своих привелегий. Сбои обычно приводят к несанкционированному раскрытию информации, изменению или уничтожению данных или выполнению бизнес-функции вне рамок привилегий пользователя.

#### Сценарий №1:
Приложение использует непроверенные данные в вызове SQL, который обращается к информации об учетной записи.

![Без имени](https://github.com/user-attachments/assets/323ecdbb-54e7-4ee9-84bb-cdd1d83c1960)

Злоумышленник просто изменяет параметр браузера 'acct'. Если проверка выполнена некорректно, злоумышленник может получить доступ к счету любого пользователя.

![Без имени](https://github.com/user-attachments/assets/f00e5c0e-7a0e-4437-80f6-bd195a11372e)

#### Сценарий №2:
Атакующий просто заставляет браузеры переходить на целевые URL-адреса. Для доступа к странице администратора требуются права администратора.

![Без имени](https://github.com/user-attachments/assets/f0535f94-27c0-435b-93f5-f1d53beaf399)

Если неаутентифицированный пользователь может получить доступ к любой из страниц, это недостаток. Если неадминистратор может получить доступ к странице администратора, это недостаток.

#### Способы противодействия:
- Настройка и управление доступом.
- Регистрация сбоев контроля доступа, оповещение администраторов при необходимости (например, о повторных сбоях).
- Идентификаторы сеансов с сохранением состояния должны быть аннулированы на сервере после выхода из системы.

### SQL-Инъекция
Приложение уязвимо для атаки, когда:
- Пользовательские данные не проверяются, не фильтруются и не очищаются приложением.
- Динамические запросы или непараметризованные вызовы без экранирования с учетом контекста используются непосредственно в интерпретаторе.
- Враждебные данные используются в параметрах поиска объектно-реляционного отображения (ORM) для извлечения дополнительных конфиденциальных записей.
- Враждебные данные используются напрямую или объединяются. SQL или команда содержат структуру и вредоносные данные в динамических запросах, командах или хранимых процедурах.

Некоторые из наиболее распространенных инъекций — это SQL, NoSQL, команды ОС, объектно-реляционное отображение (ORM), LDAP и внедрение языка выражений (EL) или библиотеки навигации графа объектов (OGNL). Концепция одинакова для всех интерпретаторов. Проверка исходного кода — лучший метод обнаружения уязвимости приложений для инъекций. Настоятельно рекомендуется автоматическое тестирование всех параметров, заголовков, URL, файлов cookie, входных данных JSON, SOAP и XML. Организации могут включать статические (SAST), динамические (DAST) и интерактивные (IAST) инструменты тестирования безопасности приложений в конвейер CI/CD для выявления недостатков, внесенных инъекцией, до развертывания в производство.

#### Сценарий №1:
Приложение использует ненадежные данные при построении следующего уязвимого вызова SQL:

![Без имени](https://github.com/user-attachments/assets/f1d91ef2-0aa7-4a37-90d6-f1a8e2d458ba)

#### Сценарий №2:
Аналогичным образом слепое доверие приложения к фреймворкам может привести к тому, что запросы будут по-прежнему уязвимы (например, Hibernate Query Language (HQL)):

![Без имени](https://github.com/user-attachments/assets/d6fcbd0b-2393-4125-8373-aca2565d16e8)

В обоих случаях злоумышленник изменяет значение параметра «id» в своем браузере, чтобы отправить: ' UNION SLEEP(10);--. Например:

![Без имени](https://github.com/user-attachments/assets/0f578efd-34e0-4f97-a10a-38923b994a8e)

Это меняет смысл обоих запросов, возвращающих все записи из таблицы счетов. Более опасные атаки могут изменять или удалять данные или даже вызывать хранимые процедуры.

#### Способы противодействия:
- Предпочтительным вариантом является использование безопасного API, который полностью избегает использования интерпретатора, предоставляет параметризованный интерфейс или переходит на инструменты объектно-реляционного отображения (ORM).
- Использование положительной проверки входных данных на стороне сервера.
- Использование LIMIT и других элементов управления SQL в запросах, чтобы предотвратить массовое раскрытие записей в случае SQL-инъекции.
- Экранирование специальных символов, используя специальный синтаксис экранирования для этого интерпретатора.

## Заключение
...

## Источники данных на котором основывался данный отчет:
#### [OWASP.ORG](https://owasp.org/Top10/)
#### [cwe.mitre.org](https://cwe.mitre.org/)
#### [zaproxy.org](https://www.zaproxy.org/getting-started/)

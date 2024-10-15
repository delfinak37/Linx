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
![Презентация1](https://github.com/user-attachments/assets/0cade5c2-6fce-4c1b-84bd-431dfa2625b1)


### Реализация инвентаря
С точки зрения практической стороны, реализация инвентаря включает в себя управление настольными играми клуба, что подразумевает регистрацию каждой игры с детальной информацией, такой как название, жанр, количество компонентов и текущее состояние. Это также включает отслеживание использования игр, фиксируя количество раз, когда они были выданы, а также их статус — находятся ли они в наличии, на выдаче или повреждены. Регулярные проверки наличия игр и их компонентов помогают поддерживать точность данных и позволяют в реальном времени обновлять информацию о состоянии инвентаря, что важно для эффективного управления и повышения качества обслуживания участников клуба. С точки зрения безопасности в сети, реализация инвентаря требует защиты данных о настольных играх. Это может быть достигнуто путем шифрования данных, что предотвращает возможность их утечки. Доступ к инвентарю должен быть ограничен только для авторизованных пользователей, таких как администраторы и ответственные за инвентарь, чтобы минимизировать риск несанкционированного доступа. Важно также вести учет всех действий, связанных с инвентарем, чтобы обеспечить прозрачность процессов и возможность отслеживания изменений, что добавляет уровень доверия к системе.

### Регистрация игроков
С практической стороны, регистрация игроков включает в себя создание системы, которая позволяет участникам легко и быстро зарегистрироваться для участия в клубных мероприятиях и турнирах. Система должна быть интуитивно понятной, чтобы пользователи могли управлять своими профилями, обновлять личную информацию и просматривать свою историю участия в мероприятиях. Удобный интерфейс для регистрации и управления личным кабинетом повышает вовлеченность участников и способствует активному участию в жизни клуба. С точки зрения безопасности в сети, регистрация игроков должна предусматривать защиту личных данных участников, включая их контактную информацию и историю посещений. Внедрение двухфакторной аутентификации для пользователей станет важным шагом в повышении безопасности, так как это добавит дополнительный уровень защиты. Все данные, собранные во время регистрации, должны быть защищены с помощью современных методов шифрования, чтобы предотвратить утечку информации или несанкционированный доступ. Кроме того, доступ к функциям регистрации должен быть ограничен, чтобы только авторизованные лица могли управлять данными участников.

### Центральный модуль
Центральный модуль служит основой для эффективного функционирования всей системы клуба настольных игр. Он координирует взаимодействие между всеми компонентами, такими как инвентаризация, регистрация игроков и расписание мероприятий, обеспечивая интеграцию процессов и обмен данными между ними. Благодаря этому модулю удается оптимизировать управление и повысить прозрачность операций, что улучшает опыт участников. Центральный модуль необходим для обеспечения согласованности действий всех подсистем, автоматизации рутинных задач и создания единой платформы для мониторинга всех процессов клуба.

### Монитор безопасности
Монитор безопасности отвечает за защиту данных участников и предотвращение несанкционированного доступа к системе. Он контролирует авторизацию пользователей и управляет доступом к различным компонентам, обеспечивая, чтобы только доверенные лица могли взаимодействовать с системой. Этот модуль также включает в себя функции для обнаружения и предотвращения угроз, таких как попытки взлома или кибератаки, что критически важно для защиты личной информации участников и сохранения доверия к клубу. Монитор безопасности является важным элементом, обеспечивающим надежную защиту данных и стабильную работу всей системы.

## Безопасность веб-сервиса клуба «В гостях у троллей»

Обеспечение безопасности передачи данных является критически важным аспектом для веб-сервиса клуба. Все данные, связанные с личной информацией участников и событиями клуба, должны передаваться по защищённым каналам. Для этого используется протокол HTTPS, который обеспечивает шифрование данных и защищает их от перехвата злоумышленниками. Применение современных алгоритмов шифрования, таких как TLS, гарантирует, что данные остаются конфиденциальными в процессе передачи.

Также необходимо гарантировать уникальность и целостность данных, связанных с транзакциями и действиями участников. Это достигается путём генерации уникальных токенов для каждой операции, а также использованием временных меток и случайных чисел, чтобы предотвратить повторные атаки. Конфиденциальность данных обеспечивается путём их шифрования и применения принципа минимальных привилегий для доступа к информации. Для обработки чувствительных данных, таких как личная информация игроков, целесообразно использовать токенизацию, что позволяет заменять реальные данные токенами при обработке.

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
- 
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


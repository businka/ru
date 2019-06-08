# 3 Термины, определения, символы и сокращения

Все термины и определения, как они определены в Основной спецификации OCF, также применимы к этой спецификации.

## 3.1 Термины и определения

Как определено в основной спецификации OCF и спецификации безопасности OCF со следующими
дополнения

### 3.1.1 Облачный провайдер

организация или организация, на которой размещено облако OCF.

### 3.1.2 Облако OCF

Облако OCF - это не Устройство OCF, а логическая сущность, которой владеет поставщик облака. Облако OCF уполномочено взаимодействовать с Устройством от имени Пользователя Облака OCF.

## 3.2 Символы и сокращения

### 3.2.1 UX

Пользовательский опыт

## 3.3 Условные обозначения

В этой спецификации ряд терминов, условий, механизмов, последовательностей, параметров, событий, состояний или аналогичных терминов печатаются с первой буквой каждого слова в верхнем регистре и остальными строчными буквами (например, Сетевая архитектура). Любое использование этих слов в нижнем регистре имеет нормальное техническое английское значение.

## 3.4 Типы данных

Как определено в основной спецификации OCF.

# 4 Соглашения о документе и организация

В этом документе функции описаны как обязательные, рекомендованные, разрешенные или УСТАРЕВШИЕ следующим образом:
Обязательный (или обязательный или обязательный) (M).

• Эти основные функции должны быть реализованы в соответствии с базовой архитектурой. Фразы «не должен» и «ЗАПРЕЩЕНО» указывают на поведение, которое запрещено, т. Е. Если выполнено, значит, реализация не соответствует. Рекомендуется (или должен) (S).

• Эти функции добавляют функциональность, поддерживаемую базовой архитектурой, и должны быть реализованы.
Рекомендованные функции используют возможности базовой архитектуры, как правило, без значительного увеличения сложности. Обратите внимание, что для тестирования соответствия, если рекомендованная функция реализована, она должна соответствовать указанным требованиям, чтобы соответствовать этим рекомендациям. Некоторые рекомендуемые функции могут стать требованиями в будущем. Фраза «не должен» указывает на поведение, которое разрешено, но не рекомендуется.
Разрешено (может или разрешено) (O).

• Эти функции не требуются и не рекомендуются базовой архитектурой, но если функция реализована, она должна соответствовать указанным требованиям, чтобы соответствовать этим рекомендациям.
DEPRECATED.

• Хотя эти функции все еще описаны в этой спецификации, они не должны быть реализованы за исключением обратной совместимости. Возникновение устаревшей функции во время работы реализации, соответствующей текущей спецификации, не влияет на работу реализации и не приводит к возникновению ошибок. Для обратной совместимости может потребоваться, чтобы функция была реализована и функционировала так, как указано, но она никогда не должна использоваться реализациями, соответствующими данной спецификации.
Условно разрешено (CA)

• Определение или поведение зависит от условия. Если указанное условие выполнено, то определение или поведение разрешено, в противном случае оно не допускается.
Условно требуется (ЧР)

• Определение или поведение зависит от условия. Если указанное условие выполнено, тогда требуется определение или поведение. В противном случае определение или поведение разрешено по умолчанию, если специально не определено как не разрешено.


Строки, которые следует понимать буквально, заключены в «двойные кавычки».

Подчеркнутые слова напечатаны курсивом.

# 5 Обзор

## 5.1 Введение

Облако OCF расширяет использование CoAP, чтобы устройство могло взаимодействовать с облаком, используя следующие функции

Протокол CoAP через TCP, определенный в основной спецификации OCF

Каталог ресурсов, определенный в разделе основной спецификации OCF

Требования в этой спецификации
Требования безопасности и SVR, определенные в Спецификации безопасности OCF

Устройства, которые не находятся в одной локальной сети, могут взаимодействовать друг с другом, используя CoAP через TCP (см. Спецификацию ядра OCF) через Облако OCF. В любой момент времени устройство настроено на использование не более одного облака OCF. Облако OCF группирует Устройства, принадлежащие одному и тому же Пользователю Облака OCF, под идентификатором пользователя, созданным в Облаке OCF. Все устройства, зарегистрированные в облаке OCF и принадлежащие к одному и тому же идентификатору пользователя, могут обмениваться данными друг с другом в зависимости от того, какие устройства авторизуют облако OCF в политиках ACE2.
Обратите внимание, что облако OCF - это не устройство OCF, а логическая сущность, которой владеет поставщик облака. Облако OCF авторизовано для связи с устройством пользователем облака OCF

## 5.2 Поток взаимодействия

В этом разделе описывается взаимодействие элементов с общим облаком OCF. Рисунок 1 представляет общее введение:

![](figure\cen01.png)

Рисунок 1 Архитектура развертывания OCF Cloud

| Steps | Description                                                  |
| ----- | ------------------------------------------------------------ |
| 1     | Посредник получает   токен доступа для пользователя облака OCF от поставщика авторизации. |
| 2     | Посредник   регистрируется в облаке OCF                      |
| 3     | Посредник предоставляет   на устройстве «oic.r.coapcloudconf» с токеном   доступа, URL-адресом облака OCF, идентификатором (UUID) облака OCF и, опционально, именем поставщика авторизации |
| 4, 5  | Устройство   устанавливает сеанс TLS в облаке OCF и впоследствии регистрируется в облаке OCF |
| 6, 7  | Облако OCF проверяет запрос на   регистрацию и авторизует токен доступа. Возврат информации на устройство в «uid» пользователя OCF Cloud и истечения срока   действия токена доступа |

Таблица 1. Поток развертывания в облаке OCF

Облако OCF - это логический объект, с которым устройство OCF связывается через постоянное соединение TLS. Он заключает в себе две функции:

• функция сервера учетных записей, которая представляет собой логический объект, который обрабатывает регистрацию устройства, проверку токена доступа и обрабатывает запросы на вход и обновление токена от устройства.
• Каталог ресурсов в соответствии с Базовой Спецификацией OCF. Каталог ресурсов предоставляет информацию о ресурсах, публикуемую устройствами. Клиент, обнаруживая Устройства, получает ответ из Каталога ресурсов от имени Устройства. С помощью информации, включенной в ответ из каталога ресурсов, клиент может подключиться к устройству через облако OCF.

## 5.3 Облачный операционный поток

В следующих подразделах приведен информативный обзор потока, в результате которого устройство регистрируется в облаке OCF, а клиент взаимодействует с этим устройством. Разделы содержат ссылки на применимые Разделы в данной Спецификации и другие Спецификации, которые предоставляют нормативные детали.

Поток состоит из следующих этапов высокого уровня:

• Предварительные требования и создание учетной записи пользователя в облаке OCF (раздел 5.3.1)
• Регистрация посредника в облаке OCF (раздел 5.3.2)
• Предоставление устройства посредником (раздел 5.3.3)
• Регистрация устройства в облаке OCF (раздел 5.3.4)
• Подключение устройства к облаку OCF (раздел 5.3.5)
• Устройства, публикующие ссылки на OCF Cloud RD (раздел 5.3.6)
• Связь между клиентом и сервером через облако OCF (раздел 5.3.7)
• Обновление устройства с помощью облака OCF (раздел 5.3.8).
• Устройство закрывает соединение с облаком OCF (раздел 5.3.9)
• Отмена регистрации устройства в облаке OCF (раздел 5.3.10)

### 5.3.1 Предварительные условия и создание учетной записи пользователя в облаке OCF

Пользователь OCF Cloud имеет устройство, которое он хочет подключить к облаку OCF, чтобы иметь к нему удаленный доступ.
Устройство подключено к сети OCF, как определено в спецификации безопасности OCF.
Пользователь OCF Cloud загружает Медиатора на свое персональное устройство (например, телефон), которое будет использоваться для предоставления Устройства. Посредник настраивается с помощью какого-либо внеполосного процесса или посредством него для получения URL-адреса облака OCF (например, посредником может быть приложение от провайдера облака).
Пользователь OCF Cloud имеет учетные данные для аутентификации пользователя OCF Cloud у провайдера авторизации (то есть имя пользователя / пароль или подобное)

### 5.3.2 Регистрация посредника в облаке OCF

См. Разделы 8.1.2.2, 0
Посредством некоторого триггера (например, UX или другого механизма вне границ) посредник аутентифицирует пользователя OCF Cloud для поставщика авторизации и запрашивает токен доступа у поставщика авторизации.
Посредник регистрируется путем предоставления своего токена доступа в облако OCF, которое проверяет токен и создает идентификатор пользователя, с которым связан посредник. Все экземпляры посредника для одного и того же пользователя облака OCF будут связаны с одним и тем же идентификатором пользователя. Точно так же один и тот же идентификатор пользователя может использоваться для назначения нескольких устройств одному и тому же пользователю облака OCF.

### 5.3.3 Предоставление устройства посредником

См. Раздел 8.1.2.3; см. также Раздел спецификации безопасности OCF 7.5.1.
Посредник подключается к устройству через обычные процессы OCF. Затем посредник запрашивает токен доступа из облака OCF для предоставляемого устройства. Посредник обновляет ресурс «oic.r.coapcloudconf» на устройстве с помощью токена доступа, полученного из облака OCF, URI облака OCF и UUID облака OCF. Посредник может также указать имя провайдера аутентификации. Обратите внимание, что этот токен доступа может использоваться только один раз для первоначальной регистрации устройства в облаке OCF.

### 5.3.4 Регистрация устройства в облаке OCF.

См. Разделы 8.1.3, 8.1.4; см. также разделы 10.4, 13.10 спецификации безопасности OCF

При настройке Посредником ресурса «oic.r.coapcloudconf» Устройство устанавливает TLS-соединение с облаком OCF, используя предоставленный URI, а также сертификат производителя устройства и сертификат (ы) привязки доверия для сертификата облака OCF. проверка, оба из которых были установлены производителем устройства. Сочетание сертификата производителя устройства и токена доступа пользователя OCF Cloud обеспечивает взаимодействие между OCF Cloud и устройствами OCF в пределах домена пользователя OCF Cloud.
Чтобы зарегистрироваться в облаке OCF, устройство затем отправляет операцию UPDATE в ресурс учетной записи в облаке OCF, который включает токен доступа, предоставленный в ресурсе «oic.r.coapcloudconf». Обратите внимание, что облако OCF поддерживает уникальный экземпляр ресурса учетной записи для каждого устройства.
Если UPDATE успешно подтвержден, то OCF Cloud предоставляет ответ UPDATE, который может предоставить обновленные значения для токена доступа и сведения о времени жизни (истечении) этого токена. Облако OCF также включает в себя идентификатор пользователя, с которым связано устройство. Все возвращенные значения надежно хранятся на устройстве. Возвращенный токен доступа не записывается в ресурс «oic.r.coapcloudconf».
Устройство теперь зарегистрировано в облаке OCF.

### 5.3.5 Соединение с облаком OCF

См. Раздел 8.1.4, см. Также раздел 13.11 спецификации безопасности OCF.
Чтобы разрешить передачу данных между устройством и облаком OCF, устройство отправляет запрос UPDATE в ресурс сеанса; После проверки Облако OCF отправляет ответное сообщение, которое включает оставшееся время жизни соответствующего Токена доступа. Устройство теперь имеет активное соединение и может обмениваться данными.

### 5.3.6 Публикация ссылок на OCF Cloud RD

См. Раздел 8.2; см. также раздел 10.4 Спецификации безопасности OCF

Как только соединение TLS установлено с облаком OCF, устройство предоставляет свои ресурсы в каталоге ресурсов в облаке OCF, чтобы их можно было видеть / получать к ним доступ удаленно.
5.3.7 Обмен данными между клиентом и сервером через облако OCF
См. Разделы 0, 8,4; см. также раздел 10.4 Спецификации безопасности OCF
Что касается сервера, клиенты следуют этому же процессу и регистрируются в облаке OCF.
Облако OCF обеспечивает связь между всеми пользовательскими устройствами в облаке OCF на основе того факта, что они имеют одинаковый идентификатор пользователя.
Когда Клиент пытается выполнить действия CRUDN для ссылок, размещенных в облаке OCF, облако OCF пересылает эти запросы на устройство. Устройство отвечает на Облако OCF, которое затем передает ответ Клиенту (то есть Клиент -> Облако OCF -> Устройство -> Облако OCF -> Клиент).

### 5.3.8 Обновление соединения с помощью OCF Cloud

См. Раздел 13.12 Спецификации безопасности OCF.
Когда (или до того) токен доступа истекает, устройство обновляет свой токен, отправляя запрос UPDATE в ресурс обновления токена.

### 5.3.9 Закрытие соединения с OCF Cloud

См. Раздел 13.11 Спецификации безопасности OCF.
Для выхода из Облака OCF Устройство отправляет запрос ОБНОВЛЕНИЯ в Ресурс сеанса с указанием состояния «входа в систему» «ложь». Это не удаляет и не удаляет любую информацию о регистрации устройства. Устройство может снова войти в Облако OCF в любой момент до истечения срока действия Токена доступа.

### 5.3.10 Отмена регистрации в облаке OCF

См. Раздел 8.5; см. также раздел 13.10 Спецификации безопасности OCF

Для отмены регистрации в облаке OCF устройство отправляет сообщение запроса DELETE на ресурс учетной записи, включая его токен доступа. Облако OCF отправляет ответное сообщение, подтверждающее, что устройство было отменено.
Чтобы снова подключиться к облаку OCF, устройство должно повторить последовательность действий, начиная с подготовки посредника (см. Раздел 5.3.3).

![](figure\cen02.png)
Рисунок 2 Общий конечный автомат операций захватывает конечный автомат, который описывается в информативной последовательности операций, представленной в разделе 5.3.

# 6 Модель ресурсов

## 6.1 Ресурс CoAPCloudConf

### 6.1.1 Введение

Ресурс CoAPCloudConf предоставляет информацию о конфигурации для подключения к облаку OCF.
Это необязательный обнаруживаемый ресурс, который может быть дополнительно включен в коллекцию Easy Setup («oic.r.easysetup») и, таким образом, используется в процессе простой настройки, как определено в базовой настройке расширения OCF для расширений Wi-Fi.

Ресурс CoAPCloudConf должен предоставлять только защищенные конечные точки (например, CoAPS); см. Основную спецификацию OCF, раздел 10.

### 6.1.2 Определение ресурса

Ресурс CoAPCloudConf определен в таблице 2.
Таблица 2 Ресурс CoAPCloudConf

| Example URI                      | Resource Type Title | Resource Type ID   (“rt” value) | Interfaces                  | Description                                                  | Related Functional Interaction |
| -------------------------------- | ------------------- | ------------------------------- | --------------------------- | ------------------------------------------------------------ | ------------------------------ |
| /exampl e/Coap CloudC onfRes URI | CoAPCloudC onf      | oic.r.coapcl oudconf            | oic.if.rw, oic.if.basel ine | Configuration information for connecting   to an OCF Cloud. The Resource properties exposed are listed in [Table 3.](#_bookmark36) |                                |

Таблица 3 определяет детали для Типа ресурса «oic.r.coapcloudconf».
Таблица 3 Определение типа ресурса oic.r.coapcloudconf

| Property title                             | Property name | Value type | Value rule                                               | Unit | Access mode         | Mandatory                 | Description                                                  |
| ------------------------------------------ | ------------- | ---------- | -------------------------------------------------------- | ---- | ------------------- | ------------------------- | ------------------------------------------------------------ |
| Auth Provider Name                         | apn           | String     |                                                          |      | RW                  | No                        | The name of the Authorisation Provider   through which access token was obtained. |
| OCF Cloud interface URL                    | cis           | String     | uri                                                      |      | RW                  | Yes                       | URL of OCF Cloud.                                            |
| Access Token                               | at            | String     | The Access Token is a string of at least   one character |      | W [1](#_bookmark37) | Yes (in an UPDATE   only) | Access token which is returned by an   Authorisation   Provider or OCF Cloud. |
| OCF Cloud UUID                             | sid           | uuid       |                                                          |      | RW                  | Yes                       | The identity of the OCF Cloud                                |
| Last Error Code during  Cloud Provisioning | clec          | integer    | enum                                                     |      | R                   | No                        | 0: No Error, 1: Error response from the OCF Cloud, 2: Failed to connect to the OCF Cloud, 3: Failed to refresh Access Token, 4~254: Reserved, 255: Unknown
error |

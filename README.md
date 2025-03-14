# Введение в протокол HTTP

Этот документ содержит теоретические основы протокола HTTP, подготовленные для студентов первого курса (ИБ, КБ, ИБАС). Материал объясняет базовые понятия доступным языком и включает схемы для наглядности.

---

# Теоритическая часть

## 1. Что такое HTTP и зачем он нужен

**HTTP (HyperText Transfer Protocol)** — это протокол прикладного уровня, используемый для передачи данных в сети Интернет. Он лежит в основе работы Всемирной паутины (World Wide Web), позволяя устройствам обмениваться информацией, такой как веб-страницы, изображения, видео и другие ресурсы. Протокол определяет, как клиент (например, веб-браузер) запрашивает данные у сервера и как сервер отвечает на эти запросы.

**Протокол** — это набор правил и соглашений, которые регулируют взаимодействие между устройствами в сети. Без протоколов, таких как HTTP, компьютеры не смогли бы "договориться" о том, как передавать и интерпретировать данные.

HTTP был разработан в 1990-х годах Тимом Бернерсом-Ли в CERN (Европейской организации по ядерным исследованиям) и с тех пор стал стандартом для веб-коммуникаций. Его ключевая задача — обеспечить простой и универсальный способ передачи гипертекста (текста с ссылками), который лежит в основе веб-страниц.

### Принцип работы HTTP

#### HTTP функционирует по модели "клиент-сервер":
1. **Клиент** (например, браузер пользователя) отправляет **HTTP-запрос** на сервер.
2. **Сервер** (компьютер, где хранятся данные) обрабатывает запрос и возвращает **HTTP-ответ**.
3. Клиент интерпретирует полученные данные и, например, отображает веб-страницу.

**Схема взаимодействия клиент-сервер:**
```text
[Клиент] ---- HTTP-запрос ----> [Сервер]
[Клиент] <---- HTTP-ответ ----- [Сервер]
```

#### HTTP работает поверх стека протоколов TCP/IP, который состоит из нескольких уровней:
- **Прикладной уровень**: HTTP — отвечает за формат и логику обмена данными.
- **Транспортный уровень**: TCP (Transmission Control Protocol) — обеспечивает надежную доставку данных.
- **Сетевой уровень**: IP (Internet Protocol) — определяет маршруты для передачи данных.
- **Канальный уровень**: Ethernet или Wi-Fi — управляет физической передачей.

**Схема стека протоколов:**
<table>
  <thead>
  </thead>
  <tbody>
    <tr>
      <td>Прикладной уровень</td>
      <td>HTTP</td>
    </tr>
    <tr>
      <td>Транспортный уровень</td>
      <td>TCP</td>
    </tr>
    <tr>
      <td>Сетевой уровень</td>
      <td>IP</td>
    </tr>
    <tr>
      <td>Канальный уровень</td>
      <td>Ethernet/Wi-Fi</td>
    </tr>
  </tbody>
</table>

---

## 2. Структура HTTP-запроса

Каждый HTTP-запрос, который отправляет клиент, состоит из нескольких обязательных и необязательных компонентов. Рассмотрим их подробно.

#### Компоненты HTTP-запроса

1. **Строка запроса (Request Line)**:
   - **Метод**: действие, которое клиент хочет выполнить (например, получить или отправить данные).
   - **URL (Uniform Resource Locator)**: адрес ресурса на сервере (например, `/page.html`).
   - **Версия протокола**: указывает версию HTTP (обычно `HTTP/1.1` или `HTTP/2`).
2. **Заголовки (Headers)**: дополнительные метаданные о запросе (например, информация о клиенте или типе данных).
3. **Тело запроса (Body)**: данные, которые клиент отправляет серверу (может отсутствовать, например, в запросах `GET`).

### Пример HTTP-запроса
```text
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
```

#### Разбор примера
1. **Метод**: `GET` — запрос на получение данных.
2. **URL**: `/index.html` — путь к файлу на сервере.
3. **Версия протокола**: `HTTP/1.1` — стандартная версия HTTP.
4. **Заголовки**:
   - `Host`: указывает доменное имя сервера.
   - `User-Agent`: описывает клиентское ПО (браузер и операционную систему).
   - `Accept`: перечисляет форматы данных, которые клиент готов принять.

### Основные методы HTTP

#### HTTP поддерживает несколько методов, каждый из которых определяет конкретное действие:

| Метод  | Описание                     | Пример использования          |
|:------:|:----------------------------:|:-----------------------------:|
| GET    | Получение ресурса            | Загрузка веб-страницы         |
| POST   | Отправка данных              | Отправка формы регистрации    |
| PUT    | Обновление ресурса           | Изменение профиля пользователя|
| DELETE | Удаление ресурса             | Удаление записи               |

---

## 3. Структура HTTP-ответа

После обработки запроса сервер формирует и отправляет клиенту HTTP-ответ. Он также состоит из нескольких частей.

#### Компоненты HTTP-ответа
1. **Строка состояния (Status Line)**:
   - `Версия протокола`: например, `HTTP/1.1`.
   - `Статус-код`: числовой код результата обработки (например, `200`).
   - `Сообщение состояния`: текстовое описание кода (например, `OK`).
2. **Заголовки (Headers)**: метаданные об ответе (например, тип содержимого).
3. **Тело ответа (Body)**: данные, возвращаемые сервером (например, HTML-код).

### Пример HTTP-ответа
```text
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 138
Date: Mon, 01 Jan 2024 10:00:00 GMT
<!DOCTYPE html> <html> <head><title>Пример</title></head> <body><h1>Привет, мир!</h1></body> </html>
```

#### Разбор примера
1. **Строка состояния**: HTTP/1.1 200 OK — запрос успешно обработан.
2. **Заголовки**:
   - `Content-Type`: указывает, что тело ответа содержит HTML с кодировкой UTF-8.
   - `Content-Length`: размер тела ответа в байтах (138).
   - `Date`: дата и время формирования ответа.
3. **Тело ответа**: HTML-код, который браузер отобразит как страницу.

### Коды состояния HTTP

**HTTP статус-код** — это трёхзначное число, с которого начинается любой ответ сервера на запрос по протоколу HTTP. Код кратко сообщает суть ответа — был ли выполнен запрос или возникла ошибка.

#### Статус-коды делятся на категории:
| Код | Значение              |
|:---:|:----------------------|
| 1XX	| Informational	        | 
| 2XX	| Success	              | 
| 3XX	| Redirection           | 
| 4XX	| Client Error          |	
| 5XX	| Server Error          |	

### Примеры статус-кодов:
| Код | Значение              |	Описание                                 |
|:---:|:----------------------|:-----------------------------------------|
| 200	| OK	                  | Запрос выполнен успешно                  |
| 301	| Moved                 | Permanently	Ресурс перемещен на новый URL|
| 404	| Not Found             |	Запрошенный ресурс не найден             |
| 500	| Internal Server Error |	Внутренняя ошибка сервера                |

---

## 4. Роль заголовков в HTTP

**Заголовки (Headers)** — это дополнительные поля в запросах и ответах, которые содержат метаданные, управляющие взаимодействием между клиентом и сервером.

#### Заголовки в запросах:
- Host: указывает домен сервера (обязателен в HTTP/1.1).
- User-Agent: идентифицирует клиентское ПО.
- Accept: перечисляет допустимые типы данных.
- Cookie: передает данные, сохраненные на стороне клиента.

#### Заголовки в ответах:
- Content-Type: описывает тип данных в теле ответа (например, text/html).
- Content-Length: размер тела ответа в байтах.
- Set-Cookie: устанавливает куки на стороне клиента.
- Location: указывает URL для перенаправления (используется с кодами 3xx).

Важно заметить, что существуют HTTP-заголовки с префиксом X-, которые традиционно используются для обозначения нестандартных, экспериментальных или специфичных для конкретного приложения/сервера заголовков.

### Пример использования заголовков:
```text
GET /secret HTTP/1.1
Host: www.example.com
User-Agent: CustomCTFClient
X-Powered-By: PHP/7.4.3
```

Сервер может проверить User-Agent и вернуть скрытые данные только для определенного клиента.

---

## 5. Куки и управление сессиями

**Куки (Cookies) — это небольшие фрагменты данных, которые сервер отправляет клиенту для хранения на его устройстве. При последующих запросах клиент возвращает куки серверу, что позволяет идентифицировать пользователя.**

#### Как работают куки:
1. Сервер отправляет заголовок Set-Cookie в ответе (например, Set-Cookie: sessionid=abc123).
2. Клиент сохраняет куки локально.
3. В следующих запросах клиент добавляет заголовок Cookie: sessionid=abc123.

#### Схема работы сессии
```text
[Клиент] ---- Логин ----> [Сервер]
[Клиент] <---- Set-Cookie: sessionid=abc123 ---- [Сервер]
[Клиент] ---- Cookie: sessionid=abc123 ----> [Сервер]
```

**Сессия** — это временной период взаимодействия между клиентом и сервером, часто связанный с аутентификацией. Куки обычно содержат идентификатор сессии, который сервер использует для распознавания пользователя.

---

## 6. HTTP и HTTPS: Различия и безопасность

**HTTPS (HyperText Transfer Protocol Secure)** — это защищенная версия HTTP, которая использует шифрование для защиты данных.

#### Ключевое различие:
- HTTP: данные передаются в открытом виде и могут быть перехвачены.
- HTTPS: данные шифруются с помощью протоколов TLS (Transport Layer Security) или SSL (Secure Sockets Layer), что обеспечивает конфиденциальность.

#### Схема сравнения:
- HTTP:  Клиент ---- "password123" ----> Сервер (перехват возможен)
- HTTPS: Клиент ---- [шифрованные данные] ----> Сервер (перехват бесполезен)

---

## 7. Заключение

**Протокол HTTP — это фундаментальная технология, обеспечивающая работу современных веб-приложений. Понимание его структуры, включая запросы, ответы, методы, заголовки и коды состояния, необходимо для студентов, изучающих сетевые технологии. HTTPS добавляет уровень безопасности, что делает его стандартом для защиты данных в Интернете.**

---

# Практическая часть

## Задание 1: User-Agent
### Описание
**Некоторые страницы доступны только Супер Секретным Браузерам...**
Попробуйте получить доступ к `/secret.html`

### Решение
**Решение через curl:**
```bash
curl -A "SuperSecretBrowser" http://localhost:8080/secret.html
```

**Решение через telnet:**
```bash
telnet localhost 8080
GET /secret.html HTTP/1.1
Host: localhost
User-Agent: SuperSecretBrowser
```

---

## Задание 2: Cookie Monster
### Описание
**Админка защищена, но у каждого админа есть свои cookie...**
Начните с `/login.html`

### Решение
**Решение через curl:**
```bash
curl -b "admin=true" http://localhost:8080/admin.html
```

**Решение через telnet:**
```bash
telnet localhost 8080
GET /admin.html HTTP/1.1
Host: localhost
Cookie: admin=true
```

---

## Задание 3: Method Challenge
### Описание
**Сервер ожидает, что вы знаете, как правильно "попросить" его дать ответ...**
Попробуйте отправить запрос на `/method_challenge`

#### Подсказка
**Сервер очень любит порядок. Он хочет знать, сколько всего заданий в этом CTF. (Amount-Tasks)**

### Решение
**Решение через curl:**
```bash
curl -X POST -H "X-Amount-Tasks: 8" http://localhost:8080/method_challenge
```

**Решение через telnet:**
```bash
telnet localhost 8080
POST /method_challenge HTTP/1.1
Host: localhost
X-Amount-Tasks: 8
```

---

## Задание 4: HTTP Status
### Описание
**Изучите ответы сервера на разных путях**
- `/moved` - куда ведет редирект?
- `/forbidden` - почему нельзя?
- `/notfound` - что потеряли?
- `/error` - что сломалось?

### Решение
**Решение через curl:**
```bash
curl -I http://localhost:8080/moved
curl -I http://localhost:8080/forbidden
curl -I http://localhost:8080/notfound
curl -I http://localhost:8080/error
```

**Решение через telnet:**
```bash
telnet localhost 8080
HEAD /moved HTTP/1.1
Host: localhost

HEAD /forbidden HTTP/1.1
Host: localhost

HEAD /notfound HTTP/1.1
Host: localhost

HEAD /error HTTP/1.1
Host: localhost
```

---

## Задание 5: Ultimate Challenge
### Описание
**Только настоящие HTTP-мастера смогут пройти это испытание...**
Начните с `/ultimate`, но помните - вежливость открывает многие двери!

### /ultimate
Говорят, где-то на сервере спрятан секретный endpoint `/challenge`...

- GET-запросы он не принимает
- Нужен специальный токен
- И не забудьте быть вежливым!

**DEBUG INFO: - Method: PUT - Required header: X-Secret-Token - Don't forget to say the magic word**

### Решение
**Решение через curl:**
```bash
curl -H "X-Secret-Token: s3cr3t" -H "X-Magic-Word: please" http://localhost:8080/challenge.html
```

**Решение через telnet:**
```bash
telnet localhost 8080
GET /challenge.html HTTP/1.1
Host: localhost
X-Secret-Token: s3cr3t
X-Magic-Word: please
```

---

## Задание 6: JSON Master
### Описание
**API любит JSON и ничего кроме JSON...**
Попробуйте получить данные от `/api/data`

### Решение
**Решение через curl:**
```bash
curl -H "Content-Type: application/json" http://localhost:8080/api/data
```

**Решение через telnet:**
```bash
telnet localhost 8080
GET /api/data HTTP/1.1
Host: localhost
Content-Type: application/json
```

---

## Задание 7: Query Challenge
### Описание
**Сервер ожидает, что вы знаете, как правильно "спросить" его...**
Попробуйте отправить запрос на `/query_challenge`

#### Подсказка
**Сервер очень внимателен к деталям. Он не ответит, если вы не укажете "корректный ключ" в запросе.**

### Решение
**Решение через curl:**
```bash
curl --get --data-urlencode "key=correct_key" "http://localhost:8080/query_challenge"
```

**Решение через telnet:**
```bash
telnet localhost 8080
POST /query_challenge?key=correct_key HTTP/1.1
Host: localhost
```

---

## Задание 8: Reverse Proxy Challenge
### Описание
**Сервер ожидает запрос через обратный прокси...**
Попробуйте получить доступ к `/proxy_challenge` через обратный прокси

#### Подсказка
**Флаг придет в заголовке, который обычно используется для передачи IP-адреса клиента**

### Решение
**Решение через curl:**
```bash
curl -H "X-Forwarded-For: 127.0.0.1" http://localhost:8080/proxy_challenge
```

**Решение через telnet:**
```bash
telnet localhost 8080
GET /proxy_challenge HTTP/1.1
Host: localhost
X-Forwarded-For: 127.0.0.1
```
 

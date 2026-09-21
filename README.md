# Gnatko_Katerina_F5_2.01
# Практична робота № 1

Дисципліна: Основи побудови інформаційних систем та мереж

Тема: Спостереження за процесом звернення до вебресурсу. Побудова власної моделі рівнів взаємодії

| | |
|---|---|
| Прізвище, ім'я |Гнатко Катерина | 
| Група |2.01 |
| Номер варіанта |5 |
| Домен варіанта |rfc-editor.org |
| Середовище виконання | Windows 11|
| Версія curl | curl 8.21.0 (Windows) libcurl/8.21.0 Schannel zlib/1.3.2 WinIDN WinLDAP |
| Дата виконання |19.09.2026 |

---

## Частина A. Збір експериментальних даних

### A.1. Запит із діагностичним виводом

Команда:

curl.exe -v https://afrinic.net

Вивід:

* Host rfc-editor.org:443 was resolved.
* IPv6: (none)
* IPv4: 104.18.20.81, 104.18.21.81
*   Trying 104.18.20.81:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to rfc-editor.org (104.18.20.81 port 443) from 192.168.1.102 port 58424
* using HTTP/1.x
> GET / HTTP/1.1
> Host: rfc-editor.org
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Date: Sat, 19 Sep 2026 18:50:05 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
< Location: https://www.rfc-editor.org/
< Server: cloudflare
< CF-RAY: a3dac626eca4667d-VIE
< alt-svc: h3=":443"; ma=86400
<
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>cloudflare</center>
</body>
</html>
* Connection #0 to host rfc-editor.org:443 left intact

---

### A.2. Запит без захисту з'єднання

Команда:

curl -v http://neverssl.com

Вивід:

(* Host neverssl.com:80 was resolved.
* IPv6: (none)
* IPv4: 34.223.124.45
*   Trying 34.223.124.45:80...)

---

### A.3. Запит до служби доменних імен

*Windows: Resolve-DnsName rfc-editor.org*

Команда (перше виконання):

Resolve-DnsName rfc-editor.org

Вивід:

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
rfc-editor.org                                 AAAA   600   Answer     2606:4700::6812:1551
rfc-editor.org                                 AAAA   600   Answer     2606:4700::6812:1451
rfc-editor.org                                 A      600   Answer     104.18.20.81
rfc-editor.org                                 A      600   Answer     104.18.21.81

Команда (повторне виконання через 5–7 хвилин):

Resolve-DnsName rfc-editor.org

Вивід:

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
rfc-editor.org                                 AAAA   108   Answer     2606:4700::6812:1451
rfc-editor.org                                 AAAA   108   Answer     2606:4700::6812:1551
rfc-editor.org                                 A      109   Answer     104.18.21.81
rfc-editor.org                                 A      109   Answer     104.18.20.81

Зафіксовані значення:

| Параметр | Перше виконання | Повторне виконання |
|---|---|---|
| Час виконання (год:хв) |22:12 |22:18 |
| IP-адреса |104.18.20.81 |104.18.20.81 |
| Значення TTL |600 |109 |

> Якщо друге значення TTL виявилося більшим за перше — це нормально: кеш резолвера встиг оновитися. Зафіксуйте як є.

---

### A.4. Контрольний ресурс

Команда:

curl.exe -v https://google.com

Вивід:

* Host google.com:443 was resolved.
* IPv6: (none)
* IPv4: 142.250.109.139, 142.250.109.113, 142.250.109.102, 142.250.109.138, 142.250.109.101, 142.250.109.100
*   Trying 142.250.109.139:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* ALPN: server accepted http/1.1
* Established connection to google.com (142.250.109.139 port 443) from 192.168.1.102 port 53943
* using HTTP/1.x
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/8.21.0
> Accept: */*
>
* Request completely sent off
* schannel: remote party requests renegotiation
* schannel: renegotiating SSL/TLS connection
* schannel: SSL/TLS connection renegotiated
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-yCSjnlcCOj13OSX0F5lieg' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
< Date: Sat, 19 Sep 2026 19:24:10 GMT
< Expires: Mon, 19 Oct 2026 19:24:10 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com:443 left intact

---

### A.5. Ресурси з некоректною конфігурацією сертифіката

Випадок 1

curl.exe -v https://expired.badssl.com

* Host expired.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
*   Trying 104.154.89.105:443...
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.
* closing connection #0
curl: (35) schannel: next InitializeSecurityContext failed: SEC_E_CERT_EXPIRED (0x80090328) - The received certificate has expired.

Випадок 2

curl.exe -v https://wrong.host.badssl.com

*   Trying 104.154.89.105:443...
* Host wrong.host.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
* closing connection #0
curl: (60) schannel: SNI or certificate check failed: SEC_E_WRONG_PRINCIPAL (0x80090322) - The target principal name is incorrect.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.

Випадок 3

curl.exe -v https://self-signed.badssl.com

*   Trying 104.154.89.105:443...
* Host self-signed.badssl.com:443 was resolved.
* IPv6: (none)
* IPv4: 104.154.89.105
* schannel: disabled automatic use of client certificate
* ALPN: curl offers http/1.1
* schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
* closing connection #0
curl: (60) schannel: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the webpage mentioned above.

> Якщо використано альтернативний спосіб із параметром --resolve — зазначити це та навести фактичну команду.

---
| № | Назва групи (власне формулювання) | Рядки виводу, віднесені до групи | Обґрунтування |
|---|---|---|---|
| 1 |Рівень представлення контенту користувачеві |<html>, <head>, <title>301 Moved Permanently</title>, <body>, <center><h1>301 Moved Permanently</h1></center>, </body>, </html> |HTML-документ є кінцевим, який передається для перегляду. |
| 2 | Рівень прикладного протоколу взаємодії (HTTP)|> GET / HTTP/1.1, > Host: rfc-editor.org, > User-Agent: curl/8.21.0, < HTTP/1.1 301 Moved Permanently, < Content-Type: text/html; charset=UTF-8, < Location: https://www.rfc-editor.org/, < Server: cloudflare |Службові методані та заголовки протоколу HTTP, які визначають параметри клієнтського запиту та статус відповіді сервера. |
| 3 |Рівень криптографічного захисту та узгодження каналу (TLS / Schannel) |* schannel: disabled automatic use of client certificate, * ALPN: curl offers http/1.1, * ALPN: server accepted http/1.1, * schannel: remote party requests renegotiation, * schannel: SSL/TLS connection renegotiated |Етап перевірки сертифіката сервера, шифрування каналу передачі даних. |
| 4 |Рівень адресації та мережевого підключення (TCP / IP) |* Host rfc-editor.org:443 was resolved., * IPv6: (none), * IPv4: 104.18.20.81, 104.18.21.81, * Trying 104.18.20.81:443..., * Established connection to rfc-editor.org (104.18.20.81 port 443) from 192.168.1.102 port 58424 |Етап розв'язання імені вузла у фізичну IP-адресу та відкриття транспортного TCP-з'єднання через порт 443. |


*Групи впорядковано від найближчої до користувача (№ 1) до найближчої до апаратного забезпечення. Зайві рядки вилучити, за потреби — додати.*

Рядки, які не вдалося віднести до жодної групи:

| Рядок виводу | Причина утруднення |
|---|---|
|* Connection #0 to host rfc-editor.org:443 left intact |Рядок є внутрішнім діагностичним повідомленням утиліти curl про стан пулу з'єднань |
| | |
| | |

---

## Контрольні питання

1. Скільки рядків діагностичного виводу передує отриманню даних сторінки (завдання A.1)?

> 25 рядків 

2. Які рядки наявні у виводі A.1 і відсутні у виводі A.2? Чим це зумовлено?

> Рядки про порт 443 і шифрування Schannel/TLS. Тому що сайт у А.1 захищений (HTTPS), а у А.2 відкривається через незахищений порт 80 (HTTP).

3. Звідки у виводі з'явилося значення `443`, якщо його не було вказано в адресі?

> curl сама його підставила, тому що у сайтах з https воно буде автоматично.

4. Як змінилося значення TTL між двома запитами (A.3)? Що означає це число?

> Зменшився з 600 до 109 с.. Це таймер, скільки ще секунд запис буде зберігатися в пам'яті, щоб не шукати його знову в мережі.

5. Чим відрізняються між собою три причини помилок із завдання A.5? Сформулювати кожну однією фразою.

| Випадок | Причина недовіри |
|---|---|
| expired |У сертифіката минув термін придатності. |
| wrong.host |Назва сайту в посиланні не підходить до сертифіката. |
| self-signed |Сертифікат зробили вручну без офіційного центру довіри. |

6. Три рядки з власних виводів, про які не йшлося на лекції 1:

| № | Рядок виводу | Джерело (номер завдання) |
|---|---|---|
| 1 |* schannel: disabled automatic use of client certificate |А.1 |
| 2 |* ALPN: curl offers http/1.1 |А.1 |
| 3 |< alt-svc: h3=":443"; ma=86400 |А.1 |

*Пояснення до цих рядків не потрібне.*

---

## Висновки

*150–300 слів. Спиратися на власні спостереження, а не на матеріал лекції.*

D.1. Що виявилося неочевидним або несподіваним

Через те, що я не замислювалась так глибоко, як саме працює інтернет, для мене майже все виявилось новим та дуже цікавим, що відбувається в терміналі, ще до відкриття сайту. Мене особливо здивувало, що буквально все фіксується. Наприклад рядки * schannel: remote party requests renegotiation та * schannel: SSL/TLS connection renegotiated у завданні А.1 гарно показали, що комп'ютер і сервер шифрують просто під час з'єднання. Також мені було прям дуже цікаво та незвично побачити на практиці в завданні А.3 як саме працює пам'ять DNS і таймер у рядку з TTL  зменшився з 600 до 109 секунд, поки я чекала 6 хвилин між спробами, мене це дуже здивувало, що інтернет сам веде зворотній відлік. Також здивувало у завданні А.5 те, як суворо комп'ютер ставиться до безпеки. Коли виникла якась незбіжність або закінчився час, або було введено не правильне ім'я сайту то система просто бере і обриває зв'язок рядком closing connection #0. Загалом, всі завдання виявились цікавими.

> 

D.2. Чому саме така кількість груп у частині B

*На якій підставі ухвалено рішення. Що змусило б його змінити.*

Я зупинилась на 4х групах, тому що мені така кількість здалась найбільш зрозумілою для послідовності. У 1 пункті я виділила сам HTML контент, заради якого користувач і відкриває сторінку. У 2 службові команди HTTP, через які клієнт просить сайт, а сервер повертає відповідь. У 3 рівень безпеки Schannel та TLS, де узгоджується шифрування каналу, щоб дані не перехопив ніхто, а в 4 рівні мережеве підключення (пошук IP адреси через DNS та саме відкриття порту 443). Менше груп я не бачила сенсу робити, тому що всі 4 виконують різні задачі, а якщо робити більше, то це буде не так зручно.

D.3. Питання, яке залишилося без відповіді

> Насправді, я ще не до кінця з усім розібралась, тому питань багато, але я буду з цим розбиратись, та можливо на інших практичних мені стане зрозуміліше.

---

## Використання штучного інтелекту

*Розділ обов'язковий. Заповнюється незалежно від того, чи використовувався ШІ. Детальні вимоги — у документі «Політика використання технологій штучного інтелекту».*

Факт використання: використано 

Установлений рівень для цієї роботи: Р3 — ШІ як співвиконавець

Фактичний рівень використання: Р2

### Використані системи

| Система | Версія або модель | Період використання |
|---|---|---|
| Google Gemini|Gemini 2.5 Flash |19.09.2026 |

### Промпти

*Наводити дослівно, у тому вигляді, у якому запит було надано системі. Переказ не приймається.*

| № | Розділ роботи | Текст промпта |
|---|---|---|
| 1 |А.2 |обьясняй как єто сделать. |
| 2 |А.2 |а чего у одногруппника другая команда и текста больше чем у меня |
| 3 |А.3 |пояснюй чому це так |
| 4 |В   |детально поясни що від мене хочуть |

### Дії з отриманим результатом

| № промпта | Що перевірено | Що змінено | Що відхилено і чому |
|---|---|---|---|
| 1 |порівнювала інформацію з методички та ші |додала до коду .exe|знайшла чому саме треба додавати .exe і вручну прописала команду |
| 2 |дивилась роботу Пікульського О., щоб перевіряти себе на помилки, помітила, що у нього прописана інша команда |нічого, зробила по методичці |прочитала пояснення його команди, зрозуміла, що краще візьму з методички |
| 3 |дізналась детальніше чому TTL зменшилось |нічого |нічого |
| 4 |зрозуміла логіку створення рівнів |зробила 4 рівні |нічого, він мені рівні не писав |

### Підтвердження

Підтверджую, що всі наведені в цьому звіті виводи команд отримано мною особисто внаслідок фактичного виконання відповідних дій, а відомості цього розділу є повними та достовірними.

> Виводи curl, dig та інші артефакти не можуть бути згенеровані. Це стосується будь-якого рівня використання ШІ.

---

## Примітки виконавця

*(необов'язковий розділ: що не спрацювало, які команди довелося змінити, які виникли труднощі)*

> Використовувала ШІ для того, щоб розібрати питання які виникли та на які я не змогла сама знайти відповіді, всі команди та висновки були прописані мною та не були згенеровані ШІ, тому мені здалось, що рівень використання Р2
## Частина B. Власна модель рівнів

Кількість виділених груп: _Р2__

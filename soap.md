# SOAP

- [Основные понятия](#основные-понятия)
- [WSDL](#wsdl)
- [Структура SOAP-сообщения](#структура-soap-сообщения)
- [WS-Security](#ws-security)
- [SOAP vs REST](#soap-vs-rest)

## Основные понятия

**SOAP (Simple Object Access Protocol)** — протокол обмена структурированными сообщениями, использующий XML. SOAP определяет формат сообщений (envelope, header, body) и набор правил для их обработки; не зависит строго от транспорта (обычно HTTP).

**Термины**:

- **Envelope** — конверт, корневой элемент сообщения.
- **Header** — заголовок, опциональный элемент, для метаданных и директив.
- **Body** — тело, содержит фактическую нагрузку / вызов.
- **Fault** — ошибка; элемент в Body для сообщения об ошибке.

## WSDL

**WSDL (Web Services Description Language)** — контракт сервиса - XML-описание веб-сервиса: какие операции (methods) доступны, какие входные/выходные сообщения, какие типы данных, и куда слать запросы (endpoint).

WSDL позволяет авто-генерировать клиентские и тестовые запросы.

## Структура SOAP-сообщения

SOAP 1.1 request:

```xml
POST /PriceService HTTP/1.1
Host: example.com
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://example.com/GetPrice"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Header>
    <!-- optional headers, e.g. auth -->
  </soap:Header>
  <soap:Body>
    <GetPriceRequest xmlns="http://example.com/prices">
      <ItemId>12345</ItemId>
    </GetPriceRequest>
  </soap:Body>
</soap:Envelope>
```

Соответствующий response (успех):

```xml
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetPriceResponse xmlns="http://example.com/prices">
      <ItemId>12345</ItemId>
      <Price>19.95</Price>
    </GetPriceResponse>
  </soap:Body>
</soap:Envelope>
```

SOAP Fault (пример ошибки):

```xml
HTTP/1.1 500 Internal Server Error
Content-Type: text/xml; charset=utf-8

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <soap:Fault>
      <faultcode>soap:Client</faultcode>
      <faultstring>Invalid ItemId</faultstring>
      <detail>
        <ErrorCode>4001</ErrorCode>
      </detail>
    </soap:Fault>
  </soap:Body>
</soap:Envelope>
```

## WS-Security

**Web Services Security (WS-Security, WSS)** - набор расширений SOAP для передачи токенов безопасности, подписи сообщений и шифрования.

Это стандарт, который обеспечивает безопасность сообщений SOAP путем защиты целостности, конфиденциальности и аутентификации. Он работает на уровне сообщений, используя такие технологии, как XML-шифрование и цифровые подписи, и может передавать токены безопасности, такие как SAML или Kerberos. WS-Security дополняет транспортный уровень безопасности (например, HTTPS) и обеспечивает защиту данных в процессе обмена сообщениями.

## SOAP vs REST

**SOAP** — протокол с жёстким форматом сообщений и встроенными стандартами (WSDL, WS-Security), больше подходит для сценариев с требованием формального контракта и расширенных возможностей безопасности/транзакций.

**REST** — архитектурный стиль, более гибкий, чаще использует JSON, проще тестировать для веб/мобильных клиентов.

## SoapUI

**SoapUI** — это инструмент для тестирования и разработки веб-сервисов, поддерживающий SOAP и REST. Он позволяет создавать и отправлять запросы, проверять ответы, автоматизировать тесты и интегрироваться с CI/CD.

**Основные возможности:**

- Создание и отправка SOAP-запросов.
- Поддержка WSDL и XML.
- Автоматизация тестирования.
- Интеграция с CI/CD.
- Поддержка REST и GraphQL.

**Пример использования:**

1. Импорт WSDL.
2. Создание тестового запроса.
3. Отправка запроса и проверка ответа.
4. Автоматизация тестов.

SoapUI — мощный инструмент для разработчиков и тестировщиков, упрощающий работу с веб-сервисами.

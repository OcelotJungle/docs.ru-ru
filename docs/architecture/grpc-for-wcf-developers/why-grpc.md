---
title: Почему мы рекомендуем gRPC для разработчиков WCF - gRPC для разработчиков WCF
description: Обсуждение того, почему gRPC хорошо подходит для разработчиков WCF, которые хотят перейти на современные архитектуры и платформы.
ms.date: 09/02/2019
ms.openlocfilehash: 664781e94c24c1796eafa6a70eb28d453b530d66
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2020
ms.locfileid: "79147650"
---
# <a name="why-we-recommend-grpc-for-wcf-developers"></a>Почему мы рекомендуем gRPC для разработчиков WCF

Прежде чем углубиться в язык и методы gRPC, стоит обсудить, почему gRPC является правильным решением для разработчиков Windows Communication Foundation (WCF), которые хотят перейти на .NET Core.

## <a name="similarity-to-wcf"></a>Сходство с WCF

Хотя реализация и подход отличаются для gRPC, опыт разработки и потребления услуг с gRPC должен быть интуитивно понятным для разработчиков WCF. Основная цель та же: сделать возможным код, как будто клиент и сервер находятся на одной платформе, не беспокоясь о сети.

Обе платформы разделяют принцип декларирования, а затем реализации интерфейса, даже несмотря на то, что процесс объявления этого интерфейса отличается. И, как вы увидите в главе 5, различные типы RPC вызывает, что gRPC поддерживает карту хорошо привязки доступны для wCF услуг.

## <a name="benefits-of-grpc"></a>Преимущества gRPC

gRPC стоит выше других решений по следующим причинам.

### <a name="performance"></a>Производительность

Использование HTTP/2, а не HTTP/1.1 удаляет требование для читаемых человеком сообщений и вместо этого использует меньший и быстрый двоичный протокол. Это более эффективно для компьютеров, чтобы разобрать. HTTP/2 также поддерживает запросы на мультиплексирование по одному подключению. Эта поддержка позволяет отправлять ответы, как только они будут готовы без необходимости ждать в очереди. (В HTTP/1.1 эта проблема называется "блокировка "глава линии (HOL)").) При использовании gRPC требуется меньше ресурсов, что делает его хорошим решением для использования для мобильных устройств и более медленных сетей.

### <a name="interoperability"></a>Совместимость

Есть инструменты и библиотеки gRPC для всех основных языков программирования и платформ, включая .NET, Java, Python, Go, C, Node.js, Swift, Dart, Ruby и PHP. Благодаря формату двоичного провода Protocol Buffers и эффективному генерации кода для каждой платформы разработчики могут создавать перформативные приложения, пользуясь при этом полной межплатформенным поддержкой.

### <a name="usability-and-productivity"></a>Удобство использования и производительность

gRPC является комплексным решением RPC. Он работает последовательно на нескольких языках и платформах. Он также обеспечивает превосходный инструмент, с большей частью необходимого шаблонного кода автоматически генерируется. Таким образом, больше времени разработчика высвобожден, чтобы сосредоточиться на бизнес-логике.

### <a name="streaming"></a>Потоковая передача

gRPC имеет полную двунаправленную потоковую передачу, которая обеспечивает аналогичную функциональность для полных дуплексных услуг WCF. gRPC потоковое может работать через регулярные подключения к Интернету, балансели нагрузочных средств и сервисные сетки.

### <a name="deadlinetimeouts-and-cancellation"></a>Срок/тайм-аут и отмена

gRPC позволяет клиентам указать максимальное время завершения RPC. Если указанный срок превышен, сервер может отменить операцию независимо от клиента. Сроки и отмены могут распространяться с помощью дальнейших вызовов gRPC, чтобы обеспечить соблюдение ограничений использования ресурсов. Клиенты также могут прекратить операции, когда срок превышен, или раньше, если это необходимо (например, из-за взаимодействия с пользователем).

### <a name="security"></a>Безопасность

gRPC неявно защищен, когда он использует HTTP/2 над сквозным зашифрованным соединением TLS. Поддержка аутентификации сертификата клиента [(см. главу 6)](security.md)еще больше повышает безопасность и доверие между клиентом и сервером.

>[!div class="step-by-step"]
>[Предыдущий](network-protocols.md)
>[Следующий](protocol-buffers.md)

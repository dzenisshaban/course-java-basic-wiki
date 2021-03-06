# Дата и время (since version 8)
До Java 8 для работы с датой и временем использовались классы `java.util.Date` и `java.util.Calendar`. У них было много недостатков, например:
- не потокобезопасный,
- изменяемые объекты
- временная зона даты – это временная зона JVM по умолчанию
- месяца начинаются с нуля

В Java 8 добавили новую библиотеку, которая содержит *неизменные* (*immutable*), *потокобезопасные* классы с более *продуманным дизайном*. Это классы `LocalDate`, `LocalTime`, `LocalDateTime`, `Instant`, `Period` и `Duration`. Содержатся они в пакете `java.time` и не содержат информацию о временной зоне (кроме класса `Instant`).

`LocalDate`, `LocalTime`, `LocalDateTime` и `Instant` реализуют интерфейс `java.time.temporal.Temporal`. `Period` и `Duration` реализуют интерфейс `java.time.temporal.TemporalAmount`.

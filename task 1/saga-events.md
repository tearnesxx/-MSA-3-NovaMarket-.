# Реестр событий Saga (оформление заказа)

| Этап | Тип события | Наименование |
|---|---|---|
| Отправка заказа | domain | OrderSubmitted |
| Проверка и резерв | domain | InventoryReserved |
| Проверка и резерв | failure | InventoryReservationFailed |
| Оплата (авторизация/списание) | domain | PaymentAuthorized |
| Оплата (авторизация/списание) | failure | PaymentFailed |
| Доставка (планирование) | domain | ShipmentScheduled |
| Доставка (планирование) | failure | ShipmentSchedulingFailed |
| Завершение | domain | OrderCompleted |
| Отмена | domain | OrderCancelled |
| Компенсация (после неуспеха оплаты/доставки) | compensation | InventoryReservationReleased |
| Компенсация (после неуспеха доставки) | compensation | RefundSucceeded |
| Компенсация (после отмены отправки) | compensation | ShipmentCancelled |

Примечания:
- События - неизменяемые факты домена. Команды оформляются синхронными вызовами или отдельными топиками команд (здесь не показано).
- `PaymentAuthorized` может означать либо успешную авторизацию+капчур, либо два события (AuthorizationSucceeded, CaptureSucceeded) - выбирается платежной интеграцией.
- Все потребители обязаны быть идемпотентными; события имеют ключи агрегатов и версии.

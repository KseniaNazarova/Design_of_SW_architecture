# Проектирование архитектуры ПО
## Назначение проектируемой системы
Автоматизация работы гостиничного комплекса.

## Функциональные требования
*Участники и их интересы*

1. Менеджер
  * Решает финансовые вопросы
  * Заключает договоры с клиентами
  * Осуществляет контроль за соблюдением правил проживания
2. Администратор на ресепшене
  * Отвечает за проверку документов клиентов
  * Оформляет клиента при заселении в гостиницу и выезде из нее
  * Заносит в систему информацию о свободных, забронированных и занятых номерах
3. Клиент
  * Бронирует номер в гостинице
  * Заключает договор с гостиницей и осуществляет оплату
  * Заселяется/выселяется

*Требуемая функциональность системы*

1. Хранение подробной информации о номерах гостинцы (стоимость проживания, количество мест, статус, сроки) и ее модификация
2. Хранение и обработка информации о клиентах
3. Бронирование номеров
4. Оформление договоров

## Варианты использования 
*Диаграмма прецедентов*

![use-cases](https://raw.githubusercontent.com/KseniaNazarova/Design_of_SW_architecture/master/res/use-case.png)

*Процесс бронирования*
 1. __Клиент__ выбирает подходящий __номер__ в __гостинице__.
 2. Клиент отправляет заявку на __бронирование__ и вносит личную информацию.
 3. __Администратор__ подтверждает запрос по почте или телефону.
 4. Клиент заносит __информацию о счете__ для предоплаты. (Оплата = предоплата в день бронирования + остаток в день заселения).
 5. Система осуществляет авторизацию карты оплаты и выполняет предоплату.
 6. Система оповещает клиента об удачном завершении предоплаты по адресу его электронной почты или номеру телефона.
 7. Система меняет статус номера на "Забронирован" и заносит сроки бронирования.

Альтернативы:
* На шаге 2 клиент вводит неверные личные данные.
Подтверждение бронирования (шаг 3) становится невозможным. Бронь снимается, клиент никак не оповещается.
* На шаге 3 регистратор отклоняет запрос на бронирование.
Регистратор оповещает клиента о невозможности бронирования и по возвожности предлагает другой номер или время. Для связи используется email или номер телефона, введенные клиентом ранее.
* На шаге 5 система получает отрицательный ответ на запрос о состоянии счета клиента.
Необходимо предоставить клиенту возможность повторно ввести информацию о карте оплаты и выполнить ее авторизацию.
* На шаге 5 система не выполняет предоплаты из-за недостаточности средств.
Система предлагает отменить бронирование или ввести другие данные о карте оплаты.
* На шаге 4 при личном присутствии клиента администратор может принять предоплату по наличному расчету. Тогда шаг 5 - 6 пропускаются.
* Клиент отменяет бронь.
Если клиент сообщает об этом при подтверждении заказа администратором, бронь просто снимается. Иначе клиент сам должен сообщить об этом администратору за сутки до заселения, последний в свою очередь меняет статус номера на "Свободен". Предоплата возвращается.

*Процесс __заселения__*
 1. Между клиентом и гостиницей (__менеджером__) заключается __договор__.
 2. Администратор принимает остаток оплаты.
 3. Администратор меняет статус номера на "Заселен".

Альтернативы:
* Клиент пытается заселиться, не бронируя место заранее.
Администратор проверяет наличие свободных мест и предлагает их клиенту. Если есть свободные места, которые удовлеворяют клиента, тогда:
 1. Клиент предоставляет личную информацию.
 2. Оплачивает полную стоимость проживания.
 3. Заколючается договор с менеджером.
 4. Администратор меняет статус номера на "Заселен".
Если свободных мест нет, администратор предлагает забронировать номер на другое время. Если клиент согласен, тогда переход к шагу 4 бронирования.
* Клиент не появляется в день заселения и не оплачивает остаток стоимости.
Администратор меняет статус номера на "Свободен". Предоплата не возвращается.
* По техническим причинам заселение не возможно.
По возможности, администратор заранее оповещает клиента о невозможности заселения. Предоплата возвращается.

*Процесс __выселения__*
 1. Менеджер проверяет состояние номера перед выселением клиента.
 2. Система менят статус номера на "Свободен".

Альтернативы:
* Преждевременное выселение.
Если клиент нарушил оговоренные в договоре правила, менеджер вправе расторгнуть договор с клиентом без возвращения оплаты.
Если гостиница нарушила оговоренные в договоре правила, клиент вправе расторгнуть договор с гостиницей и запросить возвращение оплаты.
* Если перед выселением состояние номера неудовлетворительное, менеджер вправе предъявить требования для заменты испорченных вещей или оплаты их стоимости.

*Процесс установки цен*
* Менеджер вносит в систему стоимость номеров гостиницы.


*Диаграмма классов*
![class-diag](https://raw.githubusercontent.com/KseniaNazarova/Design_of_SW_architecture/master/res/class-diag.png)

*Динамическая объектная модель*
1. Диаграмма последовательности бронирования
![seq-diag1](https://github.com/KseniaNazarova/Design_of_SW_architecture/blob/master/res/SeqDiag1.png)
2. Диаграмма последовательности заселения
![seq-diag2](https://github.com/KseniaNazarova/Design_of_SW_architecture/blob/master/res/SeqDiag3.png)
3. Диаграмма последовательности выселения
![seq-diag3](https://github.com/KseniaNazarova/Design_of_SW_architecture/blob/master/res/SeqDiag4.png)
4. Дополнительная диаграмма последовательности оплаты
![seq-diag4](https://github.com/KseniaNazarova/Design_of_SW_architecture/blob/master/res/SeqDiag2.png)

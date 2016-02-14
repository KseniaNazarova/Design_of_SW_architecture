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
  * Заносит в систему информацию о свободных, забронированных и занятых комнатах
3. Клиент
  * Бронирует комнату в гостинице
  * Заключает договор с гостиницей и осуществляет оплату
  * Заселяется/выселяется

*Требуемая функциональность системы*

1. Хранение подробной информации о комнатах гостинцы (стоимость проживания, количество мест, статус, сроки) и ее модификация
2. Хранение и обработка информации о клиентах
3. Бронирование комнат
4. Оформление договоров

## Варианты использования 
*Диаграмма прецедентов*

![use-cases](https://raw.githubusercontent.com/KseniaNazarova/Design_of_SW_architecture/b4cd9d0474eb5b0e6c5459b41eb5e87ebc763c2f/res/use-cases.png)

1. Процесс бронирования.
  Начальным этапом процесса бронирования является выбор подходящей комнаты гостиницы клиентом и отправка им заявки на бронирование. Заявка подтверждается или отклоняется администратором (или регистратором). После подтверждения начинается этап заключения договора. Договор заключается между клиентом и гостиницей (менеджером), при этом в систему заносится и обрабатывается информация о клиентах.
2. Процесс заселения.
  Заселение клиента производится администратором, который проверяет договор и завершенную оплату проживания (цены устанавливаются менеджером). Администратор изменяет статус заселенной комнаты, и заносит в систему планируемые сроки проживания.
3. Процесс выселения.
  В стандартном случае клиент выезжает из гостиницы, администратор изменяет статус комнаты в ИС. Однако возможен случай преждевременного выселения, когда клиент нарушил оговоренные в договоре правила или оказался не удовлетворен условиями проживания, что фиксируется менеджером.
 
 




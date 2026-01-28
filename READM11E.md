```mermaid
sequenceDiagram
    autonumber
    participant U as Пользователь
    participant F as Frontend
    participant B as Backend
    participant M as Monitoring System
    participant P as Payment Gateway

    U->>F: Выбор валютной пары
    F->>B: Запрос лимитов и курса
    B->>M: Проверка работоспособности шлюза
    
    alt Шлюз активен
        M-->>B: Статус: OK
        B-->>F: Данные курса (1 BTC = 50k USD)
        F-->>U: Отображение формы ввода
    else Шлюз недоступен
        M-->>B: Статус: DOWN
        B-->>F: Ошибка: Направление временно закрыто
        F-->>U: Сообщение "Попробуйте позже"
    end

    U->>F: Клик "Оплатить"
    F->>B: Создание транзакции
    B->>P: Запрос платежной ссылки
    P-->>F: Редирект на оплату
    F-->>U: Переход к оплате

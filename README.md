# wallet-api
#### Библиотека для легкого использования API Wallet

## Установка
```py
pip install vk-wallet-api
```

### Использование
```py
from vk_wallet_api import Wallet


wallet_access_token = "your access_token"
wallet_session = Wallet(wallet_access_token)
```

### Получение баланса
- Параметры не требуются

```py
response = await wallet_session.get_balance()
print(response.balance)
```

### Создания ссылки для оплаты
- Параметр payload (необяз.) - Полезная нагрузка

```py
response = await wallet_session.get_payment_url("from_my_vk_market")
print(response.url)
```

### Возвращает список последних транзакций
- Параметр type (необяз.) - Тип перевода (TranslationType.ALL, TranslationType.OUT, TranslationType.IN) (по умолчанию TranslationType.ALL)
- Параметр offset (необяз.) - Смещение (по умолчанию 0)
- Параметр limit (необяз.) - Лимит отобращения (по умолчанию 20)

```py
from vk_wallet_api import TranslationType


transactions = await wallet_session.get_transactions(type=TranslationType.OUT)
print(transactions)
```

### Получение идентификатора последней транзакции
- Параметры не требуются

```py
last_transaction_id = await wallet_session.get_last_transaction_id()
print(last_transaction_id)
```

### Проверяет зарегистрирован ли пользователь в wallet
- Параметр user_id (обяз.) - Айди пользователя

```py
user_exists = await wallet_session.checks_user_exists(317548089)
print(user_exists)
```

### Переводит coins пользователю
- Параметр recipient_id (обяз.) - Кому переводим
- Параметр amount (обяз.) - Сумма перевода
- Параметр payload (необяз.) - Полезная нагрузка

```py
response = await wallet_session.send_coins(317548089, 1, "from_my_vk_market")
print(response)
```

### Создание callback-сервера
- Параметр url (обяз.) - Ссылка на ваш новый callback-сервер

```py
response = await wallet_session.set_callback_address("http://0.0.0.0/wallet/callbac")
print(response)
```

### Удаление callback-сервера
- Параметры не требуются

```py
response = await wallet_session.delete_callback()
print(response)
```

### Валидация callback-данных
- Параметр transaction (обяз.) - Данные callback
- Параметр secret (обяз.) - Секретный ключ callback-сервера

```py
response = await Wallet.validate_sing(transaction, callback_secret)
print(response)
```

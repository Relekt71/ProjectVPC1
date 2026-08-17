# Создание VPC и NAT-инстанса в Yandex Cloud

## 📋 Описание задания


##  Архитектура


### 1. Созданные VPC и подсети

<img width="1152" height="88" alt="image" src="https://github.com/user-attachments/assets/e5ccc620-f3e6-44b9-a842-652e3a7ce911" />

---

### 2. NAT-инстанс

<img width="1631" height="54" alt="image" src="https://github.com/user-attachments/assets/8f30b685-9f24-493e-92d4-d480c5c9269b" />

**Параметры NAT-инстанса:**
- Имя: `nat-instance`
- Внутренний IP: `192.168.10.254`
- Публичный IP: `51.250.4.97`
- Образ: `fd80mrhj8fl2oe87o4e1` (NAT-инстанс из Marketplace)

---

### 3. Таблица маршрутизации

> *Вставьте скриншот: VPC → Таблицы маршрутизации → private-route-table*

<img width="1211" height="79" alt="image" src="https://github.com/user-attachments/assets/db814f8a-f9bb-4ee9-b4bc-e88a389e830e" />

**Маршрут:**
- Префикс назначения: `0.0.0.0/0`
- Next hop: `192.168.10.254` (NAT-инстанс)

---

### 4. Публичная ВМ (бастион-хост)

<img width="1673" height="49" alt="image" src="https://github.com/user-attachments/assets/50831686-3be4-42dc-8d77-16fa85511362" />

**Параметры:**
- Имя: `public-vm`
- Внутренний IP: `192.168.10.21`
- Публичный IP: `62.84.112.253`

---

### 5. Приватная ВМ

<img width="1674" height="49" alt="image" src="https://github.com/user-attachments/assets/a7c2529a-7641-4222-9c25-eb522c29374d" />

**Параметры:**
- Имя: `private-vm`
- Внутренний IP: `192.168.20.32`
- Публичный IP: `Без адреса`

---

### 6. Подключение к публичной ВМ

ssh yc-user@62.84.112.253

<img width="815" height="530" alt="image" src="https://github.com/user-attachments/assets/63338db8-f63b-4330-907c-ee73710d14f0" />

7. Подключение к приватной ВМ через публичную

bash

ssh yc-user@192.168.20.32

<img width="815" height="530" alt="image" src="https://github.com/user-attachments/assets/e967a83e-9df5-4afb-bcc2-229c66db37c1" />

8. Проверка доступа в интернет с приватной ВМ
   
<img width="736" height="224" alt="image" src="https://github.com/user-attachments/assets/bcd5cf67-4fb8-48de-a58a-98adc9ba8add" />

9. Проверка маршрутизации через NAT-инстанс

    traceroute ya.ru

<img width="909" height="160" alt="image" src="https://github.com/user-attachments/assets/7fede030-bde1-455f-9882-70b764dbe880" />

Результат:
text

1  _gateway (192.168.20.1)
3  fhmblo0ov5adc9a1gh4j.auto.internal (192.168.10.254)  ← NAT-инстанс

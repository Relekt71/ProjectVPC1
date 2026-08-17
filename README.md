# Создание VPC и NAT-инстанса в Yandex Cloud

## 📋 Описание задания


##  Архитектура


### 1. Созданные VPC и подсети

> *Вставьте скриншот: VPC → Подсети*

![VPC и подсети](screenshots/vpc-subnets.png)

---

### 2. NAT-инстанс

> *Вставьте скриншот: Compute Cloud → Виртуальные машины → nat-instance*

![NAT-инстанс](screenshots/nat-instance.png)

**Параметры NAT-инстанса:**
- Имя: `nat-instance`
- Внутренний IP: `192.168.10.254`
- Публичный IP: `51.250.4.97`
- Образ: `fd80mrhj8fl2oe87o4e1` (NAT-инстанс из Marketplace)

---

### 3. Таблица маршрутизации

> *Вставьте скриншот: VPC → Таблицы маршрутизации → private-route-table*

![Таблица маршрутизации](screenshots/route-table.png)

**Маршрут:**
- Префикс назначения: `0.0.0.0/0`
- Next hop: `192.168.10.254` (NAT-инстанс)

---

### 4. Публичная ВМ (бастион-хост)

> *Вставьте скриншот: Compute Cloud → Виртуальные машины → public-vm*

![Публичная ВМ](screenshots/public-vm.png)

**Параметры:**
- Имя: `public-vm`
- Внутренний IP: `192.168.10.21`
- Публичный IP: `62.84.112.253`

---

### 5. Приватная ВМ

> *Вставьте скриншот: Compute Cloud → Виртуальные машины → private-vm*

![Приватная ВМ](screenshots/private-vm.png)

**Параметры:**
- Имя: `private-vm`
- Внутренний IP: `192.168.20.32`
- Публичный IP: `Без адреса`

---

### 6. Подключение к публичной ВМ

> *Вставьте скриншот: Терминал с подключением к public-vm*

```bash
ssh yc-user@62.84.112.253

https://screenshots/ssh-public-vm.png
7. Подключение к приватной ВМ через публичную

    Вставьте скриншот: Терминал с подключением к private-vm через public-vm

bash

ssh yc-user@192.168.20.32

https://screenshots/ssh-private-vm.png
8. Проверка доступа в интернет с приватной ВМ

    Вставьте скриншот: Результат ping ya.ru с private-vm

bash

ping ya.ru -c 4

https://screenshots/ping-private-vm.png
9. Проверка маршрутизации через NAT-инстанс

    Вставьте скриншот: Результат traceroute ya.ru с private-vm

bash

traceroute ya.ru

https://screenshots/traceroute-private-vm.png

Результат:
text

1  _gateway (192.168.20.1)
3  fhmblo0ov5adc9a1gh4j.auto.internal (192.168.10.254)  ← NAT-инстанс

# Тестування

При розробці REST API часто використовують інтеграційні тести, які також називають API-тестами. Як правило такі тести поєднуються з unit-тестами. Пропорції поєднання інтеграційних та unit-тестів можуть бути різними. 

В традиційній піраміді тестування Майка Кона пріоритет надається unit-тестам, оскільки такі тести швидко виконуються та дозволяють протестувати більшість якщо не всі варіанти поведінки коду, що тестується.    

У свою чергу API-тести дозволяють протестувати REST API схоже до того як би його використовував користувач з прив'язкою тільки до інтерфейсу сервісу, а не його внутрішньої реалізації, що спрощує початкові етапи розробки та подальший рефакторінг. Окрім того деякі елементи коду, як наприклад об'єкти для роботи з ORM, може бути проблематично заміняти мок-об'єктами без створення залежностей на деталі реалізації. Саме тому в деяких проектах пріоритет надають саме API-тестам, залишаючи unit-тести для окремих частин коду які проблематично протестувати API-тестами. Таких підхід особливо популярний в поєднанні з мікросервісною архітектурою, оскільки для невеликих сервісів порівняно легко описати всю їх поведінку через API-тести.

Вміст більшості API-тестів можна поділити на наступні частини:
1. Задання внутрішнього стану сервісу (наприклад, створення записів в базі даних)
2. Відправка запиту до сервісу
3. Оцінка відповіді сервісу (наприклад, оцінка контенту відповіді, HTTP статус коду)
4. Оцінка внутрішнього стану сервісу після запиту (наприклад, перевірка того які записи знаходяться в базі даних)

Міграції бази даних можна застосовувати для кожного тесту окремо, що може сповільнити їх виконання, або один раз для всіх тестів загалом, однак в такому випадку кожен тест має починати роботу з пустими таблицями моделей, щоб між тестами не створювалось неявних залежностей. Тести мають проходити незалежно від того, в якому порядку вони були виконані. 

В даній лабораторній роботі потрібно створити тести для перевірки правильності роботи системи. Студенти можуть надавати пріоритет API або unit-тестам за бажанням. Тести мають покривати більше 90% коду системи (перевірити за допомогою пакету [coverage](https://coverage.readthedocs.io/en/stable/)). 

## Варіанти

Номер варіанту визначається номером студента в журналі.

Залежно від номеру визначається фреймворк для тестування, що потрібно буде використовувати:
* непарні номери - [unittest](https://docs.python.org/3/library/unittest.html)
* парні номери - [pytest](https://docs.pytest.org/en/stable/)

## Рекомендації

* Для спрощення API тестування Flask додатків фреймворком unittest зручно використовувати пакет [Flask-Testing](https://pythonhosted.org/Flask-Testing/)
* Для спрощення API тестування Flask додатків фреймворком pytest зручно використовувати пакет [pytest-flask](https://pytest-flask.readthedocs.io/en/latest/tutorial.html)
* Якщо `coverage` показує занадто низький відсоток покриття, варто перевірити чи не включаються в репорт зайві файли (включатись мають тільки файли самої системи, без включення файлів сторонніх пакетів)

## Хід роботи

1. Встановити необхідні залежності
2. Створити API та/або unit тести для перевірки функціоналу
3. Переконатись, що покриття коду системи тестами вище 90%

## Критерії оцінювання

1. Створені API та/або unit тести успішно проходять при запуску
2. В тестах виконуються авторизовані запити до системи
3. В тестах використані фікстури (pytest фікестури або setUp/tearDown для unittest)
4. Покриття коду системи тестами вище 90%

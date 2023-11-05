Домашнє завдання #12
У цьому домашньому завданні ми продовжуємо допрацьовувати наш REST API застосунок із домашнього завдання 11.

1. Змінюємо моделі
file: src/database/models.py

> poetry run docker run --name jwt_app -p 5432:5432 -e POSTGRES_PASSWORD=751953 -d postgres

2. Виконуємо міграції моделей
> poetry run alembic init migrations

migrations/env.py
    from src.database.models import Base
    from src.database.db import SQLALCHEMY_DATABASE_URL
    target_metadata = Base.metadata
	
poetry run alembic revision --autogenerate -m 'Init'
-- Створення міграцій в корені проекту: alembic revision --autogenerate -m  --
-- коротний опис оновлень в моделях ('add user')' (початкова міграція - 'Init') --

poetry run alembic upgrade head	
	
3. Додаємо схеми валідації
file: src/schemas.py	

4. Створюємо репозиторій користувача
file: src/repository/users.py
> poetry add libgravatar

5. Сервіс аутентифікації та авторизації
> poetry add python-jose["cryptography"]
> poetry add passlib["bcrypt"]
> poetry add python-multipart

file: src/services/auth.py

6. Маршрути аутентифікації
file: src/routes/auth.py

7. Змінюємо репозиторії
file: src/repository/contacts.py

8. Змінюємо маршрути
file: src/routes/contacts.py

9. Перевіряємо роботу застосунку

1) Обліковий запис (http://localhost:8000/api/auth/signup) { "username": "FirstUserTest", "email": "first@api.ua", "password": "123456" }
2) Аутентифікація користувача(http://localhost:8000/api/auth/login) { "username": "first@api.ua", "password": "123456" }
3) Контакти POST /api/contacts
4) Cписок усіх контактів GET /api/contacts/all
5) Один контакт за ідентифікатором GET /api/contacts/{contact_id}
6) Оновлення контакту за ідентифікатором PUT /api/contacts/{contact_id}
7) Видалення контакту за ідентифікатором DELETE /api/contacts/{contact_id}
8) Пошук за ім'ям, прізвищем та електронною поштою GET /api/contacts/find/{query}
9) Пошук за кількістю днів до дня народження GET api/contacts/birthday/{days}


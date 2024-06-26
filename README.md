# spring_project
## Деканат: звернення, довідки

### **Функціональні вимоги:**
1. Як користувач, я хочу мати можливість створити обліковий запис, вводячи своє ім'я, прізвище та статус особи, щоб отримати доступ до системи.
2. Як користувач, я хочу мати можливість переглядати список доступних типів довідок та звернень.
3. Як користувач, я хочу мати можливість подати заяву на отримання довідки, щоб отримати необхідний документ.
4. Як користувач, я хочу мати можливість переглядати список виданих мені довідок, щоб знати, які документи я отримав.
5. Як користувач, я хочу мати можливість подати звернення до деканату, щоб вирішити свою проблему або отримати інформацію.
6. Як користувач, я хочу мати можливість переглядати статус мого звернення, щоб знати, чи вирішена моя проблема.
7. Як працівник деканату, я хочу мати можливість створити обліковий запис, вводячи своє ім'я, прізвище та посаду, щоб отримати доступ до системи.
8. Як працівник деканату, я хочу мати можливість видавати довідки користувачам, щоб виконувати свої обов'язки.
9. Як працівник деканату, я хочу мати можливість приймати і обробляти звернення користувачів, щоб вирішувати їхні проблеми.
10. Як адміністратор системи, я хочу мати можливість додавати нових працівників деканату, щоб забезпечити їхню участь в процесах обробки заяв та видачі довідок.
11. Як адміністратор системи, я хочу мати можливість редагувати інформацію про працівників деканату, щоб підтримувати актуальність даних.


### **Поведінка системи**
**Створення облікового запису:**

- Користувач вводить ім'я, прізвище та статус особи.
- Система перевіряє, чи чи всі поля заповнені та введені дані коректні.
- Якщо дані коректні, система створює обліковий запис.
- Якщо дані некоректні, система відображає повідомлення про помилку.
  
**Подання нового звернення:**

- Користувач вибирає тип звернення, вводить тему та опис зверненн.
- Система перевіряє, чи введені дані коректні.
- Якщо дані коректні, система реєструє нове звернення та надсилає повідомлення про його надходження працівнику деканату, який відповідає за його обробку.
- Якщо дані некоректні, система відображає повідомлення про помилку.
  
**Отримання довідки:**
  
- Користувач заповнює онлайн-заявку на отримання довідки.
- Система перевіряє, чи введені дані коректні.
- Якщо дані коректні, система реєструє нову заявку та надсилає повідомлення про її надходження працівнику деканату, який відповідає за видачу довідок.
- Якщо дані некоректні, система відображає повідомлення про помилку.
- Після опрацювання заявки користувач може завантажити готову довідку з сайту.

**Перегляд інформації:**

- Користувач може переглядати інформацію про видані довідки та надіслані звернення та статус свого звернення.
- Система відображає цю інформацію у зручному форматі.

**Обробка звернень:**

- Працівник деканату може переглядати список нових звернень, приймати їх до обробки, відхиляти (з поясненням причини), а також опрацьовувати їх (збирати інформацію, контактувати з заявником, готувати відповідь).
- Система надає працівнику деканату всю необхідну інформацію для опрацювання звернень.
- Працівник деканату може закривати звернення (з позначкою, чи вирішено проблему).

**Видача довідок:**

- Працівник деканату може переглядати список нових заяв на отримання довідок, опрацьовувати їх (перевіряти дані, готувати довідку), а також видавати готові довідки користувачам.
- Система надає працівнику деканату всю необхідну інформацію для видачі довідок.


### **REST API Endpoints**

**Створення облікового запису:**

**Метод:** POST

**URI:** `/users`

**Тіло запиту:**
- first_name: Ім'я користувача (string)
- last_name: Прізвище користувача (string)
- person_status: Статус користувача (string)
  
**Відповідь:**
- person_id: ID користувача (integer)
- first_name: Ім'я користувача (string)
- last_name: Прізвище користувача (string)
- person_status: Статус користувача (string)

  
**Перегляд типів довідок та звернень:**

**Метод:** GET

**URI:** `/document-and-appeal-types`

**Відповідь:**
Масив об'єктів типу довідки та звернення:
- type_id: ID типу довідки або звернення (integer)
- topic: Тема типу довідки або звернення (string)
- main_text: Опис типу довідки або звернення (string)

  
**Подання нового звернення:**

**Метод:** POST

**URI:** `/appeals`

**Тіло запиту:**
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
  
**Відповідь:**
- appeal_id: ID звернення (integer)
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
- is_problem_solved: Чи вирішена проблема (boolean, 1 - так, 0 - ні)
- who_accepted: ID працівника деканату, який прийняв звернення (integer)
- who_applied: ID користувача, який подав звернення (integer)
- date_of_application: Дата подання звернення (datetime)


**Перегляд виданих довідок:**

**Метод:** GET

**URI:** `/documents/user/{person_id}`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати ID, що відповідає person_id у URI.

**Відповідь:**
Масив об'єктів довідок:
- document_id: ID довідки (integer)
- document_type: ID типу довідки (integer)
- who_give: ID працівника деканату, який видав довідку (integer)
- who_took: ID користувача, який отримав довідку (integer)
- date_of_issue: Дата видачі довідки (datetime)
- file_url: URL-адреса файлу з довідкою (string)


**Перегляд статусу звернення:**

**Метод:** GET

**URI:** `/appeals/{appeal_id}`

**Відповідь:**
- appeal_id: ID звернення (integer)
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
- is_problem_solved: Чи вирішена проблема (boolean, 1 - так, 0 - ні)
- who_accepted: ID працівника деканату, який прийняв звернення (integer)
- who_applied: ID користувача, який подав звернення (integer)
- date_of_application: Дата подання звернення (datetime)


**Створення облікового запису працівника деканату:**

**Метод:** POST

**URI:** `/staff`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "admin".

**Тіло запиту:**
- first_name: Ім'я працівника деканату (string)
- last_name: Прізвище працівника деканату (string)
- staff_position: Посада працівника деканату (string)

**Відповідь:**
- staff_id: ID працівника деканату (integer)
- first_name: Ім'я працівника деканату (string)
- last_name: Прізвище працівника деканату (string)
- staff_position: Посада працівника деканату (string)


**Редагування інформації про працівника деканату:**

**Метод:** PUT

**URI:** `/staff/{staff_id}`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "admin".

**Тіло запиту:**
- first_name: Ім'я працівника деканату (string)
- last_name: Прізвище працівника деканату (string)
- staff_position: Посада працівника деканату (string)

**Відповідь:**
staff_id: ID працівника деканату (integer)
first_name: Ім'я працівника деканату (string)
last_name: Прізвище працівника деканату (string)
staff_position: Посада працівника деканату (string)


**Видача довідок:**

**Метод:** POST

**URI:** `/documents`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "staff".

**Тіло запиту:**
- document_type: ID типу довідки (integer)
- who_took: ID користувача, який отримує довідку (integer)
- file: Файл з довідкою (дозволені формати: PDF, DOCX)

**Відповідь:**
- document_id: ID довідки (integer)
- document_type: ID типу довідки (integer)
- who_give: ID працівника деканату, який видав довідку (integer)
- who_took: ID користувача, який отримав довідку (integer)
- date_of_issue: Дата видачі довідки (datetime)
- file_url: URL-адреса файлу з довідкою (string)


**Прийняття та обробка звернень:**

**Метод:** PUT

**URI:** `/appeals/{appeal_id}/accept`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "staff".

**Відповідь:**
- appeal_id: ID звернення (integer)
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
- is_problem_solved: Чи вирішена проблема (boolean, 0 - ні)
- who_accepted: ID працівника деканату, який прийняв звернення (integer)
- who_applied: ID користувача, який подав звернення (integer)
- date_of_application: Дата подання звернення (datetime)

**Метод:** PUT

**URI:** `/appeals/{appeal_id}/reject`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "staff".

**Тіло запиту:**
- reason: Причина відхилення (string)

**Відповідь:**
- appeal_id: ID звернення (integer)
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
- is_problem_solved: Чи вирішена проблема (boolean, 0 - ні)
- reason: Причина відхилення (string)
- who_accepted: ID працівника деканату, який прийняв звернення (integer)
- who_applied: ID користувача, який подав звернення (integer)
- date_of_application: Дата подання звернення (datetime)

**Метод:** PUT

**URI:** `/appeals/{appeal_id}/resolve`

**Авторизація:** Користувач, який робить запит, повинен бути авторизований та мати роль "staff".

**Відповідь:**
- appeal_id: ID звернення (integer)
- appeal_type_id: ID типу звернення (integer)
- topic: Тема звернення (string)
- main_text: Опис звернення (string)
- is_problem_solved: Чи вирішена проблема (boolean, 1 - так)
- who_accepted: ID працівника деканату, який прийняв звернення (integer)
- who_applied: ID користувача, який подав звернення (integer)
- date_of_application: Дата подання звернення (datetime)


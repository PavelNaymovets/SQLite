Задание 1:

1.ALTER TABLE streams RENAME COLUMN start_date TO started_at

Задание 2:

1.ALTER TABLE streams ADD COLUMN finished_at TEXT;

Задание 3 (пример с таблицей streams):

1.INSERT INTO streams (course_id, number, started_at, number_of_students) VALUES (3, 165, '18.08.2020', 34); - вставка одной строкой
2.INSERT INTO streams (course_id, number, started_at, number_of_students) 
VALUES (2, 178, '02.10.2020',37), (1,203,'12.11.2020', 35), (1, 210,'03.12.2020', 41); - вставка несколько строк сразу
3. .mode table - меняю способ отображения данных
4.SELECT * FROM streams; - смотрю данные во всех строках в таблице

+----+-----------+--------+------------+--------------------+-------------+
| id | course_id | number | started_at | number_of_students | finished_at |
+----+-----------+--------+------------+--------------------+-------------+
| 1  | 3         | 165    | 18.08.2020 | 34                 |             |
| 2  | 2         | 178    | 02.10.2020 | 37                 |             |
| 3  | 1         | 203    | 12.11.2020 | 35                 |             |
| 4  | 1         | 210    | 03.12.2020 | 41                 |             |
+----+-----------+--------+------------+--------------------+-------------+

тоже самое проделываю для оставшихся таблиц и вывожу результат их заполнения

5.SELECT * FROM teachers;

+----+---------+----------+------------------------+
| id |  name   | surname  |         email          |
+----+---------+----------+------------------------+
| 1  | Николай | Савельев | saveliev.n@mail.ru     |
| 2  | Наталья | Петрова  | petrova.n@yandex.ru    |
| 3  | Елена   | Малышева | malisheva.e@google.com |
+----+---------+----------+------------------------+

6.SELECT * FROM grades;
+------------+-----------+-------+
| teacher_id | stream_id | grade |
+------------+-----------+-------+
| 3          | 1         | 4.7   |
| 2          | 2         | 4.9   |
| 1          | 3         | 4.8   |
| 1          | 4         | 4.9   |
+------------+-----------+-------+

7.SELECT * FROM courses;
+----+-----------------------+
| id |         name          |
+----+-----------------------+
| 1  | База данных           |
| 2  | Основы Python         |
| 3  | Linux.Рабочая станция |
+----+-----------------------+

Задание 4:

1. ALTER TABLE grades RENAME TO grades_old;
2. CREATE TABLE grades (
   ...> teacher_id INTEGER NOT NULL,
   ...> stream_id REAL NOT NULL,
   ...> grade REAL NOT NULL,
   ...> PRIMARY KEY (teacher_id, stream_id),
   ...> FOREIGN KEY (teacher_id) REFERENCES teachers (id),
   ...> FOREIGN KEY (stream_id) REFERENCES streams (id)
   ...> );
3.  INSERT INTO grades (teacher_id, stream_id, grade) SELECT * FROM grades_old;
4. SELECT * FROM grades;
+------------+-----------+-------+
| teacher_id | stream_id | grade |
+------------+-----------+-------+
| 3          | 1.0       | 4.7   |
| 2          | 2.0       | 4.9   |
| 1          | 3.0       | 4.8   |
| 1          | 4.0       | 4.9   |
+------------+-----------+-------+
5.  .schema grades
CREATE TABLE grades (
teacher_id INTEGER NOT NULL,
stream_id REAL NOT NULL, - изменил тип данных столбца "stream_id с INTEGER на REAL"
grade REAL NOT NULL,
PRIMARY KEY (teacher_id, stream_id),
FOREIGN KEY (teacher_id) REFERENCES teachers (id),
FOREIGN KEY (stream_id) REFERENCES streams (id)
);
6.  DROP TABLE grades_old;
P01.A: 
\\\Вставьте нового пользователя с вашим именем и фамилией
INSERT INTO Users (first_name, last_name)
VALUES ('Zhangirkhan', 'Kaniev');


P01.B: 
\\\Вставьте много новых пользователей с именами ваших друзей
BEGIN TRANSACTION; 
INSERT INTO Users (first_name, last_name) 
VALUES ('Arsen', 'Baimet'), 
       ('Dias', 'Jamall'),  
       ('Dilya','Kanieva');


P01.C: 
\\\Удалить из SuspiciousTransactions все сообщения из аккаунта № 8
DELETE FROM SuspiciousTransactions 
WHERE Transaction_id = 8;


P01.D: 
\\\Измените имя пользователя с номером 7 на «Майк».
UPDATE Users 
SET first_name = 'Mike'
WHERE User_id = 7; 


P01.E: 
\\\Обновить таблицу Users, если имя заканчивается на, сделайте свой пол M
UPDATE Users 
SET gender = 'M' 
WHERE first_name LIKE '%a'; 


P02.A: 
\\\Скопируйте транзакции (не путать с оператором транзакций), которые были выполнены в апреле,
 из таблицы транзакций в таблицу SuspiciousTransactions

INSERT INTO SuspiciousTransactions(Transaction_id, from_account_id, to_account_id, performed_at)
SELECT Transaction_id, from_account_id, to_account_id, performed_at
FROM Transactions 
WHERE strftime('%m', performed_at) = '04'; 


P02.B: 
\\\Удалить последние 3 транзакции
DELETE FROM SuspiciousTransactions 
ORDER BY Transaction_id DESC
LIMIT 3;


P02.C: 
\\\Обновите все учетные записи, принадлежащие пользователям
 (все таблицы учетных записей, у которых user_id не null), зарабатывайте меньше на 10 $

BEGIN TRANSACTION; 
  UPDATE Accounts 
  SET Money = Money - 10 
  WHERE User.id IS NOT NULL; 
COMMIT;


P02.D: 
\\\Вы получили новый файл с названиями компаний и должны добавить их в таблицу «Компании»Примечание.
 У каждой компании должно быть уникальное имя (поэтому две компании не могут иметь одно и то же имя). 
Если он уже существует в таблице, обновите его

BEGIN TRANSACTION; 
INSERT OR REPLACE INTO Companies(Title, Country)
VALUES ('Google', 'USA'), 
       ('Jayo', 'Russia'), 
       ('Yandex', 'Russia'), 
       ('Roombo', 'Poland');
COMMIT;


P03.B: 
\\\Использовать транзакции Обновите учетные записи, если на счете меньше 0, 
обновите как x * 1.07, если больше 0, он должен преобразоваться в x * 1.2

BEGIN TRANSACTION; 
UPDATE Accounts
SET Money = Money * 1.07
WHERE Money < 0; 

UPDATE Accounts 
SET Money = Money * 1.2
WHERE Money > 0; 
COMMIT; 








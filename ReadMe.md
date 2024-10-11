# itmo-web-task3
# Mission 3
## Part 0 (Database) Скринкаст, где есть все части
https://disk.yandex.ru/i/DtIilZk9CZaLkg
## Part1 (Authorization)
https://hmmsbx.buildship.run/me
## Part2 (Sending messages)
https://hmmsbx.buildship.run/message
## Part3 (Selects)
## usernames
#Всё максимально просто - выбираем все username из таблицы users
SELECT username FROM users;

## number of sent messages
#Считаем количество сообщений
SELECT u.username, COUNT(*) as number_of_sent_messages
FROM messages m
#Соединеям таблицы 
JOIN users u ON m.id = u.id
#Группируем
GROUP BY u.username;

## number of received messages
#Считаем количество сообщений
SELECT username, COUNT(*) as number_of_received_messages
FROM messages
#Группируем
JOIN users ON messages.id = users.id
GROUP BY username
#Сортируем по убыванию
ORDER BY number_of_received_messages DESC
#Оставляем 1 строчку (топ-1)
LIMIT 1;

## average messages per user
#Считаем общее количество
SELECT username, AVG(num_messages) as average_messages
FROM (
    SELECT u.username, COUNT(*) as num_messages
    FROM messages m
    #Соединяем
    JOIN users u ON m.id = u.id
    GROUP BY u.username
) t
#Группируем по username
GROUP BY username;

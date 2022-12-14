# TODO-AJAX

Список дел из предыдущего задания (ToDo using DOM) можно сохранять и загружать с сервера с помощью AJAX запросов

Для этого используется сервер https://jsfeajax.herokuapp.com/, который умеет принимать GET и POST запросы

Любой запрос в урле содержит уникальный компонент (например ИмяФамилия), для того, чтобы разделить данные разных пользователей.

Например, GET запрос `https://jsfeajax.herokuapp.com/IgorKorshuk/todo` вернет список дел, если пользователь `IgorKorshuk` хотя бы раз обращался к серверу, если нет, то создаст новый пустой список на сервере, с которым можно работать, и вернет пустой массив.

### Итак, API

- **GET** `'https://jsfeajax.herokuapp.com/' + UserName + '/todo'` возвращает список дел
- **POST** `'https://jsfeajax.herokuapp.com/' + UserName + '/todo'` создаёт или обновляет существующее дело и возвращает список. Если нужно создать новое дело, то посылается такой объект: 
  ``` JSON
  { 
    "text": "тут находится текст" }
  ```
  сервер создаст дело, положит его в список и вернет новый список. В том массиве, который возвращает сервер, будут такие объекты: 
  ``` JSON
  { 
    "text": "моё событие", 
    "id": "c712d8b0-7b1c-11e5-b6fc-75340f204013", 
    "status":"new"
  }
  ```
  У всех новых событий статус автоматически делается "new". 
  Если послать на этот POST запрос полный объект, с существующим id, то сервер перезапишет его (так можно статус менять)
- есть еще **POST** запрос `'https://jsfeajax.herokuapp.com/' + UserName + '/todo/delete'`. Если туда послать объект целиком (с id, статусом и текстом), то объект удалится из базы и сервер вернет список дел без него

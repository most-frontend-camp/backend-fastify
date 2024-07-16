# HTTP
HTTP messages are how data is exchanged between a server and a client. 

There are two types of messages: requests sent by the client to trigger an action on the server, and responses, the answer from the server.

Web developers, or webmasters, rarely craft these textual HTTP messages themselves: software, a Web browser, proxy, or Web server, perform this action. They provide HTTP messages through config files (for proxies or servers), APIs (for browsers), or other interfaces.



### Request

### Homework 4 part 3

```js
import fastify from 'fastify';

const app = fastify();
const port = 3000;

const state = {
  user: [
    {
      name: 'John',
    },
  ],
};

app.get('/hello', (req, res) => {
  const user = req.query;
  if (!user) {
    res.code(404).send({ message: 'Hello World' })
  } else {
    res.send("Салем" + user.name);
  }
});



app.listen({port});
```

### Homework 4 part 2


with curl parameters

```js
import fastify from 'fastify';

const app = fastify();
const port = 3000;

const state = {
  users: [
    {
      id: 1,
      name: 'John',
    },
  ],
};

app.get('/hello', (req, res) => {
  const { id } = req.query;
  const user = state.users.find(user => user.id === parseInt(id)); // Приведение к одному типу и сравнение
  if (!user) {
    res.code(404).send({ message: 'Hello World' })
  } else {
    res.send("Salem" + user.name);
  }
});

app.listen({port});
```

`localhost:3000/hello` will give `Hello World`
`localhost:3000/hello?name=John&id=1` will give `"Salem John"`


### Homework 2

Пейджинг — это механизм, позволяющий итерировать большие коллекции небольшими порциями. Его часто применяют в результатах запросов поисковых систем.

С точки зрения пользователя пейджинг выглядит как параметры запроса:

page — определяет текущую страницу
per — определяет количество элементов на страницу
Обычно эти параметры называют именно так, но имена могут быть и другими. Запрос c page со значением 1 работает аналогично запросу без указания page.

src/index.js
Реализуйте обработчик, который должен:

Обрабатывать GET-запрос на адрес /users
Отдавать по этому адресу список пользователей в виде json
Сделайте так, чтобы список пользователей отдавал только те записи, которые соответствуют текущей запрошенной странице. По умолчанию должна выдаваться первая страница и пять результатов на запрос.

Данные для пейджинга передаются в параметрах строки запроса. Примеры таких запросов:

/users – параметры строки запроса не переданы. Должна выдаваться первая страница с количеством результатов 5, то есть первые пять записей. /users?page=5&per=3 — должна выдаваться пятая страница с количеством результатов по 3 на странице. То есть должны возвращаться 13, 14 и 15 запись из списка


```js
const page = req.query.page || 1;
const per = req.query.per || 5;

const chunked = _.chunk(users, per);

return res.send(chunked[page - 1]);
```
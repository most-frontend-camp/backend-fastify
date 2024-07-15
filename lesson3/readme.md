# Controller

Request controller
```js
app.get('/', (req, res) => {
  res.send('Hello World!');
});
```


### Homework 3
Все данные находятся в переменной data.
Доработайте функцию, создающую Fastify-приложение, добавьте в него:

1. Обработчик GET /phones. Он должен возвращать список телефонов data.phones
2. Обработчик GET /domains. Он должен возвращать список доменов data.domains

```js
import fastify from 'fastify';

const app = fastify();
const port = 3000;

const data = {
  phones: ['7711', '8-700-990-77-11'],
  domains: ['jusan.kz', 'jmart.kz'],
};
// here below write your code

// answer
  
app.listen({port});
```

### Homework 3 Solution

Here is solution
```js
import fastify from 'fastify';

const app = fastify();
const port = 3000;

const data = {
  phones: ['7711', '8-700-990-77-11'],
  domains: ['jusan.kz', 'jmart.kz'],
};

app.get('/phones', (req, res) => {
    res.send(data.phones);
});

app.get('/domains', (req, res) => {
    res.send(data.domains);
});
  
app.listen({port});
```
# Dynamic routing

В этом уроке вы познакомитесь с динамическими маршрутами и узнаете, как правильно работать с множественными параметрами пути и порядком определения.

https://jmart.kz/catalog
https://jmart.kz/cart
https://jmart.kz/articles/qrlite

### Routes

Выше мы привели примеры динамических маршрутов. 

`/product/${id}`

`id` у нас изменяемая часть маршрута, а `product` будет нашим обработчиком, причем единственным. 

```bash
curl localhost:3000/users/1293129313
// User ID: 1293129313%  

curl localhost:3000/products/12
// Product ID: 12%        
                                                                                           
curl localhost:3000/products/dyson
// Product ID: dyson%  
```

### Routes summary

* Понятия «адрес» и «маршрут» обозначают разные вещи
* Если маршрут статический, то он всегда совпадает с адресом — например, /about
* Если маршрут динамический, то ему могут соответствовать бесконечное число адресов, даже если таких страниц на сайте нет — например, /courses/:id


### Error handling

Не забывайте что 
- нужно проверять есть ли данных в базе
- выкидывать ответ с кодом 404 когда нету данных которые ищем


```js
сonst state = {
  users: [
    {
      id: 1,
      name: 'user',
    },
  ],
};

app.get('/users/:id', (req, res) => {
  const { id } = req.params;
  const user = state.users.find((user) => user.id === parseInt(id));
  if (!user) {
    res.code(404).send({ message: 'User not found' });
  } else {
    res.send(user);
  }
});
```


```js
import fastify from 'fastify';
// import getUsers from './utils.js';

const app = fastify();
const port = 3000;

app.get('/shops/:shopID/products/:id', (req, res) => {
  res.send(`Shop ID: ${req.params.shopID}; Product ID: ${req.params.id}`);
});

app.listen({port});
```

```
localhost:3000/shops/:shopID/products/:id

Answer
Shop ID: 12; Product ID: 99

```


В работе с динамическими маршрутами нужно следить за порядком их определения. 

Иначе мы можем столкнуться с ситуацией, когда одному адресу соответствует несколько маршрутов. 
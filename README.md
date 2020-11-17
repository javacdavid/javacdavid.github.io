# Introduccion

Bienvenido a la aplicacion de Operacion-fuego-quasar. Esta Api consiste en el manejo de una situación ficticia para el universo de Star Wars, en el cual es necesario interceptar y decodificar, por parte de 3 satélites rebeldes, los mensajes que emite una nave imperial, rodeada de asteroides. También, a partir del conocimiento de la distancia que cada satélite tiene a la nave, la Api determinará la ubicación en coordenadas(x, y) de la misma.

Esta documentación fue creada con [Slate](https://github.com/slatedocs/slate).

El siguiente servicio descifra el mensaje que emite la nave y calcula la ubicación a partir de los mensajes y las distancias parametrizadas

# POST topsecret

```shell
https://operation-quasar-fire.herokuapp.com/api/v1/spaceship-interceptor/topsecret/
```
el request body debe respetar el siguiente formato

```json
{
    "satellites" :[
        {
            "name" : "Kenobi",
            "distance" : 500.0,
            "message" :["help!", "", "", "support", "", "we", "", "", "","asteroids"]
        },
        {
            "name" : "Skywalker",
            "distance" : 110.0,
            "message" :["", "", "", "support", "here,", "", "are", "", "by", ""]
        },
        {
            "name" : "Sato",
            "distance" : 556.3,
            "message" :["", "we", "need", "", "", "", "", "surrounded", "", ""]
        }
    ]

}
```


> La respuesta para este request será, por ejemplo:

```json
{
    "location": {
        "x": -4.346184465246722,
        "y": -134.21782045385874
    },
    "message": "help! we need support here, we are surrounded by asteroids"
}
```

Esta api permite almacenar una instancia de datos del satelite

# POST topsecret_split

```shell
https://operation-quasar-fire.herokuapp.com/api/v1/spaceship-interceptor/topsecret_split/Skywalker
```
el request body tendrá el siguiente payload

```json
{
    "distance" : 110.0,
    "message" :["", "", "un", "mensaje"]
}
```


> La respuesta para este request será el objeto almacenado:

```json
{
    "name": "Skywalker",
    "distance": 110.0,
    "message": [
        "",
        "",
        "un",
        "mensaje"
    ]
}
```

Esta api permite almacenar una instancia de datos del satelite

# GET topsecret_split

```shell
https://operation-quasar-fire.herokuapp.com/api/v1/spaceship-interceptor/topsecret_split/Skywalker
```
el request body tendrá el mismo payload que el servicio anterior

```json
{        
    "distance" : 110.0,
    "message" :["", "", "", "support", "here,", "", "are", "", "by", ""]
}
```

La diferencia es que este servicio utilizará los datos brindados en el body y buscará en la base de datos la información ya almacenada para calcular 
el mensaje y la distancia de la nave imperial

> La respuesta para este request será la misma que brinda el servicio topsecret

```json
{
    "location": {
        "x": -4.346184465246722,
        "y": -134.21782045385874
    },
    "message": "help! we need support here, we are surrounded by asteroids"
}
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete


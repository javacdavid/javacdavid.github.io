# Introduccion

Bienvenido a la aplicacion de Operacion-fuego-quasar. Esta Api consiste en el manejo de una situación ficticia para el universo de Star Wars, en el cual es necesario interceptar y decodificar, por parte de 3 satélites rebeldes, los mensajes que emite una nave imperial, rodeada de asteroides. También, a partir del conocimiento de la distancia que cada satélite tiene a la nave, la Api determinará la ubicación en coordenadas(x, y) de la misma.

Esta documentación fue creada con [Slate](https://github.com/slatedocs/slate).

A continuación se presentan los servicios disponibles, especificando su funcionalidad y uso
## HTTP Request
### POST topsecret

El siguiente servicio descifra el mensaje que emite la nave y calcula la ubicación a partir de los mensajes y las distancias parametrizadas

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


### POST topsecret_split

Esta api permite almacenar una instancia de datos del satelite

```shell
https://operation-quasar-fire.herokuapp.com/api/v1/spaceship-interceptor/topsecret_split/{name}
```
#### URL Parameters

Parameter | Description
--------- | -----------
name | el nombre del satelite. Por ejemplo: Kenobi.

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


### GET topsecret_split

```shell
https://operation-quasar-fire.herokuapp.com/api/v1/spaceship-interceptor/topsecret_split/{name}
```

#### URL Parameters

Parameter | Description
--------- | -----------
name | el nombre del satelite. Por ejemplo: Kenobi.

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

### RESPONSE CODES

Codigo | Exception | Descripcion
--------- | ----------- | ---------
404 | MessageNotFoundException | no se ha podido decodificar el mensaje de la nave imperial
404 | SpaceShipNotFoundException | no se ha podido calcular la distancia a la nave imperial

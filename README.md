## FuncionLambda-aws--MercadoPago
## Author
- BRIAN CASTRO
# Comenzando 馃殌
Esta funci贸n se crea con el prop贸sito de usarlo en lambda AWS.

- 驴Qu茅 es una funci贸n lambda AWS?

Una funci贸n Lambda de AWS es un servicio de AWS que permite ejecutar c贸digo sin provisionar ni administrar servidores, es por ello que es llamada SERVERLESS (sin sevidor). Puedes crear una funci贸n Lambda y asociarla a una variedad de eventos, como una solicitud HTTP a trav茅s de Amazon API Gateway (C贸mo se hizo en este caso). Cada vez que se activa el evento, AWS Lambda ejecuta autom谩ticamente la funci贸n y gestiona todas las tareas necesarias para escalar la ejecuci贸n seg煤n la demanda.

- 驴Qu茅 es API Gateway?

API Gateway act煤a como una "puerta" a trav茅s de la cual los clientes pueden acceder a la funcionalidad de la funci贸n Lambda mediante solicitudes HTTP.

- 驴Qu茅 hace esta funci贸n del repositorio? 

Conectarse a mercadoPago y crear un pago con la informaci贸n que viene del fronted (token, payment_method_id, transaction_amount, email, numero de DNI etc ) y devolverme el status, status_detail y el id del pago.

# Ejemplo:

C贸digo de fronted en TypeScript:
```python
onSubmit: async (cardFormData: any) => {
            const response = await fetch(
              "Aqu铆 va tu API endpoint",
              {
                method: "POST",
                headers: {
                  "Content-Type": "application/json",
                },
                body: JSON.stringify(cardFormData),
              }
            );
            console.log("response", await response.json());
```
Es este c贸digo se observa que estoy haciendo un fetch enviando toda la data mediante POST.

Esta data (informaci贸n del pago) al ser enviada al backend tiene el siguiente formato:

![Untitled](https://user-images.githubusercontent.com/109192347/212758748-8d82cfda-2952-4241-bb6a-d2836e0d6f2b.png)

Luego en mi funci贸n lambda usar茅 el siguiente c贸digo para guardar el pago:

```python
sdk.payment().create(payment_data)
```

La funci贸n lambda despu茅s de guardar el pago, retornar谩 el status y el id del pago.
Este return de la funcion lambda se recepcionar谩 en el fronted y al imprimir por consola se debe ver la siguiente informaci贸n:
![Captura de pantalla 2023-01-16 152947](https://user-images.githubusercontent.com/109192347/212761008-2ef7b375-9d07-4082-b8f8-da82ba965bac.png)

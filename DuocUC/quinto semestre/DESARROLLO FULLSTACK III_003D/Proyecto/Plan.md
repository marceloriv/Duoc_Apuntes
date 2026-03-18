# Proyecto

La plataforma será un espacio digital donde las personas puedan descubrir eventos, comprar entradas de forma sencilla y, al mismo tiempo, aportar a una causa social. Cada ticket vendido no solo genera ingresos para los organizadores, sino que también destina un porcentaje a organizaciones sin fines de lucro. Es una propuesta que combina tecnología moderna, cercanía con la comunidad y un impacto positivo, diferenciándose de las plataformas tradicionales que solo buscan rentabilidad.
Darle visibilida a los eventos pequeños, donde el cliente decide a traves de la compra de ticket a que sociedad sin fines de lucro darle esa donacion,esta donacion esta dentro del precio.

## Nombres

Posibles nombres del sistema
>[!question] ¿El cliente define el nombre del sistema?
>
>Podemos nosotros definiar un posible nombre del sistema basandonos en marketing o estudio del mercado
>Posibles Nombres
>
> - nombre 1

## Minutas

Siempre preguntarle al cliente que quiere,  y esperar las respuestas del cliente.

## Microservicios

   1. Inventario
   2. Envios(sistema de mensajeria | correo)
   3. Pedidos (Ticket)
   4. carrito de compras
   5. Eventos
   6. Donaciones
   7. Usuario

>[!note] Factor Method
>Hay que implementar por el momento este patron en:
>
>- Usuario
>- Evento
>- Ticket
>- Pago

Cada Microservicio Tiene su fallback

### Envios

Es un sistema de mensajeria, del tipo que cuando se compra un producto le llega un correo, mensaje...entre otros. Igualmente que hay un sistema de devolución

### Usuario

Tipos de usuario:

- Cliente
  - Dashboard tipo general
- administrador
  - Dashboard tipo moderacion
- Creador de Eventos
  - Interfaz de CRUD de eventos

### Evento

Tendran categorias/etiquetas segun corresponda el evento ya sea:

- Forma de Pago
  - Gratuitos
  - De pago
  -

### Pedidos

### Carrito de compras

### Donaciones

## Patrones de diseño

### Factory Method

Creacion de instancias

### Repository Pattern

persistencia de datos (JPA)

### Circuit Breaker

Manejo de fallos entre los microservicios

Hay que colocorlo en todos lado ya que uno no sabe en donde se va caer el sistema

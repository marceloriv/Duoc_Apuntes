# Proyecto

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

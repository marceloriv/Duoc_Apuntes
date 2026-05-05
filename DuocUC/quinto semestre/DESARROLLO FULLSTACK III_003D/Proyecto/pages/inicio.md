
# Pagina de incio

## Registro - Componente React

```jsx
import React, { useState } from 'react';
import { Container, Row, Col, Card, Button, Alert } from 'react-bootstrap';
import Form from 'react-bootstrap/Form';
import api from '../services/api';
import '../styles/brand.css';

export default function Registro() {
 const [formData, setFormData] = useState({
  nombre: '',
  correo: '',
  contrasena: '',
  confirmarContrasena: '',
  direccion: '',
  telefono: '',
  aceptaTerminos: false,
 });

 const [mensaje, setMensaje] = useState({ tipo: null, texto: '' });
 const [cargando, setCargando] = useState(false);

 const handleChange = (e) => {
  const { name, value, type, checked } = e.target;
  setFormData((prev) => ({
   ...prev,
   [name]: type === 'checkbox' ? checked : value,
  }));
 };

 const validarFormulario = () => {
  if (
   !formData.nombre ||
   !formData.correo ||
   !formData.contrasena ||
   !formData.direccion ||
   !formData.telefono
  ) {
   setMensaje({
    tipo: 'danger',
    texto: 'Todos los campos son obligatorios',
   });
   return false;
  }

  if (formData.contrasena !== formData.confirmarContrasena) {
   setMensaje({ tipo: 'danger', texto: 'Las contraseñas no coinciden' });
   return false;
  }

  if (
   formData.telefono.length !== 9 ||
   Number.isNaN(Number(formData.telefono))
  ) {
   setMensaje({ tipo: 'danger', texto: 'El teléfono debe tener 9 dígitos' });
   return false;
  }

  if (!formData.aceptaTerminos) {
   setMensaje({ tipo: 'danger', texto: 'Debes aceptar los términos' });
   return false;
  }

  return true;
 };

 const handleSubmit = async (e) => {
  e.preventDefault();
  setMensaje({ tipo: null, texto: '' });

  if (!validarFormulario()) return;

  setCargando(true);

  try {
   const datosRegistro = {
    nombre: formData.nombre,
    correo: formData.correo,
    contrasena: formData.contrasena,
    direccion: formData.direccion,
    telefono: formData.telefono,
    rol: 'CLIENTE', // Rol por defecto para nuevos registros
   };

   await api.post('/usuarios', datosRegistro);

   setMensaje({
    tipo: 'success',
    texto: '¡Registro exitoso! Redirigiendo a login...',
   });

   // Limpiar formulario
   setFormData({
    nombre: '',
    correo: '',
    contrasena: '',
    confirmarContrasena: '',
    direccion: '',
    telefono: '',
    aceptaTerminos: false,
   });

   // Redirigir a login después de 2 segundos
   setTimeout(() => {
    globalThis.location.href = '/login';
   }, 2000);
  } catch (error) {
   const mensajeError =
    error.response?.data?.mensaje ||
    error.response?.data?.message ||
    'Error en el registro. Intenta nuevamente.';
   setMensaje({ tipo: 'danger', texto: mensajeError });
  } finally {
   setCargando(false);
  }
 };

 return (
  <Container className="containerRegistro py-5">
   <Row className="justify-content-center">
    <Col md={10} lg={4} className="mx-auto">
     <Card className="registro-card shadow">
      <Card.Body>
       <h2 className="text-center mb-4">Registro</h2>

       {mensaje.texto && (
        <Alert variant={mensaje.tipo} className="mb-4">
         {mensaje.texto}
        </Alert>
       )}
       <Form onSubmit={handleSubmit}>
        <Row className="mb-3">
         <Form.Group as={Col} controlId="formGridEmail">
          <Form.Label>Nombre de usuario</Form.Label>
          <Form.Control
           type="text"
           placeholder="Ingresa tu nombre de usuario"
           name="nombre"
           value={formData.nombre}
           onChange={handleChange}
          />
         </Form.Group>
        </Row>
        <Row className="mb-3">
         <Form.Group as={Col} controlId="formGridEmail">
          <Form.Label>Email</Form.Label>
          <Form.Control
           type="email"
           placeholder="Ingresa tu correo"
           name="correo"
           value={formData.correo}
           onChange={handleChange}
          />
         </Form.Group>
        </Row>

        <Row className="mb-3">
         <Form.Group as={Col} controlId="formGridPassword">
          <Form.Label>Contraseña</Form.Label>
          <Form.Control
           type="password"
           placeholder="Contraseña"
           name="contrasena"
           value={formData.contrasena}
           onChange={handleChange}
          />
         </Form.Group>
        </Row>

        <Form.Group as={Col} controlId="formGridPassword">
         <Form.Label>Confirmar Contraseña</Form.Label>
         <Form.Control
          type="password"
          placeholder="Confirmar Contraseña"
          name="confirmarContrasena"
          value={formData.confirmarContrasena}
          onChange={handleChange}
         />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formGridAddress1">
         <Form.Label>Dirección</Form.Label>
         <Form.Control
          placeholder="Ej: Calle 123"
          name="direccion"
          value={formData.direccion}
          onChange={handleChange}
         />
        </Form.Group>

        <Form.Group as={Col} controlId="formGridPassword">
         <Form.Label>Teléfono</Form.Label>
         <Form.Control
          type="tel"
          placeholder="Ingresa tu teléfono"
          name="telefono"
          value={formData.telefono}
          onChange={handleChange}
         />
        </Form.Group>

        <Form.Group className="mb-3" controlId="formGridCheckbox">
         <Form.Check
          type="checkbox"
          label="Acepto los términos"
          name="aceptaTerminos"
          checked={formData.aceptaTerminos}
          onChange={handleChange}
         />
        </Form.Group>

        <div className="text-center">
         <Button variant="primary" type="submit" className="btn">
          Registrarse
          {cargando && ' ...'}
         </Button>
        </div>
       </Form>
      </Card.Body>
     </Card>
    </Col>
   </Row>
  </Container>
 );
}
```

# Guía de Elementos Básicos en React

Esta guía te enseñará cómo usar los elementos básicos de una aplicación React, incluyendo inputs, buttons, labels, text areas y más.

## Configuración Inicial

Para comenzar, asegúrate de tener un proyecto React configurado. Si no tienes uno, puedes crearlo con:

```bash
npx create-react-app mi-app
cd mi-app
npm start
```

## 1. Input (Campo de Texto)

### Input Básico
```jsx
import React, { useState } from 'react';

function MiComponente() {
  const [texto, setTexto] = useState('');

  return (
    <div>
      <input
        type="text"
        value={texto}
        onChange={(e) => setTexto(e.target.value)}
        placeholder="Escribe aquí..."
      />
      <p>Texto ingresado: {texto}</p>
    </div>
  );
}
```

### Diferentes Tipos de Input
```jsx
function TiposDeInput() {
  const [datos, setDatos] = useState({
    texto: '',
    email: '',
    password: '',
    numero: '',
    fecha: ''
  });

  const manejarCambio = (e) => {
    setDatos({
      ...datos,
      [e.target.name]: e.target.value
    });
  };

  return (
    <div>
      <input
        type="text"
        name="texto"
        placeholder="Texto"
        value={datos.texto}
        onChange={manejarCambio}
      />
      
      <input
        type="email"
        name="email"
        placeholder="Email"
        value={datos.email}
        onChange={manejarCambio}
      />
      
      <input
        type="password"
        name="password"
        placeholder="Contraseña"
        value={datos.password}
        onChange={manejarCambio}
      />
      
      <input
        type="number"
        name="numero"
        placeholder="Número"
        value={datos.numero}
        onChange={manejarCambio}
      />
      
      <input
        type="date"
        name="fecha"
        value={datos.fecha}
        onChange={manejarCambio}
      />
    </div>
  );
}
```

## 2. Button (Botón)

### Botón Básico
```jsx
function BotonBasico() {
  const manejarClick = () => {
    alert('¡Botón clickeado!');
  };

  return (
    <button onClick={manejarClick}>
      Hacer Click
    </button>
  );
}
```

### Botones con Estados
```jsx
function BotonesConEstados() {
  const [contador, setContador] = useState(0);
  const [cargando, setCargando] = useState(false);

  const incrementar = () => setContador(contador + 1);
  const decrementar = () => setContador(contador - 1);
  const resetear = () => setContador(0);

  const simularCarga = async () => {
    setCargando(true);
    await new Promise(resolve => setTimeout(resolve, 2000));
    setCargando(false);
  };

  return (
    <div>
      <p>Contador: {contador}</p>
      <button onClick={incrementar}>+</button>
      <button onClick={decrementar}>-</button>
      <button onClick={resetear}>Reset</button>
      
      <button onClick={simularCarga} disabled={cargando}>
        {cargando ? 'Cargando...' : 'Simular Carga'}
      </button>
    </div>
  );
}
```

## 3. Label (Etiqueta)

```jsx
function EjemploLabels() {
  const [nombre, setNombre] = useState('');
  const [edad, setEdad] = useState('');

  return (
    <form>
      <div>
        <label htmlFor="nombre">Nombre:</label>
        <input
          id="nombre"
          type="text"
          value={nombre}
          onChange={(e) => setNombre(e.target.value)}
        />
      </div>
      
      <div>
        <label htmlFor="edad">Edad:</label>
        <input
          id="edad"
          type="number"
          value={edad}
          onChange={(e) => setEdad(e.target.value)}
        />
      </div>
    </form>
  );
}
```

## 4. Textarea (Área de Texto)

```jsx
function EjemploTextarea() {
  const [comentario, setComentario] = useState('');

  return (
    <div>
      <label htmlFor="comentario">Comentario:</label>
      <textarea
        id="comentario"
        value={comentario}
        onChange={(e) => setComentario(e.target.value)}
        placeholder="Escribe tu comentario aquí..."
        rows={4}
        cols={50}
      />
      <p>Caracteres: {comentario.length}</p>
    </div>
  );
}
```

## 5. Select (Lista Desplegable)

```jsx
function EjemploSelect() {
  const [pais, setPais] = useState('');
  const [idiomas, setIdiomas] = useState([]);

  const paises = ['México', 'España', 'Argentina', 'Colombia', 'Chile'];

  const manejarSeleccionMultiple = (e) => {
    const valores = Array.from(e.target.selectedOptions, option => option.value);
    setIdiomas(valores);
  };

  return (
    <div>
      {/* Select simple */}
      <label htmlFor="pais">País:</label>
      <select
        id="pais"
        value={pais}
        onChange={(e) => setPais(e.target.value)}
      >
        <option value="">Selecciona un país</option>
        {paises.map(p => (
          <option key={p} value={p}>{p}</option>
        ))}
      </select>
      
      {/* Select múltiple */}
      <label htmlFor="idiomas">Idiomas (mantén Ctrl para seleccionar varios):</label>
      <select
        id="idiomas"
        multiple
        value={idiomas}
        onChange={manejarSeleccionMultiple}
      >
        <option value="español">Español</option>
        <option value="ingles">Inglés</option>
        <option value="frances">Francés</option>
        <option value="italiano">Italiano</option>
      </select>
      
      <p>País seleccionado: {pais}</p>
      <p>Idiomas seleccionados: {idiomas.join(', ')}</p>
    </div>
  );
}
```

## 6. Checkbox y Radio Buttons

```jsx
function EjemploCheckboxRadio() {
  const [acepta, setAcepta] = useState(false);
  const [hobbies, setHobbies] = useState([]);
  const [genero, setGenero] = useState('');

  const manejarHobby = (hobby) => {
    if (hobbies.includes(hobby)) {
      setHobbies(hobbies.filter(h => h !== hobby));
    } else {
      setHobbies([...hobbies, hobby]);
    }
  };

  return (
    <div>
      {/* Checkbox simple */}
      <label>
        <input
          type="checkbox"
          checked={acepta}
          onChange={(e) => setAcepta(e.target.checked)}
        />
        Acepto los términos y condiciones
      </label>

      {/* Checkboxes múltiples */}
      <p>Hobbies:</p>
      {['Leer', 'Deportes', 'Música', 'Videojuegos'].map(hobby => (
        <label key={hobby}>
          <input
            type="checkbox"
            checked={hobbies.includes(hobby)}
            onChange={() => manejarHobby(hobby)}
          />
          {hobby}
        </label>
      ))}

      {/* Radio buttons */}
      <p>Género:</p>
      {['Masculino', 'Femenino', 'Otro'].map(g => (
        <label key={g}>
          <input
            type="radio"
            name="genero"
            value={g}
            checked={genero === g}
            onChange={(e) => setGenero(e.target.value)}
          />
          {g}
        </label>
      ))}

      <p>Acepta términos: {acepta ? 'Sí' : 'No'}</p>
      <p>Hobbies: {hobbies.join(', ')}</p>
      <p>Género: {genero}</p>
    </div>
  );
}
```

## 7. Formulario Completo

```jsx
function FormularioCompleto() {
  const [formData, setFormData] = useState({
    nombre: '',
    email: '',
    edad: '',
    comentario: '',
    pais: '',
    acepta: false,
    genero: ''
  });

  const manejarCambio = (e) => {
    const { name, value, type, checked } = e.target;
    setFormData({
      ...formData,
      [name]: type === 'checkbox' ? checked : value
    });
  };

  const manejarEnvio = (e) => {
    e.preventDefault();
    console.log('Datos del formulario:', formData);
    alert('Formulario enviado! Revisa la consola.');
  };

  return (
    <form onSubmit={manejarEnvio}>
      <div>
        <label htmlFor="nombre">Nombre:</label>
        <input
          id="nombre"
          name="nombre"
          type="text"
          value={formData.nombre}
          onChange={manejarCambio}
          required
        />
      </div>

      <div>
        <label htmlFor="email">Email:</label>
        <input
          id="email"
          name="email"
          type="email"
          value={formData.email}
          onChange={manejarCambio}
          required
        />
      </div>

      <div>
        <label htmlFor="edad">Edad:</label>
        <input
          id="edad"
          name="edad"
          type="number"
          value={formData.edad}
          onChange={manejarCambio}
          min="1"
          max="120"
        />
      </div>

      <div>
        <label htmlFor="comentario">Comentario:</label>
        <textarea
          id="comentario"
          name="comentario"
          value={formData.comentario}
          onChange={manejarCambio}
          rows={3}
        />
      </div>

      <div>
        <label htmlFor="pais">País:</label>
        <select
          id="pais"
          name="pais"
          value={formData.pais}
          onChange={manejarCambio}
        >
          <option value="">Selecciona un país</option>
          <option value="mexico">México</option>
          <option value="espana">España</option>
          <option value="argentina">Argentina</option>
        </select>
      </div>

      <div>
        <label>
          <input
            name="acepta"
            type="checkbox"
            checked={formData.acepta}
            onChange={manejarCambio}
            required
          />
          Acepto los términos y condiciones
        </label>
      </div>

      <div>
        <p>Género:</p>
        {['masculino', 'femenino', 'otro'].map(g => (
          <label key={g}>
            <input
              name="genero"
              type="radio"
              value={g}
              checked={formData.genero === g}
              onChange={manejarCambio}
            />
            {g.charAt(0).toUpperCase() + g.slice(1)}
          </label>
        ))}
      </div>

      <button type="submit">Enviar</button>
      <button type="button" onClick={() => setFormData({
        nombre: '', email: '', edad: '', comentario: '', 
        pais: '', acepta: false, genero: ''
      })}>
        Limpiar
      </button>
    </form>
  );
}
```

## Consejos Importantes

### 1. Manejo de Estado
- Siempre usa `useState` para manejar el estado de los elementos del formulario
- Para formularios complejos, considera usar `useReducer` o bibliotecas como Formik

### 2. Validación
```jsx
const validarEmail = (email) => {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
};

const validarFormulario = (datos) => {
  const errores = {};
  
  if (!datos.nombre.trim()) {
    errores.nombre = 'El nombre es requerido';
  }
  
  if (!validarEmail(datos.email)) {
    errores.email = 'Email inválido';
  }
  
  return errores;
};
```

### 3. Accesibilidad
- Siempre usa `htmlFor` en los labels
- Usa `aria-label` cuando sea necesario
- Asegúrate de que los elementos sean navegables con teclado

### 4. Buenas Prácticas
- Usa nombres descriptivos para los estados
- Mantén los componentes pequeños y enfocados
- Separa la lógica de presentación
- Usa controlled components (componentes controlados)

## Ejemplo de Uso Completo

```jsx
import React, { useState } from 'react';

function App() {
  return (
    <div style={{ padding: '20px', maxWidth: '600px', margin: '0 auto' }}>
      <h1>Elementos Básicos de React</h1>
      <FormularioCompleto />
    </div>
  );
}

export default App;
```

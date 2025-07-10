# Comer-en-Camino
Web para encontrar restaurantes
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Encuentra tu Restaurante</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>🍽️ Encuentra tu Restaurante</h1>
    <p>Filtra según tus gustos y necesidades de viaje.</p>
  </header>

  <section id="filtros">
    <label>
      Distancia (km):
      <input type="number" id="distancia" placeholder="Ej: 5" />
    </label>
    <label>
      Tipo de comida:
      <select id="tipoComida">
        <option value="">Todos</option>
        <option value="italiana">Italiana</option>
        <option value="japonesa">Japonesa</option>
        <option value="mexicana">Mexicana</option>
        <option value="española">Española</option>
      </select>
    </label>
    <label>
      Precio:
      <select id="precio">
        <option value="">Todos</option>
        <option value="€">€</option>
        <option value="€€">€€</option>
        <option value="€€€">€€€</option>
      </select>
    </label>
    <label>
      Tipo de restaurante:
      <select id="tipoRestaurante">
        <option value="">Todos</option>
        <option value="menu">Menú</option>
        <option value="carta">A la carta</option>
        <option value="bocadillos">Bocadillos</option>
        <option value="raciones">Raciones</option>
        <option value="comida_rapida">Comida rápida</option>
        <option value="degustacion">Menú degustación</option>
      </select>
    </label>
    <button onclick="filtrarRestaurantes()">Filtrar</button>
  </section>

  <section id="resultados"></section>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  background: #f4f4f4;
  margin: 0;
  padding: 0;
}

header {
  background: #0077cc;
  color: white;
  text-align: center;
  padding: 2rem 1rem;
}

#filtros {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  padding: 1rem;
  background: white;
  justify-content: center;
}

#filtros label {
  display: flex;
  flex-direction: column;
  font-size: 0.9rem;
}

#resultados {
  padding: 1rem;
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

.tarjeta {
  background: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 1rem;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.tarjeta h3 {
  margin-top: 0;
  color: #0077cc;
}
const restaurantes = [
  {
    nombre: "La Trattoria",
    distancia: 3,
    tipoComida: "italiana",
    precio: "€€",
    tipoRestaurante: "carta",
  },
  {
    nombre: "Sushi Go",
    distancia: 2,
    tipoComida: "japonesa",
    precio: "€€€",
    tipoRestaurante: "degustacion",
  },
  {
    nombre: "Taco Fiesta",
    distancia: 5,
    tipoComida: "mexicana",
    precio: "€",
    tipoRestaurante: "comida_rapida",
  },
  {
    nombre: "Casa Pepe",
    distancia: 1,
    tipoComida: "española",
    precio: "€€",
    tipoRestaurante: "menu",
  },
  {
    nombre: "Pans & Company",
    distancia: 4,
    tipoComida: "española",
    precio: "€",
    tipoRestaurante: "bocadillos",
  }
];

function filtrarRestaurantes() {
  const distancia = parseFloat(document.getElementById("distancia").value);
  const tipoComida = document.getElementById("tipoComida").value;
  const precio = document.getElementById("precio").value;
  const tipoRestaurante = document.getElementById("tipoRestaurante").value;

  const filtrados = restaurantes.filter(r => {
    return (
      (!distancia || r.distancia <= distancia) &&
      (!tipoComida || r.tipoComida === tipoComida) &&
      (!precio || r.precio === precio) &&
      (!tipoRestaurante || r.tipoRestaurante === tipoRestaurante)
    );
  });

  mostrarResultados(filtrados);
}

function mostrarResultados(lista) {
  const contenedor = document.getElementById("resultados");
  contenedor.innerHTML = "";

  if (lista.length === 0) {
    contenedor.innerHTML = "<p>No se encontraron resultados.</p>";
    return;
  }

  lista.forEach(r => {
    const div = document.createElement("div");
    div.className = "tarjeta";
    div.innerHTML = `
      <h3>${r.nombre}</h3>
      <p>Distancia: ${r.distancia} km</p>
      <p>Tipo de comida: ${r.tipoComida}</p>
      <p>Precio: ${r.precio}</p>
      <p>Tipo: ${r.tipoRestaurante.replace("_", " ")}</p>
    `;
    contenedor.appendChild(div);
  });
}

// Mostrar todos al cargar
filtrarRestaurantes();

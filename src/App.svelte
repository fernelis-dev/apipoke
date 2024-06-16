<!-- App.svelte -->
<script>
  let pokemonName = "";
  let pokemonData = null;

  async function fetchPokemon() {
    const pokemonURL = `https://pokeapi.co/api/v2/pokemon/${pokemonName.toLowerCase()}`;

    try {
      const response = await fetch(pokemonURL);
      const data = await response.json();
      pokemonData = data;
    } catch (error) {
      console.error("Error:", error);
      alert("Ocurrió un error al obtener la información del Pokémon.");
    }
  }
</script>

<h1>POKEMON!</h1>

<div class="contenedor">
  <section class="nav">
    <input
      type="text"
      bind:value={pokemonName}
      placeholder="Buscar todos los Pokémones"
      class="search-input"
    />
    <button class="search-button" on:click={fetchPokemon}>Buscar</button>
  </section>

  {#if pokemonData}
    <section id="pokemon">
      <h2>Información del Pokémon</h2>
      <div class="pokemon-info">
        <div class="pokemon-image-container">
          <img
            src={pokemonData.sprites.front_default}
            alt="Imagen de Pokemon"
            class="pokemon-image"
          />
        </div>
        <div class="pokemon-details">
          <table>
            <tr>
              <td><strong>Nombre:</strong></td>
              <td>{pokemonData.name}</td>
            </tr>
            <tr>
              <td><strong>Tipo:</strong></td>
              <td>{pokemonData.types[0].type.name}</td>
            </tr>
            <tr>
              <td><strong>Habilidades:</strong></td>
              <td>{pokemonData.abilities[1].ability.name}</td>
            </tr>
          </table>
        </div>
      </div>
    </section>
  {:else}
    <div class="centrado">
      <p style="font-size: 60px;">BIENVENIDO A LA POKE API</p>
    </div>
  {/if}
</div>

<div id="resultado"></div>

<style>

  .contenedor {
    background-image: url("pokemon-3840x2160.jpg");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    height: 80vh;
  }
  .nav {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px;
    background-color: #f0f0f0;
    border-radius: 10px;
  }
  .centrado {
    background-color: #ffffff;
    text-align: center;
    font-size: 24px; /* Puedes ajustar este valor según lo necesites */
    margin-top: 300px;
  }

  .search-input {
    padding: 8px 12px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
    font-size: 16px;
  }

  .search-button {
    padding: 8px 16px;
    background-color: #eeff00;
    color: #000000;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }

  .search-button:hover {
    background-color: #eeff00;
  }

  #pokemon {
    text-align: center;
  }

  .pokemon-info {
    display: flex;
    justify-content: center;
  }

  .pokemon-image-container {
    margin-right: 20px;
  }

  .pokemon-details table {
    border-collapse: collapse;
    margin-top: 20px;
  }

  .pokemon-details td {
    padding: 8px 12px;
    border: 1px solid #ccc;
  }

  .pokemon-details td:first-child {
    font-weight: bold;
    background-color: #f0f0f0;
  }

  h1,
  h2 {
    font-size: 2em;
    color: #eff305;
    animation: cambioColor 1s infinite alternate;
    text-align: center;
  }

  section#pokemon {
    background-color: white;
    margin-top: 50px;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    border: 3px solid #eff305;
    border-radius: 5px;
    padding: 20px;
    max-width: 600px;
  }

  .megusta {
    background-color: #eff305;
  }

  div#resultado {
    text-align: center;
    height: 10px;
  }

  .pokemon-image {
    display: block;
    margin: 0 auto;
    max-width: 300px;
    height: 200px;
  }

  @keyframes cambioColor {
    0% {
      color: #ca10e2;
    }
    50% {
      color: #0cd9e7;
    }
    100% {
      color: #cc540f;
    }
  }
</style>

<template>
  <main>
    <div id="card-wrapper">
        <div id="card" v-for="pokemon in allpokemon">
          <div class="card-content">
              <div class="card-front">
                <div class="border">
                  <p>{{ pokemon.id }}.</p>
                  <p>{{ pokemon.name }}</p>
                </div>
                <img :src="pokemon.image" alt="pokemon" />
              </div>
              <div class="card-back">
                <p>{{ pokemon.description }}</p>
              </div>
            </div>
        </div>
      </div>
      
  </main>
</template>

<style>
html{
  scroll-behavior: smooth;
}

#card-wrapper {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  margin-top: 90px;
  margin-left: 8%;
  gap: 25px;
}

#card {
  perspective: 1000px;
  width: 110px;
  height: 140px;
  position: relative;
}

.card-content {
  width: 100%;
  height: 100%;
  position: absolute;
  text-align: center;
  transition: transform 1s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
}

#card:hover .card-content {
  transform: rotateY(180deg);
}

.card-front, .card-back {
  width: 100%;
  height: 100%;
  position: absolute;
  backface-visibility: hidden;
}

.card-back {
  transform: rotateY(180deg);
  font-size:x-small; /* Adjust this value as needed */
}

.border {
  border: 1px solid black;
}
</style>

<script>
export default {
  data() {
    return {
      allpokemon: [],
    };
  },
  created() {
  fetch('https://pokeapi.co/api/v2/pokemon?limit=151')
    .then(response => response.json())
    .then(data => {
      const promises = data.results.map((pokemon, index) => {
        return fetch(`https://pokeapi.co/api/v2/pokemon/${index + 1}`)
          .then(response => response.json())
          .then(details => {
            return fetch(details.species.url) // Fetch species data
              .then(response => response.json())
              .then(speciesData => {
                const descriptionObj = speciesData.flavor_text_entries.find(entry => entry.language.name === 'en'); // Find English description
                const description = descriptionObj ? descriptionObj.flavor_text : 'No description available'; // Extract description
                return {
                  id: details.id,
                  name: pokemon.name,
                  image: details.sprites.front_default,
                  description, // Add description to Pokemon data
                };
              });
          });
      });

      Promise.all(promises).then(allpokemon => {
        this.allpokemon = allpokemon;
      });
    });
}
};
</script>
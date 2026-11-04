# api-tree-client

Cliente REST funcional em que os endpoints formam uma árvore e são consultados com uma sintaxe parecida com a do Firebase. Cada ramo é "aguardável" (`then`), então basta chamar `.then()` ou usar `await`.

```js
import { ApiTree } from './ApiTree';

const api = ApiTree.root('https://pokeapi.co/api/v2', {
  headers: { accept: 'application/json' },
});

api.branch('pokemon/pikachu');                                    // cria os ramos pokemon e pokemon/pikachu
const caterpie = api.branch('pokemon/10', { name: 'caterpie' });  // ramo com nome próprio

api.tree.pokemon.then(console.log);          // GET /pokemon
api.tree.pokemon.pikachu.then(console.log);  // GET /pokemon/pikachu
caterpie.then(console.log);                  // GET /pokemon/10
```

As opções (headers etc.) do ramo raiz são herdadas pelos filhos. A busca usa `fetch` e devolve o JSON.

## Rodando o exemplo
```
npm install
npm run dev
```
Experimento de estudo: sem testes e sem tratamento de erros HTTP além da rejeição do `fetch`.

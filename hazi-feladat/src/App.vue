<template>
  <div class="container">
    <h1>Vue.js Elméleti és Gyakorlati Feladat</h1>

    <!-- NAVIGÁCIÓS MENÜ -->
    <nav class="navigation">
      <button 
        :class="{ active: aktualisOldal === 'methods' }" 
        @click="aktualisOldal = 'methods'"
      >
        1. Vue Methods Témakör
      </button>
      <button 
        :class="{ active: aktualisOldal === 'forms' }" 
        @click="aktualisOldal = 'forms'"
      >
        2. Vue Forms Témakör
      </button>
    </nav>

    <!-- VUE METHODS -->
    <div v-if="aktualisOldal === 'methods'" class="page-content">
      <div class="theory-card">
        <h2>Vue Methods — Elméleti Összefoglaló & Működés Leírása</h2>
        <p>A Vue.js keretrendszerben a <strong>metódusok (methods)</strong> olyan függvények, amelyek a komponens belső logikáját, számításait és a felhasználói események lekezelését végzik.</p>
        
        <h3>Főbb jellemzők és működési elv:</h3>
        <ul>
          <li><strong>Eseménykezelés:</strong> A metódusokat a HTML sablonban a <code>v-on:esemény</code> vagy röviden a <code>@esemény</code> direktívával kötjük össze az elemekkel (pl. <code>@click="fuggveny"</code>).</li>
          <li><strong>Reaktivitás kiváltása:</strong> Amikor egy metódus módosítja a Vue reaktív állapotát (változóit), a Vue automatikusan észleli a változást, és azonnal frissíti a böngészőben látható felületet.</li>
          <li><strong>Composition API szintaxis:</strong> A modern Vue 3-ban a metódusok egyszerű JavaScript függvényként kerülnek deklarálásra a <code>&lt;script setup&gt;</code> blokkban.</li>
        </ul>
      </div>

      <!-- PÉLDA KÓD-->
      <div class="code-card">
        <h3>Felhasznált Minta Kód</h3>
        <pre><code>// HTML
&lt;button @click="novelSzamlalo"&gt;Számláló Növelése&lt;/button&gt;
&lt;p&gt;Kattintások száma: &#123;&#123; szamlalo &#125;&#125;&lt;/p&gt;

// JavaScript
const szamlalo = ref(0);
const novelSzamlalo = () => &#123;
  szamlalo.value++;
&#125;;</code></pre>
      </div>

      <div class="practice-card">
        <h3>Gyakorlati Működés:</h3>
        <p>Kattints a gombra a fenti metódus futtatásához!</p>
        <div class="demo-box">
          <p class="counter-text">Kattintások száma: <strong>{{ szamlalo }}</strong></p>
          <button @click="novelSzamlalo" class="btn-action">Számláló Növelése (Metódus)</button>
        </div>
      </div>
    </div>

    <!--VUE FORMS -->
    <div v-if="aktualisOldal === 'forms'" class="page-content">
      <div class="theory-card">
        <h2>Vue Forms — Elméleti Összefoglaló & Működés Leírása</h2>
        <p>A Vue.js az űrlapok (beviteli mezők, jelölőnégyzetek, rádiógombok) kezelését egy rendkívül hatékony mechanizmussal végzi.</p>
        
        <h3>Főbb jellemzők és működési elv:</h3>
        <ul>
          <li><strong>Kétirányú adatköttetés (Two-Way Data Binding):</strong> A <code>v-model</code> direktíva szorosan összeláncolja a HTML input mezőt a JavaScript változóval. Ha a felhasználó gépel, a változó azonnal frissül. Ha a kód módosítja a változót, az input mező értéke is megváltozik.</li>
          <li><strong>Esemény elfojtás (.prevent):</strong> A <code>@submit.prevent</code> módosító megakadályozza, hogy a böngésző hagyományos módon újratöltse az oldalt küldéskor. Így az adatok feldolgozását teljesen JavaScript oldalon tarthatjuk.</li>
        </ul>
      </div>

      <!-- PÉLDA KÓD MEGJELENÍTÉSE -->
      <div class="code-card">
        <h3>Felhasznált Minta Kód:</h3>
        <pre><code>// HTML
&lt;form @submit.prevent="adatFeldolgozas"&gt;
  &lt;input type="text" v-model="urlap.nev"&gt;
  &lt;input type="email" v-model="urlap.email"&gt;
  &lt;button type="submit"&gt;Küldés&lt;/button&gt;
&lt;/form&gt;

// JavaScript
const urlap = reactive(&#123; nev: '', email: '' &#125;);
const adatFeldolgozas = () => &#123;
  // Itt dolgozzuk fel a beküldött v-model adatokat...
&#125;;</code></pre>
      </div>

      <div class="practice-card">
        <h3>Gyakorlati Működés:</h3>
        <p>Töltsd ki az űrlapot az élő kétirányú adatköttetés teszteléséhez!</p>
        <div class="demo-box">
          <form @submit.prevent="adatFeldolgozas">
            <div class="form-group">
              <label>Felhasználónév (v-model):</label>
              <input type="text" v-model="urlap.nev" placeholder="Írd be a neved...">
            </div>
            <div class="form-group">
              <label>E-mail cím (v-model):</label>
              <input type="email" v-model="urlap.email" placeholder="valaki@email.com">
            </div>
            <button type="submit" class="btn-action btn-green">Űrlap elküldése</button>
          </form>

          <div v-if="urlapElkuldve" class="result-box">
            <h4>Feldolgozott adatok az űrlapból:</h4>
            <p><strong>Név:</strong> {{ mentettAdat.nev }}</p>
            <p><strong>E-mail:</strong> {{ mentettAdat.email }}</p>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const aktualisOldal = ref('methods')

// --- METHODS LOGIKA ---
const szamlalo = ref(0)
const novelSzamlalo = () => {
  szamlalo.value++
}

// --- FORMS LOGIKA ---
const urlap = reactive({ nev: '', email: '' })
const mentettAdat = reactive({ nev: '', email: '' })
const urlapElkuldve = ref(false)

const adatFeldolgozas = () => {
  if (urlap.nev.trim() === '' || urlap.email.trim() === '') {
    alert('Kérlek töltsd ki a mezőket!')
    return
  }
  
  mentettAdat.nev = urlap.nev
  mentettAdat.email = urlap.email
  urlapElkuldve.value = true
  
  urlap.nev = ''
  urlap.email = ''
}
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 30px auto;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  padding: 0 20px;
  color: #2c3e50;
}

h1 { text-align: center; color: #42b983; margin-bottom: 5px; }
.subtitle { text-align: center; color: #7f8c8d; margin-bottom: 25px; }

.navigation { display: flex; gap: 10px; margin-bottom: 25px; justify-content: center; }
.navigation button {
  padding: 12px 24px;
  font-size: 1rem;
  font-weight: bold;
  border: 2px solid #42b983;
  background: transparent;
  color: #42b983;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  width: auto;
}
.navigation button.active, .navigation button:hover { background: #42b983; color: white; }

.theory-card { background: #f8fafc; border-left: 5px solid #35495e; padding: 20px; border-radius: 6px; margin-bottom: 20px; }
h2 { color: #35495e; margin-top: 0; font-size: 1.4rem; }
ul { padding-left: 20px; li { margin-bottom: 6px; } }

/* Forráskód blokk stílusa */
.code-card {
  background: #2c3e50;
  color: #ecf0f1;
  padding: 15px 20px;
  border-radius: 8px;
  margin-bottom: 20px;
}
.code-card h3 { margin-top: 0; color: #42b983; font-size: 1.1rem; }
pre { margin: 0; overflow-x: auto; font-family: 'Courier New', Courier, monospace; line-height: 1.4; }

.practice-card { background: #ffffff; border: 1px solid #e2e8f0; padding: 20px; border-radius: 12px; box-shadow: 0 4px 6px rgba(0,0,0,0.02); }
.practice-card h3 { margin-top: 0; color: #35495e; }

.demo-box { background: #f1f5f9; padding: 20px; border-radius: 8px; text-align: center; }
.counter-text { font-size: 1.2rem; margin-bottom: 15px; }

.form-group { text-align: left; margin-bottom: 15px; }
label { display: block; margin-bottom: 5px; font-weight: bold; }
input { width: 100%; padding: 10px; border: 1px solid #cbd5e1; border-radius: 6px; box-sizing: border-box; }

.btn-action {
  padding: 12px 20px; background: #35495e; color: white; border: none; border-radius: 6px;
  font-size: 1rem; font-weight: bold; cursor: pointer; width: 100%; max-width: 280px;
}
.btn-action:hover { background: #2c3e50; }
.btn-green { background: #42b983; max-width: 100%; }
.btn-green:hover { background: #38a173; }

.result-box { margin-top: 20px; background: #e8f5e9; border: 1px solid #c8e6c9; padding: 15px; border-radius: 6px; text-align: left; }
.result-box h4 { margin-top: 0; color: #2e7d32; }
</style>

<template>
  <div class="about">
    <h1>Zadání:</h1>
    <div>
      Úkolem je vytvořit single-page applikaci, kterou může uživatel použít jako
      svůj osobní slovník
    </div>
    <ul>
      <li>
        do aplikace se bude fetchovat min 10k dummy slov. Je možno využít tool
        <a href="https://designer.mocky.io/"> esigner.mocky.io</a>, vytvořit
        vlastní express.js server a nebo slova jednoduše nalejt do firebase
      </li>
      <li>
        slova se budou vykreslovat na jedné stránce bez stránkování (ujistěte
        se, že aplikace bude mít stále skvělou výkonost)
      </li>
      <li>
        umožnit uživateli přidat, editovat a mazat jednotlivá slova (není
        potřeba posílat API request)
      </li>
      <li>
        jednotlivá slova budou draggable, takže bude uživatel schopný měnit
        jejich pozice podle vůle (pozici ukládat do localStoreage, aby se i po
        refreshi zobrazovali slova stejně seřazené)
      </li>
    </ul>
    <div></div>
    <div><strong>Požadavky</strong></div>
    <ul>
      <li>
        není potřeba žádé skutečné API, stačí jen simulovat asynchronní načítání
      </li>
      <li>použijte Vue.js verze 2, nebo 3 podle vašeho uvážení</li>
      <li>
        aplikace by měla vypadat dobře, ale stylování není předmětem posouzení
      </li>
      <li>kód by měl proběhnout linterem bez chyb</li>
      <li>
        Unit a Cypress testy na místech, kde si myslíte, že je to potřebné,
        budou oceněny kladně
      </li>
    </ul>
    <div></div>
    <div><strong>Výsledek</strong></div>
    <ul>
      <li>
        výsledkem by měl být link na vlastní repositář, kde je možno kód projít
        a stáhnout
      </li>
      <li>
        projekt by měl jít pustit na jakémkoliv lokálním počítači (doporučuji
        node verze 16+)
      </li>
    </ul>
    <div></div>
    <div><strong>Nezapomeň přiložit</strong></div>
    <ul>
      <li>README jak postupovat pro spuštění projektu</li>
      <li>kolik času jste na úkolu strávil</li>
      <li>cokoliv dalšího, co považujete za důležité zmínit</li>
    </ul>
  </div>
</template>
<style scoped>
.about {
  margin: 0 auto;
  text-align: left;
  width: 800px;
}
</style>

<template>
  <button class="botao" :class="{double, triple, operation}"
   @click="$emit('onClick', label)">{{ label }}</button>
</template>

<script>
export default {
name: 'Botao',
props: {
    label: {},
    operation: {type: Boolean},
    double: {type: Boolean},
    triple: {type: Boolean}
}
}
</script>

<style>
:root {
    --bg-button: #f0f0f0;
    --border-button: solid 1px #888;
}
.botao {
    font-size: 1.4em;
    background-color: var(--bg-button);
    border: none;
    border-right: var(--border-button);
    border-bottom: var(--border-button);
    outline: none;
}
.botao:active {
    background-color: #ccc;
}
.botao.double {
    grid-column: span 2;
}
.botao.triple {
    grid-column: span 3;
}
.botao.operation {
    background-color: #fa8231;
    color: white;
}
.botao.operation:active {
    background-color: #fa8231cc;
}
</style>
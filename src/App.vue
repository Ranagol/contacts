<template>
  <div id="app">
    <app-hello-world></app-hello-world>
    <app-contact-list></app-contact-list>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import ContactList from './components/ContactList.vue';

export default {
  name: 'App',
  components: {
    'app-hello-world': HelloWorld,
    'app-contact-list': ContactList,
  }
}
</script>

<style>

</style>

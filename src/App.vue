<template>
  <Header/>
  <Main/>
  <Footer/>
</template>

<script>
  import './style/style.scss';

  import Header from './components/ym-header.vue';
  import Main from './components/ym-content.vue';
  import Footer from './components/ym-footer.vue';

  export default {
    name: 'App',
    components: {
      Header,
      Main,
      Footer
    }
  }
</script>

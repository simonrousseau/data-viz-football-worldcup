<template>
    <div class="contenu">
        <h3>Rapport d'étonnement:</h3>
        <iframe id="iframe" frameborder="0" border="0" cellspacing="0" src="https://docs.google.com/document/d/e/2PACX-1vT1RHuILaeG4Dny1ZYGWGwUF0gg9qJOL1Jm5SuZBmuszK11zXUpsTV5oc2ZWcWRWvH8GVPTI-FYqrR4/pub?embedded=true"></iframe>
    </div>
</template>

<script>

export default {
  name: "Intro",
  components: {

  },
  data: function() {
    return {
      
    };
  },
  props: []
}
</script>

<style>
.contenu{
    height: 80vh;
}
#iframe{
    border-style: none;
    margin: auto;
    width: 50%;
    height: 90%;
}
</style>
<template>
  <div class="lobby">
    <GameList/>
  </div>
</template>

<script>
// @ is an alias to /src
import GameList from '@/components/GameList'
export default {
  name: 'Lobby',
  components: {
    GameList
  }
}
</script>

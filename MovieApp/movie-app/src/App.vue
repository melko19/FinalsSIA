<template>
<div class="container">
      <header>
      <router-link to="/">
          <h1><span>Lezgoo</span>Movie</h1>
      </router-link>
    </header>
</div>
  <main>
    <router-view/>
  </main>
</template>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Cambria Math;

    &::selection{
      background: transparentize(#42B883, 0.5);
    }
  }

  body{
    background-color: #07393f;
  }

  a{
    text-decoration: none;
  }

  header{
    display: flex;
    align-items: center;
    justify-content:center;
    padding: 10px 16px;
    background-color: #07393f;

    h1{
      color: #fff;
      font-size: 28px;

      span{
        color: #42B883;
      }
    }
  }

</style>

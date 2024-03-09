<script>
export default {}

</script>

<template>
    <div>
        <header class="main-header">
            <nav class="main-nav" style="display: flex;">

                                <button class="nav-btn btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" class="nav-style">Home</nuxt-link></button>

                <button class="nav-btn btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" class="nav-style">Pages</nuxt-link></button>
                
                <button class="nav-btn btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" class="nav-style">About</nuxt-link></button>
                
                <button class="nav-btn btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" class="nav-style">Contact</nuxt-link></button>
                
                <div class="container-fluid">
    <form class="nav-btn d-flex">
      <input style="width: auto;" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
      <button style="color: black;" class="btn btn-outline-success" type="submit">Search</button>
    </form>
  </div>
</nav>
        </header>

<br/>
        <slot />
    </div>
    
</template>

<style>
html, body{
    margin: 0;
    padding: 0;
    font-family:'Arial,  sans-serif';
}
.nav-style{
    color: black; text-decoration: none; font-weight: 500; font-size: medium;
}
.nav-btn{
    margin-left: 1rem; margin-top: 10px;
}
.main-header{
    background-color: #d5fadb;
    padding:15px;
}
</style>
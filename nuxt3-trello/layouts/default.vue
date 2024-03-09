<script>
export default {}

</script>

<template>
    <div>
        <nav style="display: flex;">
            <button style="margin-left: 1rem; margin-top: 10px;" class="btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" style="color: black; text-decoration: none; font-weight: 600;">Home</nuxt-link></button>

                <button style="margin-left: 1rem; margin-top: 10px;" class="btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" style="color: black; text-decoration: none; font-weight: 600;">Pages</nuxt-link></button>
                
                <button style="margin-left: 1rem; margin-top: 10px;" class="btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" style="color: black; text-decoration: none; font-weight: 600;">About</nuxt-link></button>
                
                <button style="margin-left: 1rem; margin-top: 10px;" class="btn btn-outline-success btn-sm" type="button">
                <nuxt-link to="/" style="color: black; text-decoration: none; font-weight: 600;">Contact</nuxt-link></button>
                
                <div class="container-fluid">
    <form class="d-flex" style="margin-left: 1rem; margin-top: 10px;">
      <input style="width: auto;" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
      <button style="color: black;" class="btn btn-outline-success" type="submit">Search</button>
    </form>
  </div>
</nav>
                <hr/>

        <slot />
    </div>
    
</template>

<style></style>
<template>
  <div>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
      <div class="container-fluid">
        <NuxtLink class="navbar-brand" href="/">Telusur</NuxtLink>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <NuxtLink
                class="nav-link active"
                aria-current="page"
                to="/product"
                >Product</NuxtLink
              >
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" to="/productcategory"
                >Product Category</NuxtLink
              >
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" to="/tags">Tags</NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script></script>

<style></style>

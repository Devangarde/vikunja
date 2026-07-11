<script setup lang="ts">
// Served by the reverse proxy, not bundled - keep this a runtime string (:src)
// rather than a static src="..." attribute, or Vite's build will try to
// resolve it as a module import and fail since the file isn't in the repo.
const logoSrc = '/logo-bianco_2.png'
</script>

<template>
	<div class="logo">
		<img
			:src="logoSrc"
			alt="Vikunja"
			class="logo-img"
		>
	</div>
</template>

<style lang="scss" scoped>
/* Kept as a wrapper (not the img itself) so callers passing class="logo"
   (e.g. NoAuthWrapper.vue's height: 64px !important) size/center this
   container instead of forcing width and height directly onto the img,
   which stretched it out of its aspect ratio. */
.logo-img {
	inline-size: 168px;
	block-size: auto;
}
</style>

<script setup lang="ts">
// Served by the reverse proxy, not bundled - keep this a runtime string (:src)
// rather than a static src="..." attribute, or Vite's build will try to
// resolve it as a module import and fail since the file isn't in the repo.
const logoSrc = '/logo-bianco_2.png'
</script>

<template>
	<img
		:src="logoSrc"
		alt="Vikunja"
		class="logo-img"
	>
</template>

<style lang="scss" scoped>
.logo-img {
	/* Fixed width like the previous SVG wordmark (.logo svg { width: 168px }),
	   which took priority over the width/height attributes callers pass
	   through (Navigation.vue, NoAuthWrapper.vue) so the logo renders at a
	   consistent size everywhere instead of being stretched to fit them. */
	inline-size: 168px;
	block-size: auto;
}
</style>

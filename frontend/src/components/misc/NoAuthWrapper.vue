<template>
	<div class="no-auth-wrapper">
		<Logo
			class="logo"
			width="200"
			height="58"
		/>
		<div class="noauth-container">
			<section
				class="image"
				:class="{'has-message': motd !== ''}"
			>
				<Message v-if="motd !== ''">
					{{ motd }}
				</Message>
			</section>
			<section class="content">
				<div>
					<h2
						v-if="title"
						class="title"
					>
						{{ title }}
					</h2>
					<Message
						v-if="motd !== ''"
						class="is-hidden-tablet mb-4"
					>
						{{ motd }}
					</Message>
					<slot />
				</div>
				<Legal />
			</section>
		</div>
	</div>
</template>

<script lang="ts" setup>
import {computed} from 'vue'
import {useRoute} from 'vue-router'
import {useI18n} from 'vue-i18n'

import Logo from '@/components/home/Logo.vue'
import Message from '@/components/misc/Message.vue'
import Legal from '@/components/misc/Legal.vue'

import {useTitle} from '@/composables/useTitle'
import {useConfigStore} from '@/stores/config'

withDefaults(defineProps<{
	showApiConfig?: boolean
}>(), {
	showApiConfig: false,
})
const configStore = useConfigStore()
const motd = computed(() => configStore.motd)

const route = useRoute()
const {t} = useI18n({useScope: 'global'})
const title = computed(() => route.meta?.title ? t(route.meta.title as string) : '')
useTitle(() => title.value)

</script>

<style lang="scss" scoped>
.no-auth-wrapper {
	min-height: 100vh;
	display: flex;
	flex-direction: column;
	place-items: center;

	@media screen and (max-width: $fullhd) {
		padding-bottom: 15rem;
	}
}

.noauth-container {
	max-width: $desktop;
	width: 100%;
	min-height: 60vh;
	display: flex;
	background-color: var(--white);
	box-shadow: var(--shadow-md);
	overflow: hidden;

	@media screen and (min-width: $desktop) {
		border-radius: $radius;
	}
}

.image {
	width: 50%;
	padding: 1rem;
	display: flex;
	flex-direction: column;
	justify-content: flex-end;

	@media screen and (max-width: $tablet) {
		display: none;
	}

	@media screen and (min-width: $tablet) {
		background: url('@/assets/no-auth-image.jpg') no-repeat bottom/cover;
		position: relative;

		&.has-message {
			justify-content: space-between;
		}

		&::before {
			content: '';
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			background-color: rgba(0, 0, 0, .2);
		}

		> * {
			position: relative;
		}
	}
}

.content {
	display: flex;
	justify-content: space-between;
	flex-direction: column;
	padding: 2rem 2rem 1.5rem;

	@media screen and (max-width: $desktop) {
		width: 100%;
		max-width: 450px;
		margin-inline: auto;
	}

	@media screen and (min-width: $desktop) {
		width: 50%;
	}
}

.logo {
	max-width: 100%;
	display: flex;
	margin: 0;
	height: 64px !important;
	align-items: center;
}
</style>

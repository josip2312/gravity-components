<script lang="ts">
import { defineComponent, reactive, computed, PropType } from 'vue';

export default /*#__PURE__*/ defineComponent({
	name: 'NButton',

	props: {
		primary: {
			type: Boolean as PropType<boolean>,
			default: () => false,
		},
		ghost: {
			type: Boolean as PropType<boolean>,
			default: () => false,
		},
		variant: {
			type: String as PropType<string>,
			validator: (value: string) => {
				return ['negative', 'positive', 'neutral', ''].indexOf(value) !== -1;
			},
			default: () => '',
		},
		size: {
			type: String as PropType<string>,
			validator: (value: string) => {
				return ['sm', 'md', 'lg'].indexOf(value) !== -1;
			},
			default: () => 'md',
		},
		disabled: {
			type: Boolean as PropType<boolean>,
			default: () => false,
		},
	},

	emits: ['click'],

	setup(props, { emit }) {
		const { primary, ghost, variant, size, disabled } = reactive(props);

		const classes = computed(() => ({
			'btn-ghost': ghost,
			'btn-primary': primary,
			[`btn-${variant}`]: variant,
			disabled: disabled,
			[`btn-${size}`]: true,
		}));

		const onClick = () => emit('click');

		return {
			classes,
			disabled,
			onClick,
		};
	},
});
</script>

<template>
	<button class="btn" :class="classes" :disabled="disabled" @click="onClick">
		<slot />
	</button>
</template>

<style lang="scss" scoped>
@import "../styles/abstracts/_index";

.btn {
	position: relative;
	min-width: 10rem;
	color: var(--font-primary-1-dark);
	font-size: var(--fs-300);
	padding: var(--btn-padding);
	background: var(--bg-button);
	border-radius: var(--br-sm);

	@include statesOverlay;

	&.btn-ghost {
		color: var(--font-primary-1);
		background: transparent;
	}

	&.btn-primary {
		background: var(--brand);
	}

	&.btn-positive {
		background: var(--positive);
	}

	&.btn-negative {
		background: var(--negative);
	}

	&.btn-neutral {
		background: var(--neutral);
		color: var(--font-secondary-1-dark);
	}

	&.btn-lg {
		font-size: var(--fs-500);
	}

	&.btn-sm {
		font-size: var(--fs-200);
	}

	&.disabled {
		opacity: 0.3;
		pointer-events: none;
	}
}
</style>

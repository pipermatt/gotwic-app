<script lang="ts">
	import type { Snippet } from 'svelte';
	import { browser } from '$app/environment';

	interface Props {
		storageKey: string;
		header: Snippet;
		children: Snippet;
		defaultCollapsed?: boolean;
	}

	let { storageKey, header, children, defaultCollapsed = false }: Props = $props();

	const STORAGE_PREFIX = 'gotwic-collapsed:';

	let collapsed = $state(getInitialState());

	function getInitialState(): boolean {
		if (!browser) return defaultCollapsed;
		const stored = localStorage.getItem(STORAGE_PREFIX + storageKey);
		if (stored !== null) return stored === 'true';
		return defaultCollapsed;
	}

	function toggle() {
		collapsed = !collapsed;
		if (browser) {
			localStorage.setItem(STORAGE_PREFIX + storageKey, String(collapsed));
		}
	}
</script>

<div class="panel overflow-hidden">
	<button
		class="panel-header flex w-full cursor-pointer items-center px-4 py-2.5"
		onclick={toggle}
		aria-expanded={!collapsed}
	>
		<div class="relative z-10 flex items-center gap-2">
			{@render header()}
			<svg
				class="h-3.5 w-3.5 text-(--color-gold)/60 transition-transform duration-200"
				class:rotate-180={!collapsed}
				fill="none"
				stroke="currentColor"
				viewBox="0 0 24 24"
			>
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
			</svg>
		</div>
	</button>
	{#if !collapsed}
		<div class="divide-y divide-(--color-gold)/10">
			{@render children()}
		</div>
	{/if}
</div>

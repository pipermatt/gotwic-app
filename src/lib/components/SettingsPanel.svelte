<script lang="ts">
	import { friendshipStore } from '$lib/stores/friendship.svelte';
	import CollapsiblePanel from './CollapsiblePanel.svelte';
</script>

<CollapsiblePanel storageKey="settings">
	{#snippet header()}
		<h3 class="font-display font-bold tracking-wide text-(--color-gold)">Settings</h3>
	{/snippet}
	<label class="table-row-hover flex cursor-pointer items-center gap-3 px-4 py-3">
		<input
			type="checkbox"
			checked={friendshipStore.profileSettings.hideUnlocked}
			onchange={(e) =>
				friendshipStore.updateSetting('hideUnlocked', (e.target as HTMLInputElement).checked)}
			class="checkbox-gold"
		/>
		<span class="text-(--color-parchment)">Hide Locked Commanders</span>
	</label>
	<label class="table-row-hover flex cursor-pointer items-center gap-3 px-4 py-3">
		<input
			type="checkbox"
			checked={friendshipStore.profileSettings.hideCompleted}
			onchange={(e) =>
				friendshipStore.updateSetting('hideCompleted', (e.target as HTMLInputElement).checked)}
			class="checkbox-gold"
		/>
		<span class="text-(--color-parchment)">Hide Completed Commanders</span>
	</label>
	<label class="table-row-hover flex cursor-pointer items-center gap-3 px-4 py-3">
		<input
			type="checkbox"
			checked={friendshipStore.profileSettings.suggestUpgrades}
			onchange={(e) =>
				friendshipStore.updateSetting('suggestUpgrades', (e.target as HTMLInputElement).checked)}
			class="checkbox-gold"
		/>
		<span class="text-(--color-parchment)">Suggest Quality Upgrades</span>
	</label>
	<label class="table-row-hover flex cursor-pointer items-center gap-3 px-4 py-3">
		<input
			type="checkbox"
			checked={friendshipStore.profileSettings.suggestUnlocks}
			onchange={(e) =>
				friendshipStore.updateSetting('suggestUnlocks', (e.target as HTMLInputElement).checked)}
			class="checkbox-gold"
		/>
		<span class="text-(--color-parchment)">Suggest Commander Unlocks</span>
	</label>
</CollapsiblePanel>

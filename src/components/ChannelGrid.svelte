<script>
	import ChannelItem from './ChannelItem.svelte'

	export let channels = []
</script>

<div class="flex flex-col">
	<div class="overflow-x-auto">
		<div class="inline-block min-w-full align-middle">
			<div class="overflow-hidden">
				<table
					class="min-w-full divide-y divide-gray-200 dark:divide-gray-700 table-fixed md:w-[62rem]"
				>
					<thead class="bg-gray-50 dark:bg-gray-700">
						<tr>
							<th scope="col" class="min-w-[10rem] md:w-[13rem] relative"></th>
							<th scope="col" class="relative min-w-[13rem]">
								<span class="sr-only">Actions</span>
							</th>
						</tr>
					</thead>
					<tbody class="bg-white dark:bg-gray-800">
						{#each channels as channel}
						{#if channel._streams.length > 0}
						<ChannelItem bind:channel="{channel}" />
						{/if}
						{/each}
					</tbody>
				</table>
			</div>
		</div>
	</div>
</div>

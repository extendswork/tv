<script>
	import { getContext } from 'svelte'
	import StreamsPopup from './StreamsPopup.svelte'
	import GuidesPopup from './GuidesPopup.svelte'
	import ChannelPopup from './ChannelPopup.svelte'

	export let channel

	const guides = channel._guides
	const streams = channel._streams

	const { open } = getContext('simple-modal')
	const showGuides = () =>
		open(
			GuidesPopup,
			{ guides, title: channel.name },
			{ transitionBgProps: { duration: 0 }, transitionWindowProps: { duration: 0 } }
		)
	const showStreams = () =>
		open(
			StreamsPopup,
			{ streams, title: channel.name },
			{ transitionBgProps: { duration: 0 }, transitionWindowProps: { duration: 0 } }
		)
	const showChannelData = () => {
		open(
			ChannelPopup,
			{ channel },
			{ transitionBgProps: { duration: 0 }, transitionWindowProps: { duration: 0 } }
		)
	}
</script>

<tr
	class="border-b last:border-b-0 border-gray-200 dark:border-gray-700 hover:bg-gray-50 hover:dark:bg-gray-700 h-16"
>
	<td class="pl-2 pr-4 md:pr-7">
		<div class="flex items-center" on:click="{showStreams}">
			<div class="flex-shrink-0">
				<img
					class="h-8 w-8 rounded-full"
					src="{channel.logo}"
					alt="{channel.name}"
				/>
			</div>
			<div class="ml-3 text-gray-500 dark:text-gray-100">
					{channel.name}
			</div>
		</div>
	</td>
	<td class="pl-2 pr-5">
		<div class="text-right flex justify-end space-x-3 items-center">
			{#if streams.length}
			<button
				on:click="{showStreams}"
				class="text-sm text-gray-500 dark:text-gray-100 inline-flex space-x-1 flex items-center hover:text-blue-500 dark:hover:text-blue-400"
			>
				<svg
					class="w-5 h-5"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M5.636 18.364a9 9 0 010-12.728m12.728 0a9 9 0 010 12.728m-9.9-2.829a5 5 0 010-7.07m7.072 0a5 5 0 010 7.07M13 12a1 1 0 11-2 0 1 1 0 012 0z"
					></path>
				</svg>
				<div class="font-semibold">{streams.length}</div>
				<div>streams</div>
			</button>
			{/if}
		</div>
	</td>
</tr>

<script lang="ts">
	import { Switch } from '$lib/components/ui/switch';
	import { Button } from '$lib/components/ui/button';
	import { Card } from '$lib/components/ui/card';
	import { Check } from 'lucide-svelte';
	import background from '$lib/assets/bg-pattern.svg';
	import rounds from '$lib/assets/pattern-circles.svg';

	let pageviews = 100;
	let isYearly = false;
	let price = 16;

	$: displayPrice = isYearly ? (price * 0.75).toFixed(2) : price.toFixed(2);
	$: pageviewsDisplay = pageviews + 'K PAGEVIEWS';

	function updatePrice(value: number) {
		pageviews = value;
		price = value / 6.25;
	}
</script>

<main class="relative flex min-h-screen w-full flex-col items-center justify-center bg-[#F9FAFE]">
	<div class="z-20 flex flex-col items-center justify-center p-4 py-16 md:py-0">
		<div class="relative mb-10 flex flex-col items-center justify-center text-center lg:mb-20">
			<h1 class="z-20 mb-2 text-2xl font-extrabold text-[#293356] md:text-4xl">
				Simple, traffic-based pricing
			</h1>
			<p class="text-[#848693]">Sign-up for our 30-day trial. No credit card required.</p>
			<img
				src={rounds}
				alt=""
				class="lg:-top-auto absolute -top-8 left-1/2 z-10 w-32 -translate-x-1/2 bg-no-repeat lg:h-[146px] lg:w-[146px]"
			/>
		</div>

		<Card class="w-full max-w-[540px] rounded-lg bg-white p-6 shadow-lg md:p-10">
			<div class="mb-8 flex flex-col md:flex-row md:items-center md:justify-between">
				<p
					class="text-center text-sm font-bold uppercase tracking-wider text-[#848693] md:text-left"
				>
					{pageviewsDisplay}
				</p>
				<div class="mt-4 flex items-center justify-center gap-2 md:mt-0 md:justify-end">
					<span class="text-4xl font-extrabold text-[#293356]">${displayPrice}</span>
					<span class="text-[#848693]">/ month</span>
				</div>
			</div>

			<div class="mb-8">
				<input
					type="range"
					min="0"
					max="200"
					step="50"
					bind:value={pageviews}
					on:input={(e) => updatePrice(Number(e.currentTarget.value))}
					class="h-2 w-full cursor-pointer appearance-none rounded-full bg-[#ECF0FB]"
				/>
			</div>

			<div class="mb-8 flex items-center justify-center gap-4">
				<span class="text-[#848693]">Monthly Billing</span>
				<Switch
					checked={isYearly}
					onCheckedChange={(checked) => (isYearly = checked)}
					class="focus:border-none data-[state=checked]:bg-[#10D5C2]"
				/>
				<div class="flex items-center gap-2">
					<span class="text-[#848693]">Yearly Billing</span>
					<span class="rounded-full bg-[#FEECE7] px-2 py-1 text-xs font-bold text-[#FF8C66]">
						-25%
					</span>
				</div>
			</div>

			<div class="border-t border-[#ECF0FB] pt-8">
				<div class="flex flex-col gap-8 md:flex-row md:items-center md:justify-between">
					<ul class="space-y-3">
						<li class="flex items-center gap-4">
							<Check class="h-4 w-4 text-[#10D5C2]" />
							<span class="text-[#848693]">Unlimited websites</span>
						</li>
						<li class="flex items-center gap-4">
							<Check class="h-4 w-4 text-[#10D5C2]" />
							<span class="text-[#848693]">100% data ownership</span>
						</li>
						<li class="flex items-center gap-4">
							<Check class="h-4 w-4 text-[#10D5C2]" />
							<span class="text-[#848693]">Email reports</span>
						</li>
					</ul>

					<Button class="rounded-full bg-[#293356] px-12 py-3 text-white hover:bg-[#293356]/90">
						Start my trial
					</Button>
				</div>
			</div>
		</Card>
	</div>
</main>
<img
	src={background}
	alt=""
	class="fixed left-0 top-0 z-10 h-96 w-full object-fill md:h-[50vh] lg:h-[60vh]"
/>

<style>
	input[type='range'] {
		-webkit-appearance: none;
		appearance: none;
		background: transparent;
		cursor: pointer;
	}

	input[type='range']::-webkit-slider-runnable-track {
		background: #ecf0fb;
		height: 8px;
		border-radius: 4px;
	}

	input[type='range']::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		margin-top: -16px;
		background-color: #10d5c2;
		height: 40px;
		width: 40px;
		border-radius: 50%;
		box-shadow: 0 10px 25px rgba(0, 255, 231, 0.6);
		cursor: pointer;
	}

	input[type='range']::-webkit-slider-thumb:hover {
		background-color: #7aeadf;
	}

	input[type='range']::-moz-range-track {
		background: #ecf0fb;
		height: 8px;
		border-radius: 4px;
	}

	input[type='range']::-moz-range-thumb {
		border: none;
		background-color: #10d5c2;
		height: 40px;
		width: 40px;
		border-radius: 50%;
		box-shadow: 0 15px 30px rgba(0, 255, 231, 0.6);
		cursor: pointer;
	}

	input[type='range']::-moz-range-thumb:hover {
		background-color: #7aeadf;
	}
</style>

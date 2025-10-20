<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import { Navbar, NavBrand, NavUl, NavLi, NavHamburger, Search, ToolbarButton, Button } from "flowbite-svelte";
	import { SearchOutline } from "flowbite-svelte-icons";
	import { page } from '$app/state';

	let { children } = $props();
	let activeUrl = $derived(page.url.pathname);
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<Navbar color="none">
	{#snippet children({ hidden, toggle })}
		<NavBrand href="/">
			H2 Technologies Store
		</NavBrand>
		
		<NavUl {activeUrl}>
			<NavLi href="https://h2technologiesllc.com/about">About</NavLi>
			<NavLi href="/contact">Contact</NavLi>
		</NavUl>

		<div class="flex md:order-2">
			<ToolbarButton class="block md:hidden" onclick={toggle}>
				<SearchOutline class="h5 w-5 text-gray-500 dark:text-gray-400" />
			</ToolbarButton>
			<div class="hidden md:block">
				<Search size="md" class="ms-auto" placeholder="Search products..." />
			</div>
			<NavHamburger />
		</div>
		{#if !hidden}
			<Search placeholder="Search products..." />
		{/if}

		<Button size="md" href="/login">Login</Button>
		
	{/snippet}
</Navbar>


{@render children?.()}

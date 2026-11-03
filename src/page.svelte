<script lang="ts">
    import { Link } from '@inertiajs/svelte';
    import { themeStyle } from '@lavertia/ui';
    import '@lavertia/ui/theme.css';
    import LavertiaRenderer from './renderer.svelte';
    import type { LavertiaPayload } from '@lavertia/ui';

    let { lavertia }: { lavertia: LavertiaPayload } = $props();
    let navigation = $derived(lavertia.navigation ?? []);
</script>

<svelte:head>
    <title>{lavertia.title ?? 'Lavertia'}</title>
</svelte:head>

<main lang={lavertia.locale ?? 'en'} dir={lavertia.direction ?? 'ltr'} style={themeStyle(lavertia.theme)} class="lvt-root min-h-[calc(100vh-8rem)] bg-gray-50/70 px-4 py-6 sm:px-6 lg:px-8 dark:bg-gray-950/40">
    <div class="mx-auto flex w-full max-w-[1440px] flex-col gap-6 lg:flex-row">
        {#if lavertia.version === 1 && navigation.length > 0}
            <aside class="w-full shrink-0 lg:w-60">
                <nav aria-label="Panel navigation" class="rounded-xl border border-gray-200 bg-white p-3 shadow-sm dark:border-white/10 dark:bg-gray-900/70">
                    <ul class="space-y-1">
                        {#each navigation as item, index (item.slug)}
                            <li>
                                {#if item.group && (index === 0 || navigation[index - 1]?.group !== item.group)}
                                    <p class="px-3 pb-1 pt-3 text-xs font-semibold uppercase tracking-wide text-gray-500 dark:text-gray-400">{item.group}</p>
                                {/if}
                                <Link href={item.url}
                                    aria-current={item.active ? 'page' : undefined}
                                    class={`block rounded-lg px-3 py-2 text-sm font-medium focus-visible:outline-2 focus-visible:outline-offset-2 lvt-focus ${item.active
                                        ? 'lvt-nav-active'
                                        : 'text-gray-700 hover:bg-gray-100 dark:text-gray-200 dark:hover:bg-gray-800'}`}>
                                    {item.label}
                                </Link>
                            </li>
                        {/each}
                    </ul>
                </nav>
            </aside>
        {/if}
        <div class="min-w-0 flex-1">
            {#if lavertia.version === 1}
                <LavertiaRenderer node={lavertia.tree} />
            {:else}
                <p role="alert" class="text-sm text-rose-700">Unsupported Lavertia protocol version.</p>
            {/if}
        </div>
    </div>
</main>

<script lang="ts">
  import { describeDiagram } from '$/util/diagramTypes';
  import { validatedState } from '$/util/state.svelte';
  import * as Tooltip from '$lib/components/ui/tooltip';
  import type { ComponentProps, Snippet } from 'svelte';
  import ExternalLinkIcon from '~icons/material-symbols/open-in-new-rounded';

  let {
    children,
    domain,
    shouldCheckDiagramType = true,
    side = 'bottom',
    labelPrefix = '打开图表的服务：',
    isVisible = true,
    sharesData = true,
    showPopup = true
  }: {
    children: Snippet;
    domain: string;
    shouldCheckDiagramType?: boolean;
    side?: ComponentProps<typeof Tooltip.Content>['side'];
    labelPrefix?: string;
    isVisible?: boolean;
    sharesData?: boolean;
    showPopup?: boolean;
  } = $props();

  let shouldDisableComponent = $derived(
    shouldCheckDiagramType &&
      describeDiagram(validatedState.current.diagramType)?.externalServices === false
  );
</script>

{#if isVisible}
  <Tooltip.Provider>
    <Tooltip.Root delayDuration={100}>
      <Tooltip.Trigger>
        <div class={[shouldDisableComponent && 'pointer-events-none cursor-not-allowed grayscale']}>
          {@render children()}
        </div>
      </Tooltip.Trigger>
      {#if showPopup}
        <Tooltip.Content {side} class="bg-secondary shadow-xl">
          <div
            class="flex cursor-help items-center gap-2"
            title={sharesData ? '图表将发送至外部服务' : '图表不会被分享'}>
            {#if shouldDisableComponent}
              <div class="text-muted-foreground">
                {domain} 不支持此图表类型
              </div>
            {:else}
              <ExternalLinkIcon />
              <span class="flex items-center gap-1">
                {labelPrefix}
                <div class="text-accent">{domain}</div>
              </span>
            {/if}
          </div>
        </Tooltip.Content>
      {/if}
    </Tooltip.Root>
  </Tooltip.Provider>
{/if}

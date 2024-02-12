<script lang="ts">
    import { browser } from "$app/environment";
    import mermaid from "mermaid";
    import { onMount } from "svelte";

    // The default diagram
    let diagram = `\
    flowchart LR
sensor1 --> Moxa1 --> firewall --> lims
sensor2 --> Moxa2 --> firewall --> lims
sensor3 --> Ethernet-adapter --> firewall --> lims
`;

    let container: HTMLSpanElement;

    async function renderDiagram() {
        if (browser) {
            const { svg } = await mermaid.render("mermaid", diagram);
            container.innerHTML = svg;
        }
    }

    $: diagram && renderDiagram();

</script>

<main>
    <pre contenteditable="true" bind:innerHTML={diagram}></pre>

    <p>
        <textarea bind:value={diagram} cols="100" rows="20"/>
    </p>

    <span bind:this={container}> </span>
</main>

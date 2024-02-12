<script lang="ts">
    import { browser } from "$app/environment";
    import mermaid from "mermaid";
    import { onMount } from "svelte";

    // The default diagram
    let diagram = `\
erDiagram
    CUSTOMER }|..|{ DELIVERY-ADDRESS : has
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER ||--o{ INVOICE : "liable for"
    DELIVERY-ADDRESS ||--o{ ORDER : receives
    INVOICE ||--|{ ORDER : covers
    ORDER ||--|{ ORDER-ITEM : includes
    PRODUCT-CATEGORY ||--|{ PRODUCT : contains
    PRODUCT ||--o{ ORDER-ITEM : "ordered in"`;

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

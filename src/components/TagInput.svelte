<script lang="ts">
    import { onMount} from "svelte";

    type Item = {
        description: string;
        id: number;
        id_v2: string;
        is_nsfw: boolean;
        name: string;
        sub: string;
    };
    type TagItem = {
        tagName: string;
        tagId: number;
    };

    let tags: TagItem[] = [];
    export let onChange: (e: Event) => void;

    onMount(async function fetchTags() {
        const res = await fetch("https://api.nekosapi.com/v3/images/tags");
        const data = await res.json();

        const fetchedTags = data.items.map((item: Item) => {
            return { tagName: item.name, tagId: item.id };
        });

        tags = [...tags, ...fetchedTags];
    });
</script>

<select
    on:change={onChange}
    class="p-2 rounded-md border border-red-500 outline-none flex-1"
>
    {#each tags as tag}
        <option value={tag.tagId}>{tag.tagName}</option>
    {/each}
</select>

<script lang="ts">
    export let clickHandler: () => void;
</script>

<button
    class="bg-red-500 p-2 rounded-md text-white"
    on:click={clickHandler}
    type="button">Get Image</button
>

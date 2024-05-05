<script lang="ts">
    import Button from "./components/Button.svelte";
    import TagInput from "./components/TagInput.svelte";

    let imgUrl = "";
    let selectedTag: string;
    let isSFW = true;

    async function fetchImage() {
        const res = await fetch(
            `https://api.nekosapi.com/v3/images/random?limit=1${isSFW ? "&rating=safe" : ""}${selectedTag ? "&tag=" + selectedTag : ""}`
        );
        const data = await res.json();
        imgUrl = data.items[0].image_url;
    }

    function setTag(e: Event) {
        const target = e.target as HTMLSelectElement;
        selectedTag = target.value;
    }

    function setRating() {
        isSFW = !isSFW;
    }
</script>

<main class="flex items-center justify-center w-screen h-screen bg-red-100">
    <div>
        <div
            class="w-[500px] h-[600px] border border-red-400 mb-4 flex items-center justify-center overflow-hidden bg-white"
        >
            <a href={imgUrl} target="_blank">
                <img src={imgUrl} alt="" class="m-auto" /></a
            >
        </div>

        <div class="flex items-center max-w-sm gap-2 w-full">
            <TagInput onChange={setTag} />
            <Button clickHandler={fetchImage} />
        </div>
        <input
            on:change={setRating}
            type="checkbox"
            name="rating"
            id="rating"
            checked={isSFW}
        />
        <label for="rating">SFW</label>
    </div>
</main>

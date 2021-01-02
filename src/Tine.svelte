<script>
    export let note;
    let c4;
    let active = false;
</script>

<style>
    .tine {
        user-select: none;
        background: peachpuff;
        height: 100px;
        display: flex;
        align-items: end;
        padding: 10px;
        color: tomato;
        font-weight: bold;
        border-radius: 0 0 10px 10px;
    }
</style>

<div
    class="tine"
    on:mousedown={() => {
        active = true;
    }}
    on:touchstart={() => {
        active = true;
        c4.currentTime = 0;
        c4.play();
    }}
    on:mouseup={() => {
        active = false;
    }}
    on:touchend={() => {
        active = false;
    }}
    on:mouseleave={() => {
        if (active) {
            c4.currentTime = 0;
            c4.play();
        }
    }}
    on:touchleave={() => {
        if (active) {
            c4.currentTime = 0;
            c4.play();
        }
    }}>
    {note}
    <audio bind:this={c4} src="/C4.wav" />
</div>

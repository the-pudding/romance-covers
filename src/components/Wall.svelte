<script>
    import * as d3 from "d3";
    import { onMount } from "svelte";

    const shelves = [0, 1, 2, 3, 4]

    export let data;

    let w = data.length/6;

    // onMount(() => {
    //     console.log(w)
    // })
</script>

<!-- <section id="wall" style="transform: translateX(-{scrollY}px)"> -->
<section id="wall">
    <div class ="books">
        {#each data as book, i}
            <div class="book" id="book_{book.ISBN}">
                <img src ="/assets/images/img_{book.ISBN}.jpg" alt="a thumbnail book cover of {book.title}">
                <!-- <p>{book.year}</p> -->
            </div>
        {/each}
    </div>
    {#if w}
        <div class="shelves" style="width: {w*100}px">
            {#each shelves as shelf, i} 
                <div class="shelf">
                    <div class="shelf-front"></div>
                    <div class="shelf-top"></div>
                    <div class="shelf-shadow"></div>
                </div>
            {/each}
        </div>
    {/if}
</section>

<style>
    #wall {
        width: 100%;
        height: 50vh;
        margin: 15rem 0 0 0;
        padding: 0 5rem;
        float: left;
    }
    .shelves {
        width: 100%;
        height: 50vh;
        position: absolute;
        z-index: 1;
    }
    .shelf {
        height: calc(100vh / 8);
        display: flex;
        align-items: end;
        position: relative;
    }
    .shelf-front {
        background: #FBF7F7;
        width: 100%;
        height: 1rem;
        position: absolute;
        bottom: -1.5rem;
        z-index: 999;
    }
    .shelf-top {
        background: var(--color-white);
        /* background: purple; */
        width: 100%;
        height: 1rem;
        position: absolute;
        left: 0.25rem;
        bottom: -0.5rem;
        transform: skew(-30deg);
        stroke: 1px solid #FBF7F7;
        z-index: 999;
    }
    .shelf-shadow {
        background: #D9D9D9;
        /* background: green; */
        transform: skew(-60deg);
        width: 100%;
        bottom: -6.5rem;
        height: 5rem;
        position: absolute;
        left: -8.75rem;
        opacity: 0.75;
        filter: blur(3rem); 
        z-index: 1;
    }
    .books {
        height: 70vh;
        position: absolute;
        z-index: 1000;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
    }
    .book {
        width: 4rem;
        margin: 0 1rem;
        height: calc(100vh / 8);
        display: flex;
        align-items: end;
    }
    .book img {
        box-shadow: -0.25rem 0 1rem  #E4D3D1;
    }
</style>
<script>
    import { getContext, onMount } from "svelte";
    const copy = getContext("copy");

    let w;
    let open = false;
    export let scrollY;

    $: if (scrollY > 100) {
        open = true;
    } else { open = false; }

</script>

<svelte:window bind:innerWidth={w} />

<section id="intro" style="width:{w}px">
    <div id="book" class:open-book={open} style="width:{w/2.5}px;height:{w/1.6}px">
        <div class="main">
            <div class="book-font">
                <div class="book-cover">
                </div>
                <div class="book-cover-back"></div>
            </div>
            <div class="book-page">
                <div id="page-1" class="page">
                    {#each copy.intro as text, i}
                        <p>{@html text.value}</p>
                    {/each}
                </div>
                <div class="page-number">- 1 -</div>
            </div>
            <div class="book-back">
            </div>
            <div class="book-bone">
                <h2>What Does A Happily Ever After Look Like?</h2>
            </div>
            <div class="book-top"></div>
            <div class="book-right"></div>
            <div class="book-bottom"></div>
        </div>
    </div>
</section>

<style>
    #intro {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        display: flex;
        flex-direction: row;
        justify-content: center;
        margin: 5rem 0 0 0;
    }
	#book {
		margin: 0 auto;
		position: relative;
		transition-duration: .5s;
		perspective: 2000px;
	}
	.main {
		width: 100%;
        height: 100%;
		color: var(--color-off-black);
		position: relative;
		transform-style: preserve-3d;
		transition-duration: .5s;
	}

/* = Book Font
-------------------------------------------------------------- */
	.book-font{
		width: 100%;
        height: 100%;
		position:absolute; top:0; bottom:0;
		font-size:15px; text-align:center;
		text-shadow:0 2px 0 rgba(30,35,45,1);
		box-shadow:inset 3px 0 10px rgba(0,0,0,0.1); /* 给书本添加光照阴影 */
		z-index:10;
		transform-style:preserve-3d;
		transform-origin:0% 50%;
		transition-duration:.5s;
		transform:translate3d(0,0,25px);
	}
	.book-cover{
		width: 100%;
        height: 100%;
		overflow:hidden;
		position:absolute; top:0; bottom:0;
		background: url("assets/images/Alice_sketch_3.jpg");
        background-size: cover;
        background-repeat: no-repeat;
		transform-style:preserve-3d;
		backface-visibility:hidden;
	}
	.book-cover-back{
		width: 100%;
        height: 100%;
		position:absolute; top:0; bottom:0;
		background:#4C7DFE;
		transform-style:preserve-3d;
		backface-visibility:hidden;
		transform:rotate3d(0,1,0,-180deg);
	}

/* = Book Page
-------------------------------------------------------------- */
	.book-page{
		width: calc(100% - 1rem);
        height: calc(100% - 1rem);
		line-height:20px;
		position:absolute; top:5px;
		z-index:9;
		box-shadow:inset 3px 0 10px rgba(0,0,0,0.1);
		transform-style:preserve-3d;
        transition-duration:.5s;
		transform-style:preserve-3d;
		transform:translate3d(0,0,24px);
	}
	.page{
        height: 100%;
		padding: 3rem 2rem;
		overflow:hidden;
	}
	.book-page h3{
		font-size:14px;
		text-align:center;
		margin-bottom:14px;
	}
	.book-page p{
		font-size:13px;
		margin-bottom:14px;
	}
	.page-number{
		width:100%;
		font-size:13px;
		text-align:center;
		position:absolute;
		bottom:10px;
	}

/* = Book Back
-------------------------------------------------------------- */
    .book-back{
		width: 396px;
		background:#4C7DFE;
		position:absolute; 
        top:0; 
        bottom:0;
		transform:rotate3d(0,1,0,-180deg) translate3d(0,0,25px);
		z-index:8;
	}

/* = Book Bone
-------------------------------------------------------------- */
	.book-bone{
		width:50px;
		background:#4C7DFE;
		box-shadow:1px 0 0 #4C7DFE,-1px 0 0 #4C7DFE; /* 旋转的时候 拼接处隐隐约约会有个缝隙 所以加上个阴影来填补它 */
		position:absolute;
		top:0; bottom:0; left:-25px;
		transform:rotate3d(0,1,0,-90deg);
	}
	.book-bone h2{
		width:530px;
		height:50px; line-height:50px; /* 对应关系-1 */
		font-size:14px; text-align:right;
		padding:0 15px;
		transform-origin:0 0;
		transform:rotate(90deg) translateY(-50px);
	}
	.book-bone span{ font-size:14px; padding-right:20px;}

/* = Order
-------------------------------------------------------------- */
	.book-cover:after,.book-back:after{ /*  */
		content:"";
		width:3px;
		position:absolute; top:0; left:10px; bottom:0;
		background:rgba(0,0,0,0.06);
		box-shadow:1px 0 3px rgba(255, 255, 255, 0.1);
	}
	.book-page,.book-top,.book-right,.book-bottom{
		background:var(--color-white);
	}
	.book-right{
		width:50px; height:550px;
		position:absolute; top:5px; right:-20px;
		box-shadow:0 1px 0 var(--color-white),0 -1px 0 var(--color-white);
		transform:rotate3d(0,1,0,90deg);
	}
	.book-top{
		width:415px; height:50px;
		position:absolute; top:-20px; left:0;
		transform:rotate3d(1,0,0,90deg);
	}
	.book-bottom{
		width:415px; height:50px;
		position:absolute; bottom:-20px; left:0;
		transform: rotate3d(1,0,0,-90deg) translate3d(0,0,0);
	}
	.book-right,.book-top,.book-bottom{
		backface-visibility:hidden;
	}

/* = Flip
-------------------------------------------------------------- */
	/* Open */
	.open-book{
		-webkit-transform:translate3d(50%,0,0);
		-moz-transform:translate3d(50%,0,0);
		-ms-transform:translate3d(50%,0,0);
		-o-transform:translate3d(50%,0,0);
		transform:translate3d(50%,0,0);
	}
	.open-book  .book-font{
		-webkit-transform:translate3d(0,0,25px) rotate3d(0,1,0,-160deg);
		-moz-transform:translate3d(0,0,25px) rotate3d(0,1,0,-160deg);
		-ms-transform:translate3d(0,0,25px) rotate3d(0,1,0,-160deg);
		-o-transform:translate3d(0,0,25px) rotate3d(0,1,0,-160deg);
		transform:translate3d(0,0,25px) rotate3d(0,1,0,-160deg);
	}
	/* .open-book:hover .main{
		-webkit-transform:rotate3d(1,1,0,15deg);
		-moz-transform:rotate3d(1,1,0,15deg);
		-ms-transform:rotate3d(1,1,0,15deg);
		-o-transform:rotate3d(1,1,0,15deg);
		transform:rotate3d(1,1,0,15deg);
	} */
</style>
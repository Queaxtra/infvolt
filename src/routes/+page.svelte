<script>
    import toast, { Toaster } from 'svelte-french-toast';
    let userID = "01GHR0XWEA8ZNA2Z4CQ8A1VPM0"

    async function getUserDetails() {
        if (userID.length > 26) {
            toast.error('The user ID must be only 26 words long!', {
                position: "top-right",
                style: 'background-color: #131316; color: #fff;',
                icon: "⚠️"
            })
        } else {
            window.location.href = `/users/${userID}`
        }
    }
</script>

<Toaster />
<div class="relative top-60 text-center">
    <h2 class="text-5xl font-bold">Infvolt</h2>
    <p class="relative top-2 text-white/50">Fetch user information through <a href="https://rvlt.gg/bScHAYGx" class="underline text-[#ff0080]/50">Revol.chat</a></p>

    <div>
        <input bind:value={userID} class="text-xs md:text-sm lg:text-sm w-80 md:w-96 lg:w-96 h-10 px-5 relative top-10 rounded-full bg-transparent/20 text-white/60" type="text">
        <button on:click={getUserDetails} class="flex ml-auto mr-auto left-0 right-0 mt-16 rounded py-2 px-10 bg-transparent/30 hover:bg-transparent/40 transition-all duration-300 text-white/60">Fetch</button>
    </div>
</div>
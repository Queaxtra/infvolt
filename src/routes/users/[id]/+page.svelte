<script lang="ts">
    import { API } from "revolt-api";
    import { page } from '$app/stores';
    import { onMount } from "svelte";
    let id = $page.params.id;
    let data = {};
    let userid = id;
    let client = new API({
        authentication: {
            revolt: import.meta.env.VITE_APP_TOKEN,
        },
    });

    let userInfo = {
        username: "",
        discriminator: "",
        online: "",
    }

    onMount(async () => {
        let res = await client.get(`/users/${userid}`);
        data = res;

        userInfo.username = data.username;
        userInfo.discriminator = data.discriminator;
        userInfo.status = data.online;

        let resProfile = await client.get(`/users/${userid}/profile`);
        data = resProfile;

        document.getElementById("userContent")?.innerHTML = data.content.replace(/\n/g, "<br>");
        document.getElementById("userPhoto").src = `https://autumn.revolt.chat/avatars/${res.avatar._id}/${res.avatar.filename}`
        document.getElementById("userBanner").src = `https://autumn.revolt.chat/backgrounds/${data.background._id}?width=384&height=135`
    });
</script>

<div class="relative ml-5 md:ml-auto lg:ml-auto mr-auto left-0 right-0 w-96 h-[27rem] bg-transparent/30 rounded-md top-60 drop-shadow-md">
    <div>
        <img id="userBanner" class="rounded-md absolute" src="https://i.hizliresim.com/q5zvyba.png" alt="User Background" /> 
        <img id="userPhoto" class="rounded-full w-20 m-4 border-[7px] border-[#110b12] relative top-24" src="https://i.hizliresim.com/ixqwh1j.png" alt="User Avatar" />
    </div>

    <div>
        <h1 class="text-lg relative top-20 ml-5">{userInfo.username || "User"}<span class="text-sm text-white/50">#{userInfo.discriminator || "0000"}</span></h1>
        <p class="text-xs relative top-20 left-5 text-white/10">{id}</p>
        
        {#if userInfo.status === true}
        <p class="text-xs relative top-1 ml-[6.5rem] text-green-500/50"><i class="fa-solid fa-circle"></i> Online</p>
        {:else}
        <p class="text-xs relative top-1 ml-[6.5rem] text-gray-500/50"><i class="fa-solid fa-circle"></i> Offline</p>
        {/if}

        <div>
            <h2 class="text-lg relative top-24 ml-5">About</h2>
            <div class="w-auto h-36 bg-transparent/10 relative top-[6.5rem]">
                <p id="userContent" class="text-xs flex py-3 px-5">Not Found!</p>
            </div>
        </div>
    </div>
</div>
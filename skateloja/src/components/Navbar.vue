<template>
    <div>
        <div id="nav">
            <router-link to="/" id="logo-url">
                <img :src="logo" :alt="alt" id="logo">
            </router-link>
            <router-link to="/">Home</router-link> |
            <router-link to="/pedidos">Pedidos</router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: "Navbar",
    props: ["logo", "alt"]
}
</script>

<style scoped>
    #nav {
        background-color: #1c1c1c;
        border-bottom: 2px solid #000000;
        padding: 5px 10px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 100px;
        height: 70px;
    }

    #nav a {
        color: #FCBA03;
        text-decoration: none;
        margin: 5px;
        transition: .5s;
    }

    #nav a:hover {
        color: #FFF;
    }

</style>

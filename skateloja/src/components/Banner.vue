<template>
    <div id="main-banner">
        <h1>skateShop</h1>
    </div>
</template>

<script>
export default {

    name: "Banner"
    
}
</script>

<style scoped>

    #main-banner {
        background-image: url('/public/img/skate.jpg');
        background-position: 0 auto;
        background-size: cover;
        height: 220px;
        display: flex;
        align-items: center;
        justify-content: flex-start;
    }
    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 30px;
        padding: 0 0 40px 20px;

    }

    @media(min-width:770px) {
        #main-banner {
            background-position: 0 -250px;
            background-size: cover;
            background-position-y: center;
            height: 600px;
            display: flex;
            align-items: center;
            justify-content: flex-start;
        }
        #main-banner h2 {
            color:#fff;
            text-align: center;
            font-size: 60px;
            background-color: #222;
        }
    }

</style>

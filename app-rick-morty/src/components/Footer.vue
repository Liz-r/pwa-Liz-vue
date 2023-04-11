<template>
    <body>
        <div class="footer">
            <hr>
            <img class="liz" src="../assets/logo.png" alt="">
            <h3>App by Lizeth Ruiz Arreola</h3>
            <a href="https://github.com/">Github</a>
        </div>
    </body>
</template>
<script>

export default {
    name: 'app',
    components: {
    },
    data() {
        return {
        }
    },

}
</script>
 
 
<style >
body {
    background-color: #002128;
}

.liz {
    width: 50px;
}

.footer {
    color: aquamarine;
    font-weight: 100;
}

a {
    text-decoration: none;
    color: aquamarine;
}

a:hover {
    color: rgb(98, 199, 165);
    text-decoration: underline;
}
</style>
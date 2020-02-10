<template>
<div class="wrapper">
    <div class="titulo"><h5>{{header}}</h5></div>
    <div class="text">{{text}}</div>
</div>
</template>

<script>
export default {
    props:{
        header: Number,
        text: String
    }
}
</script>

<style>
.wrapper{
    display: flex;
    -webkit-box-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    align-items: center;
    flex-direction: column;
    background-color: rgb(36, 41, 46);
    text-align: center;
    padding: 1rem;
    border-radius: 0.25rem;
}
.text{
    color: rgb(180, 211, 221);
}

</style>
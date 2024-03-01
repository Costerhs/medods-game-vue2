<template>
    <div class="cubes-list">
        <button 
            v-for="btn of btns"
            v-bind:class="{[`cub${btn}Active`]: activeBtn === btn,[`cub${btn}`]: true}" 
            class="cub"
            :disabled="statusBtn"
            @click="$emit('activate-btn',btn)"
            :key="btn">
        </button>
    </div>
</template>

<script>
    export default {
        props:['btns','activeBtn','statusBtn'],
        methods: {

        }
    }
</script>

<style scoped>

.cubes-list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    /*  */
    width: 400px;
    height: 400px;
    margin-top: 20px;
}
.cub {
    width: 200px;
    height: 200px;
    cursor: pointer;
    border: 0;

}
.cub1{
    background: #FF5643;
    border-radius: 20px 0 0 0 ;
}
.cub1:hover {
    border-left: 1px solid black;
    border-top: 1px solid black;
}
.cub1Active{
    background: red;
    
}

.cub2{
    background: dodgerblue;
    border-radius: 0 20px 0 0 ;
}
.cub2:hover {
    border-right: 1px solid black;
    border-top: 1px solid black;
}
.cub2Active{
    background: blue;
    
}

.cub3{
    background: #BEDE15;
    border-radius: 0 0 0 20px ;
}
.cub3:hover {
    border-left: 1px solid black;
    border-bottom: 1px solid black;
}
.cub3Active{
    background: green;
    
}

.cub4{
    background: #FEEF33;
    border-radius: 0 0 20px 0 ;
}
.cub4:hover {
    border-right: 1px solid black;
    border-bottom: 1px solid black;
}
.cub4Active{
    background: yellow;
    
}
@media (max-width:500px) {
    .cubes-list {
        width: 300px;
        height: 300px;
    }
    .cub {
        width: 50%;
        height: 50%;
    }
}
</style>
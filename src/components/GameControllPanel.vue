<template>
    <div class="gameInfo">
        <h2 class="title">Раунд {{ sequence.length }}</h2>
        <button class="startBtn" @click="$emit('start-game')"  :disabled="!statusBtn">
            START
        </button>
        <h2 class="title">Выберите сложность</h2>
        <div class="levels" v-if="levels">
            <div v-for="el of Object.entries(levels)" :key="el[0]" >
                <input class="checkbox" :checked="activeLevel == el[1]" @change="$emit('toggle-checked',el[1])" type="checkbox" :id="el[0]"/>
                <label class="label" :for='el[0]'>{{ el[0] }}</label>
            </div> 
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                levels: {
                    easy:1.5,
                    normal:1,
                    hard:0.4
                }
            }
        },
        props:['sequence','activeLevel','activeBtn','statusBtn'],
    }
</script>

<style scoped>
.gameInfo {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
.title {
    font-size: 24px;
    font-family: Arial, Helvetica, sans-serif;
    color: #333333;
}
.levels {
    display: flex;
    gap: 10px;
    /* flex-direction: column; */
}

.checkbox {
    display: none;
}

.label {
    color: white;
    font-size: 20px;
    padding: 8px 10px;
    cursor: pointer;
    border-radius: 20px;
    background: #BEDE15;
}

.checkbox:checked + .label {
    background: green;
}

.startBtn {
    background: rgb(118, 226, 118);
    color: white;
    width: 200px;
    height: 50px;
    margin-top: 20px;
    border: 0;
    border-radius: 20px;
    cursor: pointer;
}
</style>
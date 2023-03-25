<template>
    <div class="opposite-block">
        <Player class="opposite" ref="oppositeplayer" v-on:click="oppositeClicked" />
    </div>

    <div class="middle-block">
        <div class="leftplayer-div">
            <Player class="leftplayer" ref="leftplayer" v-on:click="leftClicked" />
        </div>

        <div class="rightplayer-div">
            <Player class="rightplayer" ref="rightplayer" v-on:click="rightClicked" />
        </div>
    </div>

    <div class="mine-block">
        <Player class="mine" ref="mineplayer" v-on:click="mineClicked" />
    </div>
</template>
  
<script>
import Player from './Player.vue';

export default {
    name: 'MaJiang',
    components: {
        Player
    },
    props: {
        msg: String
    },
    data() {
        return {
            names: ["wan", "tong", "tiao"]
        }
    },
    methods: {
        oppositeClicked: function () {

            console.log("oppositeClicked")
            var value = this.transorm(this.$refs.oppositeplayer.getTypeInfo())
            this.$refs.oppositeplayer.setTypeInfo(value)
            const that = this;
            setTimeout(function () {
                that.resetbackground()
            }, 200)
        },

        leftClicked: function () {
            var value = this.transorm(this.$refs.leftplayer.getTypeInfo())
            this.$refs.leftplayer.setTypeInfo(value)
            const that = this;
            setTimeout(function () {
                that.resetbackground()
            }, 200)
        },

        rightClicked: function () {
            var value = this.transorm(this.$refs.rightplayer.getTypeInfo())
            this.$refs.rightplayer.setTypeInfo(value)
            const that = this;
            setTimeout(function () {
                that.resetbackground()
            }, 200)
        },

        mineClicked: function () {
            var value = this.transorm(this.$refs.mineplayer.getTypeInfo())
            this.$refs.mineplayer.setTypeInfo(value)

            const that = this;
            setTimeout(function () {
                that.resetbackground()
            }, 200)
            
        },

        resetbackground: function () {

            var mineType = this.$refs.mineplayer.getTypeInfo()
            var opType = this.$refs.oppositeplayer.getTypeInfo()
            var letfType = this.$refs.leftplayer.getTypeInfo()
            var rightType = this.$refs.rightplayer.getTypeInfo()

            var mineBgValue = this.getSameTypeInfo(mineType, opType, letfType, rightType)
            var opBgValue = this.getSameTypeInfo(opType, mineType, letfType, rightType)
            var leftBgValue = this.getSameTypeInfo(letfType, opType, mineType, rightType)
            var rightBgValue = this.getSameTypeInfo(rightType, opType, letfType, mineType)

            this.$refs.mineplayer.setBgScore(mineBgValue)
            this.$refs.oppositeplayer.setBgScore(opBgValue)
            this.$refs.leftplayer.setBgScore(leftBgValue)
            this.$refs.rightplayer.setBgScore(rightBgValue)
        },

        getSameTypeInfo: function (type, o1, o2, o3) {
            if (o1 == o2 && o2 == o3 && o3 == type) { // 四家不要
                return 0
            }
            if (o1 == o2 && o2 == o3 && o3 != type) { // 只有我要
                return 3
            }
            if ((type == o1 && type == o2) || (type == o1 && type == o3) || (type == o2 && type == o3)) {  // 我們三家缺同一個
                return 0
            }
            if (o1 == o2 || o2 == o3 || o3 == o1) { // 另外兩家缺一樣的
                return 2
            }
            return 1
        },

        resetWanbackground: function () {

        },
        resetTiaoBackground: function () {

        },
        resetTongBackground: function () {

        },
        transorm: function (value) {
            var type = "wan"
            if (value == "tiao") {
                type = "tong"
            } else if (value == "tong") {
                type = "wan"
            } else {
                type = "tiao"
            }
            return type
        }
    }
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

.opposite-block {
    /* text-align: center;
    display: inline-block; */

    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
}

.opposite {
    width: 120px;
    height: 120px;
    margin-top: 50px;
}

.middle-block {
    text-align: center;
    margin-top: 30px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    flex-wrap: wrap;
}


.leftplayer {
    width: 120px;
    height: 120px;
    padding-left: 10px;
}

.rightplayer {
    width: 120px;
    height: 120px;
    padding-right: 10px;
}


.mine-block {
    text-align: center;
    display: inline-block;
}

.mine {
    width: 120px;
    height: 120px;
    margin-top: 30px;
}
</style>
  
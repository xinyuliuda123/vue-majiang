<template>
    <div class="card">
        <img class="panel" :src="bgImgsInfo">
        <div class="whitebg">
            <img class="info" :src="imgsInfo">
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'PlayerCard',
    props: {
        nameStr: String,
    },
    data() {
        return {
            imgs: {
                wan: require(`../assets/wan.png`),
                tong: require(`../assets/tong.png`),
                tiao: require(`../assets/tiao.png`)
            },
            bgImgs: {
                weak: require(`../assets/weak.png`),
                mid: require(`../assets/middle.png`),
                strong: require(`../assets/strong.png`)
            },
            typeInfo: "wan",
            bgImgsInfo: require(`../assets/weak.png`),
            imgsInfo: require(`../assets/wan.png`),
            typeScore: 0
        };
    },

    methods: {

        getImage: function () {
            if (this.typeInfo == "wan") {
                return this.imgs.wan
            } else if (this.typeInfo == "tong") {
                return this.imgs.tong
            } else {
                return this.imgs.tiao
            }
        },

        getTypeInfo: function() {
            return this.typeInfo
        },
        setTypeInfo: function(value) {

            this.typeInfo = value
            this.imgsInfo = this.getImage()
        },
        getBgScore: function() {
            return this.typeScore
        },
        setBgScore: function (value) {
            this.typeScore = value
            this.resetBgImgae()
        },
        resetBgImgae: function () {

            if (this.typeScore == 3) {
                var imgData = this.bgImgs.strong
            } else if (this.typeScore == 2 || this.typeScore == 1) {
                imgData = this.bgImgs.mid
            } else {
                imgData = this.bgImgs.weak
            }
            this.bgImgsInfo = imgData
            console.log("itemInfo " + this.typeInfo + " score " + this.typeScore )
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


.card {
    width: 120px;
    height: 120px;
    /* display: inline-block;
    margin-top: 50px; */
}


.panel {
    width: 120px;
    height: 120px;
    text-align: center;
    /* position: absolute */
}

.info {

    width: 100px;
    height: 100px;


}

.whitebg {
    background-color: #ffffff;
    width: 100px;
    height: 100px;
    position: relative;
    top: 10px;
    left: 10px;
    display: block;
    transform: translate(0%, -125%);
}
</style>
  
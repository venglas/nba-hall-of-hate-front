<template>
<div class="content">
    <button class="btn btn-add btn-add--hate" 
    v-if="!disabledButton"
    @click="addPoint(type)">
        <Icon name="add" />
    </button>
    <span class="number" :style="{margin: disabledButtonMargin}">{{formatedCount}}</span>
</div> 
</template>
 
<script>
import Axios from "axios";
import debounce from "lodash/debounce";
import { axiosHeaders, host_origin } from '@/components/utility/config';
import { formatNumbers } from "@/components/utility/formatBigNumbers.js";

import Icon from "@/components/utility/Icon";

export default {
name: '',
data() {
    return {
        disabledButtonMargin: 0
    }
},
components: {
    Icon
},
computed: {
    formatedCount() {
        return formatNumbers(this.count);
    }
},
props: {
    count: { type: Number },
    type: { type: String },
    disabledButton: { type: Boolean, default: false },
},
watch: {},
mounted() {},
created() {},
methods: {
    addPoint: debounce(async function(type) {
        switch(type) {
            case "Hate": {
                Axios.put( `${host_origin()}/api/player/addHate`, {
                    playerId: this.$store.state.player.selectedPlayer.playerId
                }, axiosHeaders() ).then( res => {
                    this.count = res.data.hateCount;
                }, err => {});
                break;
            };
            
            case "Respect": {
                Axios.put( `${host_origin()}/api/player/addRespect`, {
                    playerId: this.$store.state.player.selectedPlayer.playerId
                }, axiosHeaders() ).then( res => {
                    this.count = res.data.respectCount;
                }, err => {});
                break;
            }
        };
    }, 1000)
}
}

</script>

<style lang='scss'>
.content {
    .number {
        min-width: 50px;
    }
}
</style>
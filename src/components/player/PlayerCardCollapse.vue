<template>
<div id="accordion" class="collapse-box" v-bind:class="this.spacer">
    <div class="card">
        <div class="card-header" id="headingOne">
            <h5 class="mb-0">
                <span class="coment-count-info">({{replacedCommentsCount}})</span>
                <span>{{title}} comments</span>
                <button class="btn" :title="'add ' + title.toLowerCase() + ' comment'" @click="showAddCommentModal(title.toLowerCase())">
                    <Icon name="add" />
                </button>
            </h5>
        </div>
    </div>

    <div class="card">
        <Player-card-collapse-comment
        v-for="comment in comments" 
        :key="comment.commentId"
        :comment="comment"
        />
    </div>
</div>
</template>

<script>
import Axios from 'axios';
import { axiosHeaders, host_origin } from '@/components/utility/config';
import { formatNumbers } from "@/components/utility/formatBigNumbers.js";

import PlayerCardCollapseComment from '@/components/player/PlayerCardCollapseComment';
import Icon from '@/components/utility/Icon';

export default {
    name: 'Player-card-collapse', 
    components: {
        "Player-card-collapse-comment": PlayerCardCollapseComment,
        Icon
    },
    data() {
        return {}
    },
    computed: {
        replacedCommentsCount() {
            return formatNumbers(this.commentsCount);
        }
    },
    props: {
        spacer: { type: String },
        title: { type: String },
        comments: { type: Array },
        commentsCount: { type: Number }
    },
    created(){
    },
    watch: {},
    
    methods:{
        showAddCommentModal(commentType) {
            if ( this.$store.state.player.commentBox.isVisibleAddCommentModal === false ) {
                this.$store.state.player.commentBox.isVisibleAddCommentModal = true;
                this.$store.state.player.commentBox.commentType = commentType;
            }
        }
    }
};
</script>

<style lang="scss">
.collapse-box {
    flex-grow: 1;

    .card {
        .card-header {
            .coment-count-info {
                font-size: 10px;
                margin-right: 5px;
            }
        }
    }
}
</style>
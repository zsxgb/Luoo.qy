<template>
    <div
        id="vols"
        :class="$store.getters.view === 'vols' ?
            'volsShow' : 'volsHidden'"
    >
        <Vol
            v-for="(vol, index) in $store.getters.vols"
            :data="Object.freeze(vol)"
            :index="index"
            :type="'vol'"
            :key="`${vol.vol}-${index}`"
            :remote="remote"
        />
        <div
            id="loadMoreVols"
            :style="{ opacity: $store.state.vols.index <
                $store.getters._vols.length ? 1 : 0 }"
        >
            <div v-on:click.stop="loadMore">
                <img :src="'../pic/loadMore-stroked.svg'"/>
                <p>更多</p>
            </div>
        </div>
    </div>
</template>


<script>
    import Vue from 'vue';
    import Vol from './Vol.vue';


    export default {
        name: 'vols',
        components: { Vol },
        props: ['remote'],
        methods: {
            loadMore: function () {
                this.$store.dispatch('loadMore', {
                    type: 'Vols',
                    init: false
                })
            }
        }
    }
</script>


<style lang="sass" scoped>
    #vols
        position: fixed
        width: 90%
        height: calc(100% - 180px)
        top: 80px
        left: 0
        padding: 25px 5% 0 5%
        overflow-y: auto
        text-align: left
        display: flex
        flex-direction: row
        flex-wrap: wrap
        justify-content: flex-start

    .volsShow
        transform: scale(1)
        opacity: 1
        transition: all ease 500ms 350ms

    .volsHidden
        transform: scale(0.9)
        opacity: 0
        transition: all ease 500ms 0ms

    #loadMoreVols
        width: 100%
        margin: 15px 0 30px 0
        text-align: center
        font-weight: 400

        & > div
            margin-left: 47%
            cursor: pointer
            font-size: 0.9em
            opacity: 0.8
            width: 6%

            &:hover
                opacity: 1

            img
                height: 50%

            *
                cursor: pointer

</style>
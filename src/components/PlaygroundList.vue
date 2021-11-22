<template>
    <h1>Playgrounds on Amplify</h1>
    <div class="cardwrapper">
        <playground-card v-for="playground in playgrounds" :key="playground.id" :playground="playground" />
    </div>
</template>

<script>
import { API, graphqlOperation } from 'aws-amplify'
import { listPlaygrounds } from '../graphql/queries'
import PlaygroundCard from './PlaygroundCard.vue'

export default {
    components: {
        PlaygroundCard
    },
    data() {
        return {
            playgrounds: []
        }
    },
    async mounted() {
        const playgroundResponse = await API.graphql(graphqlOperation(listPlaygrounds))
        this.playgrounds = playgroundResponse.data.listPlaygrounds.items;
        // console.log(playgroundResponse)
        // const options = {
        //     method: "POST",
        //     headers: {
        //         "Content-Type":"application/json"
        //     },
        //     body: JSON.stringify({
        //         query: ` 
        //             query {
        //                 allPlaygrounds {
        //                 id
        //                 name
        //                 rating
        //                 equipment {
        //                 name
        //                 equipmentType
        //                 }
        //                 location {
        //                 city
        //                 street
        //                 zip
        //                 }
        //                 heroImage
        //                 }
        //             }
        //         `
        //     })
        // }
        // fetch("http://localhost:9002/graphql", options)
        // .then((response) => {
        //     return response.json();
        // })
        // .then((data) => {
        //     this.playgrounds = data.data.allPlaygrounds;
        // })
    }
}

</script>

<style>
.cardwrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
}
</style>
<script setup>
import WaitingForUserIcon from '../icons/finding_match/IconUser.vue'
import { useQuery, useQueryClient, useQueries } from 'vue-query';
import  * as database from '../../database/firebase-functions';
import { getAuth, onAuthStateChanged } from "firebase/auth";
import { getIdToken } from 'firebase/auth';
import { ref } from 'vue';
import router from '../../router';

const queryClient = useQueryClient();

const props = defineProps({
    matchID: String
})

const { data } = useQuery(
    ["GetMatchWithID",props.matchID],
    () => database.getMatchByID(props.matchID)
);

const playerJoinMatch = async (matchid) => {
    const result = await database.addPlayerToMatch(matchid)
    if (result == true) {
        router.push({
            path: `/match/${matchid}`,
        });
    } else {
        return;
    }
}

</script>

<template>
<section v-for="item in data" :key="item.id">
    <div class="search-match-board">
        <div id="match-time-playing">
            <p>{{ item.date }}</p>
        </div>
        <div id="match-players">
            <img src="../../assets/images/field.png">
            <ul v-for="n in 4" :key="n.id">
                <span :id="`player${n}`">
                    <div v-if="!item.players[n-1]"><WaitingForUserIcon /></div>
                    <div v-else>{{ item.players[n-1] }}</div>
                </span>
            </ul>
        </div>
        <div id="match-information">
            <ul>
                <li id="padel-facility">{{ item.facility }}</li>
                <li id="hours-playing">test</li>
                <li id="amount-paying">{{ item.cost }}<p class="price">DKK</p></li>
            </ul>
        </div>
        <div id="match-join">
            <button @click="playerJoinMatch(item.id)" id="button-join-match">
                <p>Join Match</p>
            </button>
        </div>
    </div>
</section>
</template>

<style scoped>

.search-match-board {
    position: absolute;
    width: 300px;
    height: 400px;

    box-sizing: border-box;
    border-radius: 48px;
background: linear-gradient(360deg, #203645 -5.5%, rgba(27, 142, 135, 0) 66.48%, #203645 111.63%);
    box-shadow: 0px 4px 75px rgba(0, 0, 0, 0.25);
    border-radius: 50px;
    border: none;
    outline:none;
  }


#match-players {
    position: absolute;
    left: 16.67%;
    right: 16.67%;
    top: 12%;
    bottom: 38%;
}

#match-time-playing {
    position: absolute;
    left: 0%;
    right: 0.33%;
    top: 2.75%;
    bottom: 89.17%;
    text-align: center;

    font-family: sans-serif;
    text-transform: uppercase;
    font-size: 25px;
    font-style: bold;
    font-weight: 700;


    color: rgba(255, 255, 255, 0.91);


}

#match-information ul {
    list-style-type: none;
}

#match-information ul li {
    position: absolute;
    background: rgba(241, 242, 245, 0.46);
    border: 2px solid #FFFFFF;
    overflow-wrap: break-word;
    box-sizing: border-box;
    border-radius: 10px;
    height: 54px;
    width: 83px;
    font-family: sans-serif;
    font-style: normal;
    font-weight: 700;
    font-size: 15px;
    line-height: 20px;
    text-align: center;
    font-weight: 700;
    text-transform: Uppercase;


    color: #ffffff;





}

#padel-facility {
    position: absolute;
    left: 2%;
    right: 70.27%;
    top: 67.44%;
    bottom: 18.97%;
}

#hours-playing{
    position: absolute;
    left: 36.08%;
    right: 36.19%;
    top: 67.69%;
    bottom: 18.72%;

}

#amount-paying{
    position: absolute;
    left: 70.16%;
    right: 2.12%;
    top: 67.44%;
    bottom: 18.97%;
}

#button-join-match{
    position: absolute;
    left: 24.28%;
    right: 24.16%;
    top: 84.72%;
    bottom: 4.62%;
    cursor: pointer;

    background: #1B8E87;
    border-radius: 10px;
    border: none;
    outline:none;
}

#button-join-match p{
    font-family: sans-serif;
    text-transform: uppercase;
    font-style: bold;
    font-weight: 800;
    font-size: 20px;
    line-height: 24px;
    text-align: center;

    color: rgba(255, 255, 255, 0.91);
    -webkit-text-stroke-width: 1.5px;
    -webkit-text-stroke-color: rgb(0, 0, 0);



}

#player1 {
    position: absolute;
    left: 17.5%;
    right: 62.5%;
    top: 12%;
    bottom: 68%;

    font-family: sans-serif;
    text-transform: uppercase;
    font-style: bold;
    font-weight: 700;

    color: rgba(255, 255, 255, 0.91);
    -webkit-text-stroke-width: .8px;
    -webkit-text-stroke-color: rgb(0, 0, 0);

}

#player2{
    position: absolute;
    left: 65%;
    right: 15%;
    top: 12%;
    bottom: 68%;

    font-family: sans-serif;
    text-transform: uppercase;
    font-style: bold;
    font-weight: 700;

    color: rgba(255, 255, 255, 0.91);
    -webkit-text-stroke-width: .8px;
    -webkit-text-stroke-color: rgb(0, 0, 0);

}

#player3{
    position: absolute;
    left: 17.5%;
    right: 62.5%;
    top: 64%;
    bottom: 16%;

    font-family: sans-serif;
    text-transform: uppercase;
    font-style: bold;
    font-weight: 700;

    color: rgba(255, 255, 255, 0.91);
    -webkit-text-stroke-width: .8px;
    -webkit-text-stroke-color: rgb(0, 0, 0);



}

#player4{
    position: absolute;
    left: 65%;
    right: 15%;
    top: 64%;
    bottom: 16%;

    font-family: sans-serif;
    text-transform: uppercase;
    font-style: bold;
    font-weight: 700;

    color: rgba(255, 255, 255, 0.91);
    -webkit-text-stroke-width: .8px;
    -webkit-text-stroke-color: rgb(0, 0, 0);

}


</style>
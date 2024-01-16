<template>
        <div class="container timebanner">
            
            <div class="about" style="height: 275px; margin-bottom: 20px; display: flex; flex-direction: column; align-items: center;">
                <span style="color: white; font-weight: 600; letter-spacing: 1px; margin-bottom: 10px;">Viloyatingizni tanlang</span>
                <nav aria-label="..." style="width: 100%; height: 100%; overflow-y: auto; padding: 5px; ">
                <ul class="pagination pagination-sm" style="display: flex; flex-direction: column; gap: 5px; border: none; ">
                    <li class='page-item' v-for="id in region" :class="regionId == id.id ? 'active' : ''">
                        <span class="page-link" :class="regionId == id.id ? 'text-white' : ''" @click="changeId(id.id, id.region)" style="cursor: pointer; color: black; border: none; box-shadow: 1px 1px 5px rgba(128, 128, 128, 0.226); padding: 10px; border-radius: 5px;" >{{ id.region }}</span>
                    </li>
                </ul>
                </nav>
            </div>
            <div class="times">
                <div style="display: flex;">
                    <div class="title">
                        <h1>{{ data.region }}</h1>
                        <span>{{ data.weekday }} | {{ data.date }}</span>
                    </div>
                    <div class="content">
                        <p>
                            <span v-if="this.loading">
                                Tong <span>{{ data.times['tong_saharlik'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                        <p>
                            <span v-if="this.loading">
                                Quyosh <span>{{ data.times['quyosh'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                        <p>
                            <span v-if="this.loading">
                                Peshin <span>{{ data.times['peshin'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                        <p>
                            <span v-if="this.loading">
                                Asr <span>{{ data.times['asr'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                        <p>
                            <span v-if="this.loading">
                                Shom <span>{{ data.times['asr'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                        <p>
                            <span v-if="this.loading">
                                Hufton <span>{{ data.times['hufton'] }}</span>
                            </span>
                            <span v-else>
                                <Loader/>
                            </span>
                        </p>
                    </div>

                </div>
                <!-- <div v-else class="d-flex justify-content-center">     
                    <div class="spinner-grow spinner-grow-sm" role="status" style="width: 70px; height: 70px;">
                        <span class="visually-hidden">Loading...</span>
                    </div>
                </div> -->
            </div>
        </div>
</template>
<script>
import axios from "axios";
import Loader from "../components/Loader.vue"
export default{
    components: {
        Loader
    },
    data(){
        return{
            data: [],
            region: [
                {
                    id: 1,
                    region: 'Farg\'ona',
                },
                {
                    id: 2,
                    region: 'Toshkent',
                },
                {
                    id: 3,
                    region: 'Andijon',
                },
                {
                    id: 4,
                    region: 'Buxoro',
                },
                {
                    id: 5,
                    region: 'Jizzax',
                },
                {
                    id: 6,
                    region: 'Xiva',
                },
                {
                    id: 7,
                    region: 'Namangan',
                },
                {
                    id: 8,
                    region: 'Navoiy',
                },
                {
                    id: 9,
                    region: 'Qarshi',
                },
                {
                    id: 10,
                    region: 'Samarqand',
                },
                {
                    id: 11,
                    region: 'Guliston',
                },
                {
                    id: 12,
                    region: 'Nukus',
                },
            ],
            regionId: 1,
            getRegion: 'Farg\'ona',
            loading: false,
        }
    },
    methods: {
        async fetchRegion(){
            try {
                this.region.forEach(i => {
                    if(this.regionId == i.id){
                        this.getRegion = i.region
                    }
                });
                const {data} = await axios.get('https://islomapi.uz/api/present/day',{
                    params: {
                        region: this.getRegion,
                    }
                });
                this.data = data
                this.loading = true
            } catch (error) {
                alert(error.message)
            }
        },
        changeId(id, reg){
            this.regionId = id
            this.loading = false
            this.fetchRegion()
            localStorage.id = id;
            localStorage.name = reg;
        },

    },
    
    mounted (){
        this.fetchRegion(); 
        console.log(localStorage['id']);
    },
        
}

</script>
<style scoped>
    .timebanner{
        background-image: url('https://png.pngtree.com/background/20230613/original/pngtree-muslim-mosques-in-purple-and-stars-with-the-moon-picture-image_3420381.jpg');
        background-position: center;
        background-size: cover;
        border-radius: 15px;
        height: 550px;
        padding: 10px;
    }

    .times{
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0;
    }

    .times div{
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 10px;
    }

    .times div .content{
        width: 100%;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        padding: 0;
    }
    
    .times .content p{
        width: 14%;
        height: 140px;
        display: flex;
        flex-direction: column;
        background-color: #f6f6f6cd;
        border-radius: 10px;
        font-weight: 500;
        align-items: center;
        gap: 7px;
        justify-content: center;
        color: rgb(110, 110, 110);
        font-size: 20px;
        margin: 0;
    }

    .times .content p span{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .times .title{
        color: rgb(255, 255, 255);
        font-weight: 600;
    }

    .times .title span{
        color: rgb(208, 208, 208);
        font-weight: 600;
    }

    .times .content p span{
        font-size: 17px;
    }

    @media screen and (max-width: 447px){
        .timebanner{
            height: 100%;
        }
        .times .content p{
        width: 48%;
        height: 140px;
    }
    }
</style>
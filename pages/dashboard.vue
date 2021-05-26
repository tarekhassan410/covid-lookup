<template>
    <section class="h-100 d-flex p-0">
        <div class="aside-area h-100 pt-3 d-none d-md-block" lg="2">
            <b-container>
                <Sidebar />
            </b-container>
        </div>
        <div class="main-area">

            <b-navbar class="py-2" toggleable="md" variant="secondary">

            <b-navbar-brand href="#"></b-navbar-brand>

                <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

                <b-collapse id="nav-collapse" is-nav>
                    <b-navbar-nav class="ml-auto">
                        <b-dropdown-item href="#"> <div class="text-white"> <span  class="material-icons"> notifications </span> </div> </b-dropdown-item>
                        <b-dropdown-item  href="#"> <div class="text-white d-flex align-items-center">  <span class="text-white material-icons"> person </span> demo@mytigate.com </div> </b-dropdown-item>
                    </b-navbar-nav>
                </b-collapse>

            </b-navbar>


            <main class="py-4">
                <b-container fluid>
                    <p> Dashboard </p>
                <div>
                    <b-input-group>
                        <b-form-input  v-model="country" placeholder="search" @change="getCountryCovidData" @keyup.enter.native="getCountryCovidData" ></b-form-input>
                        <template #append>
                            <b-input-group-text class="search"  @click="getCountryCovidData">Search</b-input-group-text>
                        </template>
                    </b-input-group>

                    <div v-if="stats.length == 0">
                        0 results
                    </div>
                    <div v-else>
                    <b-card v-for="stat in stats" :key="stat.countryInfo._id" 
                    class="mt-2">
                        <b-row>
                            <b-col cols="12" md="8" lg="9" class="text-center text-md-left">
                                <span class="h4"> {{stat.country}} </span>
                                <small> {{stat.countryInfo.iso2}} </small>
                            </b-col>
                            <b-col cols="12" md="4" lg="3" class="mt-2 mt-md-0 text-center text-md-right">
                            <b-img :src="stat.countryInfo.flag" fluid class="country-flag text-right" />
                            </b-col>
                        </b-row>
                        <b-row class="mt-3">
                            <b-col lg="3" class="text-center">
                                <p>Total confirmed cases<br />
                                    <span>{{stat.cases}}
                                </span></p>
                            </b-col>
                            <b-col lg="3" class="text-center">
                                <p>New cases<br />
                                <span>  
                                    {{stat.todayCases}} 
                                </span></p>
                            </b-col>
                            <b-col lg="3" class="text-center">
                                <p>Deaths<br />
                                <span class="text-danger">  
                                    {{stat.deaths}} 
                                </span></p>
                            </b-col>
                            <b-col lg="3" class="text-center">
                                <p>Recovered<br />
                                <span class="text-success">  
                                    {{stat.recovered}} 
                                </span></p>
                            </b-col>
                        </b-row>
                        <b-row class="mt-3">
                            <b-col class="text-center">
                                Recommended for traveling <br />
                                <span v-if="stat.tests / stat.cases > 10" class="text-success font-weight-bold"> yes </span>
                                <span v-else class="text-danger font-weight-bold"> No </span>
                            </b-col>
                        </b-row>
                        
                    </b-card>
                    </div>

                </div>
                </b-container>
            </main>
            <footer>
                <b-container>
                    <b-row  class="py-2">
                        <b-col cols="6" lg="3">
                            <div> version 1.0.0 </div>
                            <div>https://mytigate.de/</div>
                        </b-col>
                        <b-col cols="6" lg="3">
                            <div> &copy; copyright </div>
                            <div> MYTIGATE GmBH </div>
                            <div> All rights reserved </div>
                        </b-col>
                    </b-row>
                </b-container>
            </footer>
        </div>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                stats: [],
                country: ""
            }
        },
        created(){
            this.getCovidData()
        },
        methods:{
            getCovidData(){
                fetch('https://disease.sh/v3/covid-19/countries')
                .then( response => response.json() )
                .then( response => {
                    this.stats = response
                } )
            },
            getCountryCovidData(){
                if (this.country.length === 0){
                      fetch('https://disease.sh/v3/covid-19/countries')
                    .then( response => response.json() )
                    .then( response => {
                        this.stats = response
                    } )  
                } 
                fetch(`https://disease.sh/v3/covid-19/countries/${this.country}`)
                .then( response => response.json() )
                .then( response => {
                    if ( response.country){
                        this.stats = []
                        this.stats.push(response)

                    } else {
                        this.stats = []
                    }
                })
                
            }
        },
        
    }
</script>

<style scoped>
.country-flag{
    width: 20%;
}
.tracker{
    min-height: 99.9vh;
    height: 99.9vh;
}
.aside-area{ 
    position: -webkit-sticky;
    position: sticky;
    top: 0;
    min-height: 99.9vh;
    height: 99.9vh;
    background-color: #00264B;
}
.search{
    background-color: #00264B;
    color: white;
}
.nav-item a{
    color: #00264B;
}
.aside-area{
    width: 15%;
}
.main-area{
    width: 85%;
    position: relative;
}
main{
    min-height: 80vh;
}
footer{
    background-color: lightgray;
    
    width: 100%;
}

@media screen and (max-width: 992px) {
  .main-area{
    width: 100%;
  }
}

@media screen and (max-width: 1100px) {
  .aside-area{
    width: 20%;
  }
}


</style>
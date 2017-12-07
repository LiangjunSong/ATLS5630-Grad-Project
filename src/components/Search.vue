<style src="../../node_modules/vuetify/dist/vuetify.min.css">

</style> --> <style scoped> #inspire {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

#search-btn {
    margin-top: 10px;
}

</style>

<template>

<div>
    <v-app id="inspire">
        <v-container fluid="fluid" class="text-xs-center">
            <v-layout row wrap>
                <v-flex xs12 sm8 offset-sm2><span>Online Music Picker</span>
                    <v-card height="185px" flat color="white">
                        <v-card-text>
                            <v-container fluid text-xs-center>
                                <v-layout row wrap>
                                    <!-- <v-flex xs9>
                                        <v-text-field label="Music keywords" v-model="keywords"></v-text-field>
                                    </v-flex> -->
                                    <v-flex xs9>
                                        <v-select autocomplete :items="tags" label="Music Tag" chips tags solo append-icon="" clearable v-model="chips">
                                            <template slot="selection" slot-scope="data">
                                                <v-chip close @input="remove(data.item)" :selected="data.selected">
                                                    <strong>{{ data.item }}</strong>
                                                    <!-- <span>(musictag)</span> -->
                                                </v-chip>
                                            </template>
                                        </v-select>
                                    </v-flex>
                                    <v-flex xs3>
                                        <v-btn id="search-btn" color="primary">Go</v-btn>
                                    </v-flex>
                                </v-layout>
                            </v-container>
                        </v-card-text>
                    </v-card>
                </v-flex>
            </v-layout>

        </v-container>
    </v-app>
</div>

</template>

<script>

export default {
    name: 'Search',
    data() {
        return {
            keywords: '',
            chips: ['Sleeping'],
            tags: ['Jazz', 'Pop', 'Rock', 'Guitar', 'Piano', 'Relax', 'Male','Female','No vocal']
        }
    },
    methods: {
        remove(item) {
            this.chips.splice(this.chips.indexOf(item), 1)
            this.chips = [...this.chips]
        }
    }
}

</script>

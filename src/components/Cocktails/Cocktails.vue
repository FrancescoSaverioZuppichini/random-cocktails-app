<template>
<v-container>
    <transition-group name="fade" class='layout row wrap align-center' mode="out-in"
        <v-flex xs12 :key="cocktail.idDrink" v-for="cocktail in cocktails">
            <cocktail :cocktail="cocktail" class='mb-2'>
            </cocktail>
        </v-flex>
        <v-flex xs12 v-show="isLoading" key='loading'>
            <skeleton-card class='skeleton-card--opacity' :hasHeader="false" :isHorizontal="true"> </skeleton-card>
        </v-flex>
    </transition-group>
    <v-flex xs12>
            <v-layout column align-center>
                <v-btn primary @click="getMore()"> Get More</v-btn>
            </v-layout>
        </v-flex>
</v-container>
</template>

<script>
import axios from 'axios'

import Cocktail from './Cocktail/Cocktail.vue'
import SkeletonCard from 'skeleton-card-vuejs'

const API_URL = 'http://www.thecocktaildb.com/api/json/v1/1/random.php'

export default {
    name: "",
    components: {
        Cocktail,
        SkeletonCard
    },
    mounted() {
        this.getMore()
    },
    data: function() {
        return {
            isLoading: false,
            cocktails: []
        }
    },
    methods: {
        getMore() {
            this.isLoading = true

            axios.get(API_URL)
                .then(({ data }) => {
                    var cocktail = data.drinks[0]
                    this.cocktails.push(cocktail)
                    cocktail.ingredients = this.createIngrediens(cocktail)
                    this.isLoading = false
                })
                .catch(err => this.isLoading = false)
        },
        createIngrediens(cocktail) {
            var ingredients = []

            const ingredientKey = "strIngredient"
            const measureKey = "strMeasure"

            for (let i = 1; i < 15; i++) {

                let ingredientsString = ""
                ingredientsString += cocktail[measureKey + i]
                ingredientsString += cocktail[ingredientKey + i]
                // remove weird stuff
                ingredientsString = ingredientsString.replace(/\n/ig, '');
                ingredientsString = ingredientsString.trim()
                
                if (ingredientsString !== "") ingredients.push(ingredientsString)
            }

            return ingredients
        }
    }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity .8s
}

.fade-enter,
.fade-leave-to
/* .fade-leave-active below version 2.1.8 */

{
    opacity: 0
}

.skeleton-card--opacity{
    opacity: 0.7;
}
</style>
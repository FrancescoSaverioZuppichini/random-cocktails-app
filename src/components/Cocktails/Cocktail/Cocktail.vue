<template>
<v-card>
    <v-container fluid grid-list-lg>
        <v-card-title>
                <v-flex>
                    <div>
                        <div class="headline">{{cocktail.strDrink}}</div>
                        <br/>
                        Ingredients
                        <ul>
                            <li v-for="ingredient in cocktail.ingredients" :key="ingredient">
                                {{ingredient}}
                            </li>
                        </ul>
                    </div>
                </v-flex>
                <v-spacer></v-spacer>
                    <img :src="cocktail.strDrinkThumb" class='cocktail__image'></img>
        </v-card-title>
        <v-card-actions>
            <v-chip>
                {{cocktail.strAlcoholic}}
            </v-chip>
            <v-spacer></v-spacer>
            <v-btn flat @click.native="toogleInstructions()">
                instructions
            </v-btn>
        </v-card-actions>
        <v-card-text v-show="instructions">
            <div>{{cocktail.strInstructions}}</div>
        </v-card-text>
    </v-container>
</v-card>
</template>

<script>
export default {
    name: "",
    props: ['cocktail'],
    data: function() {
        return {
            instructions: false
        }
    },
    methods: {
        toogleInstructions() {
            this.instructions = !this.instructions
        }
    }
}
</script>

<style scoped>
.cocktail__image{
    height: 150px;
}

</style>
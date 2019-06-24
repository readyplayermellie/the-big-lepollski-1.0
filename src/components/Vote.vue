<template>
    <div id="container">
<!-- the questions div -->
        <div id="question-div">
            <div class="header-div">
                <h2> {{ title1 }} </h2>
            </div>

            <div class="question-div">
                <label>Typ your super cool question: </label>
                <input v-model="question" id="input-question" placeholder="" maxlength="80">
            </div>
            
            <div class="option-div">
                <label> Add at least two options: </label>
                <form @submit.prevent="addOption" v-if="disabled.add" id="option-form">
                    <input class="new-option" placeholder="" type="text" v-model="newOption" required maxlength="80"/>
                    <button type="submit" class="btn-add">Add</button>
                </form>
                <p v-if="answer.display">Available answers: {{ answer.count }}</p>
                <p v-else>Enough options for today</p>
            </div>    

            <div class="button-div">
                <button @click="resetPage" type="reset" class="btn-primary">Reset</button>
            </div>
        </div>
<!-- the voting div -->
        <div id="vote-div">
            <div class="header-div">
                <h2> {{ title2 }} </h2>
            </div>

            <div class="question-div">
                <p class="p-question"> {{ question }} </p>
            </div>

            <div class="option-div">
                <form id="vote-form">
                    <ul id="list">
                        <li v-for="option in options" :key="option" class="list-item">
                            <input type="radio" name="radio-options" checked>
                            <p class="p-option"> {{option.title}} </p>
                            <button @click="removeOption(option)" type="button" class="btn-remove">X</button> 
                        </li>
                    </ul>
                    <p v-if="minimum">Create at least two options.</p>
                    <button @click.prevent="voteNow" v-if="disabled.vote" type="submit" class="btn-primary" id="btn-vote">Vote</button>
                </form>
            </div>
        </div>
<!-- the results div -->
        <div id="results-div">
            <div class="header-div">
                <h2> {{ title3 }} </h2>
            </div>

            <div class="question-div">
                <p class="p-question"> {{ question }} </p>
                <p id="p-total" >Total votes:</p>
                <p id="p-vote-count"> {{ count }}</p>
            </div>

            <div class="options-div">
                <img id="sun-glasses-guy" src="../assets/guy-sun-on.svg" alt="sun glasses guy">
            </div>
            <div class="button-div">   
                
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Vote',
    data() {
        return {
            title1: 'Questions',
            title2: 'Vote',
            title3: 'Results',
            question: '',
            count: 0,
            newOption: '',
            options: [],
            answer: {
                count: 10,
                display: true
            },
            disabled: {
                add: true,
                vote: true
            },
            voteCount: 0,
            checked: false,
            minimum: false
        }
    },
    methods: {
        addOption() {
            this.options.push({
                title: this.newOption
            });
            this.options.splice(10);
            this.newOption = '';
            this.answer.count -= 1;
            if(this.answer.count < 1){
                this.answer.display = false;
                this.disabled.add = false;
            } else {
                this.answer.display = true;
                this.disabled.add = true;
            }
        },
        removeOption(option) {
            const optionIndex = this.options.indexOf(option);
            this.options.splice(optionIndex, 1);
            this.answer.count += 1;
        },
        voteNow() {
            if (this.answer.count >= 9) {
               this.minimum = true;
               this.count += 0;
            } else {
                this.minimum = false;
                this.count += 1;
            }
        },
        resetPage() {
            this.answer.display = true;
            this.disabled.add = true;
            this.options = [];
            this.answer.count = 10;
            this.count = 0;
            this.question = ''; 
        }
    }
}

</script>

<style lang="scss" scoped>

// ------ input boxes -----

#input-question,
.new-option {
    width: 290px;
    height: 30px;
    padding: 2px;
    text-align: center;
    border-radius: 4px;
    margin: 10px 10px 10px 10px;
    border: 1px solid #ccc;
}

#input-question {
    margin: 15px 10px 110px 10px;
}

.new-option {
    width: 250px;
    margin-bottom: 5px;
}

#list {
    padding: 0px;
    .list-item {
        list-style: none;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
}

.p-question {
    font-weight: bold;
    font-size: 16px;
}

.p-option {
    height: 30px;
    width: 250px;
    border-radius: 4px;
    box-shadow: 1px 1px 8px .5px rgba(232,232,232,1);
    margin: 10px;
    padding:4px;
}

#btn-vote {
    margin: 20px;
}

#sun-glasses-guy {
    height: 220px;
}


</style>

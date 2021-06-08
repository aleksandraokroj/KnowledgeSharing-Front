<template>
    <div>
        <navbar />
        <div>
            <b-card :footer="footerText">
             <template #header>
            <h1 class="title">Edytuj notatkę</h1>
            </template>
            <br><br>
            <form v-on:submit.prevent="editPost">
                <ValidationProvider name="title" rules="required:true|max:100"
                                    :custom-messages="errorMessages.titleError" v-slot="{ errors }">
                    <div class="form-group">
                        <label for="title" class="label">Tytuł notatki</label>
                        <input class="form-control form-control-lg" id="title" v-model="post.title"
                         :placeholder="post.title" type="text" :name="post.title" validation="required|title" />
                        <span class="errorMsg">{{ errors [0]}}</span>
                    </div>
                </ValidationProvider>
                <ValidationProvider name="author" :rules="{required:true}"
                                    :custom-messages="errorMessages.authorError" v-slot="{ errors }">
                    <div class="form-group">
                        <label for="author" class="label">Autor</label>
                        <input class="form-control form-control-lg" id="author" v-model="post.userInfo"
                               :placeholder="post.userInfo" type="text" name="author" validation="required|author" />
                        <span class="errorMsg">{{ errors [0]}}</span>
                    </div>
                </ValidationProvider>
                <ValidationProvider name="content" :rules="{required:true}"
                                    :custom-messages="errorMessages.contentError" v-slot="{ errors }">
                    <div class="form-group">
                        <label for="content" class="label">Treść notatki</label>
                        <textarea cols="50" rows="10" class="form-control form-control-lg" id="post" v-model="post.content" :placeholder="post.content" type="text" name="content" validation="required|post" />
                        <span class="errorMsg">{{ errors [0]}}</span>
                    </div>
                </ValidationProvider>
                <div class="form-group">
                    <label for="category" class="label">Kategoria</label>
                    <select v-model="post.category" class="custom-select custom-select-lg" aria-label="Default select example" :aria-placeholder="post.category">
                        <option value="">Wybierz przedmiot</option>
                        <option id="Polski" name="polish" value="Polski">Język polski</option>
                        <option id="Angielski" name="english" value="Angielski">Język angielski</option>
                        <option id="Historia" name="history" value="Historia">Historia</option>
                        <option id="Biologia" name="biology" value="Biologia">Biologia</option>
                        <option id="Chemia" name="chemistry" value="Chemia">Chemia</option>
                        <option id="Matematyka" name="math" value="Matematyka">Matematyka</option>
                        <option id="Fizyka" name="physics" value="Fizyka">Fizyka</option>
                        <option id="Geografia" name="geography" value="Geografia">Geografia</option>
                    </select>
                </div>
                <div class="edit-button">
                    <b-button variant="primary" type="submit">Edytuj</b-button>
                </div>
            </form>
                  <b-alert class="edited-alert"
      :show="dismissCountDown"
      dismissible
      variant="success"
      @dismissed="dismissCountDown=0"
      @dismiss-count-down="countDownChanged"
    >
      <p>Pomyślnie edytowano notatkę! Powiadomienie zniknie za:  {{ dismissCountDown }} s</p>
      <b-progress
        variant="success"
        :max="dismissSecs"
        :value="dismissCountDown"
        height="4px"
      ></b-progress>
    </b-alert>
            </b-card>
        </div>
    </div>
</template>

<script>
    import navbar from '../components/Navbar.vue';
    import $ from 'jquery';


    export default {
        name: 'EditPost',
        components: { navbar },
        data() {
            return {
               post: {
                    Title: '',
                    Category: '',
                    Content: '',
                    UserInfo: ''
                },
                showDismissibleAlert: false,
                dismissSecs: 10,
                dismissCountDown: 0,
                errorMessages: {
                    titleError: {
                        required: 'Należy podać tytuł notatki',
                        max: 'Tytuł notatki może mieć maksymalnie 100 znaków'
                    },
                    authorError: {
                        required: 'Należy wpisać swoje imię i nazwisko',
                    },
                    contentError: {
                        required: 'Należy uzupełnić treść notatki',
                    },

                }
            }
        },
        computed: {
            timestamp() {
                return new Date().toLocaleDateString();
            },
             footerText(){
                return 'Data dodania: ' + this.timestamp 
            }
        },
        methods: {
            async editPost() {
                $.ajax({
                    url: `https://localhost:44335/KnowledgeSharing/Edit-Post/`+this.$route.params.id,
                    method: 'put',
                    headers: { 'Content-Type': 'application/json' },
                    data: JSON.stringify(this.post),
                    dataType: 'json'
                })
                    .done((result) => {
                        console.log(result);
                        this.showDismissibleAlert=true;
                        this.dismissCountDown = this.dismissSecs
                    })
                    .fail((err) => {
                        console.log(err);
                    });

            },
            getDate() {
                const datet = new Date(Date.now());
                const dateISO = datet.toISOString();
                return dateISO;
            },
            countDownChanged(dismissCountDown) {
            this.dismissCountDown = dismissCountDown
      },
        },

        async created() {
       $.ajax({
            url: 'https://localhost:44335/KnowledgeSharing/Post/'+this.$route.params.id,
            method: 'get'
        })
        .done((result) => {
            this.post = result;
            console.log("result");
        })
        .fail((err) => {
            console.log(err);
        });
    },

    };
</script>
<style scoped>

    .form-group {
        align-content: center;
        align-items: center;
        padding: 10px;
        padding-left: 30%;
        padding-right: 30%;
    }

    .label {
        color: #1E90FF;
        font-size: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        padding-bottom: 10px;
        font-weight: 700;
    }

    .title {
        color: #1E90FF;
        font-size: 50px;
        text-transform: uppercase;
        text-align: center;
        padding: 30px;
        font-weight: 700;
    }

    .errorMsg {
        font-size: 20px;
        color: red;
    }

    textarea {
        resize: none;
    }

.card{
    width: 1000px;
    margin-top: 50px !important;
    align-content: center;
    margin: 0 auto; /* Added */
    float: none; /* Added */
}

.card-header, .card-footer{
        background-color: #F8F8F8;
    }

    .card-footer{
        text-align: right;
    }

    .edit-button{
        display: flex;
  justify-content: center;
    }

    .btn-primary{
        width: 100px;
        margin-top: 30px;
    }

    .edited-alert{
        margin-top: 30px;
        margin-bottom: 30px;
    }


</style>
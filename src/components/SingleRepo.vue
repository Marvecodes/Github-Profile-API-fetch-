<template>
    <div class="repos-container">
        <div class="repos">
            <p @click="redirectToHome" class="btn">Go to HomePage</p>
            <h1>{{ repo.name }}</h1>
            <p class="desc">{{ repo.description }}</p>
            <div class="space">
                <p><i class="fa-solid fa-code"></i>  Project Language</p>
                <p class="details">{{ repo.language }}</p>
            </div>
          
            <div class="space">
                <p><i class="fa-solid fa-calendar-days"></i> Date/Time of Creation </p>
                <p class="details">{{ repo.created_at }}</p>
            </div>
            <p>Link: <a class="links" :href="repo.html_url">
                    {{ repo.html_url }}</a>
            </p>

        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            repo: {},
        };
    },
    async created() {
        await new Promise((resolve) => setTimeout(resolve, 1000));
        const response = await fetch(
            `https://api.github.com/repositories/${this.$route.params.id}`
        );
        const data = await response.json();
        this.repo = data;
    },
    methods: {
        redirectToHome() {
            this.$router.push("/");
        },
    },
    mounted() { },};
</script>
  
<style lang="scss" scoped>
@use 'sass:math';

/* variables*/
$primary: #6d4417;
$base-gap: 30px;
$text-color: #020C18;
$background: #ffdcc2;
$breakpoint-miniphone:500px;


.repos-container {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 30vh 0;



    .repos {
        background-color: $background ;
        padding: $base-gap*1.5 $base-gap;
        border-radius: 6px;
        border: 1px solid rgba(169, 114, 31, 0.15);


        .btn {
            cursor: pointer;
            color: $primary;
            font-weight: 650;
            font-size: 15px;
            text-align: left;
        }

        h1 {
            font-weight: 600;
            font-size: 20px;
            text-align: center;
            color: $text-color;
            margin: 50px 0;
        }

        .desc {
            text-align: center;
            color: #616161;
        }

        .space {
            display: flex;
            justify-content: space-between;

            .fa-code,
            .fa-eye,
            .fa-calendar-days {
                color: $primary;
                font-size: 18px;
            }

            .details {
                font-weight: 600;
                font-size: 16px;

            }
        @media(max-width : $breakpoint-miniphone){
            justify-content: center;
            gap: $base-gap/3;
        }
        }

        .links{
            text-decoration: none;
            color: $primary;
            font-size: 17px;

            &:hover{
                text-decoration: underline;
            }
        }
    }
}
</style>
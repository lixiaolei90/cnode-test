<template>
    <div>
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif" alt="">
        </div>
        <div class="posts">
            <ul>
                <li>
                     <div class="toobar">
                    <span>全部</span>
                    <span>精华</span>
                    <span>分享</span>
                    <span>问答</span>
                    <span>招聘</span>
                     </div>

                </li>
                <li v-for="post in posts">
                    <img :src="post.author.avatar_url" alt="">
                    <span>
                        <span class="reply_count">{{post.reply_count}}</span>
                        /{{post.visit_count}}
                    </span>
                    <!-- <span :class="[ 
                    {put_good:(put_good == true)}, 
                    {put_top:(put_top == true)},
                    {topiclist-tab:(put_good != true && put_top != true)}
                    ]"> -->
                       
                           {{post | tabFormatter}}
                          
                    <!-- </span> -->
                    <span>
                        {{post.title}}
                    </span>
                    <span class="last_reply">
                        {{post.last_reply_at | formatDate}}
                    </span>
                </li>
            </ul>
        </div>
    </div>
</template>    

<script>
export default {
    name: "PostList",
    data() {
        return {
            isLoading: false,
            posts:[]
        }
    },
    methods: {
       getData(){
           this.$http.get('https://cnodejs.org/api/v1/topics', {
               page:1,
               limit:20
           })
            .then(res=>{
                this.isLoading = false;
                this.posts = res.data.data;
            })
            .catch(function(err) {
                console.log(err);
            })
       } 
    },
    beforeMount(){
        this.isLoading = true;
        this.getData();
    }
}
</script>

<style scoped>
    img {
        width: 30px;
        height: 30px;
    }
    ul li:not(:first-child) {
        padding: 9px;
        font-size: 15px;
        font-family: "Helvetica Neus", "Luxi Sans", "DejaVu Sans", Tahoma;
        font-weight: 400;
        background-color:white;
        color: #333;
        border-top: 1px solid #f0f0f0;
    }
    li:not(:first-child):hover {
        background: #f5f5f5;
    }
</style>
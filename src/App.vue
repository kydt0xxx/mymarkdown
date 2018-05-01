<template>
    <div id="app">
        <!-- isLoginの状態に応じてcomponents:(HomeかEditor)を表示する -->
        <Home v-if="!isLogin"></Home>
        <Editor v-if="isLogin"></Editor>
    </div>
</template>

<script>
import Home from './components/Home.vue';
import Editor from './components/Editor.vue';

export default {
    name: 'app',
    data () {
        return {
            isLogin: false
        }
    },
    //createdは「Vue.jsがそのコンポーネントを作成したタイミングで実行される。」
    created: function() {
        firebase.auth().onAuthStateChanged(user => {
            console.log("Check user :" + user);
            if (user) {
                this.isLogin = true;
            } else {
                this.isLogin = false;
            }    
        })
    },
    components:{
        //タグ名: 読み込んだvueファイル(importエイリアス)
        'Home': Home,
        'Editor': Editor,
    },
}
</script>

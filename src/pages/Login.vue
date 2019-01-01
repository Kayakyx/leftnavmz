<template>
    <div class="login">

      <button @click="loginYes">点击登录</button>

    </div>
</template>

<script>
    export default {
        name: "Login",
        //在 router-view 上传过来的 title
        props: ['title'],
        methods: {
          loginYes(){
            sessionStorage.setItem('isLogin',1);
            this.$router.push({path: '/mine'});
          }
        },
        /*
        //有bug 这里如果已经在登录页了 再点击 我的  这里就不会执行了， 所以title会乱掉（在登录页也会显示 ‘我的’）。
        //改用 局部路由拦截   的  j进入钩子
        */
        //最终解决方案为 created 配合 watch监听 解决了。
        created(){
          this.$emit('update:title', '登录');
        },

        watch: {
          title: function (val, oldval) {
            console.log(val, oldval);
            this.$emit('update:title', '登录');
          }
        },

        // mounted(){
        //   // console.log(this.title);
        // }
/*

      //进过一番测试发现这样还是不行  (；′⌒`)
      beforeRouteEnter(to, from, next){
        // console.log(this);  //注意所有的路由钩子 ，只有 beforeRouteEenter 内 this 是undefined
        // 不！能！获取组件实例 `this`
        // 因为当守卫执行前，组件实例还没被创建
        //不过，你可以通过传一个回调给 next来访问组件实例。在导航被确认的时候执行回调，并且把组件实例作为回调方法的参数。
/!*
        // console.log(to,from , next);
        this.$emit('update:title', '登录'); //  这种写法会 失败。错误代码
        next();//放行
        *!/

        //经过测试这样还是失败了。
        next(vm => {
          // 通过 `vm` 访问组件实例
          // console.log(vm);
          let title = vm.title;

          // console.log(title);
            vm.$emit('update: title', '登录');
            console.log(vm.title);
        })


      }
*/




    }
</script>

<style scoped>
    .login{

      width: 100%;
      height: 100%;
      padding-top: 2rem;
      background-color: antiquewhite;
      text-align: center;
    }

    .login button{
      font-size: .6rem;
    }

</style>

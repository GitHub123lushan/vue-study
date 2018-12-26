# 生命周期钩子 #
	 <div id="app">
        {{msg}}
        <p v-text="info()"></p>
        <a href="#">{{msg|msginfo}}</a>
        <input type="text" v-focus>
    </div>
    <script>
        var vm = new Vue({
            el: "#app",
            data: {
                msg: 123, //要使用的数据
            },
            methods: { //定义函数
                info() {
                    return "112"
                }
            },
            filters: { //定义过滤器
                msginfo(msg) {
                    return "过滤后的结果"
                }
            },
            directives: {// 指令的定义
                focus: {//全写方式
                    
                    inserted: function (el) {
                        el.focus()
                        console.log(el)
                    }
                },
                color(el){//简写形式 包含 bind 和update
                    el.style.color="blue"
                }
            },
            beforeCreate () {
                //vm实力对象初始化之后,但data和methods还没配置(此时不能发送ajax请求)
            },
           created () {
               //vm实力对象初始化完成之后,data和methods以及配置完成(此时最适合发送ajax请求)
           },
           beforeMount () {
               //数据挂载到dom树上之前的函数
           },
           mounted () {
               //数据已经完全挂载到dom树上
           },
           beforeUpdate () {
               //数据已经更新 但界面没有更新
           },
           updated () {
               //数据和界面都完全更新完全
           },
           beforeDestroy () {
               //vue实力已经从运行阶段进入到销毁阶段
           },
           destroyed () {
               //vue已经销毁
           }
        })
    </script>

# 过滤器 #
  * 调用格式


	  	{{ name | "过滤器名称" }} 
		<p :id="rowId | formotId">

   
* 定义全局过滤器:

		vue.filter("过滤器名称",(name)=>{
			return "返回过滤后的结果"
		
		})
		


 * 定义局部过滤器:


		filters : {
	
			formotId (rowId) {
				return "返回过滤后的结果"
			}

		}

## 注意: ##
	函数的形参和实参可以有多个定义多个  例: {{ a | b(c,d) }}
	
	filters: { b (a,b,c){ return "过滤后的结果"} } 
	
	形参第一个是a,第二个是b,第三个是c



# 自定义按钮修饰符 #
	
     Vue.config.keyCodes.f1 = 112 //定义
	v-on:keyup.f1  //使用

# 自定义指令 #

* 定义全局指令:


		Vue.directive('focus',{

			bind(el) {
				//当指令被绑定到标签上的时候执行该函数,只执行一次
			},
			inserted (el){
				//当被绑定元素插入到dom中的时候执行,只执行一次

			},
			update(el){
				//当vnode更新的时候执行,只执行一次
			}
		})


		directives:{
			'focus':{

			bind(el) {
				//当指令被绑定到标签上的时候执行该函数,只执行一次
				},
			inserted (el){
				//当被绑定元素插入到dom中的时候执行,只执行一次

				},
			update(el){
				//当vnode更新的时候执行,只执行一次
				}
			}
		}

### 简写: ###
	 	Vue.directive('focus',(el)=>{
			//只包含bind和update
		})
		
		directives : {
			focus (el) {
				//只包含bind和update
			}
		}
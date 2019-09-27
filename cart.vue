<template>
    <div 
    class="cart"
    @mouseenter="cartShow"
    @mouseleave="cartNo"
    > 
        <div class="cw_icon">
            <i class="iconfont left">&#xe604;</i>
            <span class="count">{{allNum}}</span>
            <a href="javascript:void(0);">我的购物车</a>
            <i class="iconfont right">&#xe6ec;</i>
        </div>
        <div :class="['dropdown-layer', flag==false? 'noshow':'show']">
            <div class="space"></div>
            <div v-if="cartList.length" class="settle-box">
                <div class="title"> 
                    <h4>最新加入的商品</h4>
                </div>
                <div class="content" v-for="(item, index) in cartList" :key="index">
                    <ul class="mcart-sigle">
                        <li class="mcart-con">
                            <div>
                                <a href="" class="mcart_item">
                                    <img :src="item.img" alt="">
                                    <span>{{item.desc}}</span>
                                </a>
                            </div>
                            <div class="price">
                                <div><strong>￥{{item.cost}}</strong>x{{item.num}}</div>
                                <div class="delete" @click="orderDelete(index)">删除</div>
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="foot_fixed">
                    <div class="cart_bottom">
                        <div>共<strong>{{allNum}}</strong>件商品</div>
                        <div>共计<strong class="total">￥{{total}}</strong></div>
                        <a class="go-cart" href="">去购物车</a>
                    </div>
                </div>
            </div>
            <div v-else class="settle-box">
                <div class="title"> 
                    <h4>最新加入的商品</h4>
                </div>
                <div class="cart-empty">
                   <i class="iconfont">&#xe62a;</i>
                   <p>你的购物车还是空的</p>
                </div>
                <div class="foot_fixed">
                    <div class="cart_bottom">
                        <div>共<strong>{{allNum}}</strong>件商品</div>
                        <div>共计<strong class="total">￥{{total}}</strong></div>
                        <a class="go-cart" href="">去购物车</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>
   
   .cart{
       display: flex;
       flex-direction: column;
       justify-content: space-around;
       align-items: center;
       & .cw_icon{
            width: 150px;
            height: 34px;
            border: 1px solid #DFDFDF;
            background: #F9F9F9;
            text-align: center;
            line-height: 34px;
            font-size: 12px;
            position: relative;
            &:hover{
                background: #fff;
                border: 1px solid #ddd;
                box-shadow: 0 0 5px rgba(0,0,0,.2);
            }
            & .iconfont{
                padding: 0 6px;
            }
            & span{
                background-color: #c81623;
                display: block;
                position: absolute;
                top: -8px;
                right: 20px;
                border-radius: 50%;
                line-height: 16px;
                padding: 2px 3px;
                color: #Fff;
                transform: rotateZ(-14deg);
            }
            & a{
                color: #666;
                line-height: 34px;
                padding-right: 6px;
            }
             & a:hover{
                 color: #f30213;
             }
           & .left{
               color: #c81623;
           }
           & .right{
               color: #999;
               float: right;
           }
       }
        .dropdown-layer{
            position: absolute;
            top: 40px;
            right: 0;
            width:320px;
            background: #fff;
            border: 1px solid #ddd;
            box-shadow: 0 0 5px rgba(0,0,0,.2);
            & .space{
                position: absolute;
                right: 0;
                top: -7px;
                width: 150px;
                height: 12px;
                background: #fff;
            }
            .settle-box{
                    max-height: 373px;
                    overflow: auto;
                    position: relative;
                    z-index: 2;
                    width: 100%;
                    background: #fff;
                     display: flex;
                    flex-direction: column;
                    justify-content: space-around;
                    .title{
                            text-align: left;
                            position: sticky;
                            background-color: #fff;
                            width: 100%;
                            top: -2px;
                            margin-bottom: 40px;
                        h4{
                            font-size:14px; padding:4px 3px;
                        }
                    }
                    .content{
                        padding: 10px 8px;
                        margin:10px 0;
                        background-color: #f5f5f5;
                         border:1px solid transparent;
                        &:hover{
                            background-color: #ffffff;
                            border:1px solid #f5f5f5;
                        }
                       .mcart-con{
                        display: flex;
                        flex-direction: row;
                        flex-wrap: nowrap;
                        justify-content: space-around;
                        align-items: flex-start;
                        
                        .mcart_item{
                            display: flex;
                            flex-direction: row;
                            flex-wrap: nowrap;
                            justify-content: space-between;
                            align-items: flex-start;
                            color: #666;
                            span{
                                padding:0 8px;
                                text-align: left;
                                font-size: 14px;
                            }
                        }
                        .price{
                            color:  #e4393c;
                            .delete{
                                color: #666;
                                font-size: 14px;
                                cursor: pointer;
                            }
                            .delete:hover{
                                    color:#e4393c;
                            }
                        }
                       } 
                    }
                    .foot_fixed{
                        position: sticky;
                        bottom: 0px;
                        .cart_bottom{
                         display: flex;
                        flex-direction: row;
                        flex-wrap: nowrap;
                        justify-content: space-around;
                        align-items: flex-start;
                        font-size: 12px;
                        padding: 6px 3px;
                        background-color: #f5f5f5;
                        .total{
                            color: #e4393c;
                        }
                        .go-cart{
                            font-size: 14px;
                            background-color: #e4393c;
                            color: #fff;
                            padding:2px 10px;
                        }
                    }}
                .cart-empty{
                    height: 100px;
                    .iconfont{
                        font-size: 52px;
                    }
                }    
            }
        }
   }
.show{
    display: flex;
}
.noshow{
    display: none;
}
</style>

<script>
export default {
    data(){
        return {
            allNum:0,
            total:0,
            flag:false,
            cartList:[{
                img:"https://img10.360buyimg.com/n5/jfs/t1/34687/29/1523/83595/5cb98e20Eace6accb/91f34a7ec6df6dbc.jpg",
                desc:"阿萨撒旦画说的佛收到货iOS多福is核对粉红色",
                cost:1234,
                num:3,
            },
            {
                img:"https://img10.360buyimg.com/n5/jfs/t1/34687/29/1523/83595/5cb98e20Eace6accb/91f34a7ec6df6dbc.jpg",
                desc:"阿萨撒旦画说的佛收到货iOS多福is核对粉红色",
                cost:1234,
                num:3,
            },
            {
                img:"https://img10.360buyimg.com/n5/jfs/t1/34687/29/1523/83595/5cb98e20Eace6accb/91f34a7ec6df6dbc.jpg",
                desc:"阿萨撒旦画说的佛收到货iOS多福is核对粉红色",
                cost:1234,
                num:3,
            },
            {
                img:"https://img10.360buyimg.com/n5/jfs/t1/34687/29/1523/83595/5cb98e20Eace6accb/91f34a7ec6df6dbc.jpg",
                desc:"阿萨撒旦画说的佛收到货iOS多福is核对粉红色",
                cost:1234,
                num:3,
            }
            ]
        }
    },
    mounted(){
        this.calculateNum();
    },
    methods:{
        orderDelete(index){
            console.log(index)
            this.cartList.splice(index, 1);
        },
         calculateNum(){
            if(this.cartList){
                 this.cartList.forEach((ele, index)=>{
                 this.allNum += this.cartList[index].num;
                 this.total += this.cartList[index].cost;
             })
            }
         },
         cartShow(){
             this.flag = true;
         },
        cartNo(){
            this.flag = false;
        }
    }
}
</script>

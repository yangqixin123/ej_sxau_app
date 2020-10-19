<template>
    <briup-fulllayout title="常用地址">
        <!-- <van-address-list
        v-model="chosenAddressId"
        :list="list"
        :disabled-list="disabledList"
        disabled-text="以下地址超出配送范围"
        default-tag-text="默认"
        @add="onAdd"
        @edit="onEdit"
        /> -->

        <van-list>
            <van-cell
                v-for="item in addresses"
                :key="item.id"
                :title="item.province+' '+item.city+' '+item.area+' '+item.address"
            />
        </van-list>
        <br>
        <van-button block type="primary" @click="toAddressEditHandler" >添加</van-button>
    </briup-fulllayout>
</template>

<script>
import { get } from '../../../http/axios';
import {mapState} from 'vuex'
export default {
    data(){
        return{
            addresses:[],
            // chosenAddressId: '1',
            // list: [
            //     {
            //     id: '1',
            //     name: '张三',
            //     tel: '13000000000',
            //     address: '浙江省杭州市西湖区文三路 138 号东方通信大厦 7 楼 501 室'
            //     },
            //     {
            //     id: '2',
            //     name: '李四',
            //     tel: '1310000000',
            //     address: '浙江省杭州市拱墅区莫干山路 50 号'
            //     }
            // ],
            // disabledList: [
            //     {
            //     id: '3',
            //     name: '王五',
            //     tel: '1320000000',
            //     address: '浙江省杭州市滨江区江南大道 15 号'
            //     }
            // ]

        }
    },

    computed:{//计算属性
        //将状态机中的user对象中的info对象获取到
      ...mapState("user",["info"])  
    },

    created(){
        this.loadAddress();
    },

    methods:{
        //  onAdd() {
        //     Toast('新增地址');
        // },

        // onEdit(item, index) {
        //     Toast('编辑地址:' + index);
        //  },

        //加载当前用户信息
        loadAddress(){
            let id=this.info.id; //当前用户的id
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.addresses=response.data;
            })
        },

        toAddressEditHandler(){
            //编程跳转
            this.$router.push("/manager/address_edit");
        }
    }
}

</script>
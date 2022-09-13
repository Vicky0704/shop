<script setup>
import { computed } from '@vue/reactivity';
import { ref,reactive } from 'vue';
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
// const count = ref(1)
const list = reactive([
    {id:1,Item_title:"MARNI",Item_main:"Blue Trunk Bag In Buffalo",Shipped_from:"Marni",Attributes_color:"Blue",Attributes_size:"One Size",Shipping_cost:15,value:1},
    {id:2,Item_title:"COMMON",Item_main:"White Achilles Retro Low Sneaker",Shipped_from:"Ssense",Attributes_color:"White",Attributes_size:"IT 36",Shipping_cost:485,value:1},
    {id:3,Item_title:"MAJE",Item_main:"ECLAIR Ethnic poncho",Shipped_from:"Maje",Attributes_color:"Grey",Attributes_size:"One Size",Shipping_cost:220,value:1}
])
const price = computed(()=>{
    let target = 0
    for(const item of list) target+=item.value*item.Shipping_cost
    return target
})
const sub=(index,val)=>{
    if( val == '-'){
        if(list[index].value>1)   list[index].value--;
    }
    else{
        list[index].value++;
    }
    
}
const remove=(index)=>{
    list.splice(index,1);
}
</script>

<template>
  <header>
    
  </header>

  <main>
        <div id="main">
            <div class="div1">
                <div><span class="t5">TEMPLATE</span></div>
                <div><a href="#"><span class="t1">SHOPPING BAG(</span><span class="t3">{{list.length}}</span><span class="t1">)</span></a></div>
            </div>
            <div class="div_t">
            <table class="table2">
                <tr>
                    <td colspan="2" class="t6">Your Shopping Bag</td>
                    <td></td><td></td><td></td><td></td>
                    <td><button class="button1">Continue Shopping</button></td>
                </tr>
                <tr class="t3 tr_line">
                    <td colspan="2" style="width: 400px;">Item</td>
                    <td style="width: 120px;">Shipped from</td>
                    <td style="width: 120px;">Attributes</td>
                    <td style="width: 120px;">Quantity</td>
                    <td style="width: 120px;">Shipping Cost</td>
                    <td style="width: 120px;">Price</td>
                </tr>
                <tr v-for="(item,index) of list" :key="item.id" class="tr_line">
                    <td style="width: 100px;"><img id="Item_img" width="100px" height="100px" /></td>
                    <td>
                        <div id="Item">
                            <p class="t1" id="Item_title">{{item.Item_title}}</p>
                            <p class="t1" id="Item_main">{{item.Item_main}}</p>
                            <p><a @click="remove(index)" class="t3" href="#">Remove</a></p>
                        </div>
                    </td>
                    <td id="Shipped_from" class="t1">{{item.Shipped_from}}</td>
                    <td id="Attributes">
                        <p><span class="t2">Color:</span><span class="t1">{{item.Attributes_color}}</span></p>
                        <p><span class="t2">Size:</span><span class="t1">{{item.Attributes_size}}</span></p>
                    </td>
                    <td id="Quantity"><button @click="sub(index,'-')" class="sub"><span class="t2">-</span></button><span class="t1" name="num">&emsp;{{item.value}}&emsp;</span><button @click="sub(index,'+')" class="add"><span class="t2">+</span></button></td>
                    <td id="Shipping_Cost">
                        <span class="t2">Est. shipping:</span><br>
                        <span class="t1">${{item.Shipping_cost}}.00</span>
                    </td>
                    <td id="Price"><div class="t1">${{computed(()=>item.value*item.Shipping_cost)}}.00</div></td>
                </tr>
            </table>
            </div>
            <div class="div1 div3">
                <div style="width: 760px;">
                    <p><div class="t3">Accepted payment options:</div></p>
                    <p><img width="200px" height="30px" /></p>
                    <p></p><br>
                    <p><button class="button1">Continue Shopping</button></p>
                </div>
                <div style="width: 240px;">
                    <p class="div2"><span class="t3">Subtotal:</span><span id="Subtotal" class="t1" style="margin-right:5px;">${{price}}.00</span></p>
                    <p class="div2"><span class="t3">Estimated Shipping:</span><span id="Estimated_Shipping" class="t1" style="margin-right:5px;">$15.00</span></p>
                    <p class="div2"><span class="t3">Totle:</span><span id="Total" class="t4" style="margin-right:5px;">$2880.00</span></p>
                    <button class="button2">Secure Checkout</button>
                </div>
            </div>
        </div>
    </main>
</template>



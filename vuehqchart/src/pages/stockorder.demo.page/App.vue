<template>
    <div id="app2" >
        <div style="height:300px; width:500px;">
            <StockOrder ref='stockorder' DefaultSymbol='SHA.ci' :DefaultOrderFiled='OrderFiled' :DefaultOrder='Order'/>
        </div>
    </div>
</template>

<script>

import StockOrder from '../../jscommon/umychart.vue.components/stockorder.vue'


var TEST_DATA=
[
    {OrderFiled:StockOrder.STOCK_FIELD_NAME.INCREASE, Order:-1}, //涨幅排名
    {OrderFiled:StockOrder.STOCK_FIELD_NAME.INCREASE, Order:1}, //跌幅排名

    {OrderFiled:StockOrder.STOCK_FIELD_NAME.RISEFALLSPEED_5, Order:-1}, //5分钟涨速排名
    {OrderFiled:StockOrder.STOCK_FIELD_NAME.RISEFALLSPEED_5, Order:1}, //5分钟跌速排名

    {OrderFiled:StockOrder.STOCK_FIELD_NAME.MINUTE_AMPLITUDE_5, Order:-1}, //5分钟振幅排名

    {OrderFiled:StockOrder.STOCK_FIELD_NAME.MINUTE_AMOUNT_5, Order:-1}, //5分钟成交金额排名
]

export default 
{
    
    data () 
    {
        return {
            OrderFiled:TEST_DATA[5].OrderFiled,
            Order:TEST_DATA[5].Order,
        }
    },   

    components: { StockOrder },

    created:function()
    {
        
    },

    mounted:function()
    {
        
    },


    methods:
    {
        OnChangeSymbol:function(symbol)
        {

        },
        
    }
}

</script>

<style>

  
</style>

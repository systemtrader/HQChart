<!-- 
    画笔工具组件
  !-->

<template>
    <div id="toolBox" v-if="isShowBrushTool">
        <ul>
            <!-- 关闭 -->
            <li class="closeBtn">
                <svg class="icon icon-close" aria-hidden="true" @click="closeBtn">
                    <use xlink:href="#icon-guanbi"></use>
                </svg>
                <!-- <i class="el-icon-close" @click="closeBtn"></i> -->
            </li>
            <!-- 图标 -->
            <li v-for="item in toolList1" :key="item.name" :class="addBackgroundColor(item.name)">
                <svg class="icon icon-style" aria-hidden="true" @click="clickIcon(item.name)">
                    <use :href="item.icon"></use>
                </svg>
            </li>
            <li class="line-style"></li>
            <li
                    v-for="item in toolList2"
                    :key="item.name"
                    class="icon-box"
                    :class="addBackgroundColor(item.name)"
            >
                <svg class="icon icon-style" aria-hidden="true" @click="clickIcon(item.name)">
                    <use :href="item.icon"></use>
                </svg>
            </li>
            <li class="line-style"></li>
            <li v-for="item in toolList3" :key="item.name" :class="addBackgroundColor(item.name)">
                <svg class="icon icon-style" aria-hidden="true" @click="clickIcon(item.name)">
                    <use :href="item.icon"></use>
                </svg>
            </li>
            <li class="line-style"></li>
            <li v-for="item in toolList4" :key="item.name" :class="addBackgroundColor(item.name)">
                <svg class="icon icon-style" aria-hidden="true" @click="clickIcon(item.name)">
                    <use :href="item.icon"></use>
                </svg>
            </li>
        </ul>
    </div>
</template>

<script>
    import "../umychart.resource/font/brushSymbol.js";
    import "../umychart.resource/font/fontSymbol.css";

    import Vue from "vue";
    import ElementUI from "element-ui";
    import "../../../node_modules/element-ui/lib/theme-default/index.css";
    import locale from "../../../node_modules/element-ui/lib/locale/lang/en";

    Vue.use(ElementUI, {locale});

    export default {
        name: "Stockdrawtool",
        data() {
            return {
                isShowBrushTool: true,
                clickName: "",
                toolList1: [
                    {name: "线段", icon: "#icon-xianduan"},
                    {name: "射线", icon: "#icon-shexian"},
                    {name: "趋势线", icon: "#icon-qushixian"},
                    {name: "水平线", icon: "#icon-shuipingxian"},
                    {name: "平行线", icon: "#icon-pinghangxian"},
                    {name: "平行通道", icon: "#icon-pinghangtongdao"},
                    {name: "价格通道线", icon: "#icon-jiagetongdaoxian"},
                    {name: "M头W底", icon: "#icon-MtouWdi"}
                ],
                toolList2: [
                    {name: "圆弧线", icon: "#icon-yuanhuxian"},
                    {name: "矩形", icon: "#icon-juxing"},
                    {name: "平行四边形", icon: "#icon-pinghangsibianxing"},
                    {name: "三角形", icon: "#icon-sanjiaoxing"},
                    {name: "圆", icon: "#icon-yuan"},
                    {name: "对称角度", icon: "#icon-duichengjiaodu"}
                ],

                toolList3: [
                    {name: "江恩角度线", icon: "#icon-jiangenjiaoduxian"},
                    {name: "斐波那契周期线", icon: "#icon-feibonaqizhouxian"},
                    {name: "阻速线", icon: "#icon-zusuxian"},
                    {name: "黄金分割", icon: "#icon-huangjinfenge"},
                    {name: "百分比线", icon: "#icon-baifenbixian"},
                    {name: "波段线", icon: "#icon-boduanxian"}
                ],

                toolList4: [
                    {name: "文本", icon: "#icon-wenben"},
                    {name: "icon-arrow_up", icon: "#icon-xiangshangjiantou"},
                    {name: "icon-arrow_down", icon: "#icon-xiangxiajiantou"},
                    {name: "icon-arrow_right", icon: "#icon-xiangyoujiantou"},
                    {name: "icon-arrow_left", icon: "#icon-xiangzuojiantou"},
                    {name: "全部删除", icon: "#icon-shanchu"}
                ]
            };
        },
        mounted: function () {
            this.toolBoxHandle();
        },
        methods: {


            toolBoxHandle() {

                ///用以获取滚动条的距离
                let getStyle = function (obj, name) {
                    if (obj.currentStyle) {
                        return obj.currentStyle[name];
                    }
                    else {
                        return getComputedStyle(obj, false)[name];
                    }
                };

                let toolBox = document.getElementById("toolBox");
                //鼠标按下坐标
                let x = 0;
                let y = 0;
                //div左部和顶部的偏移量
                let l = 0;
                let t = 0;
                //屏幕大小
                let w = 0;
                let h = 0;
                //div宽度、高度 2为变宽(border)
                let tw = parseInt(getStyle(toolBox, 'width')) + 2;
                let th = parseInt(getStyle(toolBox, 'height')) + 2;
                let isDown = false;
                //鼠标按下事件
                toolBox.onmousedown = function (e) {
                    //获取x坐标和y坐标
                    x = e.clientX;
                    y = e.clientY;

                    w = document.documentElement.clientWidth;
                    h = document.documentElement.clientHeight;
                    //获取左部和顶部的偏移量
                    l = toolBox.offsetLeft;
                    t = toolBox.offsetTop;

                    //开关打开
                    isDown = true;
                    //设置样式
                    toolBox.style.cursor = "move";

                };
                //鼠标移动
                document.onmousemove = function (e) {

                    // 鼠标未按下不获取
                    if (!isDown) {
                        return;
                    }
                    //获取x和y
                    let nx = e.clientX;
                    let ny = e.clientY;
                    //计算移动后的左偏移量和顶部的偏移量
                    let nl = nx - (x - l);
                    let nt = ny - (y - t);
                    // 父组件的顶部高度
                   let upperHight = 0;
                    //判断是否越界
                    nl = nl < 0 ? 0 : (nl > w - tw ? w - tw : nl);
                    nt = nt < 0 ? 0 : (nt > h - th ? h - th - upperHight : nt) ;
                    toolBox.style.left = nl + "px";
                    toolBox.style.top = nt + "px";
                };
                //鼠标抬起事件
                toolBox.onmouseup = function () {
                    //开关关闭
                    isDown = false;
                    toolBox.style.cursor = "default";
                };

            },

            // 关闭画笔工具
            closeBtn() {
                this.isShowBrushTool = false;
                this.$emit("isShowBrushTool", this.isShowBrushTool);
            },
            // 点击图标
            clickIcon(iconName) {
                this.clickName = iconName;
                this.$emit("CurrentIcon", iconName);
            },
            addBackgroundColor(name) {
                if (name === this.clickName) {
                    return "icon-color";
                }
            }
        }
    };
</script>


<style lang="scss" type="text/scss">
    #toolBox {
        width: 115px;
        height: 516px;
        border: 1px solid #dadada;
        position: absolute;
        z-index: 9999999999999;
        background: #fff;
        ul {
            padding: 5px 0;
            .icon-color {
                background: #d9e9f9;
            }
            .closeBtn {
                width: 100%;
                height: 30px;
                text-align: right;
                color: #8696a4;
                margin-left: 0;
            }
            li {
                list-style: none;
                margin-left: 17px;
                float: left;
                .icon-style {
                    font-size: 21px;
                    text-align: center;
                    padding: 5px;
                }
                .icon-close {
                    font-size: 18px;
                    text-align: center;
                    padding-top: 5px;
                    padding-right: 10px;
                }
            }
            .line-style {
                width: 87px;
                height: 1px;
                display: block;
                background: #e3e7ea;
                margin: 10px 14px;
            }
        }
    }
</style>
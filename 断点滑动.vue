<template>
    <div>
        <div ref="my" class="box" @touchstart="touchStart">
            <div class="head">
                <div class="avatar" />
                <text class="username">HACKER</text>
            </div>

            <div class="content">
                <text class="desc">Google announced a new version of Nearby Connections for fully offline.highbandwidth peer to peer device communications.</text>
            </div>

            <div class="footer">
                <text class="action">SHARE</text>
                <text class="action" style="color:#7C4DFF">EXPLORE</text>
            </div>
        </div>
    </div>
</template>

<script>
import Binding from 'weex-bindingx';
import Nat from 'natjs';
/**
 * 
 * 
 */
export default {
    data() {
        return {
            x: 0,
            y: 0,
            isInAnimation: false,
            gesToken: 0,
            opacity: 1
        }
    },
    methods: {
        touchStart() {
            var my = this.$refs.my.ref; // 带上 ref
            var gesTokenObj = Binding.bind({
                anchor: my,
                eventType: 'pan',
                props: [
                    {
                        element: my, 
                        property: 'transform.translateX',
                        expression: `x+${this.x}` // x 横向偏移量，如果end后没有保存设置位置，第二次滑动会出现跳动，因为x只是手势的偏移量。右滑为正，左滑为负，下滑为正，上滑为负
                    }
                ]
            }, (e) => {
                if (e.state === 'end') {
                    this.x += e.deltaX;
                    this.y += e.deltaY;
                }
            });
        }
    }
}
</script>

<style>
.box {
    width: 680px;
    height: 450px;
    background-color: #651FFF;
}
.head {
    background-color: #651FFF;
    width: 680px;
    height: 120px;
    flex-direction: row;
    align-items: center;
}
.content {
    width: 680px;
    height: 240px;
    background-color: #651FFF;
    padding-left: 24px;
    padding-top: 24px;
    padding-right: 24px;
    box-sizing: border-box;
}

.footer {
    width: 680px;
    height: 90px;
    background-color: #fff;
    align-items: center;
    justify-content: flex-end;
    padding-right: 25px;
    flex-direction: row;
    box-sizing: border-box;
}
</style>


### uniapp使用 uni.pageScrollTo无法生效

```js
setTimeout(()=>{
    uni.pageScrollTo({
        scrollTop: 2000000,
        duration : 0
    })
},50)
```



### 使用注意事项

- 在APP端使用时不能使用selector
- 在小程序中使用时，selector不能使用纯数字作为id，最好使用英文小写字母
- app端使用duration必须设置为0
- app端使用时最好放在延时函数之中
- 在view中使用uni.pageScrollTo不能设置固定高度，否则会不起作用
- 在view中使用v-for需要注意页面加载顺序以及是否存在使用null数据进行页面渲染，一旦出错也会造成uni.pageScrollTo失效
- uni生命周期先把子组件加载完了逐级往上走 最后挂主页面(在子页面上加载时emit 在主页面监听听不到）

### view和scroll-view的坑

- scroll-view中不设置顶部会造成列表信息循环滚动，同时onPullDownRefresh方法失效

- 在iOS中会有fixed定位在底部失效的问题，此时需要把content的view设置为absolute，
   footer的view设置为fixed。这样在滑动content的滚动条时就不会带着下部fixed定位的view一起滑动

  

  
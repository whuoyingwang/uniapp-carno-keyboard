# uniapp-carno-keyboard
uniapp框架下的自定义车牌键盘插件

## 使用方法

在`script`中引入组件
```
import carnoKeyboard from '@/components/carno-keyboard/carno-keyboard.vue'
  export default {
    ......
    components: {carnoKeyboard},
    ......
  }
```

在`template`中使用组件
```
<carnoKeyboard :showKeyboard.sync="modalShow" @kInput="onInput" @kDelete="onDelete" @kConfirm="onConfirm" @kClose="onClose"></carnoKeyboard>
```

```
export default {
  data() {
    return {
      carNo: '',
      modalShow: false
    }
  },
  components: {carnoKeyboard},
  methods: {
    showCarNo () {
      this.modalShow = true
    },
    onInput (item) {
      this.carNo += item
    },
    onDelete () {
      this.carNo = this.carNo.substr(0, this.carNo.length - 1)
    },
    onConfirm () {
      uni.showModal({
        content: this.carNo,
        showCancel: false
      })
    },
    onClose () {
      this.modalShow = false
    }
  }
}
```

## 属性说明
属性名 | 类型 | 默认值 | 说明
:-:   | :-:  |   :-: | :-:
showKeyboard | Boolean | false | 是否显示输入框。 推荐使用 .sync 修饰该参数。否则将需要使用kClose方法来自定义关闭

## 事件说明
事件名 | 说明
:-:   | :-:
kInput | 点击键盘返回输入结果。将返回当前点击的内容value。使用方法kInput (item) {}
kDelete | 点击键盘 删除 按钮时，触发该事件。无参数。
kConfirm | 点击键盘 确认 按钮时，触发该事件。无参数。
kClose | 自定义关闭事件，点击蒙层或确认按钮之后，动画完成后会触发改事件。
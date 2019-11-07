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
<carnoKeyboard :showKeyboard.sync="modalShow" @onInput="onInput" @onDelete="onDelete" @onConfirm="onConfirm" @onClose="onClose"></carnoKeyboard>
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
<table border="1">
  <tr>
    <th>属性名</th>
    <th>类型</th>
    <th>默认值</th>
    <th>说明</th>
  </tr>
</table>
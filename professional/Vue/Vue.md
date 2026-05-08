明白了！你希望我用 Vue 3 的 **`<script setup>` 语法糖** 来重新梳理 Vue 2 中常见的响应式变量、props、emits、生命周期等写法，对吧？

下面我会从 Vue 2 的常见写法出发，**逐项对比并转换为 `<script setup>` 的写法**，帮助你快速过渡到 Vue 3 的现代写法。

---

## ✅ 一、声明响应式变量

### Vue 2（Options API）

```js
export default {
  data() {
    return {
      count: 0,
      message: 'Hello Vue'
    }
  }
}
```

### Vue 3（Composition API - `<script setup>`）

```vue
<script setup>
import { ref, reactive } from 'vue'

const count = ref(0)
const state = reactive({
  message: 'Hello Vue 3'
})
</script>
```

- `ref()`：用于基本类型，如 `count`
- `reactive()`：用于对象或嵌套结构，如 `state`

---

## ✅ 二、接收 props

### Vue 2（Options API）

```js
export default {
  props: ['title', 'items']
}
```

### Vue 3（Composition API - `<script setup>`）

```vue
<script setup>
const props = defineProps(['title', 'items'])
</script>
```

或者使用对象形式：

```js
defineProps({
  title: String,
  items: Array
})
```

> ✅ 不需要导入任何函数，`defineProps()` 是 `<script setup>` 中的编译器宏。

---

## ✅ 三、触发事件（emits）

### Vue 2（Options API）

```js
export default {
  methods: {
    handleClick() {
      this.$emit('update', 'new value')
    }
  }
}
```

### Vue 3（Composition API - `<script setup>`）

```vue
<script setup>
const emit = defineEmits(['update'])

function handleClick() {
  emit('update', 'new value')
}
</script>
```

> ✅ 同样不需要引入函数，`defineEmits()` 是内置的宏。

---

## ✅ 四、生命周期钩子函数

### Vue 2（Options API）

```js
export default {
  mounted() {
    console.log('Component mounted')
  },
  updated() {
    console.log('Component updated')
  }
}
```

### Vue 3（Composition API - `<script setup>`）

```vue
<script setup>
import { onMounted, onUpdated } from 'vue'

onMounted(() => {
  console.log('Component mounted')
})

onUpdated(() => {
  console.log('Component updated')
})
</script>
```

常用生命周期对应如下：

| Vue 2            | Vue 3 (`<script setup>`) |
|------------------|---------------------------|
| beforeCreate     | setup()                   |
| created          | setup()                   |
| beforeMount      | onBeforeMount             |
| mounted          | onMounted                 |
| beforeUpdate     | onBeforeUpdate            |
| updated          | onUpdated                 |
| beforeUnmount    | onBeforeUnmount           |
| unmounted        | onUnmounted               |

---

## ✅ 五、完整示例对比

### Vue 2 示例

```js
export default {
  props: ['title'],
  data() {
    return {
      count: 0
    }
  },
  mounted() {
    console.log('Mounted')
  },
  methods: {
    increment() {
      this.count++
      this.$emit('update', this.count)
    }
  }
}
```

### Vue 3 `<script setup>` 版本

```vue
<script setup>
import { ref, onMounted } from 'vue'

// 接收 props
const props = defineProps(['title'])

// 定义 emits
const emit = defineEmits(['update'])

// 响应式数据
const count = ref(0)

// 生命周期
onMounted(() => {
  console.log('Mounted')
})

// 方法
function increment() {
  count.value++
  emit('update', count.value)
}

// 暴露给模板
defineExpose({ count, increment }) // 可选：如果你需要 expose 给父组件调用
</script>

<template>
  <h1>{{ title }}</h1>
  <p>Count: {{ count }}</p>
  <button @click="increment">Increment</button>
</template>
```

---

## ✅ 总结：Vue 2 到 Vue 3 `<script setup>` 转换对照表

| 功能         | Vue 2 写法                    | Vue 3 `<script setup>` 写法                      |
|--------------|-------------------------------|--------------------------------------------------|
| 响应式变量   | `data()`                      | `ref()` / `reactive()`                           |
| 接收 props   | `props: []`                   | `defineProps()`                                  |
| 触发事件     | `this.$emit()`                | `defineEmits()` + `emit()`                       |
| 生命周期     | `mounted`, `updated` 等       | `onMounted`, `onUpdated` 等                     |
| 模板绑定     | 返回 `data`                   | 在 `setup()` 中返回变量即可                      |
| 暴露方法/属性 | `methods`                    | 使用 `defineExpose()`                            |

---

如果你有具体的 Vue 2 组件代码，我可以帮你一步步转换成 `<script setup>` 写法 😄  
也可以根据你的需求提供更详细的迁移建议。欢迎继续提问！
<script setup>
import { ref } from 'vue'

const items = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20,
    isEdit: false
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '香濃奶茶搭配QQ珍珠',
    price: 45,
    stock: 18,
    isEdit: false
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34,
    isEdit: false
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10,
    isEdit: false
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25,
    isEdit: false
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20,
    isEdit: false
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18,
    isEdit: false
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20,
    isEdit: false
  },
])
const tempName = ref('')

const edit = {
  on: (item) => {
    items.value.forEach(item => item.isEdit = false)
    const index = items.value.findIndex(i => i.id === item.id)
    items.value[index].isEdit = true
    tempName.value = item.name
  },
  save: (item) => {
    item.name = tempName.value
    items.value.forEach(item => item.isEdit = false)
  },
  cancle: (item) => {
    const index = items.value.findIndex(i => i.id === item.id)
    items.value[index].isEdit = false
  }
}

const changeStockNum = (item, action) => {
  if (action === 'plus') {
    item.stock += 1
  } else if (action === 'minus') {
    if (item.stock >= 1) item.stock -= 1
  }
}

</script>

<template>
  <h2>六角學院 2024 Vue 前端新手營</h2>
  <h3>Week1 作業 by Letitia</h3>
  <hr>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in items" :key="item.id">
        <td @dblclick="edit.on(item)">
          {{ item.isEdit ? '' : item.name }}
          <div class="edit" v-if="item.isEdit">
            <input type="text" v-model="tempName" >
            <button type="button" class="btn" @click="edit.save(item)">儲存</button>
            <button type="button" class="btn" @click="edit.cancle(item)">取消</button>
          </div>
          
        </td>
        <td><small>{{ item.description }}</small></td>
        <td>{{ item.price }}</td>
        <td>
          <button type="button" @click="changeStockNum(item, 'minus')">-</button>
          <div class="stock">
            {{ item.stock }}
          </div>
          <button type="button" @click="changeStockNum(item, 'plus')">+</button>
        </td>
      </tr>
    </tbody>
  </table>
  <hr>
  <p>💡對品項名稱點兩下即可編輯</p>
</template>

<style scoped>
td, tr {
  padding: 8px 20px;
}

.stock {
  display: inline-block;
  width: 50px;
  text-align: center;
}

.btn {
  margin-left: 10px;
}
</style>

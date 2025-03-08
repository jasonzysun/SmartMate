<!-- pages/groupList/groupList.vue -->
<template>
  <view class="container">
    <input
      placeholder="请输入新分组名称"
      v-model="newGroupName"
      @confirm="addGroup"
      style="width: 300px; margin-bottom: 10px;"
    />
    <button @click="addGroup">添加分组</button>
    
    <view class="group-list" style="margin-top: 20px;">
      <block v-for="group in groups" :key="group.id">
        <!-- 使用 navigator 组件实现页面跳转 -->
        <navigator :url="'/pages/taskList/taskList?groupId=' + group.id" hover-class="navigator-hover">
          <view class="group-item">{{ group.name }}</view>
        </navigator>
      </block>
    </view>
  </view>
</template>

<script setup lang="ts">
import { defineComponent, ref } from 'vue'
import { onLoad } from '@dcloudio/uni-app'
import { v4 as uuidv4 } from 'uuid'

interface Group {
  id: string
  name: string
}

const newGroupName = ref('')
const groups = ref<Group[]>([])

const addGroup = () => {
  if (newGroupName.value.trim() === '') return
  const newGroup: Group = {
	id: uuidv4(),
	name: newGroupName.value.trim()
  }
  groups.value.push(newGroup)
  newGroupName.value = ''
  // 使用 uni-app 内置存储 API 保存数据
  uni.setStorageSync('todo-groups', JSON.stringify(groups.value))
}

onLoad(() => {
  const data = uni.getStorageSync('todo-groups')
  if (data) {
	groups.value = JSON.parse(data)
  }
})
</script>

<style scoped>
.container {
  padding: 20px;
}
.group-item {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}
.navigator-hover {
  background-color: #f0f0f0;
}
</style>

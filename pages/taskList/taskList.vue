<!-- pages/taskList/taskList.vue -->
<template>
  <view class="container">
    <text class="title">{{ groupName }} - 待办任务</text>
    
    <view class="new-task">
      <input
        placeholder="任务名称"
        v-model="newTaskName"
        style="width: 300px; margin-bottom: 10px;"
      />
      <input
        placeholder="选择截止时间 (格式：YYYY-MM-DD HH:MM)"
        v-model="newTaskDeadline"
        style="width: 300px; margin-bottom: 10px;"
      />
      <textarea
        placeholder="任务备注"
        v-model="newTaskNote"
        style="width: 300px; margin-bottom: 10px;"
      ></textarea>
      <button @click="addTask">添加任务</button>
    </view>
    
    <view class="task-list" style="margin-top: 20px;">
      <block v-for="task in tasks" :key="task.id">
        <view class="task-item">
          <text>{{ task.name }}</text>
          <text>截止时间：{{ formatDate(task.deadline) }}</text>
          <text>备注：{{ task.note }}</text>
        </view>
      </block>
    </view>
    
    <navigator url="/pages/groupList/groupList" hover-class="navigator-hover">
      <text>返回分组列表</text>
    </navigator>
  </view>
</template>

<script setup lang="ts">
import { defineComponent, ref } from 'vue'
import { onLoad } from '@dcloudio/uni-app'
import { v4 as uuidv4 } from 'uuid'

interface Task {
  id: string
  name: string
  deadline: string | null
  note: string
}

interface Group {
  id: string
  name: string
}

const groupName = ref('分组')
const tasks = ref<Task[]>([])
const newTaskName = ref('')
const newTaskDeadline = ref('')
const newTaskNote = ref('')

// 获取页面传参（uni-app 中页面参数通过 onLoad 的 options 获取）
onLoad(function (options) {
  const groupId = options.groupId
  loadGroup(groupId)
  loadTasks(groupId)
})

const loadGroup = (groupId: string) => {
  const groupsStr = uni.getStorageSync('todo-groups')
  if (groupsStr) {
	const groups: Group[] = JSON.parse(groupsStr)
	const group = groups.find((g) => g.id === groupId)
	if (group) {
	  groupName.value = group.name
	}
  }
}

const loadTasks = (groupId: string) => {
  const tasksStr = uni.getStorageSync('tasks-' + groupId)
  if (tasksStr) {
	tasks.value = JSON.parse(tasksStr)
  }
}

const saveTasks = (groupId: string) => {
  uni.setStorageSync('tasks-' + groupId, JSON.stringify(tasks.value))
}

const addTask = () => {
  if (newTaskName.value.trim() === '') return
  // 获取当前页面参数 groupId
  const pages = getCurrentPages()
  const currentPage = pages[pages.length - 1]
  const groupId = currentPage.options.groupId
  const task: Task = {
	id: uuidv4(),
	name: newTaskName.value.trim(),
	deadline: newTaskDeadline.value.trim() || null,
	note: newTaskNote.value.trim()
  }
  tasks.value.push(task)
  newTaskName.value = ''
  newTaskDeadline.value = ''
  newTaskNote.value = ''
  saveTasks(groupId)
}

const formatDate = (dateStr: string | null) => {
  return dateStr ? dateStr : ''
}
</script>

<style scoped>
.container {
  padding: 20px;
}
.title {
  font-size: 20px;
  margin-bottom: 20px;
}
.task-item {
  padding: 10px;
  border-bottom: 1px solid #ddd;
  margin-bottom: 10px;
}
.navigator-hover {
  background-color: #f0f0f0;
}
</style>

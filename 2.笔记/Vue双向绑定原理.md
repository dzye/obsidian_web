1. vue2 Object.defindProperty,vue3 proxy


具体实现待补充

```
<template>

<div>

<div>你好，我是混圆AI</div>

<div>作为一个人工智能语言模型，我可以帮助你提高工作效率，为你提供有效信息</div>

<div>主题</div>

<el-radio-group class="template-select" v-model="templateType" @change="templateChange">

<el-radio-button :label="item.type" v-for="item in templateTypes" :key="item.type">{{ item.typeText }}</el-radio-button>

</el-radio-group>

<el-scrollbar class="chat-template">

<Waterfall :list="list">

<template #item="{ item }">

<div class="card add-btn" v-if="item.type == 'add-btn'" @click="dialogVisible = true">

<el-icon class="icon"><i-ep-circle-plus-filled /></el-icon>创建模版

</div>

<div v-else class="card">

<div class="header">

<div></div>

<div class="title">{{ item.title }}</div>

<div class="language"><el-tag size="small" type="info">{{ item.language }}</el-tag></div>

</div>

<p class="text">{{ item.language === 'CN' ? item.contentCN : item.contentEN }}</p>

<div class="footer"><el-button text type="primary">使用</el-button></div>

</div>

</template>

</Waterfall>

</el-scrollbar>

<el-dialog v-model="dialogVisible" title="创建模版" width="30%">

<el-form :model="templateForm" label-width="80px">

<el-form-item label="标题">

<el-input v-model="templateForm.title" placeholder="请填写"></el-input>

</el-form-item>

<el-form-item label="分类">

<el-select v-model="templateForm.type" placeholder="请选择">

<el-option

v-for="item in originalTemplateTypes"

:key="item.type"

:label="item.typeText"

:value="item.type"

/>

</el-select>

</el-form-item>

<el-form-item label="中文提问">

<el-input v-model="templateForm.cnContent" :rows="4" type="textarea" placeholder="请填写" />

</el-form-item>

<el-form-item label="英文提问">

<el-input v-model="templateForm.engContent" :rows="4" type="textarea" placeholder="请填写" />

</el-form-item>

</el-form>

<template #footer>

<span class="dialog-footer">

<el-button type="primary" @click="dialogVisible = false">

立即创建

</el-button>

</span>

</template>

</el-dialog>

</div>

</template>

  

<script setup lang="ts">

import { Waterfall } from 'vue-waterfall-plugin-next'

import 'vue-waterfall-plugin-next/dist/style.css'

import { getTemplateTypes,getFavoriteTemplates,getTemplateByType} from '@/api/template'

const templateType:any = ref('')

const dialogVisible:any = ref(false)

const templateTypes:any = ref([])

const originalTemplateTypes:any = ref([])

  

onMounted(() => {

getTemplateTypes().then((res: any) => {

originalTemplateTypes.value = res.data

templateTypes.value = [

{type: "MY_COLLECTION", typeText: "我的收藏"},...res.data]

})

getTemplates(templateType.value)

})

const templateForm = reactive({

title: '',

cnContent: '',

engContent: '',

type: ''

})

const getTemplates = (type:string) => {

if(type === 'MY_COLLECTION') {

getFavoriteTemplates().then((res: any) => {

list.value = res.data

})

}else{

getTemplateByType(type).then((res: any) => {

list.value = res.data

})

}

}

const templateChange = (val:string) => {

getTemplates(val)

}

const list = ref([

{

title: '公众号文章提问模版',

contentCN: '我需要一篇[xx类型的文 章】来展示我的[产品/服务】对[目标客户〕的价值，并说服他们在紧迫感中采取[期望的行动」。',

contentEN: 'I need a xx type article to demonstrate the value of mylproduct/ servicel to target customers/ and persuade them o таке expecte actions with a sense urgency.',

language: 'CN',

},

{

title: '小红书种草提问模版',

contentCN: '我需要一篇[xx类型的文 章】来展示我的[产品/服务】对[目标客户〕的价值，并说服他们在紧迫感中采取[期望的行动」。',

contentEN: 'Ineed a xx type article to demonstrate the value of mylproduct/ servicel to target customers/ and persuade them o таке expecte actions with a sense urgency.',

language: 'EN',

},

{

title: '知乎提问模版',

contentCN: '我需要一篇[xx类型的文 章】来展示我的[产品/服务】对[目标客户〕的价值，并说服他们在紧迫感中采取[期望的行动」。',

contentEN: 'I need a xx type article to demonstrate the value of mylproduct/ servicel to target customers/ and persuade them o таке expecte actions with a sense urgency.',

language: 'CN',

},

{

title: '微博提问模版',

contentCN: '我需要一篇[xx类型的文 章】来展示我的[产品/服务】对[目标客户〕的价值，并说服他们在紧迫感中采取[期望的行动」。',

contentEN: 'I need a xx type article to demonstrate the value of mylproduct/ servicel to target customers/ and persuade them o таке expecte actions with a sense urgency.',

language: 'CN',

},

{

type: 'add-btn',

}

])

</script>

<style scoped lang="scss">

.header {

display: flex;

justify-content: space-between;

align-items: center;

margin-bottom: 10px;

}

  

.card {

width: 90%;

height: 100%;

border: 1px solid #e2e2e2;

border-radius: 4px;

padding: 10px;

box-shadow: 0 2px 12px 0 rgba(0, 0, 0, .1);

  

.text {

margin: 0;

font-size: 14px;

line-height: 1.5;

color: #606266;

}

  

.footer {

text-align: right;

}

}

  

.add-btn {

display: flex;

justify-content: center;

align-items: center;

cursor: pointer;

  

.icon {

font-size: 20px;

margin-right: 5px;

}

}

  

.chat-template {

height: calc(100vh - 330px);

margin: 10px 0;

}

  

.template-select {

margin: 10px 0;

}

</style>
```
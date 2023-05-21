```
<template>

<view class="main">

<view class="textarea-box">

<u-input

height="300"

v-model="content"

type="textarea"

placeholder="说说照片背后的故事吧～比如孩子第一次独立上学/骑车/最美的全家郊游..."

maxlength="300"

:clearable="false"

/>

<view class="textarea-num">{{ content.length }}/300</view>

</view>

<view class="select-album" style="border-bottom: none">

<view class="select-item-start"><view>类型</view></view>

<view class="select-item-end">

<u-radio-group v-model="isImage" @change="typeChange">

<u-radio

icon-size="28"

label-size="28"

active-color="#6c86fa"

:name="1"

>图片</u-radio

>

<u-radio

icon-size="28"

label-size="28"

active-color="#6c86fa"

:name="0"

>视频</u-radio

>

</u-radio-group>

</view>

</view>

<view class="">

<jade-image-upload

:list="media"

:control="control"

:columnType="columnType"

:mediaType="isImage ? ['image'] : ['video']"

:maxCount="isImage ? 20 : 1"

:compressSize="compressSize"

:imageSize="imageSize"

@chooseFile="chooseFile"

@imgDelete="imgDelete"

></jade-image-upload>

</view>

<view class="tip">{{

isImage ? "*一次最多20张；照片格式：jpg、jpeg、png" : "*一次最多一段视频"

}}</view>

<view class="select-album" @click="selectCycle">

<view class="select-item-start">

<view class="icon iconfont icon-shangchuan"></view>

<view>发布到家庭圈</view>

</view>

<view class="select-item-end">

<view>

<view v-if="selected.length">

<image

v-for="item in selected"

:key="item.childMemberId"

:src="item.childAvatar"

class="min-avatar"

/>

</view>

<view v-else>请选择</view>

</view>

<view><image src="../../static/arrow.png"></image></view>

</view>

</view>

<view class="select-album" @click="selectAlbum" v-if="albumShow">

<view class="select-item-start">

<view class="icon iconfont icon-shangchuan"></view>

<view>上传到</view>

</view>

<view class="select-item-end">

<view>{{ albumTitle }}</view>

<view><image src="../../static/arrow.png"></image></view>

</view>

</view>

<u-popup

v-model="showSelectCycle"

mode="bottom"

border-radius="32"

height="600"

>

<view class="cycle-header">

<view class="cycle-cancel" @click="showSelectCycle = false">取消</view>

<view class="cycle-title">选择孩子</view>

<view class="cycle-query" @click="querySelect">确定</view>

</view>

<view class="select-all"

><u-checkbox

@change="allcheckedChange"

v-model="allchecked"

:name="all"

shape="circle"

>全部

</u-checkbox>

</view>

<view class="content">

<scroll-view scroll-y style="height: 300rpx">

<u-checkbox-group @change="checkboxGroupChange" shape="circle">

<u-checkbox

v-model="item.checked"

v-for="item in childrenData"

:key="item.childMemberId"

:name="item.childMemberId"

>

<view class="radio-label">

<view>

<image :src="item.childAvatar" />

</view>

<view class="name">{{ item.childName }}</view>

</view>

</u-checkbox>

</u-checkbox-group>

</scroll-view>

</view>

</u-popup>

<view class="bottom-box">

<view class="btn" @click="submit">确认发布</view>

</view>

</view>

</template>

  

<script>

import { uploadFile } from "@/utils/upload.js";

import { uploadVideo } from "@/utils/uploadVideo.js";

import { mapState } from "vuex";

export default {

data() {

return {

showSelectCycle: false,

isImage: 1,

content: "",

fileList: [],

albumTitle: "请选择",

albumId: "",

control: true,

columnType: "other",

maxCount: 20,

compressSize: 10,

imageSize: 2,

uploadTask: null,

media: [], //数据源

formAlbumId: "",

childrenData: [],

allchecked: false,

selected: [],

albumShow: true,

imgMedia: [],

videoMedia: []

};

},

computed: {

...mapState(["currentChild"]),

},

onLoad(option) {

if (option.id) {

this.albumTitle = option.title;

this.albumId = option.id;

this.formAlbumId = option.id;

}

uni.$on("selectAlbum", ({ id, title }) => {

this.albumTitle = title;

this.albumId = id;

});

const dynamicData = uni.getStorageSync("dynamicData");

if (dynamicData) {

const data = JSON.parse(dynamicData);

this.content = data.content ?? "";

this.media = data.media ?? [];

this.albumId = data.albumId ?? "";

this.albumTitle = data.albumTitle ?? "";

if(this.isImage){

this.imgMedia= JSON.parse(JSON.stringify(data.media)) ?? [];

}else{

this.videoMedia= JSON.parse(JSON.stringify(data.media)) ?? [];

}

}

this.getAllCycle();

},

onUnload() {

uni.$off("selectAlbum");

let params = {};

if (this.content) {

params.content = this.content;

}

if (this.media.length) {

params.media = this.media;

}

if (this.albumId && this.albumId != this.formAlbumId) {

params.albumId = this.albumId;

params.albumTitle = this.albumTitle;

}

if (Object.keys(params).length) {

params.albumId = this.albumId;

params.albumTitle = this.albumTitle;

uni.setStorageSync("dynamicData", JSON.stringify(params));

} else {

uni.setStorageSync("dynamicData", "");

}

},

methods: {

querySelect() {

this.selected = this.childrenData.filter((item) => {

return item.checked;

});

this.showSelectCycle = false;

if (this.selected.length > 1) {

this.albumTitle = "";

this.albumId = "";

this.albumShow = false;

} else {

this.albumShow = true;

}

},

checkboxGroupChange(val) {

if (val.length === this.childrenData.length) {

this.allchecked = true;

}

if (!val.length) {

this.allchecked = false;

}

},

allcheckedChange(val) {

if (val.value) {

this.childrenData.forEach((item) => {

item.checked = true;

});

} else {

this.childrenData.forEach((item) => {

item.checked = false;

});

}

},

getAllCycle() {

this.$api.getMemberByUserId().then((res) => {

this.childrenData = res.data.map((item) => {

return { ...item, checked: false };

});

});

},

selectCycle() {

this.showSelectCycle = true;

},

typeChange() {

this.media = [];

this.$nextTick(()=>{

if(this.isImage){

this.media = JSON.parse(JSON.stringify(this.imgMedia))

}else{

this.media = JSON.parse(JSON.stringify(this.videoMedia))

}

})

},

imgDelete(eq) {

this.media.splice(eq, 1);

if(this.isImage){

this.imgMedia.splice(eq, 1);

}else{

this.videoMedia.splice(eq, 1);

}

},

submit() {

if (this.content.length > 300) {

uni.showToast({

icon: "error",

title: "动态最多只能上传300字",

});

return;

}

if (!this.media || !this.media.length) {

uni.showToast({

icon: "error",

title: "请上传照片",

});

return;

}

const imgList = this.media.filter((item) => {

return item.progress == "上传成功";

});

if (imgList.length != this.media.length) {

uni.showToast({

icon: "none",

title: "存在上传失败或违规图片，请重新尝试",

});

return;

}

if (this.media.length > 20) {

uni.showToast({

icon: "error",

title: "最多上传20张照片",

});

return;

}

const childList = this.childrenData

.filter((item) => {

return item.checked;

})

.map((item) => {

return item.childMemberId;

});

if (!childList.length) {

uni.showToast({

icon: "error",

title: "请选择要发布的家庭圈",

});

return;

}

uni.showLoading({

title: "提交中",

});

let videos = 0;

let photos = 0;

const fileList = JSON.parse(JSON.stringify(this.media));

let photoList = fileList.map((item) => {

if (item.fileType == "image") {

photos++;

return {

...item,

url: item.src,

type: 1,

};

} else {

videos++;

return {

...item,

url: item.videoId,

type: 2,

};

}

});

if (videos > 1 || (videos == 1 && photos)) {

uni.showToast({

icon: "none",

title: "仅支持单视频上传",

});

return;

}

const params = childList.map((item) => {

return {

childFamilyMemberId: item,

photoList: photoList,

albumId: this.albumId,

content: this.content,

videos: videos,

photos: photos,

};

});

this.$api

.pushDynamic(params)

.then((res) => {

uni.hideLoading();

uni.$emit("refreshDynamic");

uni.$emit("refreshAlbum");

this.content = "";

this.media = [];

this.albumId = "";

this.albumTitle = "";

uni.navigateBack();

})

.catch((err) => {

uni.hideLoading();

});

},

//上传

chooseFile(e) {

this.uploadFileToServe(e);

},

//上传逻辑处理

async uploadFileToServe(urlList) {

if (!urlList || urlList.length <= 0) {

return;

}

  

if (urlList[0].fileType == "image") {

let promiseList = [];

urlList.forEach((item) => {

let response = "";

item.tempFilePaths = [item.src];

let promiseItem = new Promise(async (resolve, reject) => {

response = await uploadFile(item);

let videoPhoto = null;

const checkResult = await this.$api.imageSyncScan({

urls: [response],

});

if (!checkResult.data[0].passed) {

item.status = "error";

item.progress = "上传违规";

item.src = "";

resolve(item);

return;

}

item.playTime = item.duration;

item.videoPhoto = videoPhoto;

item.status = "success";

item.progress = "上传成功";

item.src = response;

resolve(item);

});

promiseList.push(promiseItem);

});

Promise.all(promiseList).then((resList) => {

this.media.push(...resList);

if(this.isImage){

this.imgMedia.push(...resList);

}else{

this.videoMedia.push(...resList);

}

});

} else {

let videoPhoto = null;

let response = "";

const res = await uploadVideo({

url: urlList[0].src,

coverUrl: urlList[0].thumbTempFilePath,

});

urlList[0].tempFilePaths = [urlList[0].src];

response = res.videoId;

urlList[0].tempFilePaths = [urlList[0].thumbTempFilePath];

videoPhoto = await uploadFile(urlList[0]);

const checkResult = await this.$api.imageSyncScan({

urls: [videoPhoto],

});

if (!checkResult.data[0].passed) {

urlList[0].status = "error";

urlList[0].progress = "上传违规";

urlList[0].src = "";

this.media.push(urlList[0]);

if(this.isImage){

this.imgMedia.push(urlList[0]);

}else{

this.videoMedia.push(urlList[0]);

}

return;

}

urlList[0].videoId = response;

urlList[0].playTime = urlList[0].duration;

urlList[0].videoPhoto = videoPhoto;

urlList[0].status = "success";

urlList[0].progress = "上传成功";

this.media.push(urlList[0]);

if(this.isImage){

this.imgMedia.push(urlList[0]);

}else{

this.videoMedia.push(urlList[0]);

}

}

},

selectAlbum() {

uni.navigateTo({

url: `/pagesA/albumEdit/selectAlbum?type=dynamic`,

});

},

},

};

</script>

  

<style lang="scss" scoped>

.radio-label {

display: flex;

justify-content: space-between;

width: 85vw;

padding: 32rpx;

image {

width: 64rpx;

height: 64rpx;

border-radius: 32rpx;

}

.name {

line-height: 64rpx;

}

}

.textarea-box {

position: relative;

padding-bottom: 40rpx;

.textarea-num {

position: absolute;

right: 20rpx;

bottom: 20rpx;

font-family: PingFang SC Medium;

font-size: 20rpx;

font-weight: normal;

letter-spacing: 0em;

  

/* 中性色G50 */

color: #bfbfbf;

}

}

.content {

padding: 12rpx 36rpx;

}

.select-all {

padding: 12rpx 36rpx;

}

.bottom-box {

position: fixed;

bottom: 50rpx;

width: calc(100vw - 64rpx);

  

.btn {

width: 622rpx;

height: 84rpx;

margin: 0 auto;

text-align: center;

border-radius: 306px;

background: #6c86fa;

line-height: 84rpx;

font-family: PingFangSC-Medium;

font-size: 32rpx;

font-weight: normal;

letter-spacing: 0px;

color: #ffffff;

}

}

  

.main {

padding: 32rpx;

padding-bottom: 130rpx;

}

  

.tip {

font-family: PingFangSC-Regular;

font-size: 20rpx;

font-weight: normal;

letter-spacing: 0em;

  

/* 中性色G50 */

color: #bfbfbf;

  

margin-bottom: 80rpx;

}

  

.select-album {

display: flex;

justify-content: space-between;

font-family: PingFangSC-Regular;

font-size: 28rpx;

font-weight: normal;

letter-spacing: 0em;

border-bottom: 1rpx solid #d9d9d9;

padding: 32rpx 0;

  

.select-item-start {

display: flex;

justify-content: flex-start;

color: #000000;

  

view {

display: inline-block;

vertical-align: middle;

}

  

.icon {

font-size: 32rpx;

margin-right: 16rpx;

color: #bfbfbf;

}

}

  

.select-item-end {

display: flex;

justify-content: flex-end;

color: #585858;

  

view {

display: inline-block;

vertical-align: middle;

}

  

image {

width: 9rpx;

height: 18rpx;

margin-left: 22rpx;

}

}

}

.cycle-header {

display: flex;

justify-content: space-between;

width: 100%;

height: 84rpx;

padding: 28rpx 32rpx;

}

.cycle-cancel {

font-size: 30rpx;

font-family: PingFang SC;

font-weight: normal;

color: #585858;

}

.cycle-title {

font-size: 30rpx;

font-family: PingFang SC;

font-weight: normal;

color: #000000;

}

.cycle-confirm {

font-size: 30rpx;

font-family: PingFang SC;

font-weight: normal;

color: #585858;

}

.min-avatar {

width: 48rpx !important;

height: 48rpx !important;

border-radius: 24rpx !important;

margin-right: 16rpx !important;

}

</style>
```



```
<text v-if="data.status == 'CANCELLED'">已取消</text>
```


周一：
1.  订单通知功能，邀请线索功能发布上线
2.  参与UI评审会议
3.  机构分享功能前端页面开发，机构子相册前端页面开发
周二：
1.  分享机构功能页面开发完成
2.  商户端多商户选择进入开发完成
3.  商户客服二维码配置页面开发
周三：
1.  教务学生管理列表前端页面开发完成
2.  教务学生管理详情 基础信息前端页面开发完成
3.  教务先生管理模块 缴费信息前端页面开发30%
周四：
1.  参加购物车测试用例评审
2.  参加教务的UI评审
3.  学生管理详情缴费页面前端开发完成
4.  学生管理详情家庭成员页面优化完成
周五：
1.  学员管理页面上课记录页面开发完成
2.  学员管理页面课时动态页面开发完成
3.  班级管理列表页面开发完成
4.  班级管理新增页面开发部分完成
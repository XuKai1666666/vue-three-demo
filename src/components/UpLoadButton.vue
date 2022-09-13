<template>
    <div id="container" v-if="getVisable">
        <a-upload-dragger v-model:fileList="fileList" name="file" :multiple="true"
            action="https://www.mocky.io/v2/5cc8019d300000980a055e76" @change="handleChange" @drop="handleDrop"
            accept=".pmx,.pmd"
            >
            <p class="ant-upload-drag-icon">
                <inbox-outlined></inbox-outlined>
            </p>
            <p class="ant-upload-text">点击或拖拽文件</p>
            <p class="ant-upload-hint">
                支持PMX,PMD文件
            </p>
        </a-upload-dragger>
    </div>
</template>
<script setup lang="ts">
import { InboxOutlined } from '@ant-design/icons-vue';
import { message } from 'ant-design-vue';
import { ref } from 'vue';
import type { UploadChangeParam } from 'ant-design-vue';
// const UploadDataList = [
//     {
//         name: "xxx.png",
//         status: "done",
//         url: "https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png",
//         thumbUrl: "https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png"
//     }
// ]
defineProps<{
    getVisable?: boolean
}>()
const handleChange = (info: UploadChangeParam) => {
    const status = info.file.status;
    if (status !== 'uploading') {
        console.log(info.file, info.fileList);
    }
    if (status === 'done') {
        message.success(`${info.file.name} file uploaded successfully.`);
    } else if (status === 'error') {
        message.error(`${info.file.name} file upload failed.`);
    }
};
const fileList = ref([])
function handleDrop(e: DragEvent) {
    console.log(e);
}
</script>
<style scoped>
#container {
    width: 300px;
    height: auto;
    background-color: #ffffff;
    padding: 10px;
}
</style>
  
  
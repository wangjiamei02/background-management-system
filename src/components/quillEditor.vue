<template>
  <div>
    <quill-editor
      v-model="content"
      ref="myQuillEditor"
      :options="editorOption"
      @blur="onEditorBlur($event)"
      @focus="onEditorFocus($event)"
      @ready="onEditorReady($event)"
      @change="onEditorChange($event)"
      style="height: 200px; marginBottom:50px"
    >
    </quill-editor>
  </div>
</template>

<script>
import Vue from "vue";
import VueQuillEditor from "vue-quill-editor";

// 载入样式
import "quill/dist/quill.core.css";
import "quill/dist/quill.snow.css";
import "quill/dist/quill.bubble.css";

Vue.use(VueQuillEditor /* { default global options } */);

import { quillEditor } from "vue-quill-editor";

export default {
  data() {
    return {
      content: "",
      editorOption: {
        placeholder: "",
        modules: {
          toolbar: [
            ["bold", "italic", "underline", "strike"], //加粗，斜体，下划线，删除线
            ["blockquote", "code-block"], //引用，代码块
            [{ header: 1 }, { header: 2 }], // 标题，键值对的形式；1、2表示字体大小
            [{ list: "ordered" }, { list: "bullet" }], //列表
            [{ script: "sub" }, { script: "super" }], // 上下标
            [{ indent: "-1" }, { indent: "+1" }], // 缩进
            [{ direction: "rtl" }], // 文本方向
            [{ size: ["small", false, "large", "huge"] }], // 字体大小
            [{ header: [1, 2, 3, 4, 5, 6, false] }], //几级标题
            [{ color: [] }, { background: [] }], // 字体颜色，字体背景颜色
            [{ font: [] }], //字体
            [{ align: [] }], //对齐方式
            ["clean"], //清除字体样式
            ["image", "video"], //上传图片、上传视频
          ],
        },
      },
    };
  },
  // 如果需要手动控制数据同步，父组件需要显式地处理changed事件
  methods: {
    onEditorBlur(quill) {
      // 失去焦点事件
      // console.log("editor blur!", quill);
    },
    onEditorFocus(quill) {
      // 获得焦点事件
      // console.log("editor focus!", quill);
    },
    onEditorReady(quill) {
      // 准备编辑器
      // console.log("editor ready!", quill);
    },
    onEditorChange({ quill, html, text }) {
      // 内容改变事件
      // console.log("editor change!", quill, html, text);
      // this.content = html;
    },
  },
  computed: {
    editor() {
      // return this.$refs.myQuillEditor.quill;
    },
  },
  mounted() {
    // console.log("this is current quill instance object", this.editor);
  },
  components: {
    quillEditor,
  },
};
</script>

<style lang="less" scoped>
</style>
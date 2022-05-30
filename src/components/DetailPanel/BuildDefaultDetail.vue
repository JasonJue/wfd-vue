<template>
  <div>
    <DefaultDetail :model="model" :onChange="onChange" :readOnly="readOnly" />
    <div class="panelRow">
      <div>{{ i18n["BuildMachine"] }}：</div>
      <el-select
        style="width: 90%; font-size: 12px"
        :value="model.MachineId"
        :placeholder="'请选择服务器'"
        :filterable="true"
        :disabled="readOnly"
        clearable
        @input="
          (value) => {
            onChange('MachineId', value);
          }
        "
        :transfer="true"
      >
        <el-option
          v-for="(kv, kvIndex) in this.Machines"
          :key="kvIndex"
          :label="kv.value"
          :value="kv.key"
        >
        </el-option>
      </el-select>
    </div>
    <div class="panelRow">
      <div>{{ i18n["WorkDirectory"] }}：</div>
      <el-input
        style="width: 90%; font-size: 12px"
        :disabled="readOnly"
        :value="model.WorkDirectory"
        @input="
          (value) => {
            onChange('WorkDirectory', value);
          }
        "
      />
    </div>
    <div class="panelRow">
      <div>{{ i18n["BuildScript"] }}：</div>
      <AceEditor
        :fontSize="14"
        :showPrintMargin="true"
        :showGutter="true"
        :highlightActiveLine="true"
        :value="model.BuildScript"
        :readOnly="readOnly"
        v-model="model.BuildScript"
        width="650px"
        height="450px"
        mode="sh"
        theme="monokai"
        :onChange="onScriptChange"
        name="editor2"
        :editorProps="{ $blockScrolling: true }"
      />
    </div>
  </div>
</template>
<script>
import brace from "brace";
import { Ace as AceEditor } from "vue2-brace-editor";
import "brace/mode/sh";
import "brace/theme/monokai";
import DefaultDetail from "./DefaultDetail";
export default {
  inject: ["i18n"],
  components: {
    DefaultDetail,
    AceEditor,
  },
  props: {
    model: {
      type: Object,
      default: () => ({}),
    },
    Machines: {
      type: Array,
      default: () => [],
    },
    onChange: {
      type: Function,
      default: () => {},
    },
    readOnly: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onScriptChange(newValue) {
      this.onChange("BuildScript", newValue);
    },
  },
};
</script>

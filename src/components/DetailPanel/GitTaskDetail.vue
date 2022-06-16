<template>
  <div :data-clazz="model.clazz">
    <div class="panelTitle">{{ i18n["gitTask"] }}</div>
    <div class="panelBody">
      <BuildDefaultDetail
        :model="model"
        :onChange="onChange"
        :readOnly="readOnly"
        :Machines="Machines"
      />
      <h1/>
      <div class="panelRow">
        <div>{{ i18n["Branch"] }}：</div>
        <el-select
          style="width: 90%; font-size: 12px"
          :value="model.BranchId"
          :placeholder="'请选分支'"
          :filterable="true"
          :disabled="readOnly"
          clearable
          :transfer="true"
          @input="
            (value) => {
              onChange('BranchId', value);
            }
          "
        >
          <el-option
            v-for="(kv, kvIndex) in this.Branchs"
            :key="kvIndex"
            :label="kv.value"
            :value="kv.key"
          >
          </el-option>
        </el-select>
      </div>
    </div>
  </div>
</template>
<script>
import BuildDefaultDetail from "./BuildDefaultDetail";
export default {
  inject: ["i18n"],
  components: {
    BuildDefaultDetail,
  },
  props: {
    model: {
      type: Object,
      default: () => ({
        label: "git构建任务",
        MachineId: "1",
        WorkDirectory: ".",
        BranchId: "1",
        Command: "构建命令",
      }),
    },
    Branchs: {
      type: Array,
      default: () => [],
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
  methods: {},
};
</script>

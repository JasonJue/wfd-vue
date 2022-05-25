<template>
  <div>
    <BuildDefaultDetail
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <div class="panelRow">
      <div>{{ i18n["BuildMachine"] }}：</div>
      <el-select
        style="width: 90%; font-size: 12px"
        :value="model.MachineId"
        :placeholder="'请选择服务器'"
        :filterable="true"
        :disabled="readOnly"
        clearable
        @on-change="onMachineChange"
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
    onMachineChange(event) {
      var items = this.Machines.filter((o) => o.key == event);
      if (items && items.length > 0) {
        onChange("MachineId", value);
        console.log(items[0].value);
      } else {
        onChange("MachineId", -1);
      }
    },
  },
};
</script>

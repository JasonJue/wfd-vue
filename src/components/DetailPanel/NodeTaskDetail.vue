<template>
  <div :data-clazz="model.clazz">
    <div class="panelTitle">{{ i18n["nodeTask"] }}</div>
    <div class="panelBody">
      <BuildDefaultDetail
        :model="model"
        :onChange="onChange"
        :readOnly="readOnly"
        :Machines="Machines"
      />

      <div class="panelRow">
        <div>{{ i18n["NodeVersion"] }}：</div>
        <el-select
          style="width: 90%; font-size: 12px"
          :value="model.NodeVersion"
          :placeholder="'请选Node版本'"
          :filterable="true"
          :disabled="readOnly"
          clearable
          :transfer="true"
          @input="
            (value) => {
              onChange('NodeVersion', value);
            }
          "
        >
          <el-option
            v-for="(kv, kvIndex) in this.NodeVersions"
            :key="kvIndex"
            :label="kv.value"
            :value="kv.key"
          >
          </el-option>
        </el-select>
      </div>
      <div class="panelRow">
        <div>{{ i18n["Package"] }}：</div>
        <el-select
          style="width: 90%; font-size: 12px"
          :value="model.Package"
          :placeholder="'请选部署包'"
          :filterable="true"
          :disabled="readOnly"
          clearable
          :transfer="true"
          @input="
            (value) => {
              onChange('Package', value);
            }
          "
        >
          <el-option
            v-for="(kv, kvIndex) in this.Packages"
            :key="kvIndex"
            :label="kv.value"
            :value="kv.key"
          >
          </el-option>
        </el-select>
      </div>
      <div class="panelRow">
        <div>{{ i18n["PackagePath"] }}：</div>
        <el-input
          style="width: 90%; font-size: 12px"
          :disabled="readOnly"
          :value="model.PackagePath"
          @input="
            (value) => {
              onChange('PackagePath', value);
            }
          "
        />
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
        label: "NodeJS构建任务",
        MachineId: "1",
        WorkDirectory: ".",
        NodeVersion: "1",
        MavenVersion: "",
        PackageId: 1,
        Command: "构建命令",
        PackagePath: "target",
      }),
    },
    onChange: {
      type: Function,
      default: () => {},
    },
    readOnly: {
      type: Boolean,
      default: false,
    },
    Machines: { type: Array, default: () => [] },
    Packages: {
      type: Array,
      default: () => [],
    },
    NodeVersions: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    onNodeVersionChange(event) {
      var items = this.NodeVersions.filter((o) => o.key == event);
      if (items && items.length > 0) {
        onChange("NodeVersion", value);
        console.log(items[0].value);
      } else {
        onChange("NodeVersion", -1);
      }
    },
    onPackageChange(event) {
      console.log("onPackageChange:" + event);
      var items = this.Packages.filter((o) => o.key == event);
      if (items && items.length > 0) {
        onChange("Package", value);
        console.log(items[0].value);
      } else {
        onChange("Package", -1);
      }
    },
  },
};
</script>
<template>
  <div :data-clazz="model.clazz">
    <div class="panelTitle">{{ i18n["javaTask"] }}</div>
    <div class="panelBody">
      <BuildDefaultDetail
        :model="model"
        :onChange="onChange"
        :readOnly="readOnly"
        :Machines="Machines"
      />
      <div class="panelRow">
        <div>{{ i18n["JDKVersion"] }}：</div>

        <el-select
          style="width: 90%; font-size: 12px"
          :value="model.JDKVersion"
          :placeholder="'请选JDK版本'"
          :filterable="true"
          :disabled="readOnly"
          clearable
          :transfer="true"
          @input="
            (value) => {
              onChange('JDKVersion', value);
            }
          "
        >
          <el-option
            v-for="(kv, kvIndex) in this.JDKVersions"
            :key="kvIndex"
            :label="kv.value"
            :value="kv.key"
          >
          </el-option>
        </el-select>
      </div>
      <div class="panelRow">
        <div>{{ i18n["MavenVersion"] }}：</div>
        <el-select
          style="width: 90%; font-size: 12px"
          :value="model.MavenVersion"
          :placeholder="'请选Maven版本'"
          :filterable="true"
          :disabled="readOnly"
          clearable
          :transfer="true"
          @input="
            (value) => {
              onChange('MavenVersion', value);
            }
          "
        >
          <el-option
            v-for="(kv, kvIndex) in this.MavenVersions"
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
        label: "Android构建任务",
        MachineId: "1",
        WorkDirectory: ".",
        JDKVersion: "1",
        MavenVersion: "1",
        PackageId: "1",
        Command: "构建命令",
        PackagePath: "target",
      }),
    },
    Packages: {
      type: Array,
      default: () => [],
    },
    AndroidSDKVersions: {
      type: Array,
      default: () => [],
    },
    Machines: {
      type: Array,
      default: () => [],
    },
    JDKVersions: {
      type: Array,
      default: () => [],
    },
    MavenVersions: {
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
    onJDKVersionChange(event) {
      var items = this.JDKVersions.filter((o) => o.key == event);
      if (items && items.length > 0) {
        onChange("JDKVersion", value);
        console.log(items[0].value);
      } else {
        onChange("JDKVersion", -1);
      }
    },
    onMavenVersionChange(event) {
      var items = this.MavenVersions.filter((o) => o.key == event);
      if (items && items.length > 0) {
        onChange("MavenVersion", value);
        console.log(items[0].value);
      } else {
        onChange("MavenVersion", -1);
      }
    },
    onPackageChange(event) {
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

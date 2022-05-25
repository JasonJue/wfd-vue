<template>
  <div id="app">
    <el-button
      size="small"
      style="float: right; margin-top: 6px; margin-right: 6px"
      @click="
        () => {
          this.$refs['wfd'].graph.saveXML();
        }
      "
      >导出XML</el-button
    >
    <el-button
      size="small"
      style="float: right; margin-top: 6px; margin-right: 6px"
      @click="
        () => {
          this.$refs['wfd'].graph.saveImg();
        }
      "
      >导出图片</el-button
    >
    <el-button
      size="small"
      style="float: right; margin-top: 6px; margin-right: 6px"
      @click="
        () => {
          this.modalVisible = true;
        }
      "
      >查看流程图</el-button
    >
    <wfd-vue
      ref="wfd"
      :data="demoData"
      :height="600"
      :users="candidateUsers"
      :groups="candidateGroups"
      :categorys="categorys"
      :lang="lang"
      :Machines="Machines"
      :Packages="Packages"
      :JDKVersions="JDKVersions"
      :AndroidSDKVersions="AndroidSDKVersions"
      :MavenVersions="MavenVersions"
      :DockerVersions="DockerVersions"
      :NodeVersions="NodeVersions"
    />
    <el-dialog title="查看流程图" :visible.sync="modalVisible" width="60%">
      <wfd-vue
        ref="wfd"
        :data="demoData1"
        :height="300"
        :Machines="Machines"
        :Packages="Packages"
        :JDKVersions="JDKVersions"
        :AndroidSDKVersions="AndroidSDKVersions"
        :MavenVersions="MavenVersions"
        :DockerVersions="DockerVersions"
        :NodeVersions="NodeVersions"
        isView
      />
    </el-dialog>
  </div>
</template>

<script>
import WfdVue from "../src/components/Wfd";
export default {
  name: "app",
  components: {
    WfdVue,
  },
  props: {
    isView: {
      type: Boolean,
      default: false,
    },
    mode: {
      type: String,
      default: "edit",
    },
    height: {
      type: Number,
      default: 800,
    },
    lang: {
      type: String,
      default: "zh",
    },
    data: {
      type: Object,
      default: () => ({ nodes: [], edges: [] }),
    },
    users: {
      type: Array,
      default: () => [],
    },
    groups: {
      type: Array,
      default: () => [],
    },
    categorys: {
      type: Array,
      default: () => [],
    },
    Machines: {
      type: Array,
      default: () => [
        { key: "1", value: "机器名1" },
        { key: "2", value: "机器名2" },
        { key: "3", value: "机器名3" },
        { key: "4", value: "机器名4" },
      ],
    },
    Packages: {
      type: Array,
      default: () => [
        { key: "1", value: "移动API网关" },
        { key: "2", value: "网关管理服务" },
        { key: "3", value: "移动管理服务" },
      ],
    },
    JDKVersions: {
      type: Array,
      default: () => [
        { key: "1", value: "JDK 1.6" },
        { key: "2", value: "JDK 1.7" },
        { key: "3", value: "JDK 1.8" },
        { key: "4", value: "JDK 1.9" },
        { key: "5", value: "OPENJDK 10" },
        { key: "6", value: "OPENJDK 11" },
      ],
    },
    AndroidSDKVersions: {
      type: Array,
      default: () => [
        { key: "23", value: "Android 6.0" },
        { key: "24", value: "Android 7.0" },
        { key: "25", value: "Android 7.1.1" },
        { key: "26", value: "Android 8.0" },
        { key: "27", value: "Android 8.1" },
        { key: "28", value: "Android 9" },
        { key: "29", value: "Android 10" },
        { key: "30", value: "Android 11" },
      ],
    },
    MavenVersions: {
      type: Array,
      default: () => [
        { key: "1", value: "Maven 2.2.1" },
        { key: "2", value: "Maven 3.2.5" },
        { key: "3", value: "Maven 3.5.2" },
        { key: "4", value: "Maven 3.6.1" },
        { key: "5", value: "Maven 3.6.3" },
      ],
    },
    DockerVersions: {
      type: Array,
      default: () => [
        { key: "1", value: "17.03" },
        { key: "2", value: "17.06" },
        { key: "3", value: "17.09" },
        { key: "4", value: "18.06" },
        { key: "6", value: "latest" },
      ],
    },
    NodeVersions: {
      type: Array,
      default: () => [
        { key: "1", value: "Node 6.11" },
        { key: "2", value: "Node 7.10" },
        { key: "3", value: "Node 8.13" },
        { key: "4", value: "Node 9.11" },
        { key: "5", value: "Node 10.15" },
        { key: "6", value: "Node 12.2" },
        { key: "7", value: "Node 13.14" },
        { key: "8", value: "Node 14.8" },
      ],
    },
  },
  data() {
    return {
      modalVisible: false,
      lang: "zh",
      demoData: {
        nodes: [
          { id: "startNode1", x: 50, y: 200, label: "", clazz: "start" },
          { id: "startNode2", x: 50, y: 320, label: "", clazz: "timerStart" },
          {
            id: "taskNode1",
            x: 200,
            y: 200,
            label: "主任审批",
            clazz: "userTask",
          },
          {
            id: "taskNode2",
            x: 400,
            y: 200,
            label: "经理审批",
            clazz: "scriptTask",
          },
          {
            id: "gatewayNode",
            x: 400,
            y: 320,
            label: "金额大于1000",
            clazz: "inclusiveGateway",
          },
          {
            id: "taskNode3",
            x: 400,
            y: 450,
            label: "董事长审批",
            clazz: "receiveTask",
          },
          {
            id: "catchNode1",
            x: 600,
            y: 200,
            label: "等待结束",
            clazz: "signalCatch",
          },
          { id: "endNode", x: 600, y: 320, label: "", clazz: "end" },
        ],
        edges: [
          {
            source: "startNode1",
            target: "taskNode1",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "startNode2",
            target: "gatewayNode",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "taskNode1",
            target: "catchNode1",
            sourceAnchor: 0,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "taskNode1",
            target: "taskNode2",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "taskNode2",
            target: "gatewayNode",
            sourceAnchor: 1,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "taskNode2",
            target: "taskNode1",
            sourceAnchor: 2,
            targetAnchor: 2,
            clazz: "flow",
          },
          {
            source: "gatewayNode",
            target: "taskNode3",
            sourceAnchor: 2,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "gatewayNode",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 2,
            clazz: "flow",
          },
          {
            source: "taskNode3",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 1,
            clazz: "flow",
          },
          {
            source: "catchNode1",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 0,
            clazz: "flow",
          },
        ],
      },
      demoData1: {
        nodes: [
          { id: "startNode1", x: 50, y: 200, label: "", clazz: "start" },
          { id: "startNode2", x: 50, y: 320, label: "", clazz: "timerStart" },
          {
            id: "taskNode1",
            x: 200,
            y: 200,
            label: "主任审批",
            clazz: "userTask",
          },
          {
            id: "taskNode2",
            x: 400,
            y: 200,
            label: "经理审批",
            clazz: "scriptTask",
            active: true,
          },
          {
            id: "gatewayNode",
            x: 400,
            y: 320,
            label: "金额大于1000",
            clazz: "gateway",
          },
          {
            id: "taskNode3",
            x: 400,
            y: 450,
            label: "董事长审批",
            clazz: "receiveTask",
          },
          {
            id: "catchNode1",
            x: 600,
            y: 200,
            label: "等待结束",
            clazz: "signalCatch",
          },
          { id: "endNode", x: 600, y: 320, label: "", clazz: "end" },
        ],
        edges: [
          {
            source: "startNode1",
            target: "taskNode1",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "startNode2",
            target: "gatewayNode",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "taskNode1",
            target: "catchNode1",
            sourceAnchor: 0,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "taskNode1",
            target: "taskNode2",
            sourceAnchor: 1,
            targetAnchor: 3,
            clazz: "flow",
          },
          {
            source: "taskNode2",
            target: "gatewayNode",
            sourceAnchor: 1,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "taskNode2",
            target: "taskNode1",
            sourceAnchor: 2,
            targetAnchor: 2,
            clazz: "flow",
          },
          {
            source: "gatewayNode",
            target: "taskNode3",
            sourceAnchor: 2,
            targetAnchor: 0,
            clazz: "flow",
          },
          {
            source: "gatewayNode",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 2,
            clazz: "flow",
          },
          {
            source: "taskNode3",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 1,
            clazz: "flow",
          },
          {
            source: "catchNode1",
            target: "endNode",
            sourceAnchor: 1,
            targetAnchor: 0,
            clazz: "flow",
          },
        ],
      },
      candidateUsers: [
        { id: "1", name: "Tom" },
        { id: "2", name: "Steven" },
        { id: "3", name: "Andy" },
      ],
      candidateGroups: [
        { id: "1", name: "Manager" },
        { id: "2", name: "Security" },
        { id: "3", name: "OA" },
      ],
      categorys: [
        { id: "1", name: "Common" },
        { id: "2", name: "Subsidy" },
        { id: "3", name: "Maintain" },
      ],
    };
  },
  mounted() {},
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

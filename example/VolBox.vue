<template>
  <Modal
    title="查看流程图"
    :mask-closable="false"
    :closable="false"
    :mask="mask"
    v-model="show"
    width="90%"
    class-name="vertical-center-modal"
  >
    <wfd-vue
      ref="wfd"
      :mode="'edit'"
      :data.sync="demoData"
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
  </Modal>
</template>

<script>
import WfdVue from "../src/components/Wfd";

export default {
  name: "app",
  components: {
    WfdVue,
  },
  props: {
    mask: {
      type: Boolean,
      default: true,
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
  created() {},
  data() {
    return {
      title: "流水线编辑框",
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
            label: "Node节点",
            clazz: "nodeTask",
            MachineId: "2",
            WorkDirectory: "工作目录",
            NodeVersion: "1",
            Package: "1",
            BuildScript: "1123123",
            PackagePath: "包目录",
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
      show: false,
      height: 630,
      width: 900,
      size: "800px",
      selectedNode: {},
      currentNodeHasChild: true,
      selectdrawer: false,
      editdrawer: false,
      direction: "rtl",
      tab: "pipeline",
      readonly: true,
      model: 1,
      form: {
        x: 50,
        y: 55,
        xstep: 120,
        ystep: 70,
        data: 2,
        showArrow: true,
        lineStyle: "default",
        from: 0,
        to: 0,
      },
      msg: "",
      ConfigValue: {},
      pipeLineFlowData: [],
      MainData: {},
      TaskEditMode: "Add",
      PipelineStatus: [
        { key: 1, value: "已建立" },
        { key: 2, value: "运行中" },
      ],
      EnableDic: [
        { key: 0, value: "否" },
        { key: 1, value: "是" },
      ],
      ruleValidate: {
        TaskName: [
          {
            required: true,
            message: "任务名称不能为空",
            trigger: "blur",
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
      lang: "zh",
    };
  },
  watch: {},
  methods: {
    showView(_model, data) {
      console.log("showView");
      this.resetData();
      this.model = _model;
      this.height = document.documentElement.clientHeight * 0.7;
      this.width = document.documentElement.clientWidth * 0.9;
      this.show = true;
      if (this.dataUtil.common.enumViewModel.Add == this.model) {
        this.title = "流水线-新增";
        let userId = this.$store.getters.getUserInfo().userId;
        this.pipeLineFlowData = JSON.parse(JSON.stringify(sample.nodes));
        data = {
          Id: 0,
          Name: "",
          Status: 1,
          CreateUser: userId,
          UpdateUser: userId,
        };
        this.readonly = false;
      } else {
        if (this.dataUtil.common.enumViewModel.Edit == this.model) {
          this.title = "流水线-编辑";
          this.readonly = false;
        } else {
          this.title = "流水线-查看";
          this.readonly = true;
        }
        if (
          data.PipelineFlow == "" ||
          data.PipelineFlow == "1" ||
          data.PipelineFlow == undefined
        ) {
          this.pipeLineFlowData = JSON.parse(JSON.stringify(sample.nodes));
        } else if (typeof data.PipelineFlow == "string") {
          this.pipeLineFlowData = JSON.parse(data.PipelineFlow);
        }
      }
      this.MainData = data;
      this.$refs["wfd"].render();
    },
  },
  mounted() {},
};
</script>

<style lang="less" scoped>
.vol-tabs {
  background: white;
}
.tabs1-header {
  display: flex;
  text-align: right;
  padding: 10px;
  .btn-group {
    flex: 1;
  }
}
</style>

<style lang="less">
.vertical-center-modal {
  display: flex;
  align-items: center;
  //   justify-content: center;
  .ivu-modal {
    top: 0;
  }
  .ivu-modal-close .ivu-icon-ios-close {
    color: white;
  }
  .view-model-content {
    min-height: 180px;
  }
  .srcoll-content {
    height: 100%;
    word-break: break-all;
    //  padding: 16px;
  }
  .ivu-modal-body {
    padding: 0px;
  }
  .ivu-modal-header {
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;
    padding: 12px 15px;
    background-image: linear-gradient(
      135deg,
      rgb(12, 215, 189) 10%,
      #57c5f7 100%
    );
  }
  .ivu-modal-footer {
    padding: 5px 10px;
    button {
      padding: 4px 18px;
    }
  }
  .header {
    color: white;
  }
}
</style>

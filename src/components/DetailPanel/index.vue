<template>
  <div class="detailPanel" :style="{ height: height + 'px' }">
    <UserTaskDetail
      v-if="model.clazz === 'userTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :users="users"
      :groups="groups"
    />
    <ScriptTaskDetail
      v-else-if="model.clazz === 'scriptTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <ReceiveTaskDetail
      v-else-if="model.clazz === 'receiveTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <MailTaskDetail
      v-else-if="model.clazz === 'mailTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <TimerEventDetail
      v-else-if="model.clazz === 'timerStart' || model.clazz === 'timerCatch'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <SignalEventDetail
      v-else-if="model.clazz === 'signalStart' || model.clazz === 'signalCatch'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :signalDefs="signalDefs"
    />
    <MessageEventDetail
      v-else-if="
        model.clazz === 'messageStart' || model.clazz === 'messageCatch'
      "
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :messageDefs="messageDefs"
    />
    <GatewayDetail
      v-else-if="
        model.clazz === 'gateway' ||
        model.clazz === 'exclusiveGateway' ||
        model.clazz === 'parallelGateway' ||
        model.clazz === 'inclusiveGateway'
      "
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <FlowDetail
      v-else-if="model.clazz === 'flow'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <StartEventDetail
      v-else-if="model.clazz === 'start'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <EndEventDetail
      v-else-if="model.clazz === 'end'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
    />
    <ProcessDetail
      v-else-if="model.clazz === 'process'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :categorys="categorys"
    />
    <NodeTaskDetail
      v-else-if="model.clazz === 'nodeTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :Machines="Machines"
      :Packages="Packages"
      :NodeVersions="NodeVersions"
    />
    <AndroidTaskDetail
      v-else-if="model.clazz === 'androidTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :Machines="Machines"
      :Packages="Packages"
      :JDKVersions="JDKVersions"
      :AndroidSDKVersions="AndroidSDKVersions"
    />
    <GitTaskDetail
      v-else-if="model.clazz === 'gitTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :Machines="Machines"
      :Branchs="Branchs"
    />
    <JavaTaskDetail
      v-else-if="model.clazz === 'javaTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :Machines="Machines"
      :Packages="Packages"
      :MavenVersions="MavenVersions"
      :JDKVersions="JDKVersions"
    />
    <DockerTaskDetail
      v-else-if="model.clazz === 'dockerTask'"
      :model="model"
      :onChange="onChange"
      :readOnly="readOnly"
      :Machines="Machines"
      :DockerVersions="DockerVersions"
    />
  </div>
</template>
<script>
import UserTaskDetail from "./UserTaskDetail";
import ScriptTaskDetail from "./ScriptTaskDetail";
import ReceiveTaskDetail from "./ReceiveTaskDetail";
import MailTaskDetail from "./MailTaskDetail";
import TimerEventDetail from "./TimerEventDetail";
import SignalEventDetail from "./SignalEventDetail";
import MessageEventDetail from "./MessageEventDetail";
import GatewayDetail from "./GatewayDetail";
import FlowDetail from "./FlowDetail";
import StartEventDetail from "./StartEventDetail";
import EndEventDetail from "./EndEventDetail";
import ProcessDetail from "./ProcessDetail";
import NodeTaskDetail from "./NodeTaskDetail";
import JavaTaskDetail from "./JavaTaskDetail";
import AndroidTaskDetail from "./AndroidTaskDetail";
import GitTaskDetail from "./GitTaskDetail";
import DockerTaskDetail from "./DockerTaskDetail";
export default {
  inject: ["i18n"],
  components: {
    UserTaskDetail,
    ScriptTaskDetail,
    ReceiveTaskDetail,
    MailTaskDetail,
    TimerEventDetail,
    SignalEventDetail,
    MessageEventDetail,
    GatewayDetail,
    FlowDetail,
    StartEventDetail,
    EndEventDetail,
    ProcessDetail,
    NodeTaskDetail,
    JavaTaskDetail,
    AndroidTaskDetail,
    DockerTaskDetail,
    GitTaskDetail,
  },
  props: {
    height: {
      type: Number,
      default: 800,
    },
    model: {
      type: Object,
      default: () => ({}),
    },
    Machines: {
      type: Array,
      default: () => [
        { key: "1", value: "机器名1" },
        { key: "2", value: "机器名2" },
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
    Branchs: {
      type: Array,
      default: () => [
        { key: "1", value: "Android" },
        { key: "2", value: "H5" },
        { key: "2", value: "Java" },
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
    signalDefs: {
      type: Array,
      default: () => [],
    },
    messageDefs: {
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
};
</script>
<style lang="scss">
.detailPanel {
  height: 100%;
  background: #f0f2f5;
  flex: 0 0 auto;
  float: left;
  width: 20%;
  border-right: 1px solid #e9e9e9;
  border-bottom: 1px solid #e9e9e9;
  .panelTitle {
    text-align: left;
    height: 32px;
    padding-left: 12px;
    color: #000;
    line-height: 28px;
    background: #ebeef2;
    border-bottom: 1px solid #dce3e8;
  }

  .panelBody {
    .panelRow {
      text-align: left;
      display: inline-block;
      font-size: 12px;
      width: 100%;
      padding: 5px 12px;
    }
  }
}
</style>

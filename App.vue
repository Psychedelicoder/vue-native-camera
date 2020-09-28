<template>
  <view class="container">
    <text class="main-text">Webcam Nexus</text>
    <camera class="container" :type="this.type" />
    <button
      :on-press="takePicture"
      title="Foto aufnehmen"
      color="#000"
      background-color="rgb(248, 248, 248)"
      border="1px solid #b9b9b9"
      accessibility-label="Learn more about this purple button"
    />
  </view>
</template>

<script>
import * as Permissions from "expo-permissions";
import { Camera } from "expo-camera";

export default {
  data() {
    return {
      hasCameraPermission: false,
      type: Camera.Constants.Type.back,
    };
  },
  methods: {
    takePicture() {
      Permissions.askAsync(Permissions.CAMERA)
        .then((status) => {
          hasCameraPermission = status.status == "granted" ? true : false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  components: { Camera },
};
</script>

<style>
.container {
  flex: 1;
}
.main-text {
  color: white;
  text-align: center;
  margin-top: 30px;
  background-color: #197de1;
}
</style>

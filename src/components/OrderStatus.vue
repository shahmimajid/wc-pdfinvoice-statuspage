<template>
  <div class="hello">
    <h1>Order Status</h1>
    <div>
      <p>Year of Order Process: {{ year }}</p>
      <p>Order Process / Total Order: {{ orderProcess }} / {{ totalOrder }}</p>
      <p>Last Update: {{ lastUpdate }}</p>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import io from "socket.io-client";

export default {
  setup() {
    const year = ref("");
    const orderProcess = ref(0);
    const totalOrder = ref(0);
    const lastUpdate = ref("");

    onMounted(() => {
      const socket = io("http://localhost:8000");
      socket.on("order_status", (data) => {
        year.value = data.year;
        orderProcess.value = data.orderProcess;
        totalOrder.value = data.totalOrder;
        lastUpdate.value = data.lastUpdate;
      });
    });

    return {
      year,
      orderProcess,
      totalOrder,
      lastUpdate
    };
  }
};
</script>
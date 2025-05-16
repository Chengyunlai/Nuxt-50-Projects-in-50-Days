<script setup lang="ts">
  const currentIndex = ref<Number>(0);
  const circles = ref<NodeListOf<HTMLDivElement>>();
  const process = ref<HTMLDivElement>();
  onMounted(() => {
    circles.value = document.querySelectorAll<HTMLDivElement>('.circle');
    process.value = document.getElementById('process') as HTMLDivElement;
  });

  const prevBtnClick = ()=>{
    currentIndex.value --;
    if(currentIndex.value < 0){
      currentIndex.value = 0;
    }
    update()
  }

  const nextBtnClick = ()=>{
    currentIndex.value ++;
    if(currentIndex.value > 3){
      currentIndex.value = 3;
    }
    update()
  }

  const update = () => {
    circles.value?.forEach && circles.value.forEach((circle, idx) => {
      // 如果当前索引小于当前激活的步骤，则添加active样式
      if(idx <= currentIndex.value) {
        circle.classList.add('active')
      } else {
        // 否则移除active样式
        circle.classList.remove('active')
      }
    })

    // 更新 width
    const activeCircles = document.querySelectorAll('.active')
    process.value?.style && (process.value.style.width = (activeCircles.length - 1) / (circles.value?.length - 1) * 100 + '%');
  };
</script>

<template>
  <div>
    <!--整体进度条的样式-->
    <div class="process-container w-[350px] flex justify-between text-center mb-10 relative">
      <!--process-->
      <div class="process" id="process"></div>
      <!--circle-->
      <div class="circle">1</div>
      <div class="circle">2</div>
      <div class="circle">3</div>
      <div class="circle">4</div>
    </div>
    <div class="flex justify-center space-x-4">
      <UButton :disabled="currentIndex === 0" color="neutral" variant="outline" @click="prevBtnClick()">Prev</UButton>
      <UButton :disabled="currentIndex === 3" color="neutral" variant="outline" @click="nextBtnClick()">Next</UButton>
    </div>
  </div>
</template>

<style scoped>
.process-container::before{
  content: "";
  background-color: #f2f2f2;
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  z-index: -1;
  width: 100%;
  height: 4px;
}

.process{
  background-color: #3498db;
  width: 0px;
  height: 4px;
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  z-index: -1;
  transition: 0.4s ease;
}

.circle {
  background-color: #e2e2e2;
  border: 3px solid #f2f2f2;
  color:#000;

  height: 35px;
  width: 35px;
  border-radius: 50%;

  display: flex;
  align-items: center;
  justify-content: center;

  transition: 0.4s ease;
}

.circle.active {
  border-color: #3498db;
}
</style>
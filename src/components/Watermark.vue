<script lang="ts" setup>
import { onMounted } from "vue";
onMounted(() => {
  /** 页面初始化时创建 canvas 元素,并回执画布*/
  createCanvasContainer();
  /** 监听 dom 文档,如果当子元素发生增删改都会触发该监听时间 */
  observer.observe(document.body, {
    attributes: true, /**表示观察节点和子节点属性发生变化,触发回调 */
    childList: true,/**观察目标节点和子节点标签增删改的时候触发 */
    subtree: true,/**观察目标节点的整个子树 */
  });
});

/**实例化观察标签实例 */
const observer = new MutationObserver((mutations) => {
  /**当观察到元素属性发生变化的时候,删除当前元素 */
  if (
    mutations[0].type === "attributes" &&
    (mutations[0].target as any).id === "watermarkCanvas"
  ) {
    document.getElementById("watermarkCanvas")?.remove();
  }
  /**当观察元素标签被删除后重新创建一个新的水印标签 */
  if(mutations[0].type === "childList" && (mutations[0].removedNodes[0] as any)?.id === "watermarkCanvas"){
    createCanvasContainer();
  }
});

/**创建 canvas */
const createCanvas = () => {
  var canvas = document.getElementById("watermarkCanvas");
  var ctx = (canvas as any).getContext("2d");
  // 设置Canvas尺寸为窗口大小
  (canvas as any).width = window.innerWidth;
  (canvas as any).height = window.innerHeight;
  // 设置水印样式
  var fontSize = 15;
  ctx.font = fontSize + "px Arial";
  ctx.fillStyle = "rgba(0, 0, 0, 0.1)";
  ctx.textAlign = "center";
  ctx.textBaseline = "middle";
  // 角度转弧度
  var angle = (-45 * Math.PI) / 180;
  // 计算水印密度
  var density = 100; // 每100像素间隔一个水印
  // 绘制水印
  for (
    var x = -(canvas as any).width;
    x < (canvas as any).width;
    x += density
  ) {
    for (
      var y = -(canvas as any).height;
      y < (canvas as any).height;
      y += density
    ) {
      ctx.save();
      ctx.translate(x, y);
      ctx.rotate(angle);
      ctx.fillText("龚箭前端", 0, 0);
      ctx.restore();
    }
  }
};

/**创建 canvas 容器 */
const createCanvasContainer = () => {
  const canvas: any = document.createElement("Canvas");
  canvas.width = 100;
  canvas.height = 300;
  canvas.id = "watermarkCanvas";
  canvas.style.position = "fixed";
  canvas.style.top = "0";
  canvas.style.left = "0";
  canvas.style.zIndex = "9999";
  canvas.style.pointerEvents = "none";
  document.body.appendChild(canvas);
  createCanvas();
};
</script>

<style scoped>
</style>
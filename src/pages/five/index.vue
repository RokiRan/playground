<script lang='ts' setup>
const boxContainer = ref<HTMLDivElement>()
enum ChessState {
  HIDDEN,
  NUMBER,
  SHOW,
  BOOM,
  FLAG,
}
interface Chess {
  id: number
  state: ChessState // 翻开状态
  core: boolean // 是否是炸弹
  x: number
  y: number
  boomsNum: number
}
const chessLines = 20
const chessBoard = reactive<Chess[]>([])
const posArr = [[-1, -1], [-1, 0], [-1, 1], [1, -1], [1, 0], [1, 1], [0, -1], [0, 1]]

const aroundCal = (item: Chess, fn: Function) => { // 循环周围的点，并自行处理
  posArr.forEach((arr) => {
    const targetPos = {
      x: item.x + arr[0],
      y: item.y + arr[1],
    }
    if (targetPos.x >= 0 && targetPos.y >= 0 && targetPos.x < 20 && targetPos.y < 20) {
      // 坐标有效
      const target = chessBoard[targetPos.x + targetPos.y * chessLines]
      fn(target)
    }
  })
}
const showAround = (item: Chess) => {
  aroundCal(item, (_: Chess) => {
    if (_.boomsNum === 0 && !_.core) {
      _.state = ChessState.NUMBER // 翻开
      // 显示当前点周围的炸弹数
      aroundCal(_, (__: Chess) => {
        __.state = ChessState.NUMBER
      })
    }
  })
}
const openBox = (item: Chess) => {
  // item.state = (item.state + 1) % 4
  if (item.core) {
    // 结束游戏
    item.state = ChessState.BOOM
  }
  else {
    // 翻开
    if (item.state === ChessState.NUMBER)
      return
    item.state = ChessState.NUMBER
    // 将周围的炸弹数显示出来
    showAround(item)
  }
}
const flagBox = (item: Chess) => {
  item.state = ChessState.FLAG
}
const cal = (x: number, y: number): number => {
  return chessBoard[x + y * chessLines]?.core ? 1 : 0
}
const init = () => {
  chessBoard.splice(0, chessBoard.length)
  // 初始化
  for (let item = 0; item < chessLines * chessLines; item++) {
    chessBoard.push({
      id: item,
      state: ChessState.HIDDEN,
      core: Math.random() < 0.1,
      x: parseInt((item % (chessLines)) as unknown as string), // 思考一下坐标算法
      y: parseInt((item / (chessLines)) as unknown as string),
      boomsNum: 0,
    })
  }
  // 计算每个box周围的炸弹数量
  chessBoard.forEach((item) => {
    let num = 0
    aroundCal(item, (_) => {
      num += cal(_.x, _.y)
    })
    item.boomsNum = num
  })
}
const start = () => {
  init()
}
onMounted(() => {
  init()
  boxContainer.value!.oncontextmenu = function (event: MouseEvent) {
    // 阻止右键
    event.preventDefault()
  }
})
</script>

<template>
  <div ref="boxContainer" select-none>
    <button btn @click="start">
      Start
    </button>
    <div w-160 h-160 mx-auto display="inline-block'" flex="~ wrap">
      <div v-for="box in chessBoard" :key="box.id" inline-block w-8 h-8 @click="openBox(box)" @auxclick="flagBox(box)">
        <div v-if="box.state === ChessState.NUMBER" h-8 w-8 text-5 :class="box.core ? 'c-red' : ''">
          {{ box.boomsNum !== 0 ? box.boomsNum : ' ' }}
        </div>
        <div v-else-if="box.state === ChessState.HIDDEN" i-carbon-circle-dash h-8 w-8 />
        <div v-else-if="box.state === ChessState.SHOW" i-carbon-face-activated h-8 w-8 />
        <div v-else-if="box.state === ChessState.BOOM" i-carbon-window-black-saturation h-8 w-8 />
        <div v-else i-carbon-flag h-8 w-8 />
      </div>
    </div>
  </div>
</template>

<style>
.flag{

}
</style>

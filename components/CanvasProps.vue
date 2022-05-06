<template>
  <div>
    <!-- 选中为空 -->
    <!-- <div v-if="!props.node && !props.line && !props.multi">
      <div class="title">欢迎使用le5le-topology！</div>
      <div class="group">
        <a class="star" href="https://github.com/le5le-com/topology" target="_blank">喜欢，点击这里打个star吧</a>
        <a href="https://www.yuque.com/alsmile/topology" target="_blank">使用教程</a>
        <br />
        <a
          href="http://topology.le5le.com/assets/img/topology_wechat.jpg?t=1"
          target="_blank"
        >微信交流群（大群）</a>
        <br />
        <a href="http://topology.le5le.com/assets/img/topology_wechat2.jpg" target="_blank">微信交流群2</a>
        <br />
        <a href="https://www.yuque.com/alsmile/topology/faq#EVbCgt" target="_blank">联系我们</a>
      </div>
      <div class="title">[Todo] 未来规划</div>
      <ul class="group">
        <li>Github issues</li>
        <li>React demo</li>
        <li>Vue3 demo</li>
        <li>系列教程</li>
      </ul>
      <div class="bottom">
        <div class="title">小提示</div>
        <ul class="group">
          <li>方向键：控制节点移动5个像素</li>
          <li>Ctrl + 方向键：控制节点移动1个像素</li>
          <li>Ctrl + 鼠标移动：移动整个画布</li>
          <li>Ctrl + 鼠标滚轮：缩放</li>
          <li>添加或选中节点，右侧属性支持上传各种图片哦</li>
        </ul>
      </div>
    </div> -->
    <!-- 选中节点 -->
    <div v-if="props.node">
      <div class="title">位置和大小</div>
      <div class="items">
        <div class="flex grid">
          <div>X（px）</div>
          <div class="ml5">Y（px）</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input-number
              v-model="props.node.rect.x"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
          <div class="ml5">
            <el-input-number
              v-model="props.node.rect.y"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div>宽（px）</div>
          <div class="ml5">高（px）</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input-number
              v-model="props.node.rect.width"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
          <div class="ml5">
            <el-input-number
              v-model="props.node.rect.height"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
        </div>
      </div>
      <div class="items" v-if="props.node.is3D">
        <div class="flex grid">
          <div>Z（px）</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input-number
              v-model="props.node.z"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div title="百分比%对应的小数值">圆角（0 - 1）</div>
          <div class="ml5">旋转（°）</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input-number
              v-model="props.node.borderRadius"
              controls-position="right"
              @change="onChange"
              :min="0"
              :max="1"
              :step="0.1"
            ></el-input-number>
          </div>
          <div class="ml5">
            <el-input-number
              v-model="props.node.rotate"
              controls-position="right"
              @change="onChange"
            ></el-input-number>
          </div>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div title="padding-left">内边距-左</div>
          <div title="padding-right" class="ml5">内边距-右</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input
              size="small"
              v-model="props.node.paddingLeft"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
          <div class="ml5">
            <el-input
              size="small"
              v-model="props.node.paddingRight"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div title="padding-top">内边距-上</div>
          <div title="padding-bottom" class="ml5">内边距-下</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input
              size="small"
              v-model="props.node.paddingTop"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
          <div class="ml5">
            <el-input
              size="small"
              v-model="props.node.paddingBottom"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
        </div>
      </div>
      <div class="items gray" style="line-height: 1.5">
        内边距：输入数字表示像素；输入%表示百分比
      </div>
      <div class="items" v-if="props.node.tipId == 'video'">
        <div class="flex grid">
          <div title="padding-left">视频播放地址</div>
        </div>
        <div class="flex grid">
          <el-input
            size="small"
            v-model="props.node.video"
            controls-position="right"
            @change="onChange"
          ></el-input>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div title="padding-left">Id(自定义组件的ID)</div>
        </div>
        <div class="flex grid">
          <el-input
            size="small"
            v-model="props.node.id"
            controls-position="right"
            @change="onChange"
          ></el-input>
        </div>
      </div>
      <div class="items">
        <div class="flex grid">
          <div title="padding-left">添加事件</div>
        </div>
        <div class="flex grid">
          <el-select v-model="playAnimate" size="small" @change="selectMap()">
            <el-option
              v-for="item in eventOption"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>
      <div class="title" v-if="props.node.tipId == 'dianji1'">切换状态</div>
      <div class="items" v-if="props.node.tipId == 'dianji1'">
        <div class="flex grid">
          <div title="padding-left"></div>
        </div>
        <div class="flex grid">
          <el-select
            v-model="props.node.image"
            size="small"
            @change="selectMap()"
          >
            <el-option
              v-for="item in dianjiOption"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>
      <div class="items" v-if="props.node.tipId == 'fengji'">
        <div class="flex grid">
          <div title="padding-left"></div>
        </div>
        <div class="flex grid">
          <el-select
            v-model="props.node.image"
            size="small"
            @change="selectMap()"
          >
            <el-option
              v-for="item in fengjiOption"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>
      <div class="items" v-if="props.node.tipId == 'famen'">
        <div class="flex grid">
          <div title="padding-left"></div>
        </div>
        <div class="flex grid">
          <el-select
            v-model="props.node.image"
            size="small"
            @change="selectMap()"
          >
            <el-option
              v-for="item in famenOption"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>
      <div class="items" v-if="props.node.tipId == 'tuijiu'">
        <div class="flex grid">
          <div title="padding-left"></div>
        </div>
        <div class="flex grid">
          <el-select
            v-model="props.node.image"
            size="small"
            @change="selectMap()"
          >
            <el-option
              v-for="item in tuijiuOption"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </div>
      </div>

      <div class="title" v-if="props.node.name == 'text'">字体属性</div>
      <div class="items" v-if="props.node.name == 'text'">
        <div class="flex grid">
          <div title="padding-left">文字大小</div>
          <div title="padding-right" class="ml5">文字颜色</div>
        </div>
        <div class="flex grid">
          <div>
            <el-input
              size="small"
              v-model="props.node.font.fontSize"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
          <div class="ml5">
            <el-input
              size="small"
              v-model="props.node.font.color"
              controls-position="right"
              @change="onChange"
            ></el-input>
          </div>
        </div>
      </div>
      <div class="title">自定义数据源</div>
      <div class="items">
        <div class="flex grid">
          <div>切换数据源</div>
        </div>
        <div class="flex grid">
          <div class="ml5">
            <el-select
              v-model="props.node.origin"
              size="small"
              @change="selectMap()"
            >
              <el-option
                v-for="item in originOption"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option>
            </el-select>
          </div>
        </div>
      </div>
      <div class="title"></div>
      <div class="items">
        <div class="flex grid">
          <div class="custom-data">
            自定义数据
            <i
              :class="props.expand ? 'el-icon-zoom-out' : 'el-icon-zoom-in'"
              @click="changeExpand"
              size="small"
              >{{ props.expand ? '缩小' : '放大' }}</i
            >
          </div>
        </div>
        <div class="flex grid">
          <div :class="props.expand ? 'expand-data' : ''">
            <el-input
              type="textarea"
              v-model="nodeData"
              :rows="props.expand ? 15 : 3"
              @change="onChange"
            ></el-input>
          </div>
        </div>
      </div>
    </div>
    <div class="draMap" v-else>
      <el-select
        v-model="draMap"
        placeholder="请选择背景图"
        size="small"
        @change="selectMap()"
      >
        <el-option
          v-for="item in mapOption"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
      <div class="line" v-if="props.line">
        <div class="title" v-if="props.line.name == 'line'">线条属性</div>
        <div class="items" v-if="props.line.name == 'line'">
          <div class="flex grid">
            <div title="padding-left">线条宽度</div>
            <div title="padding-right" class="ml5">线条颜色</div>
          </div>
          <div class="flex grid">
            <div>
              <el-input
                size="small"
                v-model="props.line.lineWidth"
                controls-position="right"
                @change="onChange"
              ></el-input>
            </div>
            <div class="ml5">
              <el-input
                size="small"
                v-model="props.line.strokeStyle"
                controls-position="right"
                @change="onChange"
              ></el-input>
            </div>
          </div>
          <div class="title" v-if="props.line.name == 'line'">线条动画属性</div>
          <div class="flex grid">
            <div title="padding-left">动画颜色</div>
            <div title="padding-right" class="ml5">动画速度</div>
          </div>
          <div class="flex grid">
            <div>
              <el-input
                size="small"
                v-model="props.line.animateColor"
                controls-position="right"
                @change="onChange"
              ></el-input>
            </div>
            <div class="ml5">
              <el-input
                size="small"
                v-model="props.line.animateSpan"
                controls-position="right"
                @change="onChange"
              ></el-input>
            </div>
          </div>
          <div class="flex grid">
            <div title="padding-left">动画开关</div>
            <div title="padding-right" class="ml5">动画类型</div>
          </div>
          <div class="flex grid">
            <div>
              <el-select
                v-model="props.line.animatePlay"
                size="small"
                @change="onChange(1)"
              >
                <el-option label="开" :value="true"> </el-option>
                <el-option label="关" :value="undefined"> </el-option>
              </el-select>
            </div>
            <div class="ml5">
              <el-input
                size="small"
                v-model="props.line.animateType"
                @change="onChange"
                controls-position="right"
              ></el-input>
            </div>
          </div>
        </div>
      </div>

      <!-- <el-button @click="saveMap()" size="small" style="margin-top:24px">
        保存
      </el-button> -->
    </div>
  </div>
</template>

<script >
export default {
  data() {
    return {
      nodeId: null,
      nodeIsJson: false,
      nodeData: '',
      origin: '1',
      playAnimate: null,
      eventOption: [
        {
          label: '开启动画',
          value: 1,
        },
        {
          label: '关闭动画',
          value: 0,
        },
      ],
      originOption: [
        {
          label: '简阳数据',
          value: '1',
        },
        {
          label: '北京数据',
          value: '2',
        },
      ],
      tuijiuOption: [
        {
          label: '停用',
          value: '/img/DC/tuijiu0.png',
        },
        {
          label: '正常',
          value: '/img/DC/tuijiu1.png',
        },
        {
          label: '报警',
          value: '/img/DC/tuijiu2.png',
        },
      ],
      famenOption: [
        {
          label: '开启',
          value: '/img/DC/famen11.png',
        },
        {
          label: '关闭',
          value: '/img/DC/famen12.png',
        },
      ],
      dianjiOption: [
        {
          label: '停用',
          value: '/img/DC/dianji0.png',
        },
        {
          label: '正常',
          value: '/img/DC/dianji1.png',
        },
        {
          label: '报警',
          value: '/img/DC/dianji2.png',
        },
      ],
      fengjiOption: [
        {
          label: '停用',
          value: '/img/DC/fengji0.png',
        },
        {
          label: '正常',
          value: '/img/DC/fengji1.png',
        },
        {
          label: '报警',
          value: '/img/DC/fengji2.png',
        },
      ],
      draMap: '/_nuxt/static/img/DC/ZT.png',
      mapOption: [
        {
          label: '工程图',
          value: '/_nuxt/static/img/DC/ZT.png',
        },
        {
          label: '默认空白',
          value: '',
        },
      ],
    }
  },
  props: {
    props: {
      type: Object,
      require: true,
    },
  },
  updated() {
    console.log(this.props, 3333333333333)
    if (!this.props.node || this.nodeId === this.props.node.id) {
      return
    }

    this.props.expand = false
    this.nodeId = this.props.node.id
    let originData = this.props.node.data
    this.nodeIsJson = this.isJson(originData)
    this.nodeData = this.nodeIsJson
      ? JSON.stringify(originData, null, 4)
      : (this.nodeData = originData)
  },
  methods: {
    selectMap() {
      this.$emit('mapChange', this.draMap)
    },
    onChange(type = 0) {
      if (this.props.node) {
        this.props.node.data = this.nodeIsJson
          ? JSON.parse(this.nodeData)
          : this.nodeData
      }
      if (type == 1) {
        this.props.line.animateStart = null
        this.$emit('change', type,this.props.line)
      }
      this.$emit('change', type,this.props.node)
    },
    changeExpand() {
      this.props.expand = !this.props.expand
    },
    isJson(obj) {
      return (
        typeof obj == 'object' &&
        Object.prototype.toString.call(obj).toLowerCase() ==
          '[object object]' &&
        !obj.length
      )
    },
  },
}
</script>

<style lang="scss">
.star {
  display: block;
  color: #f60 !important;
  text-decoration: underline;
  margin-bottom: 0.1rem;
}

.title {
  color: #0d1a26;
  font-weight: 600;
  padding: 0.05rem 0.15rem;
  border-bottom: 1px solid #ccc;
}

.group {
  margin: 0.1rem 0 0.2rem 0.3rem;
  padding: 0;

  a,
  li {
    line-height: 2;
  }

  li {
    list-style: initial;
  }
}

.bottom {
  position: absolute;
  bottom: 0.1rem;
}

.items {
  padding: 0.05rem 0.15rem;

  .el-input-number {
    width: 1.02rem;
    line-height: 0.32rem;

    .el-input__inner {
      padding-left: 0;
      padding-right: 40px;
      height: 0.34rem;
      line-height: 0.34rem;
    }

    .el-input-number__increase {
      line-height: 0.16rem;
    }
  }

  .custom-data i {
    cursor: pointer;
    float: right;
    color: #409eff;
    height: 2em;
    line-height: 2em;
  }

  .expand-data {
    position: absolute;
    right: 0.15rem;
    width: 5rem;
  }
}

.formItem {
  margin-bottom: 0.1rem;
}
.draMap {
  padding: 8px;
}
</style>

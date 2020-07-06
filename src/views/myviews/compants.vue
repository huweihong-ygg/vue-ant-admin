<template>
  <div class="myheader">
    <header>header</header>
    <div>
      <div class>倒计时功能</div>
      <count-down :target="new Date().getTime() + 3000000" :on-end="onEndHandle" />
    </div>
    <div>
      <div class>用户头像列表</div>
      <avatar-list size="mini">
        <avatar-list-item
          tips="Jake"
          src="https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png"
        />
        <avatar-list-item
          tips="Andy"
          src="https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
      </avatar-list>
      <avatar-list :max-length="3">
        <avatar-list-item
          tips="Jake"
          src="https://gw.alipayobjects.com/zos/rmsportal/zOsKZmFRdUtvpqCImOVY.png"
        />
        <avatar-list-item
          tips="Andy"
          src="https://gw.alipayobjects.com/zos/rmsportal/sfjbOqnsXXJgNCjCzDBL.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
        <avatar-list-item
          tips="Niko"
          src="https://gw.alipayobjects.com/zos/rmsportal/kZzEzemZyKLKFsojXItE.png"
        />
      </avatar-list>
    </div>
    <div>
      <div>chart图表</div>
      <chart-card title="总销售量">
        <a-icon type="buy" slot="action" />
        <span slot="total">$ 100.00</span>
        <span>周同比 12%</span>
      </chart-card>

      <chart-card title="总销售量" :total="() => '$ 1100.00'">
        <a-icon type="buy" slot="action" />
        <span>周同比 12%</span>
      </chart-card>

      <chart-card title="总销售量" total="$ 100.00">
        <a-icon type="buy" slot="action" />
        <span>周同比 12%</span>
      </chart-card>
    </div>
   

    <div>
      <div>图标选择</div>
      <a-card :body-style="{padding: '24px 32px'}" :bordered="false">
        <icon-selector v-model="currentSelectedIcon" @change="handleIconChange" />

        <a-divider />
        <p>测试 IconSelector 组件 v-model 功能</p>
        <a-button @click="changeIcon('down')">改变 Icon-down</a-button>
        <a-divider type="vertical" />
        <a-button @click="changeIcon('cloud-download')">改变 Icon-cloud-download</a-button>
      </a-card>
    </div>
    <div>
      <a-button v-action:add>添加用户</a-button>
      <a-button v-action:delete>删除用户</a-button>
      <a v-action:edit @click="edit(record)">修改</a>
    </div>
  </div>
</template>

<script>
import { CountDown } from '@/components'
import { AvatarList } from '@/components'
import { ChartCard } from '@/components'
import IconSelector from '@/components/IconSelector'
const AvatarListItem = AvatarList.AvatarItem
export default {
  components: {
    CountDown,
    AvatarList,
    AvatarListItem,
    ChartCard,
    IconSelector
  },
  data() {
    return {
        loading:true,
      currentSelectedIcon: 'pause-circle'
    }
  },
  methods: {
      validate(){},
      onEndHandle(){},
    handleIconChange(icon) {
      console.log('change Icon', icon)
      this.$message.info(
        <span>
          选中图标 <code>{icon}</code>
        </span>
      )
    },
    changeIcon(type) {
      this.currentSelectedIcon = type
    }
  }
}
</script>

<style>
.myheader {
  width: 100%;
  /* height: 60vh; */
  background: #fff;
}
</style>
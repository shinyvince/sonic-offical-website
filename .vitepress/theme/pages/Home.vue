<template>
  <!-- 开屏内容 -->
  <section class="hero">
    <div class="hero__left">
      <!-- 开屏背景 -->
      <div class="os-bg-base"></div>
      <div class="os-bg-base os-bg1"></div>
      <div class="os-bg-base os-bg2"></div>

      <!-- 品牌标语 -->
      <h1 class="brand-slogan">“ For You，For Free，Forever ”</h1>

      <!-- 品牌数据统计 -->
      <div class="statistics">
        <template v-for="item in statisticsData" :key="item.tipContent">
          <client-only>
            <el-tooltip :content="item.tipContent" placement="top">
              <a :href="item.linkUrl" class="statistics-link" target="_blank">
                <img :src="item.img" />
              </a>
            </el-tooltip>
          </client-only>
        </template>
      </div>

      <!-- 品牌描述 -->
      <h4 class="brand-desc">
        免费开源的云真机测试平台，用心打造更好的使用体验。
      </h4>

      <!-- entry -->
      <div class="entry-operation">
        <el-button
          type="primary"
          size="large"
          round
          @click="router.go('/deploy/back-end-deploy')"
        >
          马上使用
        </el-button>
        <el-button
          type="primary"
          size="large"
          round
          @click="open('https://sonic-cloud.wiki/')"
        >
          用户社区
        </el-button>
      </div>

      <!-- 脚标 -->
      <h5 class="footmark">Made with 🧡 by SonicCloudOrg</h5>
    </div>
    <div class="hero__right">
      <video width="800" controls :src="demo" />
    </div>
  </section>

  <!-- 主体内容 -->
  <div class="container">
    <section-box title="最新动态">
      <div class="news">
        <el-carousel
          style="margin-top: 30px"
          height="400px"
          indicator-position="outside"
          :interval="3000"
        >
          <el-carousel-item v-for="item in news">
            <div
              :style="
                'background:linear-gradient(to bottom right, rgba(64,158,255, 0.3), rgba(0, 0, 0, 0.8)) ,url(' +
                item.pic +
                ');'
              "
              class="news-banner"
            >
              <span class="news-banner__title">
                {{ item.title }}
              </span>
              <h3 class="news-banner__time" v-if="item.time">
                {{ item.time }}
              </h3>
              <el-button v-if="item.url" type="primary" @click="open(item.url)">
                查看
              </el-button>
            </div>
          </el-carousel-item>
        </el-carousel>
      </div>
    </section-box>
    <section-box title="Sonic荣誉墙">
      <div class="honor-wall">🎉 MTSC 2022年度最佳开源项目评选第一名</div>
    </section-box>

    <section-box title="Sonic支持哪些设备？">
      <div class="devices">
        <el-card
          class="card-content"
          :body-style="{
            display: 'flex',
            flexDirection: 'column',
            justifyContent: 'center',
            alignItems: 'center',
            width: '180px'
          }"
          shadow="hover"
          v-for="item in devices"
        >
          <img width="50" :src="item.image" />
          <p>{{ item.name }}</p>
        </el-card>
      </div>
    </section-box>
    <section-box title="为什么使用Sonic？">
      <div class="use-case">
        <el-card class="case-content" shadow="hover">
          <img :src="team4" width="40" />
          <h3>0编码UI自动化</h3>
          <p>积木式创建步骤</p>
          <p>一键分发多设备任务</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team" width="40" />
          <h3>在线代理抓包</h3>
          <p>一键连接代理抓包</p>
          <p>团队协作轻松快捷</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team2" width="40" />
          <h3>设备分布式集群</h3>
          <p>支持跨网段多机房</p>
          <p>支持Windows、Mac、Linux平台</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team3" width="40" />
          <h3>优秀周边生态</h3>
          <p>安卓Apk、iOS调试工具</p>
          <p>Jenkins插件、在线抓包工具</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team5" width="40" />
          <h3>低成本维护</h3>
          <p>拖拽式排序交互</p>
          <p>使用简单便捷</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team6" width="40" />
          <h3>在线WebView</h3>
          <p>提供在线调试WebView</p>
          <p>一键便利连接devtools</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team7" width="40" />
          <h3>可视化报表</h3>
          <p>测试截图、日志、录像</p>
          <p>图表展示项目运行情况</p>
        </el-card>
        <el-card class="case-content" shadow="hover">
          <img :src="team8" width="40" />
          <h3>轻松部署维护</h3>
          <p>Docker一键去中心化分布式</p>
          <p>扩容缩容不再繁琐</p>
        </el-card>
      </div>
    </section-box>
    <section-box title="Sonic的价值与产出">
      <div class="capacity-wrapper">
        <img class="capacity-img" :src="msg" />
        <el-timeline class="capacity-list" style="text-align: left">
          <el-timeline-item type="primary" :hollow="true">
            Sonic提供图像识别，支持获取poco控件，助力游戏公司测试效率。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            使用Sonic进行跨网段部署，助力海外业务的公司进行专项检测。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            提供定时任务充分利用无人值守时间回归UI测试，省时省力。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            完全开源免费的平台，快速的更新迭代速度，创造了多个领域新技术。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            支持打通Jenkins的DevOps流程，推进项目自动化流程。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            支持无限扩容设备，一键使用Android、iOS设备调试，设备管理不再繁琐。
          </el-timeline-item>
          <el-timeline-item type="primary" :hollow="true">
            丰富图表展示，用户实时洞察用例执行情况，把控产品质量。
          </el-timeline-item>
        </el-timeline>
      </div>
    </section-box>

    <section-box title="金牌赞助商">
      <div class="sponsor">
        <div class="sponsor__list">
          <a href="https://www.testing-studio.com/" target="_blank">
            <img
              src="https://ceshiren.com/uploads/default/original/3X/7/0/70299922296e93e2dcab223153a928c4bfb27df9.jpeg"
              alt="霍格沃兹测试开发学社"
              width="350"
            />
          </a>
          <a
            style="margin-left: 20px"
            href="https://ec.diwork.com/"
            target="_blank"
          >
            <img
              src="https://ec.diwork.com/html/index/img/newlogo.png"
              alt="友空间"
              width="350"
            />
          </a>
        </div>
        <a class="" href="mailto:291028775@qq.com" target="_blank">
          <el-button
            type="primary"
            plain
            style="width: 150px; margin-top: 30px"
          >
            成为赞助商
          </el-button>
        </a>
      </div>
    </section-box>

    <section-box title="Sonic摘星计划贡献墙">
      <div class="cons-wall">
        <div class="more-user">部分用户荣誉证书展示</div>
        <el-carousel type="card" height="280px">
          <el-carousel-item v-for="conItem in conList" :key="conItem">
            <el-image style="height: 280px" :src="conItem" />
          </el-carousel-item>
        </el-carousel>
        <el-button
          type="primary"
          size="large"
          @click="open('https://sonic-cloud.wiki/d/1510-soniccommitsonic')"
        >
          我要上墙
        </el-button>
      </div>
    </section-box>

    <section-box title="贡献者们">
      <div style="text-align: center">
        <img
          style="display: inline-block"
          src="https://opencollective.com/soniccloudorg/contributors.svg?width=800&button=false"
          alt="contribute"
          width="950"
        />
      </div>
    </section-box>
  </div>
</template>

<script setup lang="ts">
import SectionBox from '../components/SectionBox.vue'

// 图片资源
// news
import honor from '../assets/honor.png'
import c1 from '../assets/banner.png'
import c2 from '../assets/banner2.png'
import c5 from '../assets/banner4.png'
import demo from '../assets/video/demo.mp4'
// 贡献墙
import con1 from '../assets/cons/con1.jpg'
import con2 from '../assets/cons/con2.jpg'
import con3 from '../assets/cons/con3.jpg'
import con4 from '../assets/cons/con4.jpg'
import con5 from '../assets/cons/con5.jpg'
// 支持设备
import a1 from '../assets/ANDROID.jpg'
import a2 from '../assets/APPLE.jpg'
import a3 from '../assets/CAR.png'
import a4 from '../assets/WATCH.png'
// 使用场景
import team from '../assets/team.png'
import team2 from '../assets/team2.png'
import team3 from '../assets/team3.png'
import team4 from '../assets/team4.png'
import team5 from '../assets/team5.png'
import team6 from '../assets/team6.png'
import team7 from '../assets/team7.png'
import team8 from '../assets/docker.png'
// 价值与产出
import msg from '../assets/msg.png'
import { useRouter } from 'vitepress'

// 品牌数据统计
const statisticsData = [
  {
    tipContent: 'Sonic组织Follower数量',
    linkUrl: 'https://github.com/SonicCloudOrg',
    img: 'https://img.shields.io/github/followers/SonicCloudOrg?style=social'
  },
  {
    tipContent: 'Sonic组织所有仓库总Star数量',
    linkUrl: 'https://github.com/SonicCloudOrg',
    img: 'https://img.shields.io/github/stars/SonicCloudOrg?affiliations=OWNER&style=social'
  },
  {
    tipContent: 'Sonic社区总回复数',
    linkUrl: 'https://sonic-cloud.wiki',
    img: 'https://img.shields.io/badge/replies%20-14.2k-ff69b4?style=social&logo=LiveChat'
  },
  {
    tipContent: 'Agent端总下载量',
    linkUrl: 'https://github.com/SonicCloudOrg/sonic-agent/releases',
    img: 'https://img.shields.io/github/downloads/SonicCloudOrg/sonic-agent/total'
  }
]

// 最新动态
const news = [
  {
    title: 'Sonic 平台的移动性能监控初次探索',
    time: '万众期待下，Sonic还是把iOS和安卓的性能监控初版的答卷做出来了',
    url: 'https://sonic-cloud.wiki/d/2503-sonic',
    pic: honor
  },
  {
    title: '重磅！全新sib remote功能上线，iOS远程调试的福音！',
    time: '用户可以自己本地sib remote connect就可以像本地链接一样使用啦！',
    url: 'https://sonic-cloud.wiki/d/2058-sib-remoteios',
    pic: c5
  },
  {
    title: '恭喜Sonic获得MTSC 2022年度最佳开源项目评选第一名',
    time: '历时两个多月的初选、海选和专家评审后，「MTSC 2022年度最佳开源项目」评选终于尘埃落定',
    url: 'https://sonic-cloud.wiki/d/1471-sonicmtsc-2022',
    pic: c2
  }
]

// 贡献墙
const conList = [con1, con2, con3, con4, con5]

// 支持设备
const devices = [
  {
    image: a1,
    name: '安卓设备'
  },
  {
    image: a2,
    name: 'iOS设备'
  },
  {
    image: a3,
    name: '车载设备'
  },
  {
    image: a4,
    name: '智能手表'
  }
]

// 页面跳转
const open = (url: string): void => {
  window.open(url, '_blank')
}

const router = useRouter()
</script>

<style scoped lang="scss">
/* 开屏内容*/
.hero {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
  /* 减去顶部导航栏高度 */
  height: calc(100vh - 72px);
  padding: 120px 0;
  overflow-x: hidden;

  &__left {
    margin-right: 50px;
    text-align: center;
  }

  &__right {
    width: 800px;
  }
}

/* 开屏背景样式 */
.os-bg-base {
  position: absolute;
  bottom: 0;
  left: -50%;
  right: -50%;
  top: 0;
  opacity: 0.5;
  animation: slide 3s ease-in-out infinite alternate;
  background-image: linear-gradient(-60deg, #d1e3f6 50%, #9bdcf7 50%);
  z-index: -1;
}

.os-bg1 {
  animation-direction: alternate-reverse;
  animation-duration: 4s;
}

.os-bg2 {
  animation-duration: 5s;
}

@keyframes slide {
  0% {
    transform: translateX(-25%);
  }
  100% {
    transform: translateX(25%);
  }
}

/* 品牌标语 */
.brand-slogan {
  margin-top: 0;
  margin-bottom: 20px;
  line-height: 64px;
  font-size: 2.2rem;
  font-weight: 700;
  white-space: pre-wrap;
}

/* 品牌描述 */
.brand-desc {
  margin: 24px 0;
  font-size: 20px;
  font-weight: bold;
}

/* 品牌静态数据统计 */
.statistics {
  height: 20px;
}

.statistics-link {
  display: inline-block;
  height: 20px;
  margin-left: 20px;
}

.statistics-link:first-child {
  margin-left: 0;
}

/* entry */
// .entry-operation {
// }

/* 脚标 */
.footmark {
  margin-top: 20px;
}

/* 主体内容 */
.container {
  width: 1200px;
  margin: 0 auto;
}

/* 最新动态 */
.news {
  padding: 0 140px;
}

.news-banner {
  position: fixed;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-size: cover;
  color: aliceblue;
  overflow: hidden;

  &__title {
    display: block;
    font-size: 1.5em;
    margin-block-start: 0.83em;
    margin-block-end: 0.83em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    font-weight: bold;
  }

  &__time {
    font-size: 1.2em;
    font-weight: bold;
    margin-bottom: 0.83em;
  }
}

/* 荣誉墙 */
.honor-wall {
  text-align: center;
}

/* 贡献墙 */
.cons-wall {
  padding: 0 20%;
  text-align: center;
}

.more-user {
  margin-bottom: 15px;
  color: #909399;
  font-size: 14px;
}

/* 支持设备 */
.devices {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  margin: 0 190px;
}

.card-content {
  border-radius: 25px;
  img {
    display: block;
  }
  p {
    font-weight: bold;
    margin: 0;
  }
}

/* 使用场景 */
.use-case {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

.case-content {
  width: 270px;
  margin-bottom: 20px;
  border-radius: 25px;
  text-align: center;
  img {
    display: inline-block;
  }
  h3 {
    margin: 18px 0;
    font-size: 1.17em;
    font-weight: bold;
  }
  p {
    margin: 16px 0;
    font-size: 15px;
  }
}

/* 价值与产出 */
.capacity-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}

.capacity-img {
  height: 300px;
}

/* 快速开始 */
.quick-start {
  display: flex;
  justify-content: center;
}

/* 赞助商 */
.sponsor {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  &__list {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  a {
    display: inline-block;
  }
}

@media screen and (max-width: 820px) {
  .container {
    width: 100%;
    margin: 0 auto;
  }

  .news {
    padding: 0;
  }

  .news-title {
    font-size: 22px;
  }

  .news-time {
    font-size: 14px;
  }

  .sponsor img {
    width: 300px;
  }

  .devices {
    margin: 0;
  }

  .card-content {
    width: 165px;
    margin-bottom: 14px;
  }
  .case-content {
    width: 170px;
    margin-bottom: 10px;
  }

  .capacity-wrapper {
    position: relative;
    display: inline-block;
    margin-top: 10px;
  }

  .capacity-img {
    position: absolute;
    left: 50%;
    top: 50%;
    height: 300px;
    margin-bottom: 30px;
    transform: translate(-50%, -50%);
    opacity: 0.05;
    filter: blur(2px);
  }

  .capacity-list {
    padding-right: 40px;
  }
}
</style>

<template>
  <section class="md:fixed md:h-20 shadow-lg border-b z-30 md:bg-white w-full">
    <section class="container mx-auto relative hidden md:block">
      <NuxtLink to="/">
        <img src="http://www.cdymzs.com/statics/pc/images/logo.jpg" class="inline-block h-9 md:h-16" alt="logo" />
      </NuxtLink>
      <ul class="hidden md:inline-flex ml-72 h-14 space-x-16 mt-7">
        <li v-for="(nav, i) in navs" class="group">
          <NuxtLink :to="nav.url" class="flex items-center hover:text-red-600">
            {{nav.title}}
            <span v-show="nav.children">
              <i class="iconfont icon-caret-down group-hover:hidden duration-200"></i>
              <i class="iconfont icon-caret-up hidden group-hover:inline-block duration-200"></i>
            </span>
          </NuxtLink>
          <div 
            v-show="nav.children"
            class="absolute left-0 w-full top-20 shadow-lg justify-center bg-white space-x-32 group-hover:flex hidden py-3 text-gray-600"
            >
            <NuxtLink :to="child.url" v-for="child in nav.children" class="flex flex-col items-center hover:text-red-600">
              <i class="iconfont" :class="child.icon" style="font-size: 35px"></i>
              <p>{{child.title}}</p>
            </NuxtLink>
          </div>
        </li>
      </ul>
      
      <section class="hidden md:inline-flex float-right mt-5 items-center">
        <i class="iconfont icon-lianxi" style="font-size: 26px"></i>
        <span class="ml-2">{{web.tel}}</span>
      </section>
    </section>
  </section>
  <div class="md:hidden flex justify-center w-full">
    <NuxtLink to="/">
      <img src="http://www.cdymzs.com/statics/pc/images/logo.jpg" alt="logo" class="h-12" />
    </NuxtLink>
  </div>
  <div class="overflow-x-scroll md:hidden sticky bg-white shadow-md top-0 z-50 w-full overflow-hidden whitespace-nowrap py-1.5 scro space-x-6 px-3">
    <span v-for="(item, i) in mnavs" :class="{'text-red-500': i === activeId}" @click="menuBtn(i, item.url)">{{item.title}}</span>
  </div>
  <div class="md:h-20"></div>
</template>

<script lang='ts' setup>
import { IWebSite } from '@/config/tyings';
const { web } = inject<IWebSite>('website')!;
const router = useRouter();
const navs = [
  {title: '??????', url: '/'},
  {title: '????????????', url: '/house', children: [
    {title: '????????????', url: '/house', icon: 'icon-gonglve'},
    {title: '????????????', url: '/ruanzhuang', icon: 'icon-ruanzhuang'},
    {title: '????????????', url: '/old', icon: 'icon-yemianzhuangxiu'}
  ]},
  {title: '????????????', url: '/baojia'},
  {title: '????????????', url: '/case', children: [
    {title: '????????????', url: '/case?type=1', icon: 'icon-xingzhuang-tupian'},
    {title: 'VR??????', url: '/case?type=0', icon: 'icon-VR'},
    {title: '????????????', url: '/room', icon: 'icon-icon1'}
  ]},
  {title: '????????????', url: '/team'},
  {title: '????????????', url: '/news', children: [
    {title: '????????????', url: '/news?cate=1', icon: 'icon-taiji'},
    {title: '????????????', url: '/news?cate=2', icon: 'icon-book'},
    {title: '????????????', url: '/news?cate=3', icon: 'icon-wentijieda'},
  ]},
  {title: '????????????', url: '/about', children: [
    {title: '????????????', url: '/about', icon: 'icon-huiyuanhuangguanguanjun-xianxing'},
    {title: '????????????', url: '/news?cate=4', icon: 'icon-book'},
  ]},
]
const mnavs = [
  {title: '??????', url: '/'},
  {title: '????????????', url: '/house'},
  {title: '????????????', url: '/ruanzhuang'},
  {title: '????????????', url: '/old'},
  {title: '????????????', url: '/case?type=1'},
  {title: 'VR??????', url: '/case?type=0'},
  {title: '????????????', url: '/room'},
  {title: '????????????', url: '/team'},
  {title: '????????????', url: '/news?cate=1'},
  {title: '????????????', url: '/news?cate=2'},
  {title: '????????????', url: '/news?cate=3'},
  {title: '????????????', url: '/about'},
]

const activeId = ref(0)
const menuBtn = (i: number, url: string) => {
  activeId.value = i;
  router.push(url)
}
</script>

<style lang='less' scoped>
.scro::-webkit-scrollbar{
  display: none; /* Chrome Safari */
}
</style>
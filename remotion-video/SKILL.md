---
name: "remotion-video"
description: "Remotion React视频生成器：用React代码编写、渲染和导出视频。当用户说'生成视频'、'做动画视频'、'React视频'、'把图表做成视频'、'产品演示视频'、'数据动画'、'字幕视频'时触发。核心特点：React组件化视频、30+composition最佳实践、FFmpeg导出、程序化视频生成。"
---

> **来源**: 改编自 Remotion 官方 skill（github.com/remotion-dev/skills）
>
> **发布时间**: 2026-05-29
>
> **理念**: "视频不是拍出来的，是写代码写出来的。"

# 🎬 Remotion Video — React 视频生成器

用 **React + Remotion** 把代码变成视频——数据动画、产品演示、字幕视频、宣传短片，全部程序化生成。

---

## 🎯 和 HTML PPT 的区别

| 维度 | HTML PPT（html-ppt-skill） | Remotion Video |
|------|---------------------------|----------------|
| **输出格式** | HTML 幻灯片（浏览器播放） | MP4 / WebM 视频文件 |
| **交互性** | 可交互（点击、切换） | 不可交互，线性播放 |
| **动画能力** | CSS 动画 | 逐帧渲染、时间轴控制 |
| **音频** | ❌ 无 | ✅ 支持旁白、BGM、音效 |
| **适用场景** | 现场演示、汇报 | 社交媒体、宣传片、教程 |
| **技术栈** | HTML + CSS | React + Remotion + FFmpeg |

---

## 🛠️ 核心技术栈

```
Remotion        # React 视频框架
React 18+       # 组件化视频编写
TypeScript      # 类型安全
FFmpeg          # 视频编码导出
@remotion/player # 预览播放器
@remotion/cli    # 渲染命令行
```

### Remotion 核心概念

| 概念 | 说明 | 类比 |
|------|------|------|
| **Composition** | 视频场景定义（宽高、FPS、时长） | 舞台布景 |
| **Sequence** | 时间轴上的片段（什么时候开始、持续多久） | 镜头 |
| **Frame** | 单帧画面（Remotion 按 FPS 逐帧渲染） | 胶片格 |
| `useCurrentFrame()` | 获取当前帧号，驱动动画 | 时间指针 |
| `interpolate()` | 数值插值（实现缓动动画） | 动画曲线 |
| `spring()` | 弹簧物理动画 | 弹性动效 |

---

## 📁 项目结构模板

```
my-video/
├── src/
│   ├── compositions/       # 视频场景定义
│   │   ├── Main.tsx        # 主合成入口
│   │   ├── Intro.tsx       # 片头
│   │   └── DataViz.tsx     # 数据可视化片段
│   ├── components/         # 可复用视频组件
│   │   ├── TitleCard.tsx   # 标题卡片
│   │   ├── AnimatedBar.tsx # 动画柱状图
│   │   └── Subtitle.tsx    # 字幕组件
│   ├── hooks/
│   │   └── useAudio.ts     # 音频控制
│   ├── types/
│   │   └── video.ts        # 类型定义
│   └── index.tsx           # 注册所有 Composition
├── public/
│   ├── audio/              # 音频资源
│   ├── fonts/              # 字体文件
│   └── images/             # 图片素材
├── remotion.config.ts      # Remotion 配置
├── package.json
└── tsconfig.json
```

---

## 💡 使用示例

### 示例 1：数据动画视频（销售增长）

**用户**：把这张销售增长图表做成 15 秒动画视频，带字幕

**AI 输出**：

```tsx
// src/compositions/SalesGrowth.tsx
import { useCurrentFrame, interpolate, spring, Sequence } from "remotion";
import { AbsoluteFill, Text } from "remotion";

const data = [
  { month: "1月", value: 100 },
  { month: "2月", value: 150 },
  { month: "3月", value: 300 },
  { month: "4月", value: 280 },
  { month: "5月", value: 500 },
];

export function SalesGrowth() {
  const frame = useCurrentFrame();
  
  return (
    <AbsoluteFill className="bg-slate-900 text-white flex flex-col items-center justify-center">
      {/* 标题 */}
      <Sequence from={0} durationInFrames={30}>
        <Text className="text-4xl font-bold"
          style={{
            opacity: interpolate(frame, [0, 15], [0, 1]),
            transform: `translateY(${interpolate(frame, [0, 15], [20, 0])}px)`
          }}
        >
          2026年销售增长趋势
        </Text>
      </Sequence>
      
      {/* 柱状图动画 */}
      <div className="flex items-end gap-4 mt-12 h-64">
        {data.map((item, index) => {
          const delay = index * 10;
          const barHeight = spring({
            frame: frame - delay,
            fps: 30,
            config: { damping: 10, stiffness: 100 }
          }) * item.value;
          
          return (
            <Sequence from={30 + delay} durationInFrames={60}>
              <div key={index} className="flex flex-col items-center">
                <div
                  className="w-16 bg-blue-500 rounded-t-lg"
                  style={{ height: `${barHeight}px` }}
                />
                <Text className="mt-2 text-sm">{item.month}</Text>
              </div>
            </Sequence>
          );
        })}
      </div>
      
      {/* 总结字幕 */}
      <Sequence from={120} durationInFrames={90}>
        <Text className="text-2xl mt-8 text-green-400"
          style={{
            opacity: interpolate(frame, [120, 135], [0, 1])
          }}
        >
          5月销售额同比增长 500%
        </Text>
      </Sequence>
    </AbsoluteFill>
  );
}

// 注册 Composition
// src/index.tsx
import { Composition } from "remotion";
import { SalesGrowth } from "./compositions/SalesGrowth";

export const RemotionRoot = () => (
  <>
    <Composition
      id="SalesGrowth"
      component={SalesGrowth}
      durationInFrames={210}  // 7秒 @ 30fps
      fps={30}
      width={1920}
      height={1080}
    />
  </>
);
```

**渲染命令**：
```bash
npx remotion render src/index.tsx SalesGrowth output.mp4
```

---

### 示例 2：产品演示视频（带字幕和 BGM）

```tsx
import { Audio, Sequence, useCurrentFrame, interpolate } from "remotion";
import { AbsoluteFill, Img, Text } from "remotion";

export function ProductDemo() {
  const frame = useCurrentFrame();
  
  return (
    <AbsoluteFill className="bg-white">
      {/* BGM */}
      <Audio src="/audio/background-music.mp3" />
      
      {/* 场景1: 产品亮相 (0-3秒) */}
      <Sequence from={0} durationInFrames={90}>
        <AbsoluteFill className="flex items-center justify-center">
          <Img
            src="/images/product-hero.png"
            style={{
              transform: `scale(${interpolate(frame, [0, 60], [0.8, 1])})`,
              opacity: interpolate(frame, [0, 30], [0, 1])
            }}
          />
          <Text className="absolute bottom-20 text-3xl font-bold"
            style={{ opacity: interpolate(frame, [30, 60], [0, 1]) }}
          >
            全新智能手表 Pro
          </Text>
        </AbsoluteFill>
      </Sequence>
      
      {/* 场景2: 功能展示 (3-6秒) */}
      <Sequence from={90} durationInFrames={90}>
        <FeatureShowcase frame={frame} />
      </Sequence>
      
      {/* 场景3: CTA (6-8秒) */}
      <Sequence from={180} durationInFrames={60}>
        <AbsoluteFill className="bg-blue-600 flex flex-col items-center justify-center text-white">
          <Text className="text-4xl font-bold mb-4">立即体验</Text>
          <Text className="text-xl">www.example.com</Text>
        </AbsoluteFill>
      </Sequence>
    </AbsoluteFill>
  );
}
```

---

### 示例 3：字幕视频（口播/播客转视频）

```tsx
// 字幕逐字出现效果
function Subtitle({ text, startFrame }: { text: string; startFrame: number }) {
  const frame = useCurrentFrame();
  const charsToShow = Math.max(0, frame - startFrame);
  const visibleText = text.slice(0, charsToShow);
  
  return (
    <Text className="text-2xl text-white text-center px-12"
      style={{
        textShadow: "0 2px 4px rgba(0,0,0,0.5)"
      }}
    >
      {visibleText}
      <span className="animate-pulse">|</span>
    </Text>
  );
}

// 使用
<Sequence from={0} durationInFrames={120}>
  <Subtitle text="大家好，今天我们来聊聊AI编程的最新趋势" startFrame={0} />
</Sequence>
```

---

## 📐 Composition 最佳实践（30+ 条精选）

```markdown
1. FPS 选择：
   - 社交媒体短视频: 30fps
   - 流畅动画/宣传片: 60fps
   - 电影感: 24fps

2. 分辨率：
   - 抖音/小红书: 1080x1920 (9:16)
   - YouTube/B站: 1920x1080 (16:9)
   - 微信公众号: 1080x1080 (1:1)

3. 动画缓动：
   - 入场: spring({ damping: 10 })
   - 退场: interpolate + ease-out
   - 持续: linear

4. 颜色管理：
   - 使用 Tailwind 色板保持一致性
   - 文字必须加 textShadow 保证可读性

5. 音频同步：
   - 用 <Audio/> 组件嵌入 BGM
   - 字幕时间轴精确到帧

6. 性能优化：
   - 复杂动画拆分为多个 Sequence
   - 避免每帧重计算，用 useMemo
   - 图片预加载到 public/ 目录

7. 字体：
   - 必须加载本地字体文件，不能依赖系统字体
   - 中文字体推荐: Noto Sans SC

8. 导出设置：
   - 预览: npx remotion preview
   - 渲染: npx remotion render
   - 编码: H.264 (兼容性好) / H.265 (体积小)
```

---

## 🚀 快速入口

```
"生成视频" → Remotion React 视频项目搭建
"做动画视频" → 数据动画/产品动画/字幕动画
"React视频" → Remotion Composition + Sequence
"把图表做成视频" → interpolate + spring 驱动图表动画
"产品演示视频" → 多场景 Composition + BGM + 字幕
"数据动画" → 柱状图/折线图逐帧动画
"字幕视频" → 逐字出现/卡拉OK字幕效果
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 场景对比 |
|-------|------|---------|
| **html-ppt-skill** | 互补 | `html-ppt` 是交互式演示文稿，本 Skill 是视频导出 |
| **diagram-design** | 互补 | `diagram-design` 是静态图表（SVG），本 Skill 是动态视频（MP4） |
| **web-artifacts-builder** | 互补 | `web-artifacts-builder` 是复杂 Web 应用，本 Skill 是视频渲染 |
| **frontend-design** | 前置 | `frontend-design` 定视觉方向，本 Skill 执行视频编码 |

**最佳实践链**：
```
数据/内容 → diagram-design（静态图表设计）
  → remotion-video（动态视频化）
  → 导出 MP4 → 社交媒体发布
```

---

> "视频是时间的艺术。Remotion 让你用代码精确控制每一帧。"

---
name: "algorithmic-art"
description: "算法艺术生成器：用p5.js/Canvas代码生成程序化艺术作品，包括粒子系统、几何图形、种子随机、噪声纹理、动态壁纸。当用户说'生成艺术'、'算法壁纸'、'p5.js艺术'、'代码画画'、'生成海报'、'粒子效果'、'噪声纹理'、'程序化艺术'时触发。核心特点：种子可控复现、参数化设计、数学美学、代码即画布。"
---

> **来源**: 改编自 Anthropic 官方 skill（github.com/anthropics/skills/algorithmic-art）
>
> **发布时间**: 2026-05-29
>
> **理念**: "艺术不是画出来的，是算出来的。"

# 🎨 Algorithmic Art — 算法艺术生成器

用 **p5.js + Canvas API** 把数学公式变成视觉艺术——壁纸、海报、封面、头像，全部程序化生成，种子可控，无限复现。

---

## 🎯 和 huashu-design / diagram-design 的区别

| 维度 | huashu-design | diagram-design | algorithmic-art |
|------|--------------|----------------|-----------------|
| **核心** | HTML 原生设计哲学 | 数据图表（13种类型） | 数学驱动的视觉艺术 |
| **输出** | 网页/落地页 | 信息图表 | 壁纸/海报/抽象画 |
| **交互** | 可交互 | 静态 | 可动态/可静态 |
| **风格** | 商业设计 | 编辑级图表 | 生成艺术/抽象美学 |
| **技术** | HTML+CSS | SVG+JS | p5.js+Canvas |

---

## 🛠️ 核心技术栈

```
p5.js           # Processing 的 JS 版本，创意编程首选
Canvas 2D       # 底层绘图 API
WebGL (可选)     # 3D/高性能渲染
seed-random     # 种子随机，保证复现
simplex-noise   # 噪声函数（Perlin/Simplex）
chromajs        # 颜色插值与调和
```

### p5.js 核心函数速查

```javascript
// 画布设置
function setup() {
  createCanvas(800, 800);  // 创建 800x800 画布
  background(255);          // 白色背景
  noLoop();                 // 只画一帧（静态）
}

// 绘图循环
function draw() {
  circle(x, y, r);          // 画圆
  line(x1, y1, x2, y2);     // 画线
  rect(x, y, w, h);         // 矩形
  triangle(x1,y1, x2,y2, x3,y3); // 三角形
  
  fill(r, g, b, a);         // 填充色
  stroke(r, g, b);          // 描边色
  noStroke();               // 无描边
  
  randomSeed(42);           // 设置随机种子
  noise(x, y);              // Perlin 噪声 (0-1)
  map(value, 0, 1, 0, 255); // 数值映射
}
```

---

## 🎨 艺术风格体系

### 1. 粒子系统（Particle System）

```javascript
class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector(0, 0);
    this.life = 255;
  }
  
  applyForce(force) {
    this.acc.add(force);
  }
  
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.life -= 2;
  }
  
  show() {
    stroke(255, this.life);
    strokeWeight(2);
    point(this.pos.x, this.pos.y);
  }
}

// 使用：在 draw() 中创建数百个 Particle，受噪声场驱动
```

**效果**：流动的光点、烟花、星云、尘埃

---

### 2. 几何分形（Geometric Fractals）

```javascript
function drawCircle(x, y, r) {
  noFill();
  stroke(255);
  circle(x, y, r * 2);
  
  if (r > 10) {
    drawCircle(x + r, y, r * 0.5);
    drawCircle(x - r, y, r * 0.5);
    drawCircle(x, y + r, r * 0.5);
  }
}
```

**效果**：曼陀罗、递归圆、树形分形、谢尔宾斯基三角形

---

### 3. 噪声地形（Noise Terrain）

```javascript
function draw() {
  loadPixels();
  for (let x = 0; x < width; x++) {
    for (let y = 0; y < height; y++) {
      let n = noise(x * 0.01, y * 0.01, frameCount * 0.01);
      let bright = map(n, 0, 1, 0, 255);
      set(x, y, color(bright, bright * 0.5, 255));
    }
  }
  updatePixels();
}
```

**效果**：等高线地形图、流体纹理、云彩、大理石纹

---

### 4. 参数化几何（Parametric Geometry）

```javascript
function draw() {
  translate(width / 2, height / 2);
  
  for (let i = 0; i < 100; i++) {
    let t = i / 100 * TWO_PI;
    let r = 200 + sin(t * 5) * 50;  // 花瓣形状
    let x = r * cos(t);
    let y = r * sin(t);
    
    line(0, 0, x, y);
  }
}
```

**效果**：玫瑰曲线、利萨如图形、螺旋、 parametric 花朵

---

### 5. 流体模拟（Fluid Simulation）

```javascript
// 简化版：噪声驱动的流线
function draw() {
  background(0);
  
  for (let y = 0; y < height; y += 10) {
    for (let x = 0; x < width; x += 10) {
      let angle = noise(x * 0.005, y * 0.005, frameCount * 0.01) * TWO_PI * 2;
      let len = 10;
      
      stroke(255, 100);
      line(x, y, x + cos(angle) * len, y + sin(angle) * len);
    }
  }
}
```

**效果**：风向图、磁场线、水流、抽象笔触

---

## 💡 使用示例

### 示例 1：生成一张手机壁纸

**用户**：帮我生成一张蓝色调的抽象粒子壁纸，1080x1920

**AI 输出**：

```javascript
function setup() {
  createCanvas(1080, 1920);
  background(10, 20, 40);
  
  randomSeed(42);  // 种子固定，可复现
  
  // 绘制 1000 个发光粒子
  for (let i = 0; i < 1000; i++) {
    let x = random(width);
    let y = random(height);
    let size = random(1, 4);
    let alpha = random(50, 200);
    
    noStroke();
    fill(
      random(50, 150),   // R
      random(100, 200),  // G
      255,                // B
      alpha
    );
    circle(x, y, size);
  }
  
  // 绘制几条流光曲线
  noFill();
  for (let i = 0; i < 5; i++) {
    stroke(100, 200, 255, 80);
    strokeWeight(2);
    beginShape();
    for (let x = 0; x < width; x += 10) {
      let y = height / 2 + noise(x * 0.005, i) * 400 - 200;
      vertex(x, y);
    }
    endShape();
  }
  
  saveCanvas('blue-particle-wallpaper', 'png');
}
```

---

### 示例 2：生成活动海报

**用户**：生成一张科技大会海报，带"AI FUTURE 2026"字样

**AI 输出**：

```javascript
function setup() {
  createCanvas(1200, 1600);
  colorMode(HSB);
  
  // 背景：噪声纹理
  for (let x = 0; x < width; x += 4) {
    for (let y = 0; y < height; y += 4) {
      let n = noise(x * 0.003, y * 0.003);
      let h = map(n, 0, 1, 220, 280);  // 蓝紫色调
      fill(h, 60, 20);
      noStroke();
      rect(x, y, 4, 4);
    }
  }
  
  // 中心几何图形
  translate(width / 2, height / 2);
  
  for (let i = 0; i < 20; i++) {
    rotate(TWO_PI / 20);
    stroke(255, 0.3);
    noFill();
    let r = 300 + sin(frameCount * 0.02 + i) * 50;
    circle(0, 0, r);
  }
  
  // 文字
  textAlign(CENTER, CENTER);
  textFont('Noto Sans SC');
  
  fill(255);
  textSize(80);
  textStyle(BOLD);
  text("AI FUTURE", 0, -60);
  
  textSize(120);
  text("2026", 0, 60);
  
  textSize(30);
  textStyle(NORMAL);
  text("SHANGHAI · OCT 15-17", 0, 180);
  
  saveCanvas('ai-future-poster', 'png');
}
```

---

### 示例 3：动态生成艺术（GIF/视频）

```javascript
function setup() {
  createCanvas(800, 800);
  frameRate(30);
}

function draw() {
  background(0, 30);  // 拖尾效果
  translate(width / 2, height / 2);
  
  let t = frameCount * 0.02;
  
  for (let i = 0; i < 50; i++) {
    let angle = i / 50 * TWO_PI + t;
    let r = 200 + sin(angle * 3 + t) * 100;
    
    let x = r * cos(angle);
    let y = r * sin(angle);
    
    stroke(
      map(sin(t + i * 0.1), -1, 1, 100, 255),
      map(cos(t + i * 0.1), -1, 1, 50, 200),
      255,
      150
    );
    
    line(0, 0, x, y);
  }
}

// 导出 GIF: 使用 p5.js + CCapture 库
```

---

## 🎛️ 参数化控制面板

让用户通过调整参数生成不同风格：

```javascript
// 可调参数
let params = {
  seed: 42,           // 随机种子
  complexity: 0.5,    // 复杂度 (0-1)
  colorTheme: "blue", // 主题色
  density: 100,       // 元素密度
  noiseScale: 0.01,   // 噪声尺度
  symmetry: 6,        // 对称轴数
  animation: false    // 是否动画
};

// 根据参数生成不同效果
// complexity → 递归深度 / 粒子数量
// colorTheme → HSB 色相偏移
// density → 循环次数
// symmetry → rotate(TWO_PI / symmetry)
```

---

## 🚀 快速入口

```
"生成艺术" → p5.js 抽象艺术项目
"算法壁纸" → 指定分辨率 + 风格 → 导出 PNG
"p5.js艺术" → 完整 p5.js 项目结构
"代码画画" → 数学公式 → 视觉图形
"生成海报" → 指定主题文字 + 风格 → 海报尺寸
"粒子效果" → Particle System + 噪声场驱动
"噪声纹理" → Perlin/Simplex 噪声 → 地形/云彩/流体
"程序化艺术" → 参数化生成 + 种子控制
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 场景对比 |
|-------|------|---------|
| **huashu-design** | 互补 | `huashu-design` 是商业网页设计，本 Skill 是抽象生成艺术 |
| **diagram-design** | 互补 | `diagram-design` 是信息图表，本 Skill 是纯视觉美学 |
| **remotion-video** | 互补 | 本 Skill 生成静态/动态图像，`remotion-video` 生成视频 |
| **qiaopi-style** | 平行 | 同属文化创意类，一个文字一个视觉 |

**最佳实践链**：
```
创意灵感 → algorithmic-art（生成视觉素材）
  → remotion-video（动画化）
  → 导出为社交媒体内容
```

---

> "代码即画布，数学即画笔。"

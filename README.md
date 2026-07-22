# 鱼类网站数据整理指南

## 1. 文档目的

本指南用于统一整理鱼类网站中的物种资料。网站中的每一种鱼都应使用相同的数据字段和图片命名方式，以便实现以下功能：

- 按“目 → 科 → 属 → 种”浏览鱼类；
- 搜索中文名、英文名和学名；
- 按分布地区、生活水域、体形等条件筛选；
- 自动生成鱼种详情页面；
- 实现交互式“物种查询”功能；
- 后续方便增加新的鱼种，而不需要重复编写页面代码。

*建议先选择 5 种鱼完成试填。确认所有字段和选项统一后，再批量整理其他文档。*

---

## 2. 项目文件结构

鱼类数据保存在 `src/data/fishData.json` 中，图片保存在 `public/images/fish/` 中。

```text
project/
├── public/
│   └── images/
│       └── fish/
│           ├── esox-lucius/
│           │   ├── adult.jpg
│           │   ├── juvenile.jpg
│           │   └── habitat.jpg
│           ├── siniperca-chuatsi/
│           │   ├── adult.jpg
│           │   └── juvenile.jpg
│           └── tanakia-chii/
│               └── adult-male.jpg
└── src/
    ├── components/
    ├── pages/
    └── data/
        └── fishData.json
```

### 鱼种文件夹命名规则

每个鱼种单独建立一个图片文件夹。文件夹名称使用该鱼学名中的“属名-种名”，全部小写，并用连字符连接。<br>
例如：
| 学名 | 文件夹名称 |
|---|---|
| Esox lucius | `esox-lucius` |
| Siniperca chuatsi | `siniperca-chuatsi` |
| Tanakia chii | `tanakia-chii` |

不要在文件夹名或图片名中使用中文、空格、括号和特殊符号。

---

## 3. 完整 JSON 模板

模版在 `fishData.json` 中，并替换为对应鱼种的资料。

> 注意：JSON 文件不能包含注释。缺少可靠资料时，请使用空字符串 `""`、空数组 `[]` 或 `null`，不要猜测，也不要填写“同上”。

```json
[
  {
    // =========================
    // 1. 物种基本名称
    // =========================

    // 唯一识别码：通常使用“小写属名-小写种名”
    // 同时建议作为图片文件夹名称
    "id": "esox-lucius",

    // 中文名
    "chineseName": "白斑狗鱼",

    // 英文名
    "englishName": "Northern Pike",

    // 拉丁学名：属名首字母大写，种名全部小写
    "scientificName": "Esox lucius",

    // 最初描述该物种的学者及发表年份
    // 这一部分在网页上不需要使用斜体
    "scientificAuthor": "Linnaeus, 1758",


    // =========================
    // 2. 生物分类
    // =========================

    "taxonomy": {
      // 目：较大的分类层级
      "order": "狗鱼目",

      // 科：目下面的分类层级
      "family": "狗鱼科",

      // 属：科下面亲缘关系较接近的一组物种
      "genus": "狗鱼属"
    },


    // =========================
    // 3. 原生与保护状态
    // =========================

    "status": {
      // 该物种对中国而言属于哪种身份
      // 固定选项：中国原生、中国外来、中国入侵、尚不确定
      "nativeStatus": "中国原生"
    },


    // =========================
    // 4. 基础信息
    // =========================

    "basicInfo": {
      // 可靠资料记载的最大体长，单位为厘米
      // 数字未知时使用 null，不要写“未知”
      "maximumLengthCm": null,

      // 常见或平均体长，单位为厘米
      "averageLengthCm": null,

      // 预期寿命，单位为年
      "lifespanYears": null,

      // 食性，可以填写多个
      // 例如：草食性、肉食性、杂食性、滤食性
      "diet": ["肉食性"],

      // 主要活动或捕食方式
      // 例如：伏击型、追击型、底栖、群游
      "activity": ["伏击型"],

      // 生活水域
      // 例如：淡水、海水、咸淡水
      "waterType": ["淡水"],

      // 通常活动的水层
      // 例如：上层、中层、底层
      "waterLayer": ["中层", "底层"]
    },


    // =========================
    // 5. 外形特征
    // =========================

    "appearance": {
      // 用1～3句话概括最明显的外形
      "summary": "身体细长，灰绿色或暗褐色的侧面布满浅色斑点。",

      // 中文体形描述
      // 例如：细长型、纺锤型、侧扁型、平扁型、鳗形
      "bodyShape": "细长型",

      // 身体主要颜色，可以填写多个
      "primaryColors": ["灰绿色", "暗褐色"],

      // 身体上的明显花纹
      // 例如：浅色斑点、深色斑点、水平纵带、垂直条纹
      "patterns": ["浅色斑点"],

      // 嘴在头部的位置
      // 固定选项：上位、端位、下位
      "mouthPosition": "端位",

      // 是否有触须
      // true表示有；false表示没有；不确定可以暂时使用null
      "barbels": false,

      // 鳞片类型或特殊鳞片特征
      // 没有可靠资料时填写空字符串
      "scaleType": "",

      // 背鳍数量
      // 不确定时使用null
      "dorsalFinCount": 1,

      // 尾鳍形状
      // 例如：分叉形、圆形、截形、新月形
      "tailShape": "分叉形",

      // 最有助于识别该鱼的特征
      "keyFeatures": [
        "身体细长",
        "吻部较长",
        "侧面具有浅色斑点"
      ],

      // 雌鱼和雄鱼之间的差异
      // 没有明显差异或没有资料时填写空字符串
      "sexualDifferences": "雌性生长速度通常高于雄性，成年雌性个体更大。"
    },


    // =========================
    // 6. 分布区域
    // =========================

    "distribution": {
      // 在中国分布的省份或地区
      "chinaRegions": ["新疆"],

      // 具体分布的流域、河流或湖泊
      "riverSystems": ["额尔齐斯河流域"],

      // 中国以外的分布区域
      "globalRegions": [
        "欧洲",
        "俄罗斯",
        "北美洲北部"
      ],

      // 用完整语句总结分布情况
      "description": "在中国主要分布于新疆额尔齐斯河流域，全球广泛分布于北半球寒冷和温带水域。"
    },


    // =========================
    // 7. 栖息环境
    // =========================

    "habitat": {
      // 常见生活环境
      // 例如：河流、湖泊、溪流、水库、湿地、珊瑚礁
      "environment": ["湖泊", "河流"],

      // 水流情况
      // 例如：静水、缓流、流水、急流
      "waterFlow": ["缓流", "流水"],

      // 水底类型
      // 例如：泥底、沙底、石底、水草区
      "bottomType": [],

      // 可生存或适宜的最低水温，单位为摄氏度
      "temperatureMinC": null,

      // 可生存或适宜的最高水温，单位为摄氏度
      "temperatureMaxC": null,

      // 适宜的最低pH
      "phMin": null,

      // 适宜的最高pH
      "phMax": null,

      // 对溶氧量的要求
      "dissolvedOxygen": "偏好溶氧量较高的水体",

      // 用完整语句概括栖息环境
      "description": "典型冷水性鱼类，偏好水质清澈、溶氧量高且流动性良好的水体。"
    },


    // =========================
    // 8. 生态习性
    // =========================

    "ecology": {
      // 主要捕食或摄食方式
      "feedingBehavior": "伏击其他鱼类",

      // 主要食物，可以填写多个
      "food": ["小型鱼类"],

      // 游泳、群居、领地、攻击性等行为
      "behavior": "属于伏击型捕食者，也可能出现同类相食。",

      // 繁殖时间、产卵方式或护卵行为
      // 没有可靠资料时填写空字符串
      "reproduction": ""
    },


    // =========================
    // 9. 饲养信息
    // =========================

    "care": {
      // 是否适合作为水族箱观赏鱼
      "suitableForAquarium": false,

      // 饲养难度
      // 固定选项：容易、中等、困难、不建议饲养
      "difficulty": "困难",

      // 是否适合没有经验的新手
      "beginnerFriendly": false,

      // 建议的最低鱼缸容量，单位为升
      // 没有可靠资料时使用null
      "minimumTankLiters": null,

      // 建议饲养温度，可以写成范围
      "recommendedTemperatureC": "",

      // 饲料和喂食建议
      "feedingAdvice": "",

      // 对水质、空间、氧气等方面的特殊要求
      "specialRequirements": [
        "需要较大的活动空间",
        "需要高溶氧水体"
      ],

      // 重要提醒
      "warning": "不建议新手饲养。"
    },


    // =========================
    // 10. 物种查询专用字段
    // =========================
    // 这里必须使用统一的英文代码，
    // 用于程序进行筛选和匹配。

    "identification": {
      // freshwater：淡水
      // marine：海水
      // brackish：咸淡水
      "waterType": ["freshwater"],

      // elongated：细长型
      // fusiform：纺锤型
      // compressed：侧扁型
      // flattened：平扁型
      // eel-like：鳗形
      // special：特殊体型
      "bodyShape": "elongated",

      // upper：上位口
      // terminal：端位口
      // lower：下位口
      "mouthPosition": "terminal",

      // true：有触须
      // false：无触须
      "barbels": false,

      // forked：分叉形
      // rounded：圆形
      // truncate：截形
      // lunate：新月形
      "tailShape": "forked",

      // light-spots：浅色斑点
      // dark-spots：深色斑点
      // horizontal-stripe：水平纵带
      // vertical-bars：垂直条纹
      // irregular-blotches：不规则斑块
      // reticulated：网状花纹
      // none：无明显花纹
      "patterns": ["light-spots"],

      // 使用统一的地区代码
      // 例如：xinjiang、yangtze-river、pearl-river
      "regions": ["xinjiang"],

      // 可用于网站搜索的关键词
      "keywords": [
        "冷水鱼",
        "细长",
        "浅色斑点",
        "伏击型"
      ]
    },


    // =========================
    // 11. 图片
    // =========================

    "images": {
      // 物种详情页和列表页使用的主要图片
      "cover": {
        // 图片实际放在：
        // public/images/fish/esox-lucius/adult.jpg
        //
        // JSON中不要写public，应从/images开始
        "src": "/images/fish/esox-lucius/adult.jpg",

        // 用于无障碍阅读，应客观描述图片内容
        "alt": "成年白斑狗鱼的侧面照片",

        // 显示在图片下方的简短说明
        "caption": "成年白斑狗鱼",

        // 摄影者、机构名称或图片来源网页
        "source": "",

        // 图片授权，例如：CC BY 4.0
        "license": ""
      },

      // 其他图片，例如幼体、雌雄差异和栖息环境
      "gallery": [
        {
          "src": "/images/fish/esox-lucius/juvenile.jpg",
          "alt": "白斑狗鱼幼体的侧面照片",
          "caption": "幼年白斑狗鱼",
          "source": "",
          "license": ""
        },
        {
          "src": "/images/fish/esox-lucius/habitat.jpg",
          "alt": "白斑狗鱼生活的冷水湖泊环境",
          "caption": "典型栖息环境",
          "source": "",
          "license": ""
        }
      ]
    },


    // =========================
    // 12. 资料来源
    // =========================

    "sources": [
      {
        // 资料页面、论文或图鉴的标题
        "title": "FishBase: Esox lucius",

        // 完整网页链接
        "url": "",

        // 发布该资料的机构
        "organization": "FishBase",

        // 学生查看资料的日期
        "accessDate": "2026-07-21"
      }
    ],


    // =========================
    // 13. 最后更新时间
    // =========================

    // 使用YYYY-MM-DD格式
    "lastUpdated": "2026-07-21"
  }
]
```

---

## 4. 字段填写要求

### 4.1 必填字段

每个鱼种至少需要填写：

```text
id
chineseName
englishName
scientificName
taxonomy.order
taxonomy.family
taxonomy.genus
appearance.summary
distribution.description
habitat.description
ecology.behavior
images.cover
sources
```

### 4.2 “物种查询”必填字段

如果一种鱼需要出现在物种识别工具中，还必须填写：

```text
identification.waterType
identification.bodyShape
identification.mouthPosition
identification.barbels
identification.tailShape
identification.patterns
identification.regions
```

### 4.3 缺失资料的处理

没有可靠数据时使用以下方式：

```json
"maximumLengthCm": null,
"reproduction": "",
"globalRegions": []
```

- 数字未知：使用 `null`；
- 文字未知：使用空字符串 `""`；
- 列表未知：使用空数组 `[]`；
- 布尔值必须根据资料填写 `true` 或 `false`；无法判断时可以暂时使用 `null`；
- 不要为了让页面看起来完整而自行猜测；
- 不要写“同上”，每条鱼的数据都必须能够独立使用。

---

## 5. 如何添加多条鱼

`fishData.json` 最外层是一个数组。每一种鱼是一个独立的 `{ }` 对象，不同对象之间使用英文逗号分隔。

```json
[
  {
    "id": "esox-lucius",
    "chineseName": "白斑狗鱼"
  },
  {
    "id": "esox-reicherti",
    "chineseName": "黑斑狗鱼"
  },
  {
    "id": "siniperca-chuatsi",
    "chineseName": "鳜鱼"
  }
]
```

最后一个对象后面不能添加逗号，否则 JSON 文件会报错。

---

## 6. 图片如何放入项目

### 第一步：建立鱼种文件夹

以鳜鱼为例，在 `public/images/fish/` 中建立：

```text
public/images/fish/siniperca-chuatsi/
```

### 第二步：将图片放入文件夹

```text
public/images/fish/siniperca-chuatsi/adult.jpg
public/images/fish/siniperca-chuatsi/juvenile.jpg
public/images/fish/siniperca-chuatsi/habitat.jpg
```

建议使用以下固定名称：

| 图片内容 | 推荐文件名 |
|---|---|
| 成年个体 | `adult.jpg` |
| 幼年个体 | `juvenile.jpg` |
| 成年雄鱼 | `adult-male.jpg` |
| 成年雌鱼 | `adult-female.jpg` |
| 栖息环境 | `habitat.jpg` |
| 形态细节 | `detail-mouth.jpg`、`detail-fin.jpg` |

### 第三步：在 JSON 中记录图片路径

```json
"images": {
  "cover": {
    "src": "/images/fish/siniperca-chuatsi/adult.jpg",
    "alt": "成年鳜鱼的侧面照片",
    "caption": "成年鳜鱼",
    "source": "摄影者或来源网站",
    "license": "CC BY 4.0"
  },
  "gallery": [
    {
      "src": "/images/fish/siniperca-chuatsi/juvenile.jpg",
      "alt": "幼年鳜鱼的侧面照片",
      "caption": "幼年鳜鱼",
      "source": "摄影者或来源网站",
      "license": ""
    }
  ]
}
```

图片位于 `public` 文件夹内，因此路径应直接从 `/images/` 开始。

正确写法：

```json
"src": "/images/fish/siniperca-chuatsi/adult.jpg"
```

错误写法：

```json
"src": "public/images/fish/siniperca-chuatsi/adult.jpg"
```

---

## 7. 图片使用要求

- 可使用自己拍摄的图片；
- 可以使用公共领域、Creative Commons 或明确允许转载的图片；
- 不要直接使用带有视频网站、社交媒体或其他平台水印的截图；
- 每张图片都要记录来源链接、摄影者或机构名称；
- 每张图片必须填写准确的 `alt`，说明图片展示的内容；
- 封面图尽量使用横向、鱼体完整、背景简单的侧面照片；
- 同类图片尽量保持相同宽高比，例如 `4:3`；
- 网站展示图可以压缩至约 1200 像素宽；
- 普通照片优先使用 `.jpg` 或 `.webp`；
- 只有需要透明背景时才使用 `.png`。

### `alt` 与 `caption` 的区别

- `alt`：用于无障碍阅读和图片无法加载时的替代说明，应客观描述图片；
- `caption`：显示在网页图片下方，可以使用较短的名称。

示例：

```json
{
  "alt": "一条成年鳜鱼的左侧面照片，身体具有不规则深褐色斑块",
  "caption": "成年鳜鱼"
}
```

---

## 8. React 中显示图片

### 显示封面图

```jsx
<img
  src={fish.images.cover.src}
  alt={fish.images.cover.alt}
/>
```

### 显示图片和说明

```jsx
<figure>
  <img
    src={fish.images.cover.src}
    alt={fish.images.cover.alt}
  />

  <figcaption>
    {fish.images.cover.caption}
  </figcaption>
</figure>
```

### 显示图片图库

```jsx
<div className="fish-gallery">
  {fish.images.gallery.map((image) => (
    <figure key={image.src}>
      <img src={image.src} alt={image.alt} />
      <figcaption>{image.caption}</figcaption>
    </figure>
  ))}
</div>
```

---

## 9. 物种查询数据词典

“物种查询”使用固定的英文代码进行匹配，网页再将代码显示为中文。学生不能随意发明新的写法，否则系统会将相同特征当成不同特征。

### 9.1 生活水域 `waterType`

| 英文代码 | 中文显示 |
|---|---|
| `freshwater` | 淡水 |
| `marine` | 海水 |
| `brackish` | 咸淡水或河口水域 |

示例：

```json
"waterType": ["freshwater"]
```

### 9.2 身体形状 `bodyShape`

| 英文代码 | 中文显示 |
|---|---|
| `elongated` | 细长型 |
| `fusiform` | 纺锤型 |
| `compressed` | 侧扁型 |
| `flattened` | 平扁型 |
| `eel-like` | 鳗形 |
| `special` | 特殊体型 |

### 9.3 嘴的位置 `mouthPosition`

| 英文代码 | 中文显示 |
|---|---|
| `upper` | 上位口 |
| `terminal` | 端位口 |
| `lower` | 下位口 |

### 9.4 是否有触须 `barbels`

```json
"barbels": true
```

表示有触须。

```json
"barbels": false
```

表示没有触须。

### 9.5 尾鳍形状 `tailShape`

| 英文代码 | 中文显示 |
|---|---|
| `forked` | 分叉形 |
| `rounded` | 圆形 |
| `truncate` | 截形 |
| `lunate` | 新月形 |

### 9.6 身体花纹 `patterns`

| 英文代码 | 中文显示 |
|---|---|
| `light-spots` | 浅色斑点 |
| `dark-spots` | 深色斑点 |
| `horizontal-stripe` | 水平纵带 |
| `vertical-bars` | 垂直条纹 |
| `irregular-blotches` | 不规则斑块 |
| `reticulated` | 网状花纹 |
| `none` | 无明显花纹 |

一条鱼可以同时具有多种花纹：

```json
"patterns": ["dark-spots", "irregular-blotches"]
```

### 9.7 地区 `regions`

地区代码也应统一，例如：

| 英文代码 | 中文显示 |
|---|---|
| `heilongjiang` | 黑龙江流域 |
| `yellow-river` | 黄河流域 |
| `yangtze-river` | 长江流域 |
| `pearl-river` | 珠江流域 |
| `xinjiang` | 新疆水系 |
| `qinghai-tibet` | 青藏高原水系 |
| `coastal` | 沿海地区 |

如果网站后续增加更细的地区，应先更新统一的数据词典，再让所有鱼种使用新选项。

---

## 10. 参考资料记录规范

每个鱼种建议至少使用两个可靠来源，并优先考虑：

- FishBase；
- 中国科学院相关数据库或研究机构；
- IUCN Red List；
- 专业鱼类图鉴；
- 学术论文；
- 博物馆、自然保护区或政府生物多样性数据库。

不要只依赖个人博客、短视频或无法查明来源的转载文章。

参考资料格式：

```json
"sources": [
  {
    "title": "资料页面标题",
    "url": "https://example.com/fish-page",
    "organization": "发布机构",
    "accessDate": "2026-07-21"
  }
]
```

如果某条资料只支持某一字段，也可以在整理笔记中单独标明它支持的是分布、体长、生态习性还是保护状态。

---

## 11. 提交前检查清单

每整理完一种鱼，请检查：

- [ ] `id` 与图片文件夹名称完全一致；
- [ ] 中文名、英文名和学名拼写正确；
- [ ] 学名中的属名首字母大写、种名小写；
- [ ] 目、科、属、种的分类层级正确；
- [ ] 没有使用“同上”；
- [ ] 未知数据使用 `null`、`""` 或 `[]`；
- [ ] 识别字段全部使用数据词典中的英文代码；
- [ ] 图片路径以 `/images/` 开头；
- [ ] 图片文件名不含中文、空格或括号；
- [ ] 每张图片都填写了 `alt`；
- [ ] 每张外部图片都记录了来源和授权信息；
- [ ] 每个鱼种至少有一个可靠文字来源；
- [ ] JSON 中使用英文双引号；
- [ ] 最后一个对象或数组项目后面没有多余逗号；
- [ ] 使用 JSON 验证工具检查文件没有语法错误。

---

## 12. 第一阶段作业建议

先选择 5 种具有不同特征的鱼进行整理，例如：

1. 一种细长型鱼类；
2. 一种侧扁型鱼类；
3. 一种有触须的鱼类；
4. 一种具有明显斑点或条纹的鱼类；
5. 一种生活环境或分布区域明显不同的鱼类。

每种鱼需要提交：

- 一份符合模板的数据；
- 至少一张封面图片；
- 图片来源和授权信息；
- 至少两个可靠文字资料来源；
- 完整填写物种查询所需的识别字段。

完成这 5 种鱼后，先检查字段是否足以支持网站页面和物种识别，再决定是否需要增加或删减字段。

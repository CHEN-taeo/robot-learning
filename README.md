# 🤖 Arduino & Python 嵌入式学习项目

> 作者：陈韬 | 时间：2026.04

---

## 📁 项目结构

```
├── led_blink/
│   └── led_blink.ino          # LED 闪烁实验（数字输出）
├── breathing_light/
│   └── breathing_light.ino    # 呼吸灯实验（PWM 模拟输出）
└── robot_sensor/
    ├── robot_sensor_basic.py          # 距离传感器基础版
    ├── robot_sensor_data_numpy.py     # 距离传感器进阶版（含可视化）
    └── results/
        └── sensor_data_analysis.png  # 生成的分析图表
```

---

## 🔬 实验一：LED 闪烁

**文件：** `led_blink.ino`

通过控制 Arduino 数字引脚 13 的高低电平，实现 LED 灯以 0.5 秒为间隔交替亮灭。

### 核心知识点

- `pinMode(pin, OUTPUT)` — 设置引脚为输出模式
- `digitalWrite(pin, HIGH/LOW)` — 数字写入，控制高低电平
- `delay(ms)` — 毫秒级延时

### 接线方式

| 组件 | Arduino 引脚 |
|------|-------------|
| LED 正极（长脚）| 13 |
| LED 负极（短脚）| GND |

---

## 💡 实验二：呼吸灯（PWM）

**文件：** `breathing_light.ino`

利用 PWM（脉冲宽度调制）技术，使 LED 灯亮度平滑地从暗到亮、再从亮到暗循环变化，形成"呼吸"效果。

### 核心知识点

- `analogWrite(pin, value)` — PWM 输出，value 范围 0~255
- Arduino UNO PWM 引脚：**3、5、6、9、10、11**
- PWM 原理：通过数字开关的时序控制，利用人眼视觉暂留等效模拟连续亮度变化

### PWM vs 数字信号

| 类型 | 特点 | 类比 |
|------|------|------|
| Digital（数字） | 只有 0 和 1 两种状态 | 只有开/关的水龙头 |
| Analog（模拟） | 连续变化的信号 | 可调节任意水流的水龙头 |

### 接线方式

| 组件 | Arduino 引脚 |
|------|-------------|
| LED 正极（长脚）| 9（PWM）|
| LED 负极（短脚）| GND |

---

## 📡 实验三：机器人距离传感器数据处理

**文件：** `robot_sensor_data_numpy.py`

对机器人距离传感器采集的数据进行处理，实现分级预警、连续危险检测和数据可视化。

### 功能特性

- ✅ **分级预警**：根据距离值输出不同级别的警报信息
- ✅ **连续危险检测**：连续 3 次低于安全阈值时触发紧急停车
- ✅ **统计分析**：自动计算最大值、最小值、平均值
- ✅ **数据可视化**：生成折线图，直观展示距离变化趋势及危险区间

### 预警逻辑

```
距离 < 0.2 米  →  🔴 紧急预警：请立即停止！
距离 < 0.5 米  →  🟡 预警：前方有障碍物
距离 ≥ 0.5 米  →  🟢 安全
连续 3 次低于安全阈值  →  🚨 触发紧急停车
```

### 函数接口

```python
robot_sense_data(
    sense_data,              # 传感器数据列表（单位：米）
    safe_distance=0.5,       # 安全距离阈值（默认 0.5 米）
    emergency_distance=0.2   # 紧急距离阈值（默认 0.2 米）
)
```

### 依赖环境

```bash
pip install matplotlib
```

### 运行方式

```bash
python robot_sensor_data_numpy.py
```

运行后将在 `results/` 文件夹中生成 `sensor_data_analysis.png` 图表。

---

## 🛠️ 开发环境

| 工具 | 版本 |
|------|------|
| Arduino IDE | 建议 2.x |
| Arduino 开发板 | UNO R3 |
| Python | 3.x |
| matplotlib | 最新版 |

---

## 📚 学习收获

1. 掌握 Arduino 数字/模拟输出的基本用法
2. 理解 PWM 的工作原理及其在亮度控制中的应用
3. 学会用 Python 处理传感器数据并实现分级预警逻辑
4. 使用 matplotlib 完成数据可视化，生成带阈值线和危险区间标注的折线图

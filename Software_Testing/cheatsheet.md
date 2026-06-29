# Software Testing — Cheat Sheet

## Core Vocabulary of Failure (1.1)

| Term | Where it lives | Definition |
|------|---------------|------------|
| **Error** | Human's mind / fingers | A mistake made by a developer (wrong assumption, misread requirement, typo) |
| **Fault / Defect / Bug** | Source code | The incorrect code that results from an error |
| **Failure** | Runtime / output | Observable wrong behavior when the fault is triggered |

## Error → Fault → Failure Chain

```
Error (人犯错)
  ↓
Fault (错误的代码)
  ↓
Failure (运行时出错，用户看到)
```

**Key rule:** Fault 存在 ≠ Failure 一定发生。只有特定输入路径经过 fault，failure 才触发。

## Cost of Late Defects

| Discovery Stage | Relative Cost |
|----------------|--------------|
| During development | 1x |
| During testing | 10x |
| In production (post-release) | 100x |

> 越晚发现 bug，修复成本越高。测试的存在就是为了把 failure 挡在生产环境之外。

---

## What Is Software Testing (1.2)

**Testing** = 运行软件，收集行为是否符合预期的证据。

### Verification vs Validation

| 术语 | 问的问题 | 关注点 |
|------|---------|-------|
| **Verification** | "我们把东西做对了吗？" | 符合规格说明（specification） |
| **Validation** | "我们做的是对的东西吗？" | 满足用户的真实需求 |

### Expected vs Actual Behavior

```
Expected behavior ≠ Actual behavior → Test FAIL
Expected behavior = Actual behavior → Test PASS
```

### Testing vs Debugging

| | Testing | Debugging |
|-|---------|-----------|
| 目的 | 发现 failure 是否存在 | 找到并修复 fault |
| 输出 | Pass / Fail | 修复后的代码 |

### Dijkstra's Law

> "Testing can show the **presence** of bugs, but never their **absence**."

测试通过 ≠ 没有 bug。测试只能降低风险，不能消灭所有风险。

### QA vs Testing

- **Testing** ⊂ **QA**
- QA 还包括 code review、static analysis、process standards 等

---

## Test Case Anatomy (1.3)

| Part | 作用 |
|------|------|
| **Precondition** | 测试开始前，系统必须处于的状态 |
| **Input** | 传给程序的数据，触发被测行为 |
| **Expected Output** | 根据需求，程序应该返回的结果（必须事先定好） |
| **Actual Output** | 程序实际运行后产生的结果 |
| **Pass/Fail Criteria** | 判断测试结果的规则，在运行前定好 |
| **Assertion** | 在代码里执行比较的语句；没有 assertion = 没有测试 |

```python
def test_example():
    # Precondition: (setup if needed)
    # Input
    result = my_function(input_value)
    # Assertion = expected output 的代码实现
    assert result == expected_value
```

**Key rule:** 没有 assertion 的"测试"只是运行程序，不是测试程序。

---

## Arrange-Act-Assert Pattern (1.4)

```python
def test_example():
    # Arrange — 准备初始状态和输入
    obj = MyClass()
    input_value = 42

    # Act — 调用被测功能（通常只有一行）
    result = obj.my_method(input_value)

    # Assert — 验证结果
    assert result == expected_value
```

| Phase | 对应 1.3 | 做什么 |
|-------|---------|-------|
| **Arrange** | Precondition + Input 准备 | 搭建初始状态 |
| **Act** | 运行被测功能 | 触发一个行为，通常一行 |
| **Assert** | Expected Output + Assertion | 检查结果是否符合预期 |

**Single Behavior Focus:** 一个测试只测一个行为，通常只有一个 assertion。失败时立刻知道哪里出问题。

---

## Unit Testing (2.1)

**Unit** = 可以独立测试的最小代码块（通常是一个函数或方法）

**Unit Testing** = 针对单个 unit 写测试，只验证它自己的逻辑是否正确

### 四大原则

| 原则 | 含义 |
|------|------|
| **Isolation（隔离）** | 被测 unit 与数据库、网络等依赖隔离；失败时确定是 unit 本身的问题 |
| **Fast Feedback（快速反馈）** | 毫秒级运行，开发者可以频繁执行 |
| **Function-level Testing** | 专注测函数的各种输入场景（正常、边界、无效） |
| **Independence（独立性）** | 每个测试自己 Arrange，不依赖其他测试的执行顺序 |

```python
# 独立、隔离、快速的 unit test 模板
def test_some_behavior():
    # Arrange — 自己创建所需对象，不共享全局状态
    obj = MyClass()
    # Act
    result = obj.method(input)
    # Assert
    assert result == expected
```

---

## Integration Testing (2.2)

**Integration Testing** = 测试多个组件连接在一起时，它们之间的交互是否正确

Unit test 发现不了的问题：两个 unit 各自通过，但接口对不上（字段名、数据格式不匹配）

| 术语 | 含义 |
|------|------|
| **Component Interaction** | 组件之间互相调用、传递数据的过程 |
| **Interface** | 两个组件之间的约定（传什么、返回什么） |
| **Integration Point** | 两个组件连接的位置（函数调用、数据库、HTTP API 等） |
| **Module Contract** | 一个模块对外的承诺（输入→输出的格式保证） |

### Bottom-up vs Top-down

| | Bottom-up | Top-down |
|-|-----------|----------|
| 方向 | 从最底层开始，逐层向上 | 从最顶层开始，底层用 stub 代替 |
| 适合 | 底层已完成 | 底层还未完成，先验证高层逻辑 |

---

## System & End-to-End Testing (2.3)

**System Testing** = 把整个软件系统当作一个完整产品来测试，验证它是否满足需求规格

**E2E Testing** = 模拟真实用户的完整操作流程，从 UI 入口跑到数据库，整条链路都覆盖

| 层次 | 测什么 |
|------|--------|
| Unit test | 单个函数的逻辑 |
| Integration test | 模块之间的接口 |
| System / E2E test | 整个应用，从用户操作到数据持久化 |

### 核心概念

| 术语 | 含义 |
|------|------|
| **User Flow** | 用户为完成一个目标按顺序执行的一系列操作（E2E test 的核心单位） |
| **Real Environment** | 真实浏览器 + 真实数据库 + 真实后端，不用 mock |
| **System-level Black-box** | 从外部观察行为，不看源代码内部实现 |

### 优点 vs 代价

| 优点 | 代价 |
|------|------|
| 最高信心，场景与真实用户一致 | 慢（要启动浏览器、连数据库） |
| 发现 Unit / Integration 遗漏的系统级问题 | 脆弱（UI 改个 ID，test 就坏） |
| 可直接用于验收 | 调试难（不知道是哪一层出问题） |

**Key rule:** E2E test 数量要少（放在 Test Pyramid 顶端），只覆盖最重要的 User Flow。

---

## The Test Pyramid (2.4)

**Test Pyramid** = 描述三层测试理想数量比例的视觉模型：Unit 最多，Integration 适量，E2E 最少

```
        /\
       /E2E\         ← 少（个位数到几十）
      /------\
     /Integrat\      ← 中等
    /----------\
   / Unit Tests \    ← 大量（几百~上千）
  /--------------\
```

### Speed vs Confidence

| 层次 | Speed | Confidence | Cost |
|------|-------|------------|------|
| Unit | 毫秒级 | 低（只测一个函数） | 最低 |
| Integration | 秒级 | 中 | 中 |
| E2E | 十秒~分钟 | 最高（模拟真实用户） | 最高 |

**规则：越往上越贵，写越少；越往下越便宜，写越多。**

### Ice-cream cone anti-pattern

E2E 最多、Unit 几乎没有 → CI 极慢，flaky tests 多，调试困难，开发者开始跳过测试。

**典型比例：** Unit 200~500+，Integration 20~50，E2E 5~10

---

## Black-Box vs White-Box (3.1)

| | Black-Box | White-Box |
|-|-----------|-----------|
| **设计依据** | 需求规格（specification） | 源代码结构 |
| **需要看代码？** | 不需要 | 需要 |
| **目标** | 验证行为符合需求 | 确保所有代码路径被执行 |
| **别名** | Specification-based | Structure-based |
| **盲区** | 无法发现代码里未被执行的死路径 | 无法发现缺失的功能（需求没写进代码） |

**Gray-Box** = 对内部实现有部分了解，结合两者设计用例（实际工作中最常见）

**一句话：** Black-box 验证"做了该做的事"，White-box 验证"做的事都能跑到"。

---

## Equivalence Partitioning (3.2)

**Equivalence Class** = 一组对程序产生相同行为的输入值（走相同代码路径，得相同类型输出）

**Equivalence Partitioning** = 把输入空间切分成若干等价类，每类只选一个代表值来测

| 等价类类型 | 含义 |
|----------|------|
| **Valid Partition** | 程序应该接受的输入，产生正常输出 |
| **Invalid Partition** | 程序应该拒绝的输入，触发错误处理 |

**流程：**
1. 根据规格识别所有等价类（valid + invalid）
2. 每类选一个代表值
3. 写测试用例

**局限：** EP 不指定选等价类中哪个值 → 遗漏边界 bug → 配合 BVA (3.3) 使用

---

## Boundary Value Analysis (3.3)

**Off-by-one error** = 条件判断边界偏移了 1（`>=` 误写成 `>`），只有测边界值才能发现

对等价类 `[min_val, max_val]`，标准 BVA 测试值：

```
min_val - 1  (just outside, 下边界外)
min_val      (just inside,  Min)
max_val      (just inside,  Max)
max_val + 1  (just outside, 上边界外)
```

**EP + BVA 配合：** 先用 EP 划等价类，再用 BVA 在每个边界选测试值。两者互补，不是二选一。

---

## Decision Table Testing (3.4)

**适用场景：** 多个条件共同决定结果（n 个条件 → 2ⁿ 种组合）

| 术语 | 含义 |
|------|------|
| **Condition** | 影响行为的布尔判断（T/F） |
| **Action** | 特定条件组合下系统执行的行为 |
| **Rule** | 一种条件组合 + 对应动作 = 一列 = 一个测试用例 |

```
                Rule 1   Rule 2   Rule 3   Rule 4
  C1: 条件A      T        T        F        F
  C2: 条件B      T        F        T        F
  ─────────────────────────────────────────────
  A1: 动作X      ✓        ✗        ✗        ✗
  A2: 动作Y      ✗        ✓        ✓        ✗
```

**减少 Rule：** 条件对动作无影响时用 `—`（don't care）合并；不可能出现的组合可删除

**vs EP/BVA：** EP/BVA 处理单个输入的值选择；Decision Table 处理多个条件的组合覆盖

---

## State Transition Testing (3.5)

**适用场景：** 同一个输入在不同历史状态下产生不同结果（stateful system）

| 术语 | 含义 |
|------|------|
| **State** | 系统当前的"模式"，决定对下一个输入如何响应 |
| **Transition** | 系统从一个 State 移动到另一个 State |
| **Event / Trigger** | 引起 Transition 发生的动作 |
| **Invalid Transition** | 某个 State 下不应该被接受的 Event |

**State Diagram：** 圆圈 = State，箭头 = Transition，箭头标签 = Event

**测试策略：**
- All Transitions Coverage：每条有效 Transition 至少触发一次（推荐）
- Invalid Transitions：验证系统正确拒绝不该发生的操作

---

## 第3章设计技术总览

| 技术 | 解决什么问题 |
|------|------------|
| EP (3.2) | 单个输入范围太大 → 等价类缩减 |
| BVA (3.3) | 边界处 off-by-one bug → 测 min-1、min、max、max+1 |
| Decision Table (3.4) | 多个条件组合 → 每种 Rule 一个测试用例 |
| State Transition (3.5) | 行为依赖历史状态 → 测所有 Transition + Invalid |

---

## Code Coverage Basics (4.1)

**Code Coverage** = 测试套件实际执行了多少比例的代码（White-Box 视角）

```
Coverage % = (被执行的代码行数 / 总代码行数) × 100
```

| Coverage % | 含义 |
|-----------|------|
| 100% | 每行代码都被至少一个测试执行过 |
| 低 % | 有代码死角，bug 可能藏在从未被测试的路径里 |
| 0% | 该段代码完全没被测试触碰 |

**Coverage Report 颜色含义：**
- 绿色行 = 测试执行过
- 红色行 = 测试从没执行过 → 需要补测试

**Instrumentation（插桩）：** Coverage Tool 在运行时自动插入记录器追踪执行路径，不需要修改源代码。

### 常见 Coverage Tool

| 语言 | 工具 |
|------|------|
| Python | `pytest-cov` |
| JavaScript | `Istanbul / Jest` 内建 |
| Java | `JaCoCo` |
| Go | `go test -cover`（内建） |

```bash
# Python 运行示例
pytest --cov=your_module tests/
pytest --cov=your_module --cov-report=html tests/
```

**关键警告：** Coverage 高 ≠ 没有 bug。执行过不等于验证了结果正确（见 4.3）。

---

## Statement & Branch Coverage (4.2)

| | Statement Coverage | Branch Coverage |
|-|-------------------|-----------------|
| **衡量对象** | 每条语句是否被执行 | 每个判断点的每条分支是否被走过 |
| **粒度** | 行级别 | 决策点级别 |
| **强度** | 弱 | 强 |

```
Branch Coverage 100% → Statement Coverage 一定 100%
Statement Coverage 100% → Branch Coverage 不一定 100%
```

**Decision Point** = 让程序做选择的地方（`if` / `while` / `for` / 三元表达式），每个产生 **2 条分支（True / False）**。

**Branch Coverage 公式：**
```
Branch Coverage % = (被执行的分支数 / 总分支数) × 100
```

**Untested Branch 危险：** 没走过的分支里的 bug 完全不可见——测试通过不代表那条路径是对的。

**记忆规则：** Statement 测"有没有跑到这行"，Branch 测"判断点的两个结果都测到了吗"。

---

## Coverage Pitfalls (4.3)

**核心原则：执行 ≠ 验证。Coverage 高 ≠ 测试质量高。**

| 陷阱 | 含义 |
|------|------|
| **100% Coverage Myth** | 每行都执行过，不代表结果是对的 |
| **Coverage Without Assertions** | 没有 `assert` 的测试可以骗到 100% coverage，但发现不了任何 bug |
| **Vanity Metric** | 把 coverage % 当 KPI → 开发者凑数字，写无意义测试 |
| **False Confidence** | 高 coverage 让团队误以为测得很好，放松对质量的关注 |

**Coverage 的正确用法：**
- ✅ 诊断工具：找出哪些代码路径从没被测试过（coverage 低的地方值得关注）
- ❌ 不是 KPI：不要以达到某个 % 为目标

**好测试的标准：有 assertion、测有意义的场景、基于需求设计、能抓住真实 bug。**

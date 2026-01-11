# 代码解释器 - 使用示例

这里展示 `code-explainer` Skill 的使用示例。

## 示例 1：解释简单的函数

### 输入代码

```python
def calculate_discount(price, discount_rate):
    return price * (1 - discount_rate)

original_price = 100
discount = 0.2
final_price = calculate_discount(original_price, discount)
print(f"最终价格: {final_price}")
```

### 输出解释

# 代码解释

## 这段代码做什么？

计算商品打折后的价格。

## 类比理解

这就像在商店购物：

- 商品有原价（`original_price`）
- 有一个折扣率（`discount_rate`）
- 函数就像收银员，帮你计算最终要付多少钱

## 逐步分析

### 第 1 部分：定义函数

```python
def calculate_discount(price, discount_rate):
    return price * (1 - discount_rate)
```

**作用**：创建一个"打折计算器"

- 输入：原价和折扣率
- 输出：打折后的价格
- 计算公式：原价 × (1 - 折扣率)
  - 如果折扣是 20%（0.2），那么付 80%（1 - 0.2 = 0.8）

### 第 2 部分：使用函数

```python
original_price = 100
discount = 0.2
final_price = calculate_discount(original_price, discount)
print(f"最终价格: {final_price}")
```

**作用**：

1. 设置原价为 100 元
2. 设置折扣率为 20%（0.2）
3. 调用函数计算最终价格（应该是 80 元）
4. 打印结果

## 关键概念

- **函数（Function）**：可重用的代码块，就像一个工具
- **参数（Parameter）**：函数的输入，就像机器的原料
- **返回值（Return value）**：函数的输出，就像机器的产品
- **变量（Variable）**：存储数据的容器

## 可能的改进

- 可以添加输入验证（确保价格和折扣率是合理的数值）
- 可以处理多个商品的折扣

---

## 示例 2：解释列表推导式

### 输入代码

```python
numbers = [1, 2, 3, 4, 5]
squared = [n ** 2 for n in numbers if n % 2 == 1]
print(squared)  # [1, 9, 25]
```

### 输出解释

# 代码解释

## 这段代码做什么？

从一组数字中选出奇数，然后计算它们的平方。

## 类比理解

这就像筛沙子：

1. 先用筛子筛出奇数（过滤）
2. 然后对筛出来的数字进行平方处理（转换）

## 逐步分析

### 列表推导式

```python
squared = [n ** 2 for n in numbers if n % 2 == 1]
```

这是 Python 的**列表推导式**，可以理解为：

```
[   结果    for 每个元素 in 列表    if 条件]
```

**分解步骤**：

1. `for n in numbers` - 遍历每个数字
2. `if n % 2 == 1` - 只保留奇数（除以 2 余 1）
3. `n ** 2` - 对保留的数字求平方

**等价的传统写法**：

```python
squared = []
for n in numbers:
    if n % 2 == 1:
        squared.append(n ** 2)
```

## 关键概念

- **列表推导式**：简洁地创建列表的方式
- **取模运算符（%）**：计算余数，`n % 2 == 1` 判断是否为奇数
- **幂运算（**）**：`n ** 2` 表示 n 的平方

## 可能的改进

- 如果数字列表很大，可以考虑使用生成器表达式节省内存
- 可以添加注释说明复杂逻辑

---

## 示例 3：解释异步函数

### 输入代码

```javascript
async function fetchUserData(userId) {
    try {
        const response = await fetch(`/api/users/${userId}`);
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('获取用户数据失败:', error);
    }
}
```

### 输出解释

# 代码解释

## 这段代码做什么？

异步地从服务器获取用户数据，如果出错则记录错误信息。

## 类比理解

这就像在餐厅点餐：

- 你下单后不会一直站在柜台等（同步）
- 而是可以先找座位坐下（异步）
- 菜做好了服务员会叫你（await）
- 如果厨房出问题了，会有人告诉你（catch）

## 逐步分析

### async/await

```javascript
async function fetchUserData(userId) {
```

- `async`：声明这是一个异步函数
- 异步函数可以"暂停"执行，等待某些操作完成

### await 等待

```javascript
const response = await fetch(`/api/users/${userId}`);
const data = await response.json();
```

- `await`：暂停函数执行，等待网络请求完成
- 第一个 `await`：等待服务器响应
- 第二个 `await`：等待解析 JSON 数据

### 错误处理

```javascript
try {
    // 可能出错的代码
} catch (error) {
    console.error('获取用户数据失败:', error);
}
```

- `try/catch`：捕获和处理错误
- 如果网络请求失败，不会导致程序崩溃
- 而是会执行 `catch` 块中的代码

## 关键概念

- **异步编程**：不阻塞主线程的编程方式
- **Promise**：表示未来可能完成的操作
- **async/await**：更优雅地处理异步操作
- **错误处理**：预防和管理错误情况

## 可能的改进

- 可以添加重试逻辑
- 可以添加请求超时处理
- 可以验证返回数据的格式

---

## 如何使用这个 Skill

### 在 Claude Code 中

1. **直接提供代码**

   ```
   code-explainer
   然后粘贴你的代码
   ```

2. **指定文件路径**

   ```
   code-explainer
   请解释 src/utils/calculate.js 文件
   ```

3. **搜索特定函数**

   ```
   code-explainer
   请解释项目中名为 processData 的函数
   ```

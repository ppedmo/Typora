# 一些遗忘点

- 头文件：提供了函数和类的声明

  源文件：提供了它们的实现

  ![image-20240923103010328](C:\Users\honor\AppData\Roaming\Typora\typora-user-images\image-20240923103010328.png)

- std::（命名空间）

- ```
  auto shortest_job = std::min_element(available_jobs.begin(), available_jobs.end(),
              [](const Job& a, const Job& b) {
                  return a.estimated_runtime < b.estimated_runtime;
              });
  ```

  ### 关键点解析

  1. **`std::min_element`**:
     - 这是一个来自 `<algorithm>` 头文件的标准库函数，用于查找给定范围内的最小元素。
     - 该函数返回一个指向范围内最小元素的迭代器。
  2. **`available_jobs.begin()` 和 `available_jobs.end()`**:
     - `available_jobs.begin()` 返回指向可用作业列表第一个元素的迭代器。
     - `available_jobs.end()` 返回指向可用作业列表尾后位置的迭代器（即超出最后一个元素的迭代器）。
  3. **比较函数**:
     - 这里使用了一个 lambda 表达式作为第三个参数，定义了两个 `Job` 对象之间的比较规则。
     - 函数体 `return a.estimated_runtime < b.estimated_runtime;` 比较两个作业的估计运行时间，返回 `true` 表示 `a` 的运行时间小于 `b` 的运行时间。
  4. **`auto` 关键字**:
     - `auto` 用于类型推导，在这里，`shortest_job` 被推导为 `std::vector<Job>::iterator`，表示它是一个指向 `available_jobs` 中最小元素的迭代器。

# 输入操作

- 不定长数组输入

  ```c++
  std::string line;
      std::getline(std::cin, line); // 读取一行输入
  
      std::istringstream iss(line);
      int num;
      std::vector<int> nums; // 用来存储输入的数字
  
      // 从输入中提取所有数字
      while (iss >> num) {
          nums.push_back(num);
      }
  ```

- 接收一串字符串信息

  ```c++
  
      std::string str;
      std::cin >> str;
  
  ```

  

- const//不会修改数组的值

  - ```cpp
    std::vector<int> multiply(const std::vector<int>& A, const std::vector<int>& B)
    ```


- 在 C++ 中，`for (char c : str)` 是一个范围基于的 for 循环（range-based for loop），它用于遍历字符串 `str` 中的每个字符。这个循环会逐个取出字符串中的字符，并将它们赋值给变量 `c`。（有点像是python的东西）

- 一对数据一对数据输入

  ```cpp
  std::vector<std::pair<int, int>> inputs; // 存储输入数据
      int n, m;
      while (std::cin >> n >> m) {
          inputs.push_back({n, m});
          if (std::cin.eof()) {
              break;
          }
      }
  ```
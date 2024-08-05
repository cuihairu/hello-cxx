## `<list>` 数据结构

`<list>` 是 C++ 标准库中的一个双向链表类模板，提供了灵活的元素插入和删除操作。`std::list` 是一种序列容器，支持高效的前插和后插操作，适用于需要频繁修改元素位置的场景。

### 1. **类介绍**

`std::list` 是一个双向链表容器，每个元素都包含指向前一个和后一个元素的指针。这种结构使得在链表中插入和删除元素变得非常高效，但随机访问性能较差。

#### 1.1 基本操作

**创建和初始化：**

```cpp
#include <iostream>
#include <list>

int main() {
    // 创建一个空的 list
    std::list<int> lst1;

    // 创建一个指定大小并用默认值初始化的 list
    std::list<int> lst2(10); // 包含 10 个 int 元素，每个元素初始化为 0

    // 创建一个指定大小并用特定值初始化的 list
    std::list<int> lst3(5, 42); // 包含 5 个 int 元素，每个元素初始化为 42

    // 使用列表初始化
    std::list<int> lst4 = {1, 2, 3, 4, 5}; // 使用列表初始化

    return 0;
}
```

**访问元素：**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> lst = {10, 20, 30, 40, 50};

    // 访问元素
    for (const auto& value : lst) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**添加和删除元素：**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> lst = {1, 2, 3};

    // 在前面插入元素
    lst.push_front(0);

    // 在末尾插入元素
    lst.push_back(4);

    // 插入元素到指定位置
    auto it = lst.begin();
    ++it; // 移动到第二个位置
    lst.insert(it, 10); // 在第二个位置插入 10

    // 删除指定位置的元素
    it = lst.begin();
    ++it; // 移动到第二个位置
    lst.erase(it); // 删除第二个位置的元素

    // 删除前面和末尾的元素
    lst.pop_front();
    lst.pop_back();

    // 清空所有元素
    lst.clear();

    return 0;
}
```

**合并和排序：**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> lst1 = {3, 1, 4, 1, 5};
    std::list<int> lst2 = {9, 2, 6, 5};

    // 合并两个 list
    lst1.merge(lst2);

    // 排序 list
    lst1.sort();

    // 输出合并和排序后的 list
    for (const auto& value : lst1) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 2. **高级操作**

**迭代器：**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> lst = {1, 2, 3, 4, 5};

    // 使用迭代器遍历
    for (std::list<int>::iterator it = lst.begin(); it != lst.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << std::endl;

    // 使用范围-based for 循环
    for (const auto& value : lst) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**反转和遍历：**

```cpp
#include <iostream>
#include <list>

int main() {
    std::list<int> lst = {1, 2, 3, 4, 5};

    // 反转 list
    lst.reverse();

    // 输出反转后的 list
    for (const auto& value : lst) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 3. **总结**

`<list>` 提供了一个双向链表的实现，支持高效的插入和删除操作。由于其双向链表的特性，`std::list` 在插入和删除操作中表现优异，但其随机访问性能较差。通过掌握 `std::list` 的基本操作和高级功能，可以有效地处理需要频繁插入和删除元素的场景。
# actionRPG

## URPGItem::UPrimaryDataAsset

所有物品的基类 不可直接派生蓝图类

抽象 ， 蓝图类型

### 属性

- 价格    int32
- 最大容量    int32
- 能力等级    int32
- 物品种类    FPrimaryAssetType
- 名称            FText
- 描述            FText
- 被赋予的能力  Subclass<URPGGameplayAbility>
- 图标Icon          FSlateBrush

### 方法

- bool 是否为可消耗品 const
- FString 获取身份字符 const


```mermaid
graph LR
    start[开始] --> input[输入A,B,C]
    input --> conditionA{A是否大于B}
    conditionA -- YES --> conditionC{A是否大于C}
    conditionA -- NO --> conditionB{B是否大于C}
    conditionC -- YES --> printA[输出A]
    conditionC -- NO --> printC[输出C]
    conditionB -- YES --> printB[输出B]
    conditionB -- NO --> printC[输出C]
    printA --> stop[结束]
    printC --> stop
    printB --> stop
```

```mermaid
graph LR
你 -- 爱-->我
我-- 爱 -->你

蜜雪冰城-->ice
蜜雪冰城-->tea
```

| asdsd | sdasd | asdas |
| ----- | ----- | ----- |
| xxx   | ddd   | aaa   |
| xxx   | ddd   | ddd   |
| sss   | as    | ss    |

```mermaid
graph 
a-->b
b-->e
subgraph one
e-->c{as}
c-- yes-->d[ass]
c-- no -->a

d-->f
f-->a
b-->f
e-->d
f-->e
d-->e
b-->d
f-->b
end
subgraph LR two
	f-->g
	g-->h
end

```


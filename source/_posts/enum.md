---
title: enum应用
date: 2021-10-15 19:05:22
tags: enum
categories: Enum
excerpt: enum是 JavaScript 中的保留字，JavaScript 不支持传统的枚举。但是定义枚举非常简单，枚举的好处在于方便多状态的管理,以及可读性更强
---

## 方式一（适用于简易过滤器中）

```javascript
// enum.js**文件
/**
 * 获取枚举值：STATUSMAP.TTT
 * 获取枚举描述：STATUSMAP.getDesc('SH')
 * 通过枚举值获取描述：STATUSMAP.getDescFromValue('TG')
 */
const STATUSMAP = createEnum({
  SH: ["SH", "审核中"],
  TG: ["TG", "审核通过"],
});

function createEnum(definition) {
  const valueMap = {};
  const descMap = {};
  for (const key of Object.keys(definition)) {
    const [value, desc] = definition[key];
    valueMap[key] = value;
    descMap[value] = desc;
  }
  return {
    ...valueMap,
    getDesc(key) {
      return (definition[key] && definition[key][1]) || "无";
    },
    getDescFromValue(value) {
      return descMap[value] || "无";
    },
  };
}

export default STATUSMAP;
```

**view**文件

```html
<!-- 过滤器中使用 则在filters过滤器中直接使用函数返回值 -->
<el-row>
  <el-button>枚举测试</el-button>
  <p>当前状态：{{STATUS.getDescFromValue('SH')}}</p>
  <p>也可用通过枚举名称获取描述：{{STATUS.getDesc('HHH')}}</p>
</el-row>
```

## 方拾二（过滤器，循环列表）

```js
// order.js文件
/**
 * 定义枚举值 [{value: '', label: ''}]
 */
export default {
  order: [
    { value: "TJ", label: "已提交" },
    { value: "CZ", label: "处理中" },
    { value: "CL", label: "已处理" },
  ],
  orderDetail: [
    { value: "DF", label: "待发货" },
    { value: "FH", label: "已发货" },
    { value: "QS", label: "已签收" },
  ],
};
```

```js
// constants.js文件
/**
 * 定义枚举工具
 */
import order from "./order/index.js";

let constants = {
  ...order,
};

let valueMap = {};
let nameMap = {};
Object.keys(constants).forEach((key) => {
  valueMap[key] = [];
  nameMap[key] = {};
  constants[key].forEach((event) => {
    valueMap[key].push(event);
    nameMap[key][event.value] = event.label;
  });
});

export { valueMap, nameMap };
```

```js
/**
* view文件
*/
<template>
	<h3>枚举值用于展示</h3>
	<el-row>
		<el-button v-for="(item, index) in valueMap.order" :key="index">{{item.label}}</el-button>
	</el-row>
	<h3>枚举值过滤器</h3>
	<el-row>
		<el-button>{{enumValue | filterStatus('orderDetail')}}</el-button>
	</el-row>
</template>

<script>
import { valueMap, nameMap } from '@/constants';
export default {
  data() {
    return {
      STATUS: STATUS,
      valueMap,
      enumValue: 'FH', // 发货
    }
  },
  filters:{
    filterStatus: function(val, key){
      if(!val && val !== 0) return '无';
      return nameMap[key][val];
    }
  }
}
```

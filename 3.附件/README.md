### 系统预设模板响应示例

```json
{
  "id": "template_id_1",
  "merchantId": "123",
  "bannerImageUrl": "https://example.com/1.jpg",
  "title": "活动标题",
  "startAt": "2022-12-01 08:00:00",
  "endAt": "2022-12-20 18:00:00",
  "widgetSettings": [
    {
      "widgetId": "W_ACTIVITY_ADVANCED_SETTING",
      "primaryButtonName": "点我购买",
      "virtualCustomerEnabled": true,
      "autoRefundEnabled": true,
      "buyRestrictionEnabled": false,
      "buyRecordsEnabled": true
    },
    {
      "widgetId": "W_NORMAL_SETTING",
      "groupListEnabled": true,
      "guestListEnabled": true,
      "bgColor": "#c3c3c3"
    },
    {
      "widgetId": "W_ACTIVITY_DESC"
    },
    {
      "widgetId": "W_ACTIVITY_DISTRIBUTION",
      "distributionRule": "APPLY_TO_PAID",
      "lockDistributionRelation": true,
      "distributionRankEnabled": false
    },
    {
      "widgetId": "W_ACTIVITY_GOODS",
      "firstDistribution": {
        "type": "ABSOLUT"
      },
      "secondDistribution": {
        "type": "PERCENT"
      },
      "groupBuyPhases": [
        {
          "num": 2
        }
      ],
      "payMethod": {
        "method": "DEPOSIT"
      }
    },
    {
      "widgetId": "W_CUSTOMER_INFO_COLLECTION"
    }
  ]
}
```

### 创建活动请求参数示例

```json
{
  "templateId": "1",
  "bannerImageUrl": "https://www.baidu.com/img/flexible/logo/pc/result@2.png",
  "title": "我要活动",
  "startAt": "2022-12-01 09:00:00",
  "endAt": "2022-12-20 09:00:00",
  "widgetSettings": [
    {
      "widgetId": "W_ACTIVITY_ADVANCED_SETTING",
      "primaryButtonName": "点我购买",
      "virtualCustomerEnabled": true,
      "autoRefundEnabled": true,
      "buyRestrictionEnabled": false,
      "buyRecordsEnabled": true
    },
    {
      "widgetId": "W_ACTIVITY_DESC",
      "description": "我来描述一下这个活动"
    },
    {
      "widgetId": "W_NORMAL_SETTING",
      "groupListEnabled": false,
      "guestListEnabled": true,
      "bgColor": "#c3c3c3"
    },
    {
      "widgetId": "W_ACTIVITY_DISTRIBUTION",
      "distributionRule": "APPLY_TO_PAID",
      "lockDistributionRelation": true,
      "distributionRankEnabled": false
    },
    {
      "widgetId": "W_ACTIVITY_GOODS",
      "goodsId": "11111",
      "skuId": "22222",
      "name": "商品名称",
      "price": 399,
      "firstDistribution": {
        "type": "ABSOLUT",
        "amount": 68
      },
      "secondDistribution": {
        "type": "PERCENT",
        "percent": 15
      },
      "groupBuyPhases": [
        {
          "num": 2,
          "price": 299
        },
        {
          "num": 5,
          "price": 199
        }
      ],
      "payMethod": {
        "method": "DEPOSIT",
        "amount": 50
      }
    },
    {
      "widgetId": "W_CUSTOMER_INFO_COLLECTION",
      "items": [
        {
          "widgetId": "W_TEXT",
          "required": true,
          "label": "身份证号"
        },
        {
          "widgetId": "W_TEXT",
          "required": false,
          "label": "地址"
        }
      ]
    }
  ]
}
```

### 编辑活动请求参数示例

```json
{
  "templateId": "1",
  "bannerImageUrl": "https://www.baidu.com/img/flexible/logo/pc/result@2.png",
  "title": "我要活动",
  "startAt": "2022-12-01 09:00:00",
  "endAt": "2022-12-20 09:00:00",
  "widgetSettings": [
    {
      "widgetId": "W_ACTIVITY_ADVANCED_SETTING",
      "primaryButtonName": "点我购买",
      "virtualCustomerEnabled": true,
      "autoRefundEnabled": true,
      "buyRestrictionEnabled": false,
      "buyRecordsEnabled": true
    },
    {
      "widgetId": "W_ACTIVITY_DESC",
      "description": "我来描述一下这个活动"
    },
    {
      "widgetId": "W_NORMAL_SETTING",
      "groupListEnabled": false,
      "guestListEnabled": true,
      "bgColor": "#c3c3c3"
    },
    {
      "widgetId": "W_ACTIVITY_DISTRIBUTION",
      "distributionRule": "APPLY_TO_PAID",
      "lockDistributionRelation": true,
      "distributionRankEnabled": false
    },
    {
      "widgetId": "W_ACTIVITY_GOODS",
      "goodsId": "11111",
      "skuId": "22222",
      "name": "商品名称",
      "price": 399,
      "firstDistribution": {
        "type": "ABSOLUT",
        "amount": 66
      },
      "secondDistribution": {
        "type": "PERCENT",
        "percent": 15
      },
      "groupBuyPhases": [
        {
          "num": 2,
          "price": 299
        },
        {
          "num": 5,
          "price": 199
        }
      ],
      "payMethod": {
        "method": "DEPOSIT",
        "amount": 50
      }
    },
    {
      "widgetId": "W_CUSTOMER_INFO_COLLECTION",
      "items": [
        {
          "widgetId": "W_TEXT",
          "required": true,
          "label": "身份证号"
        },
        {
          "widgetId": "W_TEXT",
          "required": false,
          "label": "性别"
        }
      ]
    }
  ]
}
```

### 各个组件传参说明

#### 活动基本设置 ID：W_NORMAL_SETTING

```json
{
  "widgetId": "W_NORMAL_SETTING",
  "groupListEnabled": true,
  "guestListEnabled": true,
  "bgColor": "#c3c3c3"
}
```

### 活动分销设置 ID：W_ACTIVITY_DISTRIBUTION

```json
{
  "distributionRule": "APPLY_TO_UNPAID",
  "lockDistributionRelation": true,
  "distributionRankEnabled": false
}
```

#### 活动商品 ID：W_ACTIVITY_GOODS

```json
{
  "widgetId": "W_ACTIVITY_GOODS",
  "goodsId": "123",
  "skuId": "321",
  "name": "商品名称",
  "price": 300,
  "firstDistribution": {
    "type": "ABSOLUT",
    "amount": 50
  },
  "secondDistribution": {
    "type": "PERCENT",
    "percent": 10
  },
  "groupBuyPhases": [
    {
      "num": 2,
      "price": 268
    }
  ],
  "payMethod": {
    "method": "TOTAL 拼团价购买 或者 DEPOSIT 付定金，DEPOSIT 情况 amount 必传",
    "amount": 50
  }
}
```

#### 活动介绍 ID：W_ACTIVITY_DESC

```json
{
  "widgetId": "W_ACTIVITY_DESC",
  "description": "这个是描述"
}
```

#### 活动高级设置 ID：W_ACTIVITY_ADVANCED_SETTING

```json
{
  "widgetId": "W_ACTIVITY_ADVANCED_SETTING",
  "primaryButtonName": "点我购买",
  "virtualCustomerEnabled": true,
  "autoRefundEnabled": true,
  "buyRestrictionEnabled": false,
  "buyRecordsEnabled": true
}
```

#### 客户信息收集 ID：W_CUSTOMER_INFO_COLLECTION

```json
{
  "widgetId": "W_CUSTOMER_INFO_COLLECTION",
  "name": "张三",
  "phone": "18888888888",
  "params": [
    {
      "label": "身份证号",
      "value": "320505200010101121"
    }
  ]
}
```
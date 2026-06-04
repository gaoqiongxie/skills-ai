---
name: "enterprise-crm-fullstack"
description: "企业级CRM全栈开发规范：基于Vue 2 + Element UI + Java Spring Boot的标准化开发指南。覆盖前端配置式列表页、详情页、国际化、权限控制，后端分层架构、接口规范、数据库设计。当用户说'CRM开发'、'Vue 2列表页'、'Element UI表单'、'Java后端接口'、'全栈开发规范'、'中后台系统开发'、'工单系统开发'、'客户管理系统开发'时触发。核心特点：前后端标准化、配置式开发、企业级权限、国际化支持。"
---

> **来源**: 基于企业级CRM项目实战经验 + Vue 2 + Element UI + Spring Boot 技术栈
>
> **发布时间**: 2026-06-04
>
> **理念**: "标准化不是束缚，是让团队协作更高效的契约。"

# Enterprise CRM Fullstack — 企业级CRM全栈开发规范

一套完整的企业级中后台系统全栈开发规范，前端基于 Vue 2 + Element UI，后端基于 Java Spring Boot + MyBatis，覆盖从数据库设计到前端页面的完整开发链路。

---

## 🎯 技术栈概览

### 前端

| 技术 | 版本/说明 |
|------|----------|
| Vue | 2.6.x (Options API) |
| Vue Router | 3.x (hash 模式) |
| Vuex | 3.x (模块自动加载) |
| Element UI | 2.13.x |
| Axios | 0.18.x |
| SCSS | node-sass |
| 代码规范 | ESLint + Prettier + Standard |

### 后端

| 技术 | 版本/说明 |
|------|----------|
| Java | 8+ |
| Spring Boot | 2.x |
| MyBatis / MyBatis-Plus | 数据访问 |
| Maven | 构建工具 |
| OAuth2 + JWT | 认证授权 |

---

## 📁 前端项目结构规范

```
src/
├── api/                    # API 接口定义（按业务模块拆分）
│   ├── customer.js         # 客户相关
│   ├── workOrder.js        # 工单相关
│   └── silentCustomer.js   # 沉默客户相关
├── components/             # 公共/业务组件
│   ├── common/            # 全局注册基础组件
│   └── business/          # 业务组件（按模块分目录）
├── layout/                # 布局组件（Sidebar/Navbar/AppMain）
├── router/                # 路由配置（单文件 index.js）
├── store/                 # Vuex store（自动加载 modules）
├── styles/                # 全局 SCSS 样式
│   ├── variables.scss     # SCSS 变量
│   └── index.scss         # 全局样式入口
├── utils/                 # 工具函数
│   ├── request.js         # Axios 封装
│   └── directives.js      # 自定义指令（权限等）
├── views/                 # 页面级组件（按菜单结构分目录）
│   └── customerMarketing/
│       ├── SilentCustomer/    # 沉默客户池
│       │   └── index.vue
│       └── WorkOrder/         # 电销工单
│           ├── index.vue
│           └── Detail.vue
├── main.js                # 应用入口
├── permission.js          # 路由守卫
└── settings.js            # 应用配置
```

---

## 🎨 前端开发规范

### 1. 页面开发模式

#### 模式 A：配置式列表页（推荐）

适用于数据列表+筛选+分页的场景：

```vue
<template>
  <SearchListPage
    ref="listPage"
    :columns="columns"
    :form-item-list="formItemList"
    :api="queryApi"
    :btn-list="btnList"
    @selection-change="handleSelectionChange"
  />
</template>

<script>
import { querySilentCustomerList, transferCustomers } from '@/api/silentCustomer'

export default {
  data() {
    return {
      columns: [
        { type: 'selection' },
        { label: this.$i18n({ key: 'column.score', desc: '客户评分' }), prop: 'score',
          render: (h, { row }) => {
            const type = row.score >= 90 ? 'danger' : row.score >= 80 ? 'warning' : 'info'
            return <el-tag type={type}>{row.score}</el-tag>
          }
        },
        { label: this.$i18n({ key: 'column.name', desc: '客户名称' }), prop: 'customerName' },
        // ... 其他列
      ],
      formItemList: [
        { label: this.$i18n({ key: 'filter.name', desc: '客户名称' }), prop: 'customerName', type: 'input' },
        { label: this.$i18n({ key: 'filter.level', desc: '客户等级' }), prop: 'customerLevel', 
          type: 'select', options: [{ label: 'C4', value: 'C4' }, { label: 'D4', value: 'D4' }, { label: 'E', value: 'E' }] 
        },
        { label: this.$i18n({ key: 'filter.days', desc: '沉默天数' }), prop: 'silentDays', type: 'conditionNumber' },
        { label: this.$i18n({ key: 'filter.amount', desc: '逾期金额' }), prop: 'overdueAmount', type: 'conditionNumber' },
        { label: this.$i18n({ key: 'filter.time', desc: '最后分配时间' }), prop: 'lastAssignTime', type: 'dateRange' },
      ],
      btnList: [
        { code: 'btn_transfer', label: this.$i18n({ key: 'btn.transfer', desc: '转派' }), handler: this.handleTransfer }
      ],
      selectedRows: []
    }
  },
  methods: {
    queryApi(params) {
      return querySilentCustomerList(params)
    },
    handleSelectionChange(rows) {
      this.selectedRows = rows
    },
    handleTransfer() {
      if (this.selectedRows.length === 0) {
        this.$message.warning(this.$i18n({ key: 'msg.selectFirst', desc: '请先选择要转派的客户' }))
        return
      }
      // 转派逻辑
    }
  }
}
</script>
```

#### 模式 B：自定义详情页

适用于表单编辑、复杂交互的详情页：

```vue
<template>
  <div class="work-order-detail">
    <!-- 操作按钮区 -->
    <div class="action-bar">
      <el-button @click="handleBack">{{ $i18n({ key: 'btn.back', desc: '返回' }) }}</el-button>
      <el-button v-btn-permission="['btn_edit']" type="primary" @click="handleEdit">
        {{ isEditing ? $i18n({ key: 'btn.save', desc: '保存' }) : $i18n({ key: 'btn.edit', desc: '编辑' }) }}
      </el-button>
      <el-button v-btn-permission="['btn_complete']" type="success" @click="handleComplete">
        {{ $i18n({ key: 'btn.complete', desc: '完成工单' }) }}
      </el-button>
    </div>

    <!-- 基础信息卡片 -->
    <el-card class="info-card">
      <div slot="header">{{ $i18n({ key: 'card.baseInfo', desc: '基础信息' }) }}</div>
      <el-row :gutter="20">
        <el-col v-for="field in baseInfoFields" :key="field.prop" :span="6">
          <div class="info-item">
            <label>{{ field.label }}：</label>
            <span v-if="field.prop !== 'remark'">{{ detail[field.prop] }}</span>
            <el-input v-else v-model="detail.remark" :maxlength="500" show-word-limit />
          </div>
        </el-col>
      </el-row>
    </el-card>

    <!-- 跟进信息卡片 -->
    <el-card class="follow-up-card">
      <div slot="header">{{ $i18n({ key: 'card.followUp', desc: '跟进信息' }) }}</div>
      
      <!-- 快捷录入 -->
      <div class="quick-input">
        <el-form :inline="true">
          <el-form-item :label="$i18n({ key: 'form.wechat', desc: '是否添加企微' })">
            <el-radio-group v-model="followUp.isAddWechat">
              <el-radio :label="true">{{ $i18n({ key: 'common.yes', desc: '是' }) }}</el-radio>
              <el-radio :label="false">{{ $i18n({ key: 'common.no', desc: '否' }) }}</el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item :label="$i18n({ key: 'form.connected', desc: '是否接通' })">
            <el-select v-model="followUp.isConnected">
              <el-option :label="$i18n({ key: 'status.connected', desc: '已接通' })" value="connected" />
              <el-option :label="$i18n({ key: 'status.noAnswer', desc: '未接通' })" value="no_answer" />
              <el-option :label="$i18n({ key: 'status.empty', desc: '空号' })" value="empty" />
              <el-option :label="$i18n({ key: 'status.shutdown', desc: '停机' })" value="shutdown" />
            </el-select>
          </el-form-item>
        </el-form>
      </div>

      <!-- 跟进记录表格（内联编辑） -->
      <el-table :data="followUp.records">
        <el-table-column type="index" width="50" />
        <el-table-column :label="$i18n({ key: 'column.time', desc: '跟进时间' })">
          <template slot-scope="{ row }">
            <el-date-picker v-if="row.isEditing" v-model="row.followTime" type="datetime" />
            <span v-else>{{ row.followTime }}</span>
          </template>
        </el-table-column>
        <el-table-column :label="$i18n({ key: 'column.content', desc: '跟进内容' })">
          <template slot-scope="{ row }">
            <el-input v-if="row.isEditing" v-model="row.content" type="textarea" :rows="2" />
            <span v-else>{{ row.content }}</span>
          </template>
        </el-table-column>
        <el-table-column :label="$i18n({ key: 'column.operator', desc: '操作人' })" prop="operator" />
        <el-table-column :label="$i18n({ key: 'column.action', desc: '操作' })">
          <template slot-scope="{ row, $index }">
            <el-button v-if="!row.isEditing" type="text" @click="handleEditRow(row)">编辑</el-button>
            <el-button v-else type="text" @click="handleSaveRow(row)">保存</el-button>
            <el-button type="text" @click="handleDeleteRow($index)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>

      <el-button v-if="isEditing" type="primary" icon="el-icon-plus" @click="handleAddRow">
        {{ $i18n({ key: 'btn.addFollowUp', desc: '新增跟进' }) }}
      </el-button>
    </el-card>
  </div>
</template>

<script>
import { getWorkOrderDetail, saveFollowUp } from '@/api/workOrder'

export default {
  data() {
    return {
      isEditing: false,
      detail: {},
      followUp: {
        isAddWechat: false,
        isConnected: '',
        callCount: 0,
        records: []
      },
      baseInfoFields: [
        { prop: 'orderNo', label: this.$i18n({ key: 'field.orderNo', desc: '工单编号' }) },
        { prop: 'status', label: this.$i18n({ key: 'field.status', desc: '工单状态' }) },
        { prop: 'customerName', label: this.$i18n({ key: 'field.customerName', desc: '关联客户' }) },
        { prop: 'contactPhone', label: this.$i18n({ key: 'field.contactPhone', desc: '联系人电话' }) },
        // ... 其他字段
      ]
    }
  },
  created() {
    this.fetchDetail()
  },
  methods: {
    async fetchDetail() {
      const { id } = this.$route.params
      const res = await getWorkOrderDetail(id)
      this.detail = res.data
      this.followUp.records = res.data.followUpRecords || []
    },
    handleBack() {
      this.$router.back()
    },
    handleEdit() {
      if (this.isEditing) {
        this.handleSave()
      } else {
        this.isEditing = true
      }
    },
    async handleSave() {
      // 保存逻辑
      this.isEditing = false
      this.$message.success(this.$i18n({ key: 'msg.saveSuccess', desc: '保存成功' }))
    },
    handleComplete() {
      this.$confirm(
        this.$i18n({ key: 'confirm.complete', desc: '确定要完成此工单吗？' }),
        this.$i18n({ key: 'common.tip', desc: '提示' }),
        { type: 'warning' }
      ).then(() => {
        // 完成工单逻辑
      })
    },
    handleAddRow() {
      this.followUp.records.push({
        followTime: new Date(),
        content: '',
        operator: this.$store.state.user.name,
        isEditing: true
      })
    },
    handleEditRow(row) {
      this.$set(row, 'isEditing', true)
    },
    handleSaveRow(row) {
      this.$set(row, 'isEditing', false)
    },
    handleDeleteRow(index) {
      this.followUp.records.splice(index, 1)
    }
  }
}
</script>

<style lang="scss" scoped>
.work-order-detail {
  padding: 20px;
  
  .action-bar {
    margin-bottom: 20px;
  }
  
  .info-card {
    margin-bottom: 20px;
    
    .info-item {
      margin-bottom: 16px;
      
      label {
        color: #606266;
        font-weight: 500;
      }
    }
  }
  
  .follow-up-card {
    .quick-input {
      margin-bottom: 20px;
      padding: 16px;
      background: #f5f7fa;
      border-radius: 4px;
    }
  }
}
</style>
```

### 2. API 封装规范

**统一使用命名导出模式**：

```javascript
// src/api/silentCustomer.js
import request from '@/utils/request'

/**
 * 查询沉默客户列表
 * @param {Object} data - 查询参数
 */
export function querySilentCustomerList(data) {
  return request({
    url: '/api/customer/silent/list',
    method: 'post',
    data
  })
}

/**
 * 批量转派沉默客户
 * @param {Object} data - { customerIds: [], assigneeId: '' }
 */
export function transferCustomers(data) {
  return request({
    url: '/api/customer/silent/transfer',
    method: 'post',
    data
  })
}

/**
 * 查询工单详情
 * @param {string} id - 工单ID
 */
export function getWorkOrderDetail(id) {
  return request({
    url: `/api/work-order/${id}`,
    method: 'get'
  })
}
```

### 3. 国际化规范

**所有用户可见文本必须使用 `$i18n()`**：

```javascript
// 正确
<label>{{ $i18n({ key: 'field.customerName', desc: '客户名称' }) }}</label>

// 错误
<label>客户名称</label>
```

**key 命名规范**：
- 页面标题：`page.xxx`
- 按钮：`btn.xxx`
- 表单字段：`field.xxx` / `form.xxx`
- 表格列：`column.xxx`
- 筛选条件：`filter.xxx`
- 提示信息：`msg.xxx`
- 确认框：`confirm.xxx`

### 4. 权限控制规范

**按钮权限**：

```vue
<!-- 正确 -->
<el-button v-btn-permission="['btn_transfer']">转派</el-button>

<!-- 错误 -->
<el-button>转派</el-button>
```

**页面权限**：
- 路由守卫仅设置标题，不做登录校验
- 实际权限由后端接口控制
- 前端路由全部静态注册

### 5. 路由添加规范

```javascript
// src/router/index.js
{
  path: '/customer-marketing/silent-customer',
  component: Layout,
  children: [
    {
      path: '',
      name: 'SilentCustomer',
      component: () => import('@/views/customerMarketing/SilentCustomer/index'),
      meta: { 
        title: $i18n({ key: 'page.silentCustomer', desc: '沉默客户池' }),
        icon: 'customer'
      }
    }
  ]
}
```

---

## 🔧 后端开发规范

### 1. 分层架构

```
controller/     # 表现层：处理HTTP请求和响应
service/        # 业务逻辑层：实现业务逻辑
mapper/         # 数据访问层：MyBatis Mapper接口
entity/         # 模型层：实体类
```

### 2. Controller 规范

```java
@RestController
@RequestMapping("/api/customer")
public class SilentCustomerController {

    @Autowired
    private SilentCustomerService silentCustomerService;

    /**
     * 查询沉默客户列表
     */
    @PostMapping("/silent/list")
    public Result<PageResult<SilentCustomerVO>> queryList(@RequestBody SilentCustomerQueryDTO query) {
        return Result.success(silentCustomerService.queryList(query));
    }

    /**
     * 批量转派客户
     */
    @PostMapping("/silent/transfer")
    public Result<Void> transfer(@RequestBody TransferDTO dto) {
        silentCustomerService.transfer(dto);
        return Result.success();
    }
}
```

### 3. Service 规范

```java
@Service
public class SilentCustomerServiceImpl implements SilentCustomerService {

    @Autowired
    private SilentCustomerMapper silentCustomerMapper;

    @Override
    public PageResult<SilentCustomerVO> queryList(SilentCustomerQueryDTO query) {
        // 业务逻辑处理
        PageHelper.startPage(query.getPage(), query.getLimit());
        List<SilentCustomerVO> list = silentCustomerMapper.selectList(query);
        return PageResult.of(list);
    }

    @Override
    @Transactional(rollbackFor = Exception.class)
    public void transfer(TransferDTO dto) {
        // 转派逻辑：创建工单 + 更新客户跟进人
        // 事务控制
    }
}
```

### 4. 接口返回规范

```java
public class Result<T> {
    private Integer code;      // 200成功，其他失败
    private String message;
    private T data;
    
    public static <T> Result<T> success(T data) {
        Result<T> result = new Result<>();
        result.setCode(200);
        result.setData(data);
        return result;
    }
    
    public static <T> Result<T> error(String message) {
        Result<T> result = new Result<>();
        result.setCode(500);
        result.setMessage(message);
        return result;
    }
}
```

### 5. 数据库设计规范

**必须字段**（所有表）：

```sql
`remark`      VARCHAR(200)  NOT NULL DEFAULT ''     COMMENT '系统备注',
`create_time` datetime      NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
`edit_time`   datetime      NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '编辑时间',
`delete_flag` tinyint(4)    NOT NULL DEFAULT '0' COMMENT '是否删除 0未删除 1已删除'
```

**表名命名**：小写下划线分隔，如 `silent_customer`、`work_order`、`follow_up_record`

**索引命名**：`idx_` 前缀，如 `idx_customer_name`

---

## 🔒 安全规范

### 前端
- 按钮权限必须使用 `v-btn-permission`
- 敏感数据（手机号）显示需遵循脱敏规则
- 所有请求自动注入 Token + 签名

### 后端
- 接口前缀规范：
  - `/api/`：前端调用（需鉴权）
  - `/feign/`：微服务内部调用（禁止外部访问）
  - `/job/`：定时任务（禁止外部访问）
- 参数校验：使用 `@Valid` + DTO 注解
- SQL 注入防护：使用 MyBatis 参数化查询

---

## 🧪 测试规范

### 前端
```javascript
// Jest + Vue Test Utils
describe('SilentCustomerList', () => {
  it('should render columns correctly', () => {
    // 测试列渲染
  })
  
  it('should handle transfer button click', () => {
    // 测试转派按钮
  })
})
```

### 后端
```java
@SpringBootTest
class SilentCustomerServiceTest {
    
    @Autowired
    private SilentCustomerService silentCustomerService;
    
    @Test
    void shouldQueryListSuccessfully() {
        SilentCustomerQueryDTO query = new SilentCustomerQueryDTO();
        query.setPage(1);
        query.setLimit(20);
        
        PageResult<SilentCustomerVO> result = silentCustomerService.queryList(query);
        
        assertNotNull(result);
        assertTrue(result.getList().size() > 0);
    }
}
```

---

## 🚀 快速入口

```
"CRM开发" → Vue 2 + Element UI + Java 全栈开发规范
"Vue 2列表页" → 配置式 SearchListPage 开发指南
"Element UI表单" → 详情页表单开发规范
"Java后端接口" → Controller/Service/Mapper 分层规范
"全栈开发规范" → 完整的前后端标准化开发流程
"中后台系统开发" → 企业级中后台系统开发最佳实践
"工单系统开发" → 工单CRUD + 状态管理 + 跟进记录
"客户管理系统开发" → 客户池 + 筛选 + 转派 + 评分
```

---

## 🆚 与现有 Skill 的关系

| Skill | 关系 | 协作方式 |
|-------|------|---------|
| **web-artifacts-builder** | 替代 | 本 Skill 更贴合 Vue 2 + Element UI 实际项目，`web-artifacts-builder` 面向 React 技术栈 |
| **database-designer** | 前置 | `database-designer` 设计表结构，本 Skill 执行前后端开发 |
| **api-doc-generator** | 前置 | `api-doc-generator` 生成接口文档，本 Skill 按文档实现接口 |
| **frontend-code-review** | 后置 | 本 Skill 编码完成后，用 `frontend-code-review` 审查 Vue 代码质量 |
| **backend-change-flow** | 互补 | 后端变更时，用 `backend-change-flow` 规范变更流程 |
| **git-commit** | 协同 | 本 Skill 遵循项目的 Conventional Commits 规范 |
| **testing-patterns** | 互补 | 本 Skill 编码，用 `testing-patterns` 设计测试策略 |

---

> "在企业级开发中，一致性比创新性更重要。每个开发者写出的代码，应该像是一个人写的。"

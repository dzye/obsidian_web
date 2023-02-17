export const addRouters = [{

path: '/account',

component: Layout,

meta: {

title: '账号管理',

icon: 'account',

},

redirect: {

name: 'accountList',

},

children: [{

path: '/account/index',

name: 'accountList',

component: () => import(

/*webpackChunkName:"account"*/

/* webpackPrefetch: true */

'@/views/account/index'),

meta: {

title: '平台账号管理',

},

},

{

path: '/account/role',

name: 'roleList',

component: () => import(

/*webpackChunkName:"account"*/

/* webpackPrefetch: true */

'@/views/role/index'),

meta: {

title: '平台角色管理',

},

},

],

},

{

path: '/merchantGroup',

component: Layout,

meta: {

title: '集团管理',

},

redirect: {

name: 'merchantGroupList',

},

children: [{

path: '/merchantGroup/index',

name: 'merchantGroupList',

component: () => import(

/*webpackChunkName:"merchantGroup"*/

/* webpackPrefetch: true */

'@/views/merchantGroup/list'),

meta: {

title: '集团列表',

},

}],

},

  

// 商户管理

{

path: '/merchant',

component: Layout,

meta: {

title: '商户管理',

},

redirect: {

name: 'merchantList',

},

children: [

{

path: '/merchant/index',

name: 'merchantList',

component: () => import(

/*webpackChunkName:"merchant"*/

/* webpackPrefetch: true */

'@/views/merchant/merchant'),

meta: {

title: '商户列表',

},

},

{

path: '/merchant/addMerchant',

name: 'addMerchant',

component: () => import(

/*webpackChunkName:"merchant"*/

/* webpackPrefetch: true */

'@/views/merchant/merchant/addMerchant'),

meta: {

title: '商户详情',

},

},

{

path: '/merchant/staff',

name: 'merchantStaffList',

component: () => import(

/*webpackChunkName:"merchant"*/

/* webpackPrefetch: true */

'@/views/merchant/staff'),

meta: {

title: '商户员工管理',

icon: '',

},

},

],

},

  

// 区域管理

{

path: '/region',

component: Layout,

meta: {

title: '区域管理',

icon: 'region',

},

redirect: {

name: 'regionList',

},

children: [{

path: '/region/index',

name: 'regionList',

component: () => import(

/*webpackChunkName:"region"*/

/* webpackPrefetch: true */

'@/views/region/index'),

meta: {

title: '区域列表',

icon: '',

},

},

{

path: '/region/accountList',

name: 'regionAccountList',

component: () => import(

/*webpackChunkName:"region"*/

/* webpackPrefetch: true */

'@/views/region/accountList'),

meta: {

title: '区域账号列表',

icon: '',

},

}],

},

  

// C端用户管理

{

path: '/customer',

component: Layout,

redirect: '/customer/index',

meta: {

title: 'C端用户管理',

icon: '',

},

children: [

{

path: '/customer/index',

name: 'customerList',

component: () => import(

/*webpackChunkName:"customer"*/

/* webpackPrefetch: true */

'@/views/customer/index'),

meta: {

title: 'C端用户列表',

icon: '',

},

},

{

path: '/clientUser/detail/:id',

name: 'clientUserDetail',

component: () => import(

/*webpackChunkName:"customer"*/

/* webpackPrefetch: true */

'@/views/customer/detail'),

meta: {

title: 'C端用户详情',

icon: '',

},

},

],

},

  

// 平台配置

{

path: '/settings',

component: Layout,

meta: {

title: '平台配置',

icon: '',

},

redirect: {

name: 'settingsMenuList',

},

children: [

{

path: '/settings/menuList',

name: 'settingsMenuList',

component: () => import(

/*webpackChunkName:"settings"*/

/* webpackPrefetch: true */

'@/views/settings/menuList'),

meta: {

title: '菜单配置',

icon: '',

},

},

{

path: '/settings/merchantRoleTemplate',

name: 'merchantRoleTemplateList',

component: () => import(

/*webpackChunkName:"settings"*/

/* webpackPrefetch: true */

'@/views/settings/merchantRoleTemplate'),

meta: {

title: '预设角色',

icon: '',

},

},

{

path: '/settings/category',

name: 'categoryList',

component: () => import(

/*webpackChunkName:"settings"*/

/* webpackPrefetch: true */

'@/views/settings/category'),

meta: {

title: '平台分类',

icon: '',

},

},

{

path: '/settings/label',

name: 'labelList',

component: () => import(

/*webpackChunkName:"settings"*/

/* webpackPrefetch: true */

'@/views/settings/label'),

meta: {

title: '平台标签',

icon: '',

},

},

{

path: '/settings/versionManagement',

name: 'settingsVersionManagement',

component: () => import(

/*webpackChunkName:"settings"*/

/* webpackPrefetch: true */

'@/views/settings/versionManagement'),

meta: {

title: '版本管理',

icon: '',

},

},

],

},

  

// 日志管理

{

path: '/log',

component: Layout,

redirect: '/log/index',

meta: {

title: '日志管理',

icon: '',

},

children: [{

path: '/log/index',

name: 'logList',

component: () => import(

/*webpackChunkName:"log"*/

/* webpackPrefetch: true */

'@/views/log'),

meta: {

title: '日志管理',

icon: '',

},

}],

},

  

// 运营管理

{

path: '/operation',

name: 'layout',

redirect: '/enjoOrder/index',

component: Layout,

meta: {

title: '运营管理',

icon: '',

},

children: [

{

path: '/enjoOrder/index',

name: 'orderList',

component: () => import(

/*webpackChunkName:"enjoOrder"*/

/* webpackPrefetch: true */

'@/views/enjoOrder'),

meta: {

title: '订单管理',

icon: '',

},

},

{

path: 'enjoPreview',

name: 'previewEnjoOrder',

component: () => import(

/*webpackChunkName:"enjoOrder"*/

/* webpackPrefetch: true */

'@/views/enjoOrder/preview'),

hidden: true,

meta: {

title: '查看订单',

icon: 'order',

},

},

{

path: '/goodsLib/index',

name: 'goodsLibList',

component: () => import(

/*webpackChunkName:"goodsLib"*/

/* webpackPrefetch: true */

'@/views/goodsLib'),

meta: {

title: '平台商品库列表',

},

},

{

path: '/goodsLib/create',

name: 'goodsLibDetail',

component: () => import(

/*webpackChunkName:"goodsLib"*/

/* webpackPrefetch: true */

'@/views/goodsLib/create'),

meta: {

title: '查看商品库商品',

},

},

{

path: '/coupon/index',

name: 'couponList',

component: () => import(

/*webpackChunkName:"coupon"*/

/* webpackPrefetch: true */

'@/views/coupon/index'),

meta: {

title: '优惠券列表',

},

},

{

path: '/coupon/couponAdd',

name: 'couponDetail',

component: () => import(

/*webpackChunkName:"coupon"*/

/* webpackPrefetch: true */

'@/views/coupon/create'),

meta: {

title: '优惠券详情',

},

},

],

}]
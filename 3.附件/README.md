```
/enjo-album/moment/findByPageWithMomentType   获取动态接口
/enjo-album/album/query    获取相册接口
/enjo-album/album/queryOwnAlbum  获取相册列表
/enjo-album/moment/create    发布动态接口
/enjo-album/album/create   创建相册接口
/enjo-album/album/photo/queryByType  根据类型查询全部家庭照片




0:正常进入 1:扫码 2:链接
**枚举说明**: 
ACTIVITY_VIEW_SCAN :活动浏览（扫码） 
ACTIVITY_VIEW_LINK :活动浏览（链接） 
ACTIVITY_VIEW :活动浏览 
PRODUCT_VIEW_SCAN :商品浏览（扫码） 
PRODUCT_VIEW_LINK :商品浏览（链接） 
PRODUCT_VIEW :商品浏览


// 数据埋点进入页面接口

entryPage
{
	eventKey:主键id
	pageUrl:路由
	eventType: 枚举说明
}

// 数据埋点离开页面接口

leavePage   params:eventId 主键id, departureType :离开类型 DEFAULT :默认 PURCHASE :购买
```









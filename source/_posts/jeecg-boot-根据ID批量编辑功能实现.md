---
title: jeecg-boot 根据ID批量编辑功能实现
top: false
cover: false
toc: true
mathjax: true
date: 2021-01-19 11:02:19
password:
summary:
tags:
categories:
---

```java
/**
 * 批量编辑
 *
 * @param deviceIds
 * @param groupId
 * @return
 */
@AutoLog(value = "设备管理-批量编辑")
@ApiOperation(value="设备管理-批量编辑", notes="设备管理-批量编辑")
@PutMapping(value = "/editBatch")
public Result<?> editBatch(@RequestParam(name="deviceIds") String deviceIds,
                  @RequestParam(name="groupId") Integer groupId) {
   List<Device> deviceList = new ArrayList<Device>();
   List list= Arrays.asList(deviceIds.split(","));
   for(int i = 0;i< list.size(); i++){
      Device device = new Device();
      device.setGroupId(groupId);
      device.setId(Integer.valueOf((String)list.get(i)));
      deviceList.add(device);
}
 deviceService.updateBatchById(deviceList);
 return Result.ok("编辑成功!");
}
```
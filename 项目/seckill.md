令牌桶





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104128.png)



限制某一秒网络的最大值





漏桶



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104306.png)





平滑流量







tps qps



维度



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105022.png)





总维度：各个接口总的维度





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104939.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105944.png)







用户注册



生成验证码

Random生成6位随机数，保存在在redis中，在用户注册页面提交注册信息，



登录

用户名密码校验后无误后生成token，存储在redis中并返回给前端



商品缓存：Cache, redis中否则在数据库中





使用行锁

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224101303.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224101427.png)





将库存缓存到redis中



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224104300.png)





异常的处理

校验的类

​          



用户注册：

生成一个验证码存储在redis中



用户表、用户密码表 通过用户 ID 关联



验证判断，在业务层进行用户名密码判断以及通过



```java
if (otpCodeObj == null || !(otpCode instanceof String) ||
            !((String)otpCodeObj).equals(otpCode)) {
            throw new BusinessException(EnumBusinessError.OPT_CODE_ERROR);

}

        UserModel userModel = new UserModel();
        userModel.setTelephone(telephone);
        userModel.setName(name);
        userModel.setGender(new Byte(String.valueOf(gender)));
        userModel.setAge(age);
        userModel.setEncrptPassword(EncodeByMd5(password));
		// 在业务层处理
        userService.register(userModel);
```





```java
public void register(UserModel userModel) throws BusinessException {

        if (userModel == null) {
            return;
        }
        if (StringUtils.isEmpty(userModel.getName())) {
            return;
        }

        UserDO userDO = convertDOFromModel(userModel);
        try {
            userDOMapper.insertSelective(userDO);
        } catch (Exception e) {
           throw new BusinessException(EnumBusinessError.UNKOWN_ERROR,"手机号重复");
        }

        userModel.setId(userDO.getId());
        UserPasswordDO userPasswordDO = convertUserPasswordDOFromModel(userModel);
        userPasswordDOMapper.insertSelective(userPasswordDO);
    }
```





手机号设置唯一键，添加用户名密码





### 登录

用户名密码格式的校验，

在业务层进行用户名密码匹配的校验



生成一个token存在redis中，并发送给前端



### 创建商品



```java
 @PostMapping("/create")
    public CommonReturnType createItem(@RequestParam(name = "title")String title,
                                       @RequestParam(name = "description")String description,
                                       @RequestParam(name = "price") BigDecimal price,
                                       @RequestParam(name = "stock")Integer stock,
                                       @RequestParam(name = "imgUrl")String imgUrl) throws BusinessException {

        ItemModel itemModel = new ItemModel();
        itemModel.setTitle(title);
        itemModel.setDescription(description);
        itemModel.setPrice(price);
        itemModel.setStock(stock);
        itemModel.setImgUrl(imgUrl);

        itemService.createItem(itemModel);
        ItemVO itemVO = convertVOFromModel(itemModel);
        return CommonReturnType.create(itemVO,"success");
    }

```

业务层数据的校验然后填入数据库中



商品表 商品库存表







### 商品

商品id添加唯一键









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225102841.png)





等所有完成后发送消息





数据库提交才发送消息



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225104347.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225110322.png)

如果没有明确告诉你数据库是否执行成功就会一直调用check方法







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225113257.png)





售空判断---》







qps tps







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225133725.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225134111.png)
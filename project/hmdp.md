#### 获取验证码
```
 public Result sendCode(@RequestParam("phone") String phone, HttpSession session,  HttpServletRequest request) {
        // TODO 发送短信验证码并保存验证码
        String clientIp = request.getRemoteAddr();

        // 使用Redis处理限流
        Boolean success = redisTemplate.opsForValue().setIfAbsent(phone, "exists", RATE_LIMIT_SECOND, TimeUnit.SECONDS);

        if (success != null && success) {
            // 如果上锁成功，可以继续处理请求
            return Result.ok(phone +"yes");
        } else {
            Long expire = redisTemplate.getExpire(phone); //测试
            return Result.fail(expire+"秒后再发送");
        }
    }
```
* 用IP地址作为key导致使用NAT的用户无法正常获取验证码
* 使用手机号作为key导致同一个用户可以给同时给不同用户发送验证码
---
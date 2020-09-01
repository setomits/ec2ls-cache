我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

ec2ls-cache
===
`ec2ls-cache` is a simple command for describe instances with local cache.

Why cache ?
---
To avoid MFA input.

CommandLine Option
---
|option key|description|
|---|---|
|--cachename|specify cachename. cache path is `~/.cache/ec2ls-cache/<cachename>`. default cachename is `out`|
|--columns|specify columns displaying (csv). use <`ec2.Instance` field> or `Tag:<tagKey>` or `TagAll`. see [`ec2.Instance` field](https://docs.aws.amazon.com/sdk-for-go/api/service/ec2/#Instance). default is `"InstanceId"`|
|--filters|use filters. see [aws document](https://docs.aws.amazon.com/sdk-for-go/api/service/ec2/#DescribeInstancesInput)|
|--profile|specify aws credential profile|
|--region|specify aws region|
|--sortcolumn|specify sort key column|
|--updateCache, -u|read from AWS and store cache.|

Example Usage
---
- Read from AWS and store cache.
```
$ ec2ls-cache -u --cachename stage --profile yourProfile --region ap-northeast-1
```

- Read from cache
```
$ ec2ls-cache --cachename stage
```

- Use filters
```
$ ec2ls-cache -u --cachename prod --filters "instance-state-name=running" --filters "tag:Env=production"
```
  - filters depends aws-sdk-go#ec2.DescribeInstancesInput Fiters. see [aws document](https://docs.aws.amazon.com/sdk-for-go/api/service/ec2/#DescribeInstancesInput)
  - filters sample list
    - availability-zone
    - image-id
    - instance-id
    - instance-state-code
    - instance-state-name
    - instance-type
    - ip-address
    - private-ip-address
    - subnet-id
    - tag:key=value
    - tag-key
    - tag-value
    - vpc-id
    - and more...

- Use columns
```
$ ec2ls-cache -u --cachename test --columns "PrivateIpAddress,InstanceId,Tag:Name,TagAll"
```
  - columns depends aws-sdk-go#ec2.Instance field. see [aws document](https://docs.aws.amazon.com/sdk-for-go/api/service/ec2/#Instance)
  - now support string, int, float, bool, and tags
  - tags is `Tag:<tagKey>` or `TagAll`
  - columns sample list
    - ImageId
    - InstanceId
    - InstanceType
    - PrivateIpAddress
    - PublicDnsName
    - PublicIpAddress
    - SubnetId
    - VpcId
    - and more...

- Use sortcolumn
```
$ ec2ls-cache -u --columns "PrivateIpAddress,InstanceId,Tag:Name,TagAll" --sortcolumn "Tag:Name"
```
  - columns should contains sortcolumn.


FEATURE
---
- display Slices?
- cache expired limit option?
- no cache option?
- build for windows?

LICENSE
---
MIT

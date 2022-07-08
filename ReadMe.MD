# 视频点播转码-增加自定义S3源的支持
## 背景
AWS 官方提供了视频点播转码的解决方案: [AWS 上的视频点播基础解决方案实施概述](https://aws.amazon.com/cn/solutions/implementations/video-on-demand-on-aws/) 。 目前此解决方案的源S3桶与目标S3桶均在解决方案中封装，自动生成。无法自定义输入的桶。
## 解决方案目标
这里我们基于AWS官方Cloudformation定义，增加两个入参，解决S3源桶的自定义需求。
- SourceS3Bucket 源S3桶的名字 例如：videofile
- SourceS3BucketArn 源S3桶唯一资源标识 例如：arn:aws:s3:::videofile

## 实施步骤
1. 下载文件[cfTemplate](https://github.com/RichardLeeY/video/blob/main/cloudformation/video-on-demand-on-aws-foundation.template)
2. 在CloudFormation控制台创建新的cloudformation stack，选择从本地上传Cloudformation模版的方式创建。
3. 资源创建完成后，下载job定义文件[job-settings.json](https://github.com/RichardLeeY/video/blob/main/job-settings.json)。将此文件上传到源S3桶的需要转码的视频文件夹中。

## 测试
1. 上传视频文件例如1.mp4到源s3桶。
2. 上传完成后，到MediaConvert控制台查看转码job进展。
3. 转码完成后会收到通知邮件，打开邮件中的链接，即可看到视频播放效果。根据HLS协议，根据网络情况自动调整分辨率。

# [laf-cli命令行工具导出云存储报错](https://github.com/Smileye-v/gitblog/issues/28)

### 高并发请求
**报错如下**
`@smithy/node-http-handler:WARN - socket usage at capacity=50 and 638 additional requests are enqueued.
See https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/node-configuring-maxsockets.html
or increase socketAcquisitionWarningTimeout=(millis) in the NodeHttpHandler config.`

**解决方法**
修改action/storage/s3.js，引入 @smithy/node-http-handler 的 NodeHttpHandler，并在 S3Client 配置中设置 maxSockets 和可选的 socketAcquisitionWarningTimeout
`const { NodeHttpHandler } = require("@smithy/node-http-handler");`
`requestHandler: new NodeHttpHandler({`
`    maxSockets: 500, // 增加 socket 上限`
`    socketAcquisitionWarningTimeout: 50000, // 延迟警告（毫秒，可选）`
`}),`


### 拉去文件数只有1000
**原因**
`new client_s3_1.ListObjectsCommand`，ListObjectsCommand默认返回最多 1000 个对象
**解决方案**
增加分页
`const listCommand = new client_s3_1.ListObjectsCommand({`
`    Bucket: bucketName,`
`    Delimiter: '',`
`});`
`const res = await client.send(listCommand);`
`const bucketObjects = res.Contents || [];`
将上面代码改为
`let bucketObjects = [];`
`let continuationToken = undefined;    `
`do {`
`    const listCommand = new client_s3_1.ListObjectsV2Command({`
`        Bucket: bucketName,`
`        Delimiter: '',`
`        ContinuationToken: continuationToken,`
`        MaxKeys: 1000`
`    });`
`    const res = await client.send(listCommand);`
`    if (res.Contents && res.Contents.length > 0) {`
`        bucketObjects = bucketObjects.concat(res.Contents);`
`    }`
`    continuationToken = res.NextContinuationToken;`
`} while (continuationToken);`



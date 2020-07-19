# Deploy Vue.js to AWS S3

## 建立 vue project
1. vue init webpack **your project name**
2. cd ./**your project name**
3. npm run dev


## 安裝AWS CLI 並設定
[可參考 AWS macOS 安裝文件](https://docs.aws.amazon.com/zh_tw/cli/latest/userguide/install-cliv2-mac.html)

### 設定 AWS Assess Key
`aws confiture`


### 可以先確認 AWS Assess 設定
`aws confiture list`


### 查看目前所有儲存體
`aws s3 ls`



## 開始Deploy project 到 AWS S3

### 在vue專案執行
1. `npm run build`
2. `serve ./dist`
3. `aws s3 sync ./dist s3://**your bucket name**`


### 也可以修改package.json
```
"scripts": {
   "deploy": "aws s3 sync ./dist s3://**your bucket name**`
  },
```
1. `npm run build`
2. `npm run deploy` (直接deploy到s3)

### Access Denied and S3 Bucket Policies

在 bucket 的 permissions 加入 bucket policy

```{
   "Version": "2012-10-17",
     "Statement": [
        {
			"Sid": "PublicReadAccess",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
		}
	]
}```

# Lambda-@edge Image-resizer nodejs8.0

## 1. prerequisite

### Lambda
  region = us-east-1  
  language = nodejs 8.0

### IAM (create IAM Role)

##### Permissions 
  lambda:GetFunction   
  lambda:EnableReplication  
  iam:CreateServiceLinkedRole   
  cloudfront:UpdateDistribution  
  cloudfront:CreateDistribution  
  s3:GetObject  
  s3:PutObject  
  s3:PutObjectAcl  

##### Trust Relationship
  ```
  {  
     "Version": "2012-10-17",    
     "Statement": [
        {
           "Effect": "Allow",
           "Principal": {
              "Service": [
                 "lambda.amazonaws.com",
                 "edgelambda.amazonaws.com"
              ]    
           },    
           "Action": "sts:AssumeRole"    
        }    
     ]      
  }
  ```
  
### CloudFront

#####Origin Domain Name: S3 Bucket
#####Restrict Bucket Access: Yes
#####Origin Access Identity: Create a New Identity
#####Grant Read Permissions on Bucket: Yes, Update Bucket Policy
#####Query String Forwarding and Caching: Forward all, cache based on whitelist
#####Query String Whitelist: s,t,d.
#####Compress Objects Automatically: Yes


### 2. Installation

##### 1. git clone https://github.com/doohyeong-dev/image-resizer.git
##### 2. npm i
##### 3. zip node_modules && index.html to index.zip
##### 4. create lambda
          region = us-east-1
          language = nodejs 8.0
##### 5. upload zip
##### 6. create and publish lambda version 
##### 7. cloudFront - Behaviors - Lambda Function Associations - Event Type Origin Response + copy and pase lambda arn

### 3. Usage

##### cloudfrontURL/path?s=
##### s = (width)x(height)
##### t = crop / cover
##### q = (number) <- quality
##### f = webp (optional) 

## ref
### Jinho Hong
https://engineering.huiseoul.com/lambda-%ED%95%9C%EA%B0%9C%EB%A1%9C-%EB%A7%8C%EB%93%9C%EB%8A%94-on-demand-image-resizing-d48167cc1c31

### 당근마켓
https://medium.com/daangn/lambda-edge%EB%A1%9C-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-on-the-fly-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EB%A6%AC%EC%82%AC%EC%9D%B4%EC%A7%95-f4e5052d49f3

### AWS
https://aws.amazon.com/blogs/compute/resize-images-on-the-fly-with-amazon-s3-aws-lambda-and-amazon-api-gateway/

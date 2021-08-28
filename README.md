# eks-spring-service
Simple Spring Boot rest services on EKS

# Steps

1. Check basic java build

```
./mvnw install
java -jar target/*.jar
curl localhost:8080/name
```

2. Create ECR repo
aws ecr create-repository \
    --repository-name sample-repo \
    --image-tag-mutability IMMUTABLE \
    --image-scanning-configuration scanOnPush=true

3. Push image to ECR

Get token to your ECR
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 777258879183.dkr.ecr.us-east-1.amazonaws.com
```

Build image in your local
```
./mvnw spring-boot:build-image  
```

Tag it
```
docker tag eksdemo:0.0.1-SNAPSHOT 777258879183.dkr.ecr.us-east-1.amazonaws.com/sample-repo:latest
```

Push image
```
docker push 777258879183.dkr.ecr.us-east-1.amazonaws.com/sample-repo:latest
```

### Project URL
[https://github.com/alibabacloud-howto/solution-online-leaderboard-redis](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis)

### Architecture Overview
![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/archi.png)

### Deployment
#### Terraform
Use terraform to provision ECS and Redis instances that used in this solution against this .tf file:
[https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/blob/main/deployment/terraform/main.tf](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/blob/main/deployment/terraform/main.tf)


For more information about how to use Terraform, please refer to this tutorial: [https://www.youtube.com/watch?v=zDDFQ9C9XP8](https://www.youtube.com/watch?v=zDDFQ9C9XP8)

In the file: https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/blob/main/deployment/terraform/main.tf
If you do not specify the provider parameters in the environment, please set your Alibaba Cloud access key, secret key here.

```bash
provider "alicloud" {
  #   access_key = "${var.access_key}"
  #   secret_key = "${var.secret_key}"
  region = "ap-southeast-1"
}
```

### Run Demo
#### Step 1: Log on ECS & setup environment

- Get the EIP of the ECS, and then logon to ECS via SSH. Please use the account root/N1cetest, the password has been predefined in Terraform script for this tutorial. If you changed the password, please use the correct password accordingly.

![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/step1-1.png)

![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/step1-2.png)

```bash
ssh root@<EIP_ECS>
```

- Run the following command to install required utilities on the instance, including JDK and Maven: 

```bash
sudo apt-get update
sudo apt-get install openjdk-8-jdk
apt install maven
```

#### Step 2: Modify & run application

- Run the following command to download and untar the source code of the demo: 

```bash
wget https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/source.tar.gz
tar xvf source.tar.gz && cd source
```

- Vim to modify the Java code to replace the Redis access endpoint URL and password accordingly in the Step 1.

![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/step2-1.png)

```bash
vim src/main/java/test/GameRankSample.java
```

![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/step2-2.png)

- Build the source code and package, then run the demo:

```bash
mvn clean package assembly:single -DskipTests
java -classpath target/demo-0.0.1-SNAPSHOT.jar test.GameRankSample
```

Running result:

![image.png](https://github.com/alibabacloud-howto/solution-online-leaderboard-redis/raw/main/images/step2-3.png)

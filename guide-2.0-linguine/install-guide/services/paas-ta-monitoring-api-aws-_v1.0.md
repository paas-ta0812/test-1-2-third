# Table of Contents

1. [문서 개요](paas-ta-monitoring-api-aws-_v1.0.md#1)
   * [1.1. 목적](paas-ta-monitoring-api-aws-_v1.0.md#2)
   * [1.2. 범위](paas-ta-monitoring-api-aws-_v1.0.md#3)
   * [1.3. 전제조건](paas-ta-monitoring-api-aws-_v1.0.md#4)
2. [Monitoring API Release 배포](paas-ta-monitoring-api-aws-_v1.0.md#5)
   * [2.1.  upload release](paas-ta-monitoring-api-aws-_v1.0.md#6)
   * [2.2.  manifest 파일 설정](paas-ta-monitoring-api-aws-_v1.0.md#7)
   * [2.3.  deploy](paas-ta-monitoring-api-aws-_v1.0.md#8)
   * [2.4.  확인](paas-ta-monitoring-api-aws-_v1.0.md#9)

 \# 1. 문서 개요

## 1.1. 목적

본 문서는 PaaS-TA 사용자 포탈 서비스와 연동하여, Application이 배포되어 실행되는 Container 환경의 상태정보\(cpu, memory, disk\)를 제공함으로써, auto-scaling의 지표로 활용될 수 있도록 하는데 그 목적이 있다.

 \#\#\# 1.2. 범위 본 문서는 AWS 기반에 설치하기 위한 내용으로 한정되어 있다.

## 1.3. 전제조건

Monitoring API 서버를 설치하기 위해서는 사전에 PaaS-TA 서비스가 배포되어 서비스되고 있어야 한다.

 \# 2. Monitoring API Release 배포 본 장에서는 Monitoring API Release를 배포하는 방법에 대해서 기술하였다.

## 2.1.  upload "Monitoring API" release

하단 링크로 접속하여 PaaS-TA 모니터링 패키지 파일을 다운로드하여, 압축해제한다.

> PaaS-TA 모니터링 : [https://paas-ta.kr/data/packages/2.0/PaaSTA-Monitoring.zip](https://paas-ta.kr/data/packages/2.0/PaaSTA-Monitoring.zip)   
>  다운로드 받은 PaaSTA-Monitoring.zip 파일을 압축해제한다.   
>  paasta-monitoring-api-server-2.0.tgz 파일을 확인한다.

다음의 명령어를 이용하여 릴리즈 파일을 bosh에 업로드한다.

$ bosh upload release paasta-monitoring-api-server-2.0.tgz

![](../../../.gitbook/assets/2-1-1%20%2826%29.png) ![](https://github.com/jhuhm13579/trans-test/tree/c3fa60c3f2804eba4cf4bb19f90449a85a66a625/Guide-2.0-Linguine-/Install-Guide/Services/images/monitoring-api/2-1-2.png)

 \#\#\# 2.2. manifest 파일 설정 1. "Monitoring API" 배포되는 환경에 맞게 manifest 파일의 설정 정보를 수정한다. $ vi monitoring-api-release.yml \`\`\` compilation: cloud\_properties: availability\_zone: us-east-1d \#available zone instance\_type: m3.medium network: monitoring-api-server-net \#network name reuse\_compilation\_vms: true workers: 1 \#worker count director\_uuid:  \#bosh status --uuid jobs: - cloud\_properties: name: default instances: 1 \#instance count memory\_mb: 2048 name: api\_server\_z1 \#bosh vm name networks: - name: monitoring-api-server-net \#network name static\_ips: 10.244.30.20 \#static IP properties: {} resource\_pool: monitoring-api-server \#resource name \(resource\_pools\) templates: - name: api\_server release: paasta-monitoring-api-server update: max\_in\_flight: 1 serial: false name: paasta-monitoring-api-server \#deployment name networks: - name: monitoring-api-server-net \#network name subnets: - cloud\_properties: aws\_access\_key\_id: xxxxxxxxxxx \#AWS access key aws\_secret\_access\_key: xxxxxxxxxxx \#AWS secret region: us-east-1d \#AWS availability zone security\_groups: - cf-xxxxxxxx \#AWS security group name subnet: subnet-xxxxxx \#AWS subnet id dns: - xx.xx.xx.xx \#dns ip - 10.10.0.2 gateway: 10.10.5.1 \#gateway range: 10.10.5.0/24 \#static ip range reserved: - 10.10.5.2 - 10.10.5.110 \#reserved ip range static: - 10.10.5.111 - 10.10.5.120 \#available ip range type: manual properties: syslog\_daemon\_config: address: null port: null api\_server: listen\_addr: 0.0.0.0:9999 \#api server listen address log\_level: debug \#log level dopplerUrl: wss://doppler.bosh-lite.com:4443 \#doppler websocket url uaa: url: http://uaa.bosh-lite.com \#uaa url adminId: admin \#admin account id adminPass: admin \#admin account password releases: - name: paasta-monitoring-api-server \#release name version: latest \#release version resource\_pools: - cloud\_properties: name: default name: monitoring-api-server \#resource name network: monitoring-api-server-net \#network name size: 1 stemcell: name: bosh-aws-xen-hvm-ubuntu-trusty-go\_agent \#stemcell name version: latest \#stemcell version update: canaries: 1 canary\_watch\_time: 30000-100000 max\_errors: 1 max\_in\_flight: 1 update\_watch\_time: 30000-100000 \`\`\` 2. manifest 파일 지정 $ bosh deployment monitoring-api-release.yml !\[2-2-1\]

## 2.3.  배포

$ bosh -n deploy

![](../../../.gitbook/assets/2-3-1%20%2829%29.png) ![](../../../.gitbook/assets/2-3-2%20%2817%29.png)

## 2.4.  확인

$ bosh deployments

![](../../../.gitbook/assets/2-4-1%20%2819%29.png)


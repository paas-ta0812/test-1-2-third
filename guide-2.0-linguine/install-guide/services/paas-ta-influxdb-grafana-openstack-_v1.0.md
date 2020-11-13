# Table of Contents

1. [문서 개요](paas-ta-influxdb-grafana-openstack-_v1.0.md#1)
   * [1.1. 목적](paas-ta-influxdb-grafana-openstack-_v1.0.md#2)
   * [1.2. 범위](paas-ta-influxdb-grafana-openstack-_v1.0.md#3)
   * [1.3. 참고](paas-ta-influxdb-grafana-openstack-_v1.0.md#4)
2. [InfluxDB & Grafana Release 배포](paas-ta-influxdb-grafana-openstack-_v1.0.md#5)
   * [2.1.  upload release](paas-ta-influxdb-grafana-openstack-_v1.0.md#6)
   * [2.2.  manifest 파일 설정](paas-ta-influxdb-grafana-openstack-_v1.0.md#7)
   * [2.3.  deploy](paas-ta-influxdb-grafana-openstack-_v1.0.md#8)
   * [2.4.  확인](paas-ta-influxdb-grafana-openstack-_v1.0.md#9)

 \# 1. 문서 개요

## 1.1. 목적

본 문서는 IaaS\(Infrastructure as a Service\) 중 하나인 Openstack 환경에서 모니터링 시스템의 주요 정보인 시스템 metrics 를 저장히기 위한 InfluxDB와 View 화면을 제공하는 Grafana를 설치하기 위한 가이드를 제공하는데 그 목적이 있다.

 \#\#\# 1.2. 범위 본 문서는 Openstack 기반에 설치하기 위한 내용으로 한정되어 있다.

## 1.3. 참고

> [모니터링 시스템 Architecutre](https://github.com/OpenPaaSRnD/Documents-PaaSTA-2.0/blob/master/Use-Guide/PaaS-TA%20%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81%20%EC%8B%9C%EC%8A%A4%ED%85%9C%20Architecture.md)

 \# 2. InfluxDB & Grafana Release 배포 본 장에서는 InfluxDB와 Grafana 서비스를 배포하는 방법에 대해서 기술하였다.

## 2.1.  upload "InfluxDB & Grafana" release

하단 링크로 접속하여 PaaS-TA 모니터링 패키지 파일을 다운로드하여, 압축해제한다.

> PaaS-TA 모니터링 : [https://paas-ta.kr/data/packages/2.0/PaaSTA-Monitoring.zip](https://paas-ta.kr/data/packages/2.0/PaaSTA-Monitoring.zip)
>
> 다운로드 받은 PaaSTA-Monitoring.zip 파일을 압축해제한다.   
>  paasta-influxdb-grafana-2.0.tgz 파일을 확인한다.   
>  다음의 명령어를 이용하여 릴리즈 파일을 bosh에 업로드한다.

$ bosh upload release paasta-influxdb-grafana-2.0.tgz

![](../../../.gitbook/assets/2-1-1%20%2822%29.png) ![](../../../.gitbook/assets/2-1-2%20%2813%29.png)

 \#\#\# 2.2. manifest 파일 설정 &gt; [InfluxDB 참조](https://github.com/OpenPaaSRnD/Documents-PaaSTA-2.0/blob/master/Use-Guide/PaaS-TA%20%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81%20DB%20%EB%B0%8F%20Metrics%20%EA%B0%80%EC%9D%B4%EB%93%9C.md) 1. "InfluxDB & Grafana" 서비스가 배포되는 환경에 맞게 manifest 파일의 설정 정보를 수정한다. $ vi influxdb-grafana-release.yml \`\`\` --- name: paasta-influxdb-grafana \#deployment name compilation: cloud\_properties: name: random instance\_type: monitoring \#openstack flavor availability\_zone: nova \#available zone network: paasta-influxdb-grafana-net \#network name reuse\_compilation\_vms: true workers: 2 director\_uuid:  \#bosh uuid releases: - name: paasta-influxdb-grafana \#release name version: latest \#release version disk\_pools: - cloud\_properties: type: gp2 disk\_size: 10240 \#influxdb disk pool size name: influx\_data jobs: - name: influxdb \#influxdb service name templates: - name: influxdb release: paasta-influxdb-grafana instances: 1 resource\_pool: influx \#resource name persistent\_disk\_pool: influx\_data \#disk pool name networks: - default: - gateway - dns name: paasta-influxdb-grafana-net \#network name static\_ips: - 10.10.18.51 \#static IP - name: elastic \#external network\(public\) name static\_ips: - "xxx.xxx.xxx.xxx" \#external IP \(public\) properties: influxdb: database: cf\_metric\_db \#default database user: root \#admin account password: root \#admin password replication: 1 ips: 10.10.18.51 \#local IP - name: grafana \#grafana service name templates: - name: grafana release: paasta-influxdb-grafana instances: 1 resource\_pool: grafana \#resoure name networks: - default: - gateway - dns name: paasta-influxdb-grafana-net static\_ips: - 10.10.18.53 \#local IP - name: elastic \#external network\(public\) name static\_ips: - "xxx.xxx.xxx.xxx" \#public ip properties: grafana: listen\_port: 3000 \#grafana listen port admin\_username: admin \#grafana admin account admin\_password: admin \#grafana admin password users: allow\_sign\_up: true auto\_assign\_organization: true datasource: url: http://10.10.18.51:8086/ \#database url name: Grafanadb database\_type: Influxdb \#database type user: root \#database admin account password: root \#database admin password database\_name: cf\_metric\_db \#default database networks: - name: paasta-influxdb-grafana-net subnets: - cloud\_properties: name: random net\_id: b7c8c08f-2d3b-4a86-bd10-641cb6faa317 \#openstack network id security\_groups: \[bosh\] \#security group dns: - 10.10.18.2 \#dns gateway: 10.10.18.1 \#gateway range: 10.10.18.0/24 \#static ip range reserved: - 10.10.18.2 - 10.10.18.49 \#reserved ip range static: - 10.10.18.50 - 10.10.18.55 \#available ip range type: manual - name: elastic type: vip cloud\_properties: net\_id: bb29696d-c0af-4a98-9108-edd23b27c493 security\_groups: \[bosh\] properties: openstack: &openstack auth\_url: http://"xxx.xxx.xxx.xxx":5000/v3 \#openstack auth url username: admin \#openstack admin id api\_key: admin \#openstack admin password project: admin \#related project name domain: default \#default domain region: RegionOne default\_key\_name: monitoring \#keypair name default\_security\_groups: \[bosh\] \#security group resource\_pools: - cloud\_properties: name: random instance\_type: m1.xlarge \#openstack flavor availability\_zone: nova \#available zone name: influx \#resource name network: paasta-influxdb-grafana-net \#network name stemcell: name: bosh-aws-xen-hvm-ubuntu-trusty-go\_agent \#stemcell name version: latest \#stemcell version - cloud\_properties: name: random instance\_type: m1.xlarge \#openstack flavor availability\_zone: nova \#available zone name: grafana \#resource name network: paasta-influxdb-grafana-net \#network name stemcell: name: bosh-aws-xen-hvm-ubuntu-trusty-go\_agent \#stemcell name version: 3232.17 \#stemcell version update: canaries: 1 canary\_watch\_time: 1000-180000 max\_in\_flight: 1 serial: true update\_watch\_time: 1000-180000 \`\`\` 2. manifest 파일 지정 $ bosh deployment influxdb-grafana-release.yml !\[2-2-1\]

## 2.3.  배포

$ bosh -n deploy

![](../../../.gitbook/assets/2-3-1%20%2825%29.png) ![](../../../.gitbook/assets/2-3-2%20%2811%29.png)

## 2.4.  확인

$ bosh deployments

![](../../../.gitbook/assets/2-4-1%20%2814%29.png)


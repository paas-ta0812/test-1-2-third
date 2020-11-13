# Table of Contents

1. [문서 개요](paas-ta-db-metrics.md#1)
   * [1.1. 목적](paas-ta-db-metrics.md#2)
2. [InfluxDB 데이터베이스](paas-ta-db-metrics.md#3)
   * [2.1.  용어](paas-ta-db-metrics.md#4)
   * [2.2.  데이터베이스 구조](paas-ta-db-metrics.md#5)
   * [2.3.  Measurement 구조](paas-ta-db-metrics.md#6)
3. [Metrics 설명](paas-ta-db-metrics.md#7)
   * [3.1.  Dashboard 생성](paas-ta-db-metrics.md#8)
   * [3.2.  Chart 생성](paas-ta-db-metrics.md#9)
   * [3.3.  Table 생성](paas-ta-db-metrics.md#10)
4. [PaaS-TA 모니터링 메인 화면](paas-ta-db-metrics.md#11)

 \# 1. 문서 개요

## 1.1. 목적

본 문서는 PaaS-TA 모니터링 시스템에서 사용되는 TSDB\(Time Series DataBase\)인 InfluxDB의 구조와 수집되는 Metrics 리스트를 설명하는데 그 목적이 있다.

 \# 2. InfluxDB 데이터베이스 본 장에서는 PaaS-TA 모니터링 시스템에서 사용하고 있는 TSDB인 InfluxDB의 데이터베이스 구조에 대해 기술하였다.

## 2.1. 용어

Measurement : Relational Database의 Table과 같은 개념

Tag : 조회시 데이터를 필터링하기 위한 조건 정보

Field : 사용자에게 보여주기 위한 데이터 정보

 \#\#\# 2.2. 데이터베이스 구조 !\[2-2-1\]

## 2.3. Measurement 구조

![](../../.gitbook/assets/2-3-1%20%2832%29.png)

 \# 3. Metrics 설명 본 장에서는 PaaS-TA 모니터링 시스템에서 수집하고 있는 Metrics 리스트에 대해 기술하였다.

## 3.1. Server, Bosh, PaaS-TA, Service Metrics 정보

![](../../.gitbook/assets/3-1-1%20%284%29.png)

## 3.2. Container Metrics 정보

![](../../.gitbook/assets/3-2-1%20%287%29.png)


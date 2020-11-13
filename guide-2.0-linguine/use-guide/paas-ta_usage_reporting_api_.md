# PaaS-TA\_Usage\_Reporting\_API\_가이드

### Table of Contents

1. [문서개요](paas-ta_usage_reporting_api_.md#1)
   * [목적](paas-ta_usage_reporting_api_.md#2)
   * [범위](paas-ta_usage_reporting_api_.md#3)
2. [GET org\_app\_usage\_summary](paas-ta_usage_reporting_api_.md#4)
   * [Request Parameters](paas-ta_usage_reporting_api_.md#5)
   * [cURL](paas-ta_usage_reporting_api_.md#6)
   * [Response body](paas-ta_usage_reporting_api_.md#7)
3. [GET monthly\_org\_usage](paas-ta_usage_reporting_api_.md#8)
   * [Request Parameters](paas-ta_usage_reporting_api_.md#9)
   * [cURL](paas-ta_usage_reporting_api_.md#10)
   * [Response body](paas-ta_usage_reporting_api_.md#11)
4. [GET app\_monthly\_usage](paas-ta_usage_reporting_api_.md#12)
   * [Request Parameters](paas-ta_usage_reporting_api_.md#13)
   * [cURL](paas-ta_usage_reporting_api_.md#14)
   * [Response body](paas-ta_usage_reporting_api_.md#15)

## 1.  문서 개요

### 1.1.  목적

본 문서는 PaaS-TA Usage Reporting의 API 호출에 대해 기술하였다.

### 1.2.  범위

본 문서에서는 PaaS-TA Usage Reporting의 API의 인터페이스 정보 및 호출 방법에 대해 작성되었다.

## 2. GET org\_app\_usage\_summary

해당 조회 월 1일부터 현재 시간까지의 org / space 에서 동작 중인 각 app의 메모리 사용량을 조회한다. space\_id parameter 가 ‘all’ 인 경우, org 전체의 값을 리턴한다.

### 2.1.  Request Parameters

| 이름 | 설명 | 기본값 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- | :--- |
| org\_id | 조직 아이디 | - | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d’ |
| space\_id | 스페이스 아이디 | - | space\_guid, ‘all’ | ‘b5e7f478-6f26-457f-97ce-c57a31afe157’ |

### 2.2.  cURL

```text
curl -i -X GET http://paasta-usage-reporting.your-domain.com/v1/org/:org_id/space/:space_id
```

### 2.3.  Response body

| 프로퍼티 이름 | 설명 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- |
| org\_id | 조직 guid | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d’ |
| from | 집계 시작 timestamp | timestamp | 1470009600000 |
| end | 집계 종료 timestamp | timestamp | 1472192759652 |
| sum | 합계 | number \(소수1자리\) | 6.5 |
| app\_usage\_array | 사용량 배열 객체 | array | N/A |
| space\_id | 스페이스 guid | space\_guid | ‘7b85dc3f-85f0-40bc-8532-0dabd0bc7bae’ |
| app\_id | app guid \(CF이벤트\) | app guid | ‘4566f4e8-ec03-4aae-a006-3d6b12ce7a9c’ |
| app\_name | CF push 시 정의된 앱 명칭 | String | ‘java\_demo’ |
| app\_state | 앱의 현재 상태 | ‘STARTED’,’STOPED’,’PENDDING’ | ‘STARTED’ |
| app\_instance | 할당된 인스턴스\(CF이벤트  기준\) | number \(정수값\) | 1 |
| app\_memory | 할당된 메모리\(CF이벤트  기준\) 단위 M | 512, 1024 | 512 |
| app\_usage | 현재까지의 집계 사용량 | number \(소수1자리\) | 8.5 |

```text
{
    "org_id": "e655c52a-6ee5-4cf1-89d4-eac31fb6b36f",
    "from": 1470009600000,
    "to": 1472192759652,
    "sum": 6,
    "appUsage":[
            {
                "space_id": "b5e7f478-6f26-457f-97ce-c57a31afe157",
                "app_id": "657c7e08-34eb-4d69-88a4-61262ce07685",
                "app_name": "spring-crt",
                "app_state": "STARTED",
                "app_instance": 1,
                "app_memory": 512,
                "app_usage": 0.5
            },
            {
                "space_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
                "app_id": "204f83ba-7b3a-4627-9b51-168237fd1695",
                "app_name": "node_demo",
                "app_state": "STARTED",
                "app_instance": 1,
                "app_memory": 512,
                "app_usage": 1
            }
    ]
}
```

## 3.  GET monthly\_org\_usage

org /space 내 동작 중인 각 app의 집계 기간내 월별 메모리 사용량을 조회한다.

space\_id parameter 가 ‘all’ 인 경우, org 전체의 값을 리턴한다.

### 3.1.  Request Parameters

| 이름 | 설명 | 기본값 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- | :--- |
| org\_id | 조직 아이디 | - | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d’ |
| space\_id | 스페이스 아이디 | - | space\_guid,‘all’ | ‘b5e7f478-6f26-457f-97ce-c57a31afe157’ |
| from\_month | 집계 시작 년월 yyyymm | - | yyyymm 형식 String | ‘201601’ |
| to\_month | 집계 종료 년월 yyyymm | - | yyyymm 형식 String | ‘201603’ |

### 3.2.  cURL

```text
curl -i -X GET http://pasta-usage-reporting.your-domain.com/v1/org/:org_id/space/:space_id/from/:from_month/to/:to_month
```

### 3.3.  Response body

| 프로퍼티 이름 | 설명 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- |
| org\_id | 조직 guid | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d’ |
| from\_month | 집계 시작 년월 yyyymm | yyyymm 형식String | ‘201601’ |
| to\_month | 집계 종료 년월yyyymm | yyyymm 형식String | ‘201603’ |
| sum | 집계 기간 사용량 합계 | number | 6.5 |
| monthly\_usage\_arr | 월별 사용량 배열 객체 | array | N/A |
| month | 집계 월 | String | ‘201603’ |
| sum | 월 사용량 합계 | number | 6.5 |
| spaces | 스페이스 배열 객체 | - | N/A |
| space\_id | 스페이스 guid | space\_guid | ‘7b85dc3f-85f0-40bc-8532-0dabd0bc7bae’ |
| sum | 스페이스 사용량 합계 | - | - |
| app\_usage\_arr | 앱 사용량 배열 객체 | - | - |
| app\_id | 앱 guid | app guid | ‘4566f4e8-ec03-4aae-a006-3d6b12ce7a9c’ |
| app\_name | 앱 명칭 | string | ‘java\_demo’ |
| app\_instance | 인스턴스\(CF이벤트  기준\) | number | 1 |
| app\_memory | 메모리\(CF이벤트  기준\) | 512,1024 | 512 |
| app\_usage | 현재까지의 집계 사용량 | number | 8.5 |
| total\_app\_usage\_arr | 집계 기간내 앱별 총사용량 배열 객체 | - | - |
| app\_id | 앱 guid | app guid | ‘4566f4e8-ec03-4aae-a006-3d6b12ce7a9c’ |
| app\_name | 앱 명칭 | string | ‘java\_demo’ |
| app\_usage | 집계 기간내 앱별 총사용량 | number | 3345 |

```text
{
    "org_id": "e655c52a-6ee5-4cf1-89d4-eac31fb6b36f",
    "from_month": "201601",
    "to_month": "201602",
    "sum": 8,
    "monthly_usage_arr": [{
        "month": "201601",
        "sum": 5,
        "spaces": [
            {
                "space_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
                "sum": 2,
                "app_usage": [
                    {
                        "app_id": "204f83ba-7b3a-4627-9b51-168237fd1695",
                        "app_name": "node_demo",
                        "app_instance": 1,
                        "app_memory": 512,
                        "app_usage": 1
                    },
                    {
                        "app_id": "4566f4e8-ec03-4aae-a006-3d6b12ce7a9c",
                        "app_name": "java_demo",
                        "app_instance": 1,
                        "app_memory": 512,
                        "app_usage": 1
                    }
                ]
            },
            {
                "space_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
                "sum": 3,
                "app_usage": [
                    {
                        "app_id": "204f83ba-7b3a-4627-9b51-168237fd1695",
                        "app_name": "node_demo",
                        "app_instance": 1,
                        "app_memory": 512,
                        "app_usage": 1
                    },
                    {
                        "app_id": "4566f4e8-ec03-4aae-a006-3d6b12ce7a9c",
                        "app_name": "java_demo",
                        "app_instance": 1,
                        "app_memory": 512,
                        "app_usage": 2
                    }
                ]
            }
        ]
    },
    {
        "month": "201602",
        "sum": 3,
        "spaces": [
            {
                "space_id": "b5e7f478-6f26-457f-97ce-c57a31afe157",
                "sum": 0.5,
                "app_usage": [
                    {
"app_id": "657c7e08-34eb-4d69-88a4-61262ce07685",
                        "app_name": "spring-crt",
                        "app_instance": 1,
                        "app_memory": 512,
                        "app_usage": 0.5
                    }
                ]
            },
            {
                "space_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
                "sum": 2.5,
                "app_usage_arr": [
                    {
"app_id": "657c7e08-34eb-4d69-88a4-61262ce07685",
                        "app_name": "spring-crt",
                        "app_instance": 3,
                        "app_memory": 512,
                        "app_usage": 2.5
                    }
                ]
            }
        ]
    }
    ] ,
    "total_app_usage_arr": [
        {
            "app_id": "657c7e08-34eb-4d69-88a4-61262ce0768",
            "app_name": "spring-demo",
            "app_usage": 223
        },
        {
            "app_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
            "app_name": "spring-crt",
            "app_usage": 234
        },
        {
            "app_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
            "app_name": "node_demo",
            "app_usage": 123
        },
        {
            "app_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
            "app_name": "java_demo",
            "app_usage": 423
        }
    ]
}
```

## 4. GET app\_monthly\_usage

해당 app의 집계기간 내의 월별 메모리 사용량을 조회한다.

### 4.1.  Request Parameters

| 이름 | 설명 | 기본값 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- | :--- |
| org\_id | 조직 아이디 | - | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d’ |
| space\_id | 스페이스 아이디 | - | space\_guid | ‘b5e7f478-6f26-457f-97ce-c57a31afe157’ |
| app\_id | 앱 아이디 | - | app\_guid | ‘204f83ba-7b3a-4627-9b51-168237fd1695’ |
| from\_month | 집계 시작 년월 yyyymm | - | yyyymm 형식 String | ‘201601’ |
| to\_month | 집계 종료 년월 yyyymm | - | yyyymm 형식 String | ‘201603’ |

### 4.2.  cURL

```text
curl -i -X GET http://pasta-usage-reporting.your-domain.com/v1/ org/:org_id/space/:space_id/app/:app_id/from/:from_month/to/:to_month
```

### 4.3.  Response body

| 프로퍼티 이름 | 설명 | 유효값 | 예시값 |
| :--- | :--- | :--- | :--- |
| org\_id | 조직 아이디 | org\_guid | ‘7726b51e-b7b4-4b9f-a1cf-78eab2710e2d' |
| space\_id | 스페이스 아이디 | space\_guid | ‘7b85dc3f-85f0-40bc-8532-0dabd0bc7bae’ |
| app\_id | 앱 guid \(CF이벤트\) | app\_guid | ‘4566f4e8-ec03-4aae-a006-3d6b12ce7a9c’ |
| app\_name | 앱 명칭 | string | ‘java\_demo’ |
| from\_month | 집계 시작 년월 yyyymm | yyyymm 형식 String | ‘201601’ |
| to\_month | 집계 종료 년월 yyyymm | yyyymm 형식 String | ‘201603’ |
| sum | 전체 사용량 합계 | number | 5.5 |
| monthly\_usage\_arr | 월별 사용량 배열 객체 | array | N/A |
| month | 집계 월 yyyymm | yyyymm 형식 String | ‘201601’ |
| app\_instance | 할당된 인스턴스\(CF이벤트 기준\) | number | 1 |
| app\_memory | 할당된 메모리\(CF이벤트 기준\) | number | 512 |
| app\_usage | 현재까지의 집계 사용량 | number | 8.5 |

```text
{
    "org_id": "e655c52a-6ee5-4cf1-89d4-eac31fb6b36f",
    "space_id": "7b85dc3f-85f0-40bc-8532-0dabd0bc7bae",
    "app_id": "e655c52a-6ee5-4cf1-89d4-eac31fb6b36f",
    "app_name": "node_demo",
    "from_month" : "201601",
    "to_month" : "201608",
    "sum": 5,
    "monthly_usage_arr":[
        {
            "month" : "201601",
            "app_instance": 1,
            "app_memory": 512,
            "appUsage": 5
        },
        {
            "month" : "201602",
            "app_instance": 1,
            "app_memory": 512,
            "appUsage": 8.5
        }
    ]
}
```


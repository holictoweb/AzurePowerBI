hjchung@holictoweboutlook249.onmicrosoft.com

uchung@holictoweboutlook249.onmicrosoft.com

jslee@holictoweboutlook249.onmicrosoft.com

dhkim@holictoweboutlook249.onmicrosoft.com

hichoi@holictoweboutlook249.onmicrosoft.com

>  bi 초대 완료

syhwang@holictoweboutlook249.onmicrosoft.com

joonserk.park@holictoweboutlook249.onmicrosoft.com

hs.han@holictoweboutlook249.onmicrosoft.com





Azure SQL Server 

- hosqlserver.database.windows.net

- database

  - adventureworks
  - adventureworksdw

- ID/PW

  - admin_orange
  - !1Zenithncom

  



# 1. 기본 개념 설명 ( 10min )

- MOLAP vs ROLAP
  - ROLAP의 유형으로 Analysis service 에서는 Tabular 모델을 사용
- ETL 및 ELT 작업
  - 실제 Transform 단계가  source와 target 어디에서 수행 되는지 차이
- power bi desktop과 power bi service 간단 비교
  - Dataset 생성은 desktop 에서 진행 ( Dataflow 정의를 하더라도 결국 desktop에서 dataset을 만들어서 적용 )
  - RLS 적용 등 desktop에서 실제 개발을 한 후 배포 한다는 개념
  - visualization의 경우는 service에서도 진행 가능



# 2. Modeling & Azure Analysis Service ( 20 min )

- OLAP 데이터를 사용하게 되면 미리 계산되고(pre-calculated) 미리 결합된(pre-aggreagated) 데이터를 사용함으로써 빠른 분석을 할 수 있다.



• 롤업(roll-up)
    \- 작은 단위에서 큰 단위로 이동하는 연산(차원 낮추기)
  • 드릴다운(drill-down)
    \- 큰 단위에서 작은 단위로 세분화, 롤업 프로세스의 반대(차원 높이기)
  • 슬라이스(slice, slicing)
    \- 큐브의 한 조각을 연산, 큐브의 한 단면 보기(1개 차원 선택)
  • 다이스(dice, dicing)
    \- 슬라이스와 비슷, 하위 큐브 만들기 위해 2개 이상 차원 선택
  • 피벗(pivot)
    \- 데이터 축을 회전하여 제공



![](E:\toone\holic_toone\doc\image\olapcube_2.png)

![](E:\toone\holic_toone\doc\image\olapcube_4.png)

![](E:\toone\holic_toone\doc\image\olapcube.png)



- dimDate table 생성

```python
DimDate = 

VAR BaseClandar = CALENDARAUTO(12) 
RETURN 
    GENERATE(
BaseClandar,
var BaseDate = [Date]
var YearDate = YEAR(BaseDate)
var MonthNumber = MONTH( BaseDate)
return  Row ( 
    "Day" , BaseDate,
    "Year", YearDate,
    "Month Number", MonthNumber,
    "Month", FORMAT( BaseDate, "mmmm"),
    "Year Month", FORMAT( BaseDate, "mmm yy" ) 
    )
)
```



```python
dimDate = 
VAR MinYear = 2011
VAR MaxYear = 2020
RETURN
ADDCOLUMNS (
    FILTER (
        CALENDARAUTO( ),
        AND ( YEAR ( [Date] ) >= MinYear, YEAR ( [Date] ) <= MaxYear )
    ),
    "Calendar Year", "CY " & YEAR ( [Date] ),
    "Month Name", FORMAT ( [Date], "mmmm" ),
    "Month Number", MONTH ( [Date] )
)
```







# 3. Power BI Desktop 기본 사용 ( 40min )

- ETL + Modeling + visualization 을 모두 적용 할 수 있는 개발 도구 

  - source 연결 방식에 따라 ETL 과 modeling은 다른 서비스로 분리 

  

- Data source 연결

  - load 방식

    -  pro 라이센스로 power bi service 배포 시 일 8회의 refresh 가능

    - load 방식은 실제 데이터를 모두 가져 와서 pbix 파일에 포함 하여 model을 만드는 방식
    - direct query 는 schema 정보만 가지고 작업을 진행 한 후 실제 report 에서 데이터를 호출 할때 대상 data source에서 데이터를 가져 오는 방식
    - power bi service 배포 시  model ( .pbix ) 의 개별 사이즈가 1GB를 넘길 수 없음. ( Premium은 10GB )

  - Direct query 모드
    - 실시간 변경 데이터에 대한 확인 가능
    - direct query 방식에서는 Transform 쿼리를 수행 할 수 없음.  DB 쪽에서 실제 작업을 수행 완료 한 후 ( schema 변경 ) direct query 로 연결 해야 함. 

    - irectQuery에서 100만 개 이상의 행이 반환되는 경우 Power BI가 오류를 반환합니다

- Transform 

  - 칼럼 삭제, 칼럼 생성, 조인 등의 작업을 진행 할 수 있음
  - power query 를 사용
  - 추후 model 에서도 동일한 작업을 수행 할 수 있음. 

- Modeling

  - Date dim table 생성
  - mesure 생성
  - DAX 쿼리 

- Visualization

  - slicer 생성
  - paget filtrer 생성
  - 기본 chart 
  - 기본 matrix 

  

- [Power BI를 사용하는 행 수준 보안(RLS)](https://docs.microsoft.com/ko-kr/power-bi/admin/service-admin-rls)

  - role 정의 및 테스트 가능
  - 실제 적용은 power bi service로 배포 하여 진행



>1. Azure SQL Server에 연결 
>2. AdventureWorks2017 연결
>
>3. OLTP 데이터를 통한 visualization
>4. AdventureWorksDW2017 연결
>5. OLAT 데이터를 통한 visualization





# 4. ETL Azure data factory  (40min)

> 1. Azure SQL Database 생성 
> 2. Data Factory 생성
> 3. AdventureWorks2017 -> 개별 SQL Database ETL 수행





![파이프 라인, 활동, 데이터 세트, 링크 된 서비스 간의 관계](https://docs.microsoft.com/en-us/azure/data-factory/media/concepts-datasets-linked-services/relationship-between-data-factory-entities.png)

- [Azure Data Factory의 통합 런타임](https://docs.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime)



- Pipeline
  - link  설정 방법
    - source SQL Database to Sink SQL Database
  - dataset 설정 방법
    - 대상 Dataset에 대한 명시적인 지정 및 파라미터 사용 
    - Dataset은 재활용이 가능
  - pipeline 생성 
  - trigger 생성
  - parameter 전달 방법 
    - [System variables supported by Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/control-flow-system-variables)

- Data Flow
  - Transform 작업을 수행 



> [Azure Data Factory를 사용하여 여러 테이블을 대량으로 복사](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-bulk-copy-portal)
>
> [Azure Portal을 사용하여 Azure SQL 데이터베이스에서 Azure Blob 저장소로 데이터를 증분로드](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-portal)
>
> [SQL Server의 여러 테이블에서 Azure SQL 데이터베이스로 데이터를 증분로드](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-multiple-tables-portal)





- source table

```sql
SELECT TABLE_SCHEMA, TABLE_NAME FROM information_schema.TABLES 
WHERE TABLE_TYPE = 'BASE TABLE'  
and TABLE_NAME in ('Product', 'ProductCategory' , 'ProductSubcategory' , 'ProductVendor', 'PurchaseOrderDetail', 'PurchaseOrderHeader',  'ShipMethod', 'Vendor')
```



- read table 

```sql
select * from @{item().TABLE_SCHEMA}.@{item().TABLE_NAME}
```

```sql
truncate table @{item().TABLE_SCHEMA}.@{item().TABLE_NAME}
```







# 5. Azure Analysis Service

> 여러 모델들 과 데이터 연결에 대한 부분을 한곳에서 관리 가능
>
> DataWarehouse의 기능을 하게 됨

- Tabular modeling 프로젝트 생성
- Data load
  - Load
  - Direct Query
- modeling
- publish





# 6. Visualization ( 30 min )



- Fact table과 Dim table을 사용하여 slicing 

- 모델링한 결과물을 통해 각 dim table들을 혼합하여 slicing 및 dicing이 가능해짐.

- 기본적인 DAX

  - measure
  
  ```shell
    Sales YoY Growth % =
    VAR SalesPriorYear =
        CALCULATE([Sales], PARALLELPERIOD('Date'[Date], -12, MONTH))
    RETURN
        --DIVIDE(([Sales] - SalesPriorYear), SalesPriorYear)
        SalesPriorYear
    ```
  
    
  
  - computed column



- hierachy
  - 다른 테이블의 칼럼은 hirachy 생성은 불가능 ( 각각의 칼럼을 차트에 추가해서 구성은 가능 )

```sql
-- DimProduct
select c.*, A.ProductSubcategoryID, A.name as 'Subcategoryname', B.ProductCategoryID, B.name as 'categoryname'
--select * 
from [Production].[ProductSubcategory] A
join [Production].[ProductCategory] B
	on A.ProductCategoryID = B.ProductCategoryID
join [Production].[Product] C
	on c.ProductSubcategoryID = A.ProductSubcategoryID
```











# 6. Power BI Service ( 20 min )

- 작업 영역 생성
- 레포트 배포 
- Dataset SSO 자격 증명 설정
  - dataset 설정에서 자격증명 편집 에서 SSO를 설정 후 업데이트 까지 조금 시간이 걸림 
  - SQL   Server의 AD 관리자 계정 설정이 필요합니다.  

- 온프레미스 게이트웨이
  - [온-프레미스 데이터 게이트웨이 설치](docs.microsoft.com/en-us/data-integration/gateway/service-gateway-install)





[hjchung@eukor.com](mailto:hjchung@eukor.com)

[uchung@eukor.com](mailto:uchung@eukor.com)
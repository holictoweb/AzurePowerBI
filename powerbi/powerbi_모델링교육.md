



# 0. Agenda

제목:  Power BI 데이터 분석 기초

일정: 6월 25일 (목), 14:00-14:50 

설명:  power bi 활용을 위한 기초적인 활용 방법 

아젠다: 

- Power BI achitecture의 이해
  - power bi desktop vs power bi service 
  - power bi desktop는 BI 개발 도구로서의 이해
- OLAP 모델링
  - Tabular Modeling의 이해 (ROLAP)
  - Fact 테이블과 Dimension 테이블 구성
- Visualization
  - Chart 를 통한 데이터 분석
  - Dimension Table을 통한 data slicing 방법

강사: 제니스앤컴퍼니 이준익 차장











# 1. Power BI architecutre

![](E:\toone\holic_toone\doc\Visualization\webinar\power-bi-diagram2.png)



![](E:\toone\holic_toone\doc\Visualization\webinar\Power-BI-architecture-v4.png)





### 1.1 Power BI Desktop 



### 1.2 power bi desktop - ETL



- Storage Mode
  - **DirectQuery** . 라이브 연결과 유사하지만 여기서 모델을 더 변경할 수 있습니다. Live와 마찬가지로 데이터는 서버에 유지되고 쿼리는 서버에서 실행됩니다. 그러나 예를 들어 PBI Desktop 모델에서 관계를 만들 수 있습니다.
  - **Import** . 여기에서 [Power Query query를](https://www.mssqltips.com/sqlservertip/5998/getting-started-with-power-bi-and-power-query-for-simple-etl--part-2/) 사용하여 PBI Desktop 파일 (.pbix)로 데이터를 가져옵니다 . 데이터는 **압축률**이 높기 때문에 컴퓨터의 파일에 수백만 개의 레코드를로드 할 수 있습니다. 무대 뒤에서 SSAS 테이블 형식 모델과 매우 유사한 모델이 생성됩니다. 이 모드는 가능한 모든 소스의 데이터를 결합 할 수 있으므로 가장 유연합니다. 그러나 모든 데이터를 모델로 가져와야 새로 고침 시간이 길어질 수 있습니다.

  -  **라이브** . 여기서 모든 데이터를 보유하는 서버에 연결합니다. 데이터는 전송되지 않지만 모델의 메타 데이터는 PBI Desktop으로 가져옵니다. 시각화를 만들면 쿼리가 실행될 서버로 쿼리가 전송됩니다. 결과는 바탕 화면으로 돌아와 시각화됩니다. 라이브 연결은 일반적으로 테이블 형식 또는 다차원 모델 인 SSAS ( [SQL Server Analysis Services](https://www.mssqltips.com/sqlservertutorial/4200/sql-server-analysis-services-2016-ssas-tutorial/) ) 모델 과 함께 사용됩니다 . 이 경우 PBI Desktop은 Excel 또는 Reporting Services (SSRS)와 같은 다른 씬 클라이언트처럼 작동합니다. 모델에 새로운 측정 값을 추가하여 해당 .pbix 파일에서 사용할 수 있지만 모델을 근본적으로 변경할 수는 없습니다.



- 저장 모드 관리 ( storage mode )
  - 저장소 모드를 사용하면 Power BI Desktop이 보고서를 위해 인 메모리로 테이블 데이터를 캐시할지 여부를 제어 할 수 있습니다.
  - 각 테이블의 스토리지 모드를 개별적으로 설정할 수 있습니다. 

  

- Power Query 를 통한 ETL 작업 가능 

  - Import 나 직접 생성한 테이블에 대해서만 가능



### 1.3 Modeling

- tabular modeling 을 기본적으로 사용  
- RModeling 
  - 실제 레포트를 보여 주는 단계에서 데이터 원본에 대한 연결 및 데이터 조회 작업이 발생
  - 실제적으로 최종 end user 입장에서 속도적인 이슈가 있을 수 있음.

![image-20200622110910907](E:\toone\holic_toone\doc\image\image-20200622110910907.png)



### 1.4  Visualization

- 기본 제공되는 chart 와  market place 에서 무료로 다운 받을 수 있는 custom chart가 존재함.

![image-20200622111022621](E:\toone\holic_toone\doc\image\image-20200622111022621.png)



![image-20200622112552267](E:\toone\holic_toone\doc\image\image-20200622112552267.png)



- Microsoft Power BI Blog 

https://powerbi.microsoft.com/en-us/blog/category/uncategorized/

- power bi new feature 

https://powerbi.microsoft.com/en-us/blog/power-bi-desktop-june-2020-feature-summary/







# 2. OLAP 모델링 (datawarehouse)

> **데이터 웨어하우스**(data warehouse)란 사용자의 의사 결정에 도움을 주기 위하여, 기간시스템의 [데이터베이스](https://ko.wikipedia.org/wiki/데이터베이스)에 축적된 데이터를 공통의 형식으로 변환해서 관리하는 데이터베이스를 말한다. 줄여서 **DW**로도 불린다.
>
> 데이터 웨어하우스는 방대한 조직 내에서 분산 운영되는 각각의 데이터 베이스 관리 시스템들을 효율적으로 통합하여 조정ㆍ관리하기 때문에 효율적인 의사 결정 시스템을 위한 기초를 제공하는 실무적인 활용 방법론이 제공되고 있다.
>
> 데이터 웨어하우스의 구성은 관리 하드웨어, 관리 소프트웨어, 추출ㆍ변환ㆍ정렬 도구, 데이터 베이스 마케팅 시스템, 메타 데이터(meta data), 최종 사용자 접근 및 활용 도구 등으로 구성되어 있다.
>
> 데이터 웨어하우스는 경영자의 의사 결정을 지원하는 데이터의 집합체로 주제 지향적(subjectoriented), 통합적(integrated), 시계열적(timevarient), 비휘발적(nonvolatile)인 네 가지 특성을 지닌다.
>
> 주제 지향성(subject-orientation)으로 데이터를 주제별로 구성함으로써 최종 사용자(end user)와 전산에 약한 분석자라도 이해하기 쉬운 형태가 되는 것이고 통합성(integration)으로 데이터가 데이터 웨어하우스에 들어갈 때는 일관적인 형태(데이터의 일관된 이름짓기, 일관된 변수 측정, 일관된 코드화 구조 등)로 변환되는 것이다.
>
> 그러므로 시계열성(time-variancy)로 데이터 웨어하우스의 데이터는 일정 기간 동안 정확성을 나타내고 비휘발성(nonvolatilization)로 데이터 웨어하우스에 일단 데이터가 적재되면 일괄 처리(batch) 작업에 의한 갱신 이외에는 「Insert」나 「Delete」등의 변경이 수행되지 않는 특징을 가지게 된다.
>
> <wikipidia>



- OLTP: On-Line Transaction Processing

네트워크 상의 여러 이용자가 실시간으로 데이터베이스의 데이터를 갱신하거나 조회하는 등의 단위작업을 처리하는 방식을 말한다

- OLAP: On-Line Analytic Processing

정보위주의 처리 분석을 의미한다. 의사결정에 활용할 수 있는 정보를 얻을 수 있게 해주는 기술이다.





| **특징**            | **데이터 웨어하우스**                                        | **트랜잭션 데이터베이스**                                    |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **적합한 워크로드** | 분석, 보고, [빅 데이터](https://aws.amazon.com/ko/big-data/what-is-big-data/) | 트랜잭션 처리                                                |
| **데이터 원본**     | 여러 소스로부터 수집되고 정규화된 데이터                     | 트랜잭션 시스템과 같이 단일 소스에서 있는 그대로 캡처한 데이터 |
| **데이터 캡처**     | 대개 미리 결정된 대량 배치 일정에 따른 대량 쓰기 작업        | 트랜잭션 처리량을 최대화할 수 있도록 새로운 데이터가 사용할 수 있어 지속적인 쓰기 작업에 최적화됨 |
| **데이터 정규화**   | 스타 스키마 또는 눈송이 스키마와 같이 비정규화된 스키마      | 고도로 정규화된 정적 스키마                                  |
| **데이터 스토리지** | 컬럼 방식 스토리지를 사용하여 간단한 액세스 및 고속 쿼리 성능에 대해 최적화됨 | 단일 행 지향 물리적 블록에 대한 고도의 처리량 쓰기 작업에 최적화됨 |
| **데이터 액세스**   | I/O를 최소화하고 데이터 처리량을 최대화하도록 최적화됨       | 대량의 소규모 읽기 작업                                      |







### 2.1 Multidimention Cube ( MOLAP )



[Tableau 큐브 데이터 원본](https://help.tableau.com/current/pro/desktop/ko-kr/cubes.htm)





![olapcube_2](E:\toone\holic_toone\doc\Visualization\webinar\olapcube_2.png)

![olapcube_1](E:\toone\holic_toone\doc\Visualization\webinar\olapcube_1.png)

![olapcube_4](E:\toone\holic_toone\doc\Visualization\webinar\olapcube_4.png)



![olapcube_3](E:\toone\holic_toone\doc\Visualization\webinar\olapcube_3.png)





### 2.2 Tabular Modeling  ( ROLAP )



> MSDN의 Microsoft SSAS Tabular Model 정의에 따르면 "Tabular 모델은 인 메모리 또는 DirectQuery 모드에서 실행되는 백엔드 관계형 데이터 소스에서 직접 데이터에 액세스하는 Analysis Services 데이터베이스입니다." 테이블 형식 모델은 두 가지 모드 "메모리 내"및 "DirectQuery"를 지원하는 높은 수준의 성능 및 압축 비율을 제공하는 column 형 DB입니다.
>
> [Introduction to tabular model- What and Why?](https://www.sarjen.com/introduction-to-tabular-model/)

#### - Flat Table

![](E:\toone\holic_toone\doc\Visualization\webinar\table_create-1593044830959.png)



#### - star schema

<img src="E:\toone\holic_toone\doc\image\star schema.png" style="zoom:150%;" />



#### - snow flake schema

<img src="https://cdn.softwaretestinghelp.com/wp-content/qa/uploads/2019/09/Snowflake-Schema.jpg" alt="Snowflake Schema" style="zoom:150%;" />



- 팩트 테이블에는 정의에 집계가 내장 된 열인 측정 값이 포함됩니다. 예를 들어 수익 및 단위는 측정 단위 열입니다.
- 차원 테이블에는 비즈니스 엔터티를 설명하는 특성이 포함되어 있습니다. 예를 들어 고객 이름, 지역 및 주소는 속성 열입니다.





# 3. Visualization



### 3.1 DAX ( Data Analysis Expression )

- Excel Power Pivot, Analysis Service, Power BI, SQL Management Studio 등에서 사용

```python
측정값 = CALCULATE(
	SUM( '테이블명'[변수명])
    FILTER(
    	ALLSELECTED('테이블명')
    ) 
)
```



#### 3.1.1 meaure (측정값)

- 특정 데이터에 대한 DAX 수식을 통해 미리 정의된 계산식의 모양이 되고 이후 context가 결정 되는 시점에 계산이 이루어짐

```python
Packagning sum actual = CALCULATE( 
                sum(table명[칼럼명]), 
                filter(
                    all( '테이블명'[칼럼명]), 
                    '테이블명'[칼럼명] = "포장재" && 
                	'테이블명'[칼럼명] = "식자재"
                )
		)
```



```python
change % rate = 
	var currentYear = [measure total amount]
    
    var previousYear = 
		CALCULATE ( [measure total amount], 
                     SAMEPERIODLASTYEAR('DimDate'[DATE])
                  )
    RETURN 
    (
       ( currentYear - previousYear) /  currentYear
    )
```



#### 3.1.2 calculated column

https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-tutorial-create-calculated-columns





### 3.2 Date Dimension table  

- Create With DAX

```python
Date = CALENDAR(DATE( YEAR( MIN (SalesData[SALE_DATE] ) ), 1, 1),DATE( YEAR (MAX (SalesData[SALE_DATE]) ), 12, 31 ))

YEAR = YEAR(DimDate[Date])
Quarter = FORMAT(DimDate[Date],”\QQ”)
Month = FORMAT(DimDate,"mmmm")
MonthNo = MONTH(DimDate[Date])
Day = DAY(DimDate[Date])
Day of Week No = WEEKDAY(DimDate[Date])
Day of Week = FORMAT(DimDate[Date],"dddd")

YearMon = FORMAT('Table'[Date], "YYYYMM")
```



### 3.3 slicing

- Power BI의 슬라이서는 캔버스 비주얼 필터 유형입니다. 슬라이서는 사용자가 묶은 보고서를 정렬 및 필터링하고 원하는 정보 만 볼 수 있도록합니다. 필터와 달리 슬라이서는 보고서에 시각적으로 표시되며 사용자가 보고서를 분석 할 때 값을 선택할 수 있습니다.
- Edit Interactions 를 사용하여 slicing 대상과 유형을 선택 할 수 있음. 
- 중요하고 자주 사용되는 필터를 보고서 캔버스에 배치하여 쉽게 액세스 할 수 있습니다



### 3.3 hierarchy

- 동일 table 안에서 구성 가능
- hierarchy 구성 시 drill down/up 기능 가능 



### 3.4 Performance Analyzer

- 실제 report가 수행 되는 시점의 백단에 수행 정보 확인

![image-20200623145455725](E:\toone\holic_toone\doc\Power BI\webinar\image-20200623145455725.png)







# reference

[Microsoft Power BI: Enterprise modeling with Power BI and Azure Analysis Services - BRK3064](https://www.youtube.com/watch?v=gJPgbJMC_HU)

# business_analytics_platform

다양한 bi service의 구축 방안

|platform|특징|ref|
|----------|-----------|----------------|
|power bi|visualization 과 modeling이 모두 통합된 형태. <br> tabular modeling ( ROLAP ) 을 기반으로 하며 multidiention cube 구성을 할 경우 analysis service ( arure/sql server )가 필요 ||
|superset|airbnb에서 apache project로 넘긴 bi툴로 dbms(spark, hived, mpp와 같은 warehouse 형태 포함 )기반으로 기본적인 query editor 기능을 제공하여 빠르게 시각화를 지원. 하지만|

# business_analytics_platform

다양한 bi service의 구축 방안

|platform|특징|ref|
|----------|-----------|----------------|
|power bi|visualization 과 modeling이 모두 통합된 형태. <br> tabular modeling ( ROLAP ) 을 기반으로 하며 multidiention cube 구성을 할 경우 analysis service ( arure/sql server )가 필요. <br> 브라우저를 통한 공유를 위해서는 반드시 office365 클라우드의 power bi service가 필요함. (라이센스 필요) ||
|superset|airbnb에서 apache project로 넘긴 bi툴로 dbms(spark, hived, mpp와 같은 warehouse 형태 포함 )기반으로 기본적인 query editor 기능을 제공하여 빠르게 시각화를 지원.<br> 하지만 modeling 기능이 없기 때문에 반드시 datawarehouse나 mart에서 모델링이 된 최종 결과를 통해 시각화 진행 필요.||
|redash|databricks에서 2020년 인수한 프로젝트로 query editor와 visualization을 동일 화면에서 동시에 진행 가능.||

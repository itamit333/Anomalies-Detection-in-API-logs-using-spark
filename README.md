# Anomalies-Detection-in-API-logs-using-spark
Amit Thapa project 
Pyspark code to implement different functionalities:
1)	For analyzing response codes
response_code_counts = df.groupBy("response_code").count().orderBy("count", ascending=False)
 response_code_counts.show()

2)	Traffic analyzing 
# Top Endpoints by Traffic 
top_endpoints = df.groupBy("endpoint").count().orderBy("count", ascending=False) top_endpoints.show(10) 

# Frequent Visitors 
frequent_visitors = df.groupBy("ip").count().filter("count > 10").orderBy("count", ascending=False) 
frequent_visitors.show(10)

3)	Content Size Statistics
content_stats = df.agg
( min(col("content_size")).alias("min_content_size"), max(col("content_size")).alias("max_content_size"), avg(col("content_size")).alias("avg_content_size"), count(col("content_size")).alias("count_content_size")
 ) 
content_stats.show()

4)	Top Endpoints by Content Size
top_content_endpoints=df.groupBy("endpoint").sum("content_size").orderBy("sum(content_size)", ascending=False) 
top_content_endpoints.show(10)

5)	Frequent Visitors
frequent_visitors = df.groupBy("ip").count().filter("count > 10").orderBy("count", ascending=False) 
frequent_visitors.show(10)

6)	 Analyzing Bad Requests (404)
bad_requests = df.filter(df.response_code == 404) latest_bad_requests = bad_requests.orderBy("timestamp", ascending=False).limit(10)
 latest_bad_requests.show()

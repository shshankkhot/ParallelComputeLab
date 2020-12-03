// #ParallelComputeLab
--
Question : Do reviews that mention "reviews" or "comments" differ from the overall reviews in terms of "overall" rating?
--
Distributon of rating for reviews with  "reviews" or "comments" compare to "Others" and Total Review counts with reviews
----------------------------------------------------------------
//AmazonReviewContainsComentsReview
----------------------------------------------------------------
//Step 1
javac -cp /opt/cloudera/parcels/CDH/lib/hadoop/client/*:/opt/cloudera/parcels/CDH/lib/hbase/* AmazonReviewContainsComentsReview.java -d build -Xlint
----------------------------------------------------------------
//Step2 --
jar -cvf process_reviews_comments.jar -C build/ .
----------------------------------------------------------------
//Step3 To remove existing genrated files
hadoop fs -rm -r /user/skhot/review_comments
----------------------------------------------------------------
//step 4
HADOOP_CLASSPATH=$(hbase mapredcp):/etc/hbase/conf hadoop jar process_reviews_comments.jar AmazonReviewContainsComentsReview '/user/skhot/review_comments'
----------------------------------------------------------------
//Step 5 Write Output to file
//hadoop fs -cat /user/skhot/review_comments/* > review_comments_output.txt

hadoop fs -cat /user/skhot/review_comments/* | sort -n > review_comments_output.txt
----------------------------------------------------------------

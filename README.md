# ParallelComputeLab
--
Question : Are reviews that contain images more likely to be positive or negative?  Show a distribution of # of images against 1-2 star reviews and 4-5 star reviews.
---------------------------------------------------------------------
Step 1
javac -cp /opt/cloudera/parcels/CDH/lib/hadoop/client/*:/opt/cloudera/parcels/CDH/lib/hbase/* AmazonReviewWithImages.java -d build -Xlint
---------------------------------------------------------------------
Step 2
jar -cvf process_reviews.jar -C build/ .
---------------------------------------------------------------------
Step 3
hadoop fs -rm -r /user/skhot/review_with_images
---------------------------------------------------------------------
Step 4
HADOOP_CLASSPATH=$(hbase mapredcp):/etc/hbase/conf hadoop jar process_reviews.jar AmazonReviewWithImages '/user/skhot/review_with_images'
---------------------------------------------------------------------
Step 5
hadoop fs -cat /user/skhot/review_with_images/* > review_images_output_alldata.txt
---------------------------------------------------------------------

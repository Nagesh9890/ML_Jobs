# ML_Jobs

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences
count_df = filtered_df.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Display the result
count_df.show()




from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df1 = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences for category_level1
count_df1 = filtered_df1.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Filter the DataFrame for rows where category_level2 is 'TRANSFER_FRIENDS_AND_FAMILY'
filtered_df2 = result_df.filter(result_df.category_level2 == 'TRANSFER_FRIENDS_AND_FAMILY')

# Group by account_number and count the occurrences for category_level2
count_df2 = filtered_df2.groupBy("account_number").agg(F.count("category_level2").alias("count_friends_and_family"))

# Join the two DataFrames on account_number
final_df = count_df1.join(count_df2, ["account_number"], "outer").fillna(0)

# Display the result
final_df.show()


---------------------



from pyspark.sql import functions as F
from pyspark.sql.window import Window

# Define a window specification
windowSpec = Window.partitionBy("account_number")

# Create a new column for the count of 'Personal Transfer' in category_level1
result_df = result_df.withColumn("count_personal_transfer", 
                                 F.sum(F.when(F.col("category_level1") == 'Personal Transfer', 1).otherwise(0)).over(windowSpec))

# Create a new column for the count of 'TRANSFER_FRIENDS_AND_FAMILY' in category_level2
result_df = result_df.withColumn("count_friends_and_family", 
                                 F.sum(F.when(F.col("category_level2") == 'TRANSFER_FRIENDS_AND_FAMILY', 1).otherwise(0)).over(windowSpec))

# Display the result
result_df.show()


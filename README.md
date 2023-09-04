# ML_Jobs

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences
count_df = filtered_df.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Display the result
count_df.show()

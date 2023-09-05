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

--------------------------------

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df1 = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences for category_level1
count_df1 = filtered_df1.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Filter the DataFrame for rows where category_level2 is 'TRANSFER_FRIENDS_AND_FAMILY'
filtered_df2 = result_df.filter(result_df.category_level2 == 'TRANSFER_FRIENDS_AND_FAMILY')

# Group by account_number and count the occurrences for category_level2
count_df2 = filtered_df2.groupBy("account_number").agg(F.count("category_level2").alias("count_friends_and_family"))

# Create a DataFrame with unique account_holder_name, account_ifsc, and account_type for each account_number
unique_account_details = result_df.select("account_number", "account_holder_name", "account_ifsc", "account_type").distinct()

# Join the two count DataFrames on account_number
final_df = count_df1.join(count_df2, ["account_number"], "outer").fillna(0)

# Join the final_df with unique_account_details on account_number
final_df = final_df.join(unique_account_details, ["account_number"], "left")

# Display the result
final_df.show()

-------------------------

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df1 = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences for category_level1
count_df1 = filtered_df1.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Filter the DataFrame for rows where category_level2 is 'TRANSFER_FRIENDS_AND_FAMILY'
filtered_df2 = result_df.filter(result_df.category_level2 == 'TRANSFER_FRIENDS_AND_FAMILY')

# Group by account_number and count the occurrences for category_level2
count_df2 = filtered_df2.groupBy("account_number").agg(F.count("category_level2").alias("count_friends_and_family"))

# Create a DataFrame with unique account_holder_name, account_ifsc, and account_type for each account_number
unique_account_details = result_df.select("account_number", "account_holder_name", "account_ifsc", "account_type").distinct()

# Join the two count DataFrames on account_number
final_df = count_df1.join(count_df2, ["account_number"], "outer").fillna(0)

# Join the final_df with unique_account_details on account_number
final_df = final_df.join(unique_account_details, ["account_number"], "left")

# Reorder the columns
final_df = final_df.select("account_holder_name", "account_ifsc", "account_type", "account_number", "count_personal_transfer", "count_friends_and_family")

# Display the result
final_df.show()
---------------------------------------------

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df1 = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and count the occurrences for category_level1
count_df1 = filtered_df1.groupBy("account_number").agg(F.count("category_level1").alias("count_personal_transfer"))

# Filter the DataFrame for rows where category_level2 is 'TRANSFER_FRIENDS_AND_FAMILY'
filtered_df2 = result_df.filter(result_df.category_level2 == 'TRANSFER_FRIENDS_AND_FAMILY')

# Group by account_number and count the occurrences for category_level2
count_df2 = filtered_df2.groupBy("account_number").agg(F.count("category_level2").alias("count_friends_and_family"))

# Create a DataFrame with unique account_holder_name, account_ifsc, and account_type for each account_number
unique_account_details = result_df.select("account_number", "account_holder_name", "account_ifsc", "account_type").distinct()

# Join the two count DataFrames on account_number
final_df = count_df1.join(count_df2, ["account_number"], "outer").fillna(0)

# Join the final_df with unique_account_details on account_number
final_df = final_df.join(unique_account_details, ["account_number"], "left")

# Reorder the columns
final_df = final_df.select("account_holder_name", "account_ifsc", "account_type", "account_number", "count_personal_transfer", "count_friends_and_family")

# Display the result
final_df.show()

-----------------------------------------------------

from pyspark.sql import functions as F

# Filter the DataFrame for rows where category_level1 is 'Personal Transfer'
filtered_df1 = result_df.filter(result_df.category_level1 == 'Personal Transfer')

# Group by account_number and compute the count and sum for category_level1
count_df1 = filtered_df1.groupBy("account_number").agg(
    F.count("category_level1").alias("count_personal_transfer"),
    F.sum("payer_amount").alias("sum_personal_transfer")
)

# Filter the DataFrame for rows where category_level2 is 'TRANSFER_FRIENDS_AND_FAMILY'
filtered_df2 = result_df.filter(result_df.category_level2 == 'TRANSFER_FRIENDS_AND_FAMILY')

# Group by account_number and compute the count and sum for category_level2
count_df2 = filtered_df2.groupBy("account_number").agg(
    F.count("category_level2").alias("count_friends_and_family"),
    F.sum("payer_amount").alias("sum_friends_and_family")
)

# Create a DataFrame with unique account_holder_name, account_ifsc, and account_type for each account_number
unique_account_details = result_df.select("account_number", "account_holder_name", "account_ifsc", "account_type").distinct()

# Join the two count DataFrames on account_number
final_df = count_df1.join(count_df2, ["account_number"], "outer").fillna(0)

# Join the final_df with unique_account_details on account_number
final_df = final_df.join(unique_account_details, ["account_number"], "left")

# Reorder the columns
final_df = final_df.select("account_holder_name", "account_ifsc", "account_type", "account_number", 
                           "count_personal_transfer", "sum_personal_transfer", 
                           "count_friends_and_family", "sum_friends_and_family")

# Display the result
final_df.show()

-------------------------

from pyspark.sql import functions as F

def compute_aggregates(df, category_col, amount_col):
    # Get unique categories
    unique_categories = df.select(category_col).distinct().rdd.flatMap(lambda x: x).collect()

    agg_dfs = []
    for category in unique_categories:
        # Filter the DataFrame for rows based on category
        filtered_df = df.filter(df[category_col] == category)

        # Group by account_number and compute the count and sum
        agg_df = filtered_df.groupBy("account_number").agg(
            F.count(category_col).alias(f"count_{category}"),
            F.sum(amount_col).alias(f"sum_{category}")
        )
        agg_dfs.append(agg_df)

    # Reduce by joining all aggregated DataFrames
    final_agg_df = agg_dfs[0]
    for agg_df in agg_dfs[1:]:
        final_agg_df = final_agg_df.join(agg_df, ["account_number"], "outer").fillna(0)

    return final_agg_df

# Compute aggregates for category_level1 and category_level2
agg_df1 = compute_aggregates(result_df, "category_level1", "payer_amount")
agg_df2 = compute_aggregates(result_df, "category_level2", "payer_amount")

# Join the two aggregated DataFrames
final_agg_df = agg_df1.join(agg_df2, ["account_number"], "outer").fillna(0)

# Create a DataFrame with unique account_holder_name, account_ifsc, and account_type for each account_number
unique_account_details = result_df.select("account_number", "account_holder_name", "account_ifsc", "account_type").distinct()

# Join the final_agg_df with unique_account_details on account_number
final_df = final_agg_df.join(unique_account_details, ["account_number"], "left")

# Reorder the columns to place account details first
cols = ["account_holder_name", "account_ifsc", "account_type", "account_number"] + [col for col in final_df.columns if col not in ["account_holder_name", "account_ifsc", "account_type", "account_number"]]
final_df = final_df.select(*cols)

# Display the result
final_df.show()


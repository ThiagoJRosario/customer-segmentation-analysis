# customer-segmentation-analysis
Business Problem:
The goal of this project is to group (segment) customers based on their historical data using clustering techniques. The segmented customer groups will then be analyzed and a report will be sent to the Marketing team for targeted marketing strategies.

Project Overview:
This project leverages customer data (such as age, annual income, and spending score) to identify patterns and group customers into three distinct clusters. These clusters help the marketing team to understand different customer profiles and tailor their marketing efforts accordingly.

Steps and Methodology:
Data Loading:

We load the dataset containing customer details, such as their id, age, annual income, and spending score.
python
Copiar código
df = pd.read_csv('data/clients_data.csv')
Data Cleaning:

The columns are renamed to standardized English terms for clarity:
python
Copiar código
df_dsa = df.rename(columns={
    'id': 'Id',
    'idade': 'Age',
    'renda_anual': 'annual_income',
    'pontuacao_gastos': 'spending_score'
})
Exploratory Data Analysis (EDA):

Basic statistical summaries are generated to understand the distribution of the data:
python
Copiar código
df_dsa[['Age', 'annual_income', 'spending_score']].describe()
Data Preprocessing:

To ensure that all features are on a similar scale, the data is standardized using StandardScaler:
python
Copiar código
from sklearn.preprocessing import StandardScaler
standardizer = StandardScaler()
standardizer_data = standardizer.fit_transform(df_dsa[['Age', 'annual_income', 'spending_score']])
Clustering Using K-Means:

The K-Means algorithm is applied to group customers into 3 clusters. The optimal number of clusters was defined as 3 based on the business need.
python
Copiar código
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=3)
kmeans.fit(standardizer_data)
Assigning Cluster Labels:

After the K-Means model is trained, cluster labels are assigned to each customer:
python
Copiar código
df_dsa['cluster'] = kmeans.labels_
Result Output:

The resulting dataset, including the cluster labels, is saved to a CSV file for further analysis and reporting:
python
Copiar código
df_dsa.to_csv('data/segments.csv', index=False)
Dependencies:
pandas
scikit-learn
StandardScaler for data preprocessing
KMeans for clustering
How to Run:
Clone the repository.
Ensure you have the necessary libraries installed:
bash
Copiar código
pip install pandas scikit-learn
Load the data file clients_data.csv in the data folder.
Run the Python script or Jupyter Notebook to generate the segmented customer data.
Output:
The segmented data will be saved as segments.csv in the data folder.
The report will contain customer IDs along with their respective clusters, which can be used by the Marketing team for targeted campaigns.
Next Steps:
Further analysis on the characteristics of each segment can be done to optimize marketing strategies.
Visualization of the clusters could be added to better interpret the results.

# Python-for-BI-Semantic-Data-Model-Connector

The PowerBI semantic data models can be connected via excel or PowerBI desktop or via Python connector scripts. 
By using Python script, the data can be imported directly and perform data anylicts with Python using pandas or other libraries.

[main.ipynb](https://github.com/sebsebsebsebtimes4/Python-for-BI-Semantic-Data-Model-Connector/blob/main/main.ipynb)

```
%run PowerBIDataConnector.ipynb
from IPython.display import display

dmc = DataModelCollector(dataset_id='39d72aa7-5e35-4dd1-bd28-9f5903a75881',
                         login='sebastien.hsu@esprit.com',
                         password='Sebtimes11'
                         )

dmc.create_connection()

dmc.get_all_tables()
print(dmc.df_table)

query_str = '''

DEFINE
	VAR __DS0Core = 
		SUMMARIZECOLUMNS(
			'BDSM_DataSource'[SSN],
			'BDSM_DataSource'[Style_Code],
			'BDSM_DataSource'[Prod_Cluster_Name],
			'BDSM_DataSource'[IRPCalY],
			'BDSM_DataSource'[Prod_Gender],
			'Country Group'[Country Group],
			'BDSM_DataSource'[CustomerDestination],
			"SumEES_PUR_PCS", CALCULATE(SUM('BDSM_DataSource'[EES_PUR_PCS]))
		)

	VAR __DS0PrimaryWindowed = 
		TOPN(
			501,
			__DS0Core,
			'BDSM_DataSource'[SSN],
			1,
			'BDSM_DataSource'[Style_Code],
			1,
			'BDSM_DataSource'[Prod_Cluster_Name],
			1,
			'BDSM_DataSource'[IRPCalY],
			1,
			'BDSM_DataSource'[Prod_Gender],
			1,
			'Country Group'[Country Group],
			1,
			'BDSM_DataSource'[CustomerDestination],
			1
		)

EVALUATE
	__DS0PrimaryWindowed
ORDER BY
	'BDSM_DataSource'[SSN],
	'BDSM_DataSource'[Style_Code],
	'BDSM_DataSource'[Prod_Cluster_Name],
	'BDSM_DataSource'[IRPCalY],
	'BDSM_DataSource'[Prod_Gender],
	'Country Group'[Country Group],
	'BDSM_DataSource'[CustomerDestination]
          
'''

```


[PowerBIDataConnector.ipynb](https://github.com/sebsebsebsebtimes4/Python-for-BI-Semantic-Data-Model-Connector/blob/main/PowerBIDataConnector.ipynb)



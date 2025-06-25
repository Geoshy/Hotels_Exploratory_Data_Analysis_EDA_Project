
# **Uncovering the Drivers Behind Rising Hotel Cancellation Rates: Data Analysis Project**

## **(1) Project Roadmap:**

1. **Define Problem Statement:** Address the issue of increasing cancellation orders in hotels.
2. **Data Identification:** Select the dataset `hotels.csv` for analysis.
3. **Data Preparation:** Clean and explore the data using Python to ensure quality and consistency.
4. **Data Analysis:** Extract insights to identify reasons behind the rise in hotel cancellation orders.

## **(2) Introduction:**
This project aims to identify the key factors contributing to the **increasing rate of hotel booking cancellations**. We will explore primary reasons, such as **high average daily rates**, and secondary factors, including **discrepancies between online hotel photos and actual conditions**. Utilizing the **Python** programming language, we will begin with **data cleaning, manipulation, and normalization using the Pandas library to handle outliers and null values**. Our dataset comprises information from two distinct types of hotels: **city hotel and resort hotel**. Following this, we will employ **data visualization tools like Matplotlib and Seaborn to create insightful plots**. Through detailed analysis of these visualizations, we will uncover the underlying reasons for the surge in hotel cancellation orders.

## **(3) Tools I Used:**
1. **Kaggle**: Source of the hotels dataset.
2. **Python Programming Language**: Used for overall data manipulation and analysis.
3. **Pandas Library**: Utilized for data cleaning, manipulation, standardization (normalization), and handling outliers and null values.
4. **Matplotlib**: Employed for data visualization.
5. **Seaborn**: Used for statistical data visualization.
6. **Git & GitHub**: for sharing my analysis and insights.

## **(4) Data Inspection:**
### **4.1. Import Important Libraries and Modules:**
```py
import pandas as pd
import numpy as np 
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import seaborn as sns
import datetime as dt
```

## **4.2. Export Target Dataframe:**
```py
df = pd.read_csv('D:\\IT Courses\\Data Analysis Courses\\Data Analysis Projects\\Hotels Exploratory Data Analysis (EDA) Project\\Hotels_Exploratory_Data_Analysis_EDA_Project\\Dataset\\hotels.csv')
```

## **(5) Data Cleaning and Formatting:**
### **5.1. Dealing With Nan Values:**

**5.1.1. Drop Columns ('agent', 'company'):**
```py
df_copy.drop(
    ['agent', 'company'],
    axis=1,
    inplace=True
)
```

**5.1.2. Drop Nan Values Of Columns ('country', 'children'):**
```py
df_copy.dropna(
    subset=('country', 'children'),
    axis=0,
    inplace=True
)
```
### **5.2. Type Casting of Column (reservation_status_date) to Datetime:**
```py
df_copy['reservation_status_date'] = pd.to_datetime(df_copy['reservation_status_date'])
# 118898 non-null  datetime64[ns]
```
### **5.3. Data Normalization and Standardization:**
**5.2.1. Data Normalization of Column (meal):**

**Based on common hotel meal abbreviations, here are the likely full names for each abbreviation in the column:** 

- **BB**: Bed and Breakfast
- **FB**: Full Board (typically includes breakfast, lunch, and dinner)
- **HB**: Half Board (typically includes breakfast and dinner)
- **SC**: Self Catering
- **Undefined**: Undefined (no specific meal plan specified)
```py
meal_column_dictionary = {
    'BB':'Bed & Breakfast',
    'FB':'Full Board',
    'HB':'Half Board',
    'SC':'Self Catering',
    'Undefined':'Undefined'
}
```
```py
def meal_normalization(meal_column):
    for key, value in meal_column_dictionary.items():
        if key.upper() == meal_column.upper():
            return(value)
    else:
        return(meal_column)

df_copy['meal'] = df_copy['meal'].apply(meal_normalization)
```

**5.2.2. Data Normalization of Column (country):**
```py
country_codes_to_names = {
    'PRT': 'Portugal',
    'GBR': 'United Kingdom',
    'USA': 'United States',
    'ESP': 'Spain',
    'IRL': 'Ireland',
    'FRA': 'France',
    'ROU': 'Romania',
    'NOR': 'Norway',
    'OMN': 'Oman',
    'ARG': 'Argentina',
    'POL': 'Poland',
    'DEU': 'Germany',
    'BEL': 'Belgium',
    'CHE': 'Switzerland',
    'CN': 'China', 
    'GRC': 'Greece',
    'ITA': 'Italy',
    'Unknown' : 'Not Disclose',
    'NLD': 'Netherlands',
    'DNK': 'Denmark',
    'RUS': 'Russia',
    'SWE': 'Sweden',
    'AUS': 'Australia',
    'EST': 'Estonia',
    'CZE': 'Czech Republic',
    'BRA': 'Brazil',
    'FIN': 'Finland',
    'MOZ': 'Mozambique',
    'BWA': 'Botswana',
    'LUX': 'Luxembourg',
    'SVN': 'Slovenia',
    'ALB': 'Albania',
    'IND': 'India',
    'CHN': 'China',
    'MEX': 'Mexico',
    'MAR': 'Morocco',
    'UKR': 'Ukraine',
    'SMR': 'San Marino',
    'LVA': 'Latvia',
    'PRI': 'Puerto Rico',
    'SRB': 'Serbia',
    'CHL': 'Chile',
    'AUT': 'Austria',
    'BLR': 'Belarus',
    'LTU': 'Lithuania',
    'TUR': 'Turkey',
    'ZAF': 'South Africa',
    'AGO': 'Angola',
    'CYM': 'Cayman Islands',
    'ZMB': 'Zambia',
    'CPV': 'Cabo Verde',
    'ZWE': 'Zimbabwe',
    'DZA': 'Algeria',
    'KOR': 'South Korea',
    'CRI': 'Costa Rica',
    'HUN': 'Hungary',
    'ARE': 'United Arab Emirates',
    'TUN': 'Tunisia',
    'JAM': 'Jamaica',
    'HRV': 'Croatia',
    'HKG': 'Hong Kong',
    'IRN': 'Iran',
    'GEO': 'Georgia',
    'AND': 'Andorra',
    'GIB': 'Gibraltar',
    'URY': 'Uruguay',
    'JEY': 'Jersey',
    'CAF': 'Central African Republic',
    'CYP': 'Cyprus',
    'COL': 'Colombia',
    'GGY': 'Guernsey',
    'KWT': 'Kuwait',
    'NGA': 'Nigeria',
    'MDV': 'Maldives',
    'VEN': 'Venezuela',
    'SVK': 'Slovakia',
    'FJI': 'Fiji',
    'KAZ': 'Kazakhstan',
    'PAK': 'Pakistan',
    'IDN': 'Indonesia',
    'LBN': 'Lebanon',
    'PHL': 'Philippines',
    'SEN': 'Senegal',
    'SYC': 'Seychelles',
    'AZE': 'Azerbaijan',
    'BHR': 'Bahrain',
    'NZL': 'New Zealand',
    'THA': 'Thailand',
    'DOM': 'Dominican Republic',
    'MKD': 'North Macedonia',
    'MYS': 'Malaysia',
    'ARM': 'Armenia',
    'JPN': 'Japan',
    'LKA': 'Sri Lanka',
    'CUB': 'Cuba',
    'CMR': 'Cameroon',
    'BIH': 'Bosnia and Herzegovina',
    'MUS': 'Mauritius',
    'COM': 'Comoros',
    'SUR': 'Suriname',
    'UGA': 'Uganda',
    'BGR': 'Bulgaria',
    'CIV': "Cote d'Ivoire",
    'JOR': 'Jordan',
    'SYR': 'Syria',
    'SGP': 'Singapore',
    'BDI': 'Burundi',
    'SAU': 'Saudi Arabia',
    'VNM': 'Vietnam',
    'PLW': 'Palau',
    'QAT': 'Qatar',
    'EGY': 'Egypt',
    'PER': 'Peru',
    'MLT': 'Malta',
    'MWI': 'Malawi',
    'ECU': 'Ecuador',
    'MDG': 'Madagascar',
    'ISL': 'Iceland',
    'UZB': 'Uzbekistan',
    'NPL': 'Nepal',
    'BHS': 'Bahamas',
    'MAC': 'Macau',
    'TGO': 'Togo',
    'TWN': 'Taiwan',
    'DJI': 'Djibouti',
    'STP': 'Sao Tome and Principe',
    'KNA': 'Saint Kitts and Nevis',
    'ETH': 'Ethiopia',
    'IRQ': 'Iraq',
    'HND': 'Honduras',
    'RWA': 'Rwanda',
    'KHM': 'Cambodia',
    'MCO': 'Monaco',
    'BGD': 'Bangladesh',
    'IMN': 'Isle of Man',
    'TJK': 'Tajikistan',
    'NIC': 'Nicaragua',
    'BEN': 'Benin',
    'VGB': 'British Virgin Islands',
    'TZA': 'Tanzania',
    'GAB': 'Gabon',
    'GHA': 'Ghana',
    'TMP': 'East Timor',
    'GLP': 'Guadeloupe',
    'KEN': 'Kenya',
    'LIE': 'Liechtenstein',
    'GNB': 'Guinea-Bissau',
    'MNE': 'Montenegro',
    'UMI': 'United States Minor Outlying Islands',
    'MYT': 'Mayotte',
    'FRO': 'Faroe Islands',
    'MMR': 'Myanmar',
    'PAN': 'Panama',
    'BFA': 'Burkina Faso',
    'LBY': 'Libya',
    'MLI': 'Mali',
    'NAM': 'Namibia',
    'BOL': 'Bolivia',
    'PRY': 'Paraguay',
    'BRB': 'Barbados',
    'ABW': 'Aruba',
    'AIA': 'Anguilla',
    'SLV': 'El Salvador',
    'DMA': 'Dominica',
    'PYF': 'French Polynesia',
    'GUY': 'Guyana',
    'LCA': 'Saint Lucia',
    'ATA': 'Antarctica',
    'GTM': 'Guatemala',
    'ASM': 'American Samoa',
    'MRT': 'Mauritania',
    'NCL': 'New Caledonia',
    'KIR': 'Kiribati',
    'SDN': 'Sudan',
    'ATF': 'French Southern Territories',
    'SLE': 'Sierra Leone',
    'LAO': 'Laos'
}
```
```py
def country_normalization(country_column):
    for key, value in country_codes_to_names.items():
        if key.upper() == country_column.upper():
            return(value)
    else:
        return(country_column)

df_copy['country'] = df_copy['country'].apply(country_normalization)
```
**5.2.3. Dta Normalization of Column ('is_canceled')**
```py
is_canceled_dictionary = {
    1 : 'Canceled',
    0 : 'Not Canceled'
}
```
```py
def is_canceled_normalization(is_canceled_column):
    for key, value in is_canceled_dictionary.items():
        if key == is_canceled_column:
            return(value)
    else:
        return(key)

df_copy['is_canceled'] = df_copy['is_canceled'].apply(is_canceled_normalization)
```
### **5.4. Dealing With Ouliers In Column 'adr' Average Daily Rate:**
**5.4.1. Dealing With Outliers In Column "adr" Average Daily Rate:**

**(1) Five Number Summary Of Column 'adr':**
```py
adr_Q1 = np.quantile(df_copy['adr'], 0.25) # 70
adr_Q2 = np.quantile(df_copy['adr'], 0.50) # 95.0
adr_Q3 = np.quantile(df_copy['adr'], 0.75) # 126.0

adr_min = np.min(df_copy['adr']) # -6.38
adr_max = np.max(df_copy['adr']) # 5400.0

adr_IQR = adr_Q3 - adr_Q1 # 56.0

lower_boundry = adr_Q1 - (1.5 * adr_IQR) # -14.0
upper_boundary = adr_Q3 + (1.5 * adr_IQR) # 210.0
```
**(2) "adr" Column Box Plot Visualization to Clearly Show the Variability of the "adr" column Values Before Dealing with Outliers:**
```py
plt.figure(figsize=(18,4))
plt.boxplot(
    x=df_copy['adr'],
    vert=False
)
plt.title('Average Daily Rate Box Plot')
plt.axvline(x=np.mean(df_copy['adr']), color='blue', linestyle='--', label='Mean')
plt.axvline(x=np.quantile(df_copy['adr'], 0.25), color='orange', linestyle='--', label='Q1')
plt.axvline(x=np.quantile(df_copy['adr'], 0.50), color='green', linestyle='--', label='Median')
plt.axvline(x=np.quantile(df_copy['adr'], 0.75), color='yellow', linestyle='--', label='Q3')
plt.legend(loc='upper right')
plt.yticks([])
plt.tight_layout()
```
![alt text](Figs/box_1.png)

- **Action:** Delete values in the `adr` column that are above 5000.

- **Reason:** These values have been identified as outliers and may skew the analysis or results. Removing these outliers will help ensure the accuracy and reliability of the data analysis.

- **Impact:** This action will clean the dataset, potentially improving the performance of any models or analyses that rely on this dat

```py
df_copy = df_copy[df_copy['adr'] < 5000]
```

**(3) "adr" Column Box Plot Visualization to Clearly Show the Variability of the "adr" column Values After Dealing with Outliers:**

```py
plt.figure(figsize=(18,4))
plt.boxplot(
    x=df_copy['adr'],
    vert=False
)
plt.title('Average Daily Rate Box Plot')
plt.axvline(x=np.mean(df_copy['adr']), color='blue', linestyle='--', label='Mean')
plt.axvline(x=np.quantile(df_copy['adr'], 0.25), color='orange', linestyle='--', label='Q1')
plt.axvline(x=np.quantile(df_copy['adr'], 0.50), color='green', linestyle='--', label='Median')
plt.axvline(x=np.quantile(df_copy['adr'], 0.75), color='yellow', linestyle='--', label='Q3')
plt.legend(loc='upper right')
plt.yticks([])
plt.tight_layout()
```
![alt text](Figs/box_2.png)


## **(6) Export Cleaned and Formatted Dataframe Into CSV File:**

```py
df_copy.to_csv(
    'cleaned_formatted_hotels_df.csv',
    index=False
)
```

## **(7) Exploratory Data Analysis (EDA):**
### **7.1. Hotels Reservation Status Anaysis:**
```py
plt.figure(figsize=(7,5))
round(df['is_canceled'].value_counts(normalize=True) * 100).plot(
    kind='bar',
    color=['green', 'red'],
    width=0.3,
    alpha=0.8,
    edgecolor='k'
)
plt.title('Hotels Reservation Status')
plt.xticks(rotation=0)
plt.xlabel('Reservation Status')
plt.ylabel('Percent %')
```
![alt text](Figs/p1.png)

**Key Insights:**

- A significant insight from this plot is that a majority of the reservations are **not canceled**, indicating that most customers follow through with their hotel bookings. 

- However, **there is still a notable proportion of cancellations, which suggests potential areas for improvement in understanding customer needs or addressing issues that lead to cancellations**. 

### **7.2. Comparison of Reservation Statuses Between City and Resort Hotels:**

```py
fig, ax = plt.subplots(1,2, figsize=(15,5))

hotels_labels = []
for hotel in df['hotel'].value_counts().index:
    hotels_labels.append(hotel)

df['hotel'].value_counts().plot(
    kind='bar',
    color=['blue','orange'],
    edgecolor='black',
    width=0.3,
    alpha=0.8,
    ax=ax[0]
)
ax[0].set_title('Hotels Orders Frequency')
ax[0].set_xlabel('Hotels')
ax[0].set_ylabel('Orders Frequency')
ax[0].set_xticklabels(hotels_labels, rotation=0)

df.pivot_table(index='hotel', columns='is_canceled', aggfunc='size').plot(
    kind='bar',
    color=['red', 'green'],
    edgecolor='black',
    alpha=0.8,
    ax=ax[1]
)
ax[1].legend(title='')
ax[1].set_title('(Resort Hotel - City Hotel) Reservation Status')
ax[1].set_xlabel('Hotels')
ax[1].set_ylabel('Frequency')
ax[1].set_xticklabels(hotels_labels, rotation=0)
```
![alt text](Figs/p2.png)

**Key Insights:**
- **City hotel** experience a **higher volume** of both cancellations and completed stays compared to resort hotels. 

- On the other hand, **resort hotels, while having fewer overall bookings, show a relatively lower frequency of cancellations compared to city hotel**. 

### **7.3. Time Series Analysis of Average Daily Rates for City and Resort Hotels:**
```py
adr_time_series = df.pivot_table(
    index='reservation_status_date',
    columns='hotel',
    values='adr',
    aggfunc='mean'
)
```
```py
adr_time_series['City Hotel'].fillna((df[df['hotel'] == 'City Hotel'])['adr'].mean(), inplace=True)
adr_time_series['Resort Hotel'].fillna((df[df['hotel'] == 'Resort Hotel'])['adr'].mean(), inplace=True)
```
```py
adr_time_series.plot(
    kind='line',
    figsize=(18,5),
    color=['green', 'red']
)
plt.legend()
plt.title('Average Daily Rate Time Series Analysis')
plt.xlabel('Reservation Status Date')
plt.ylabel('Average Daily Rate ($)')
plt.xlim(left=df['reservation_status_date'].min())
plt.show()
```
![alt text](Figs/p3.png)

**Key Insights:**
- **Resort hotels** exhibit significant **volatility** in their average daily rates, with **pronounced peaks that could correspond to seasonal demand or special events, suggesting a more dynamic pricing strategy**. **In contrast, city hotels maintain relatively more stable rates with fewer fluctuations**.

**

**Key Insights:**
**Key Insights:**
**Key Insights:**

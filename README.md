# ML_Project
DataScience/BangloreHomePrices
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1 style='color:purple' align='center'>Data Science Regression Project: Predicting Home Prices in Banglore</h1>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Dataset is downloaded from here: https://www.kaggle.com/amitabhajoy/bengaluru-house-price-data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np\n",
    "from matplotlib import pyplot as plt\n",
    "%matplotlib inline\n",
    "import matplotlib \n",
    "matplotlib.rcParams[\"figure.figsize\"] = (20,10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Data Load: Load banglore home prices into a dataframe</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>area_type</th>\n",
       "      <th>availability</th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>society</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>balcony</th>\n",
       "      <th>price</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Super built-up  Area</td>\n",
       "      <td>19-Dec</td>\n",
       "      <td>Electronic City Phase II</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>Coomee</td>\n",
       "      <td>1056</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>39.07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Plot  Area</td>\n",
       "      <td>Ready To Move</td>\n",
       "      <td>Chikka Tirupathi</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>Theanmp</td>\n",
       "      <td>2600</td>\n",
       "      <td>5.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>120.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Built-up  Area</td>\n",
       "      <td>Ready To Move</td>\n",
       "      <td>Uttarahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>NaN</td>\n",
       "      <td>1440</td>\n",
       "      <td>2.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>62.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Super built-up  Area</td>\n",
       "      <td>Ready To Move</td>\n",
       "      <td>Lingadheeranahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>Soiewre</td>\n",
       "      <td>1521</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>95.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Super built-up  Area</td>\n",
       "      <td>Ready To Move</td>\n",
       "      <td>Kothanur</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>NaN</td>\n",
       "      <td>1200</td>\n",
       "      <td>2.0</td>\n",
       "      <td>1.0</td>\n",
       "      <td>51.00</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              area_type   availability                  location       size  \\\n",
       "0  Super built-up  Area         19-Dec  Electronic City Phase II      2 BHK   \n",
       "1            Plot  Area  Ready To Move          Chikka Tirupathi  4 Bedroom   \n",
       "2        Built-up  Area  Ready To Move               Uttarahalli      3 BHK   \n",
       "3  Super built-up  Area  Ready To Move        Lingadheeranahalli      3 BHK   \n",
       "4  Super built-up  Area  Ready To Move                  Kothanur      2 BHK   \n",
       "\n",
       "   society total_sqft  bath  balcony   price  \n",
       "0  Coomee        1056   2.0      1.0   39.07  \n",
       "1  Theanmp       2600   5.0      3.0  120.00  \n",
       "2      NaN       1440   2.0      3.0   62.00  \n",
       "3  Soiewre       1521   3.0      1.0   95.00  \n",
       "4      NaN       1200   2.0      1.0   51.00  "
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1 = pd.read_csv(\"bengaluru_house_prices.csv\")\n",
    "df1.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(13320, 9)"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['area_type', 'availability', 'location', 'size', 'society',\n",
       "       'total_sqft', 'bath', 'balcony', 'price'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array(['Super built-up  Area', 'Plot  Area', 'Built-up  Area',\n",
       "       'Carpet  Area'], dtype=object)"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1['area_type'].unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Super built-up  Area    8790\n",
       "Built-up  Area          2418\n",
       "Plot  Area              2025\n",
       "Carpet  Area              87\n",
       "Name: area_type, dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df1['area_type'].value_counts()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Drop features that are not required to build our model**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(13320, 5)"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2 = df1.drop(['area_type','society','balcony','availability'],axis='columns')\n",
    "df2.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Data Cleaning: Handle NA values</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "location       1\n",
       "size          16\n",
       "total_sqft     0\n",
       "bath          73\n",
       "price          0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(13320, 5)"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df2.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "location      0\n",
       "size          0\n",
       "total_sqft    0\n",
       "bath          0\n",
       "price         0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df3 = df2.dropna()\n",
    "df3.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(13246, 5)"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df3.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Feature Engineering</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Add new feature(integer) for bhk (Bedrooms Hall Kitchen)**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\ProgramData\\Anaconda3\\lib\\site-packages\\ipykernel_launcher.py:1: SettingWithCopyWarning: \n",
      "A value is trying to be set on a copy of a slice from a DataFrame.\n",
      "Try using .loc[row_indexer,col_indexer] = value instead\n",
      "\n",
      "See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy\n",
      "  \"\"\"Entry point for launching an IPython kernel.\n"
     ]
    },
    {
     "data": {
      "text/plain": [
       "array([ 2,  4,  3,  6,  1,  8,  7,  5, 11,  9, 27, 10, 19, 16, 43, 14, 12,\n",
       "       13, 18], dtype=int64)"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df3['bhk'] = df3['size'].apply(lambda x: int(x.split(' ')[0]))\n",
    "df3.bhk.unique()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Explore total_sqft feature**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [],
   "source": [
    "def is_float(x):\n",
    "    try:\n",
    "        float(x)\n",
    "    except:\n",
    "        return False\n",
    "    return True"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "5"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "2+3"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>30</th>\n",
       "      <td>Yelahanka</td>\n",
       "      <td>4 BHK</td>\n",
       "      <td>2100 - 2850</td>\n",
       "      <td>4.0</td>\n",
       "      <td>186.000</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>122</th>\n",
       "      <td>Hebbal</td>\n",
       "      <td>4 BHK</td>\n",
       "      <td>3067 - 8156</td>\n",
       "      <td>4.0</td>\n",
       "      <td>477.000</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>137</th>\n",
       "      <td>8th Phase JP Nagar</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1042 - 1105</td>\n",
       "      <td>2.0</td>\n",
       "      <td>54.005</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>165</th>\n",
       "      <td>Sarjapur</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1145 - 1340</td>\n",
       "      <td>2.0</td>\n",
       "      <td>43.490</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>188</th>\n",
       "      <td>KR Puram</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1015 - 1540</td>\n",
       "      <td>2.0</td>\n",
       "      <td>56.800</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>410</th>\n",
       "      <td>Kengeri</td>\n",
       "      <td>1 BHK</td>\n",
       "      <td>34.46Sq. Meter</td>\n",
       "      <td>1.0</td>\n",
       "      <td>18.500</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>549</th>\n",
       "      <td>Hennur Road</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1195 - 1440</td>\n",
       "      <td>2.0</td>\n",
       "      <td>63.770</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>648</th>\n",
       "      <td>Arekere</td>\n",
       "      <td>9 Bedroom</td>\n",
       "      <td>4125Perch</td>\n",
       "      <td>9.0</td>\n",
       "      <td>265.000</td>\n",
       "      <td>9</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>661</th>\n",
       "      <td>Yelahanka</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1120 - 1145</td>\n",
       "      <td>2.0</td>\n",
       "      <td>48.130</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>672</th>\n",
       "      <td>Bettahalsoor</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>3090 - 5002</td>\n",
       "      <td>4.0</td>\n",
       "      <td>445.000</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               location       size      total_sqft  bath    price  bhk\n",
       "30            Yelahanka      4 BHK     2100 - 2850   4.0  186.000    4\n",
       "122              Hebbal      4 BHK     3067 - 8156   4.0  477.000    4\n",
       "137  8th Phase JP Nagar      2 BHK     1042 - 1105   2.0   54.005    2\n",
       "165            Sarjapur      2 BHK     1145 - 1340   2.0   43.490    2\n",
       "188            KR Puram      2 BHK     1015 - 1540   2.0   56.800    2\n",
       "410             Kengeri      1 BHK  34.46Sq. Meter   1.0   18.500    1\n",
       "549         Hennur Road      2 BHK     1195 - 1440   2.0   63.770    2\n",
       "648             Arekere  9 Bedroom       4125Perch   9.0  265.000    9\n",
       "661           Yelahanka      2 BHK     1120 - 1145   2.0   48.130    2\n",
       "672        Bettahalsoor  4 Bedroom     3090 - 5002   4.0  445.000    4"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df3[~df3['total_sqft'].apply(is_float)].head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Above shows that total_sqft can be a range (e.g. 2100-2850). For such case we can just take average of min and max value in the range. There are other cases such as 34.46Sq. Meter which one can convert to square ft using unit conversion. I am going to just drop such corner cases to keep things simple**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [],
   "source": [
    "def convert_sqft_to_num(x):\n",
    "    tokens = x.split('-')\n",
    "    if len(tokens) == 2:\n",
    "        return (float(tokens[0])+float(tokens[1]))/2\n",
    "    try:\n",
    "        return float(x)\n",
    "    except:\n",
    "        return None   "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Electronic City Phase II</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1056.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>39.07</td>\n",
       "      <td>2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Chikka Tirupathi</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>2600.0</td>\n",
       "      <td>5.0</td>\n",
       "      <td>120.00</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   location       size  total_sqft  bath   price  bhk\n",
       "0  Electronic City Phase II      2 BHK      1056.0   2.0   39.07    2\n",
       "1          Chikka Tirupathi  4 Bedroom      2600.0   5.0  120.00    4"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df4 = df3.copy()\n",
    "df4.total_sqft = df4.total_sqft.apply(convert_sqft_to_num)\n",
    "df4 = df4[df4.total_sqft.notnull()]\n",
    "df4.head(2)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**For below row, it shows total_sqft as 2475 which is an average of the range 2100-2850**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "location      Yelahanka\n",
       "size              4 BHK\n",
       "total_sqft         2475\n",
       "bath                  4\n",
       "price               186\n",
       "bhk                   4\n",
       "Name: 30, dtype: object"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df4.loc[30]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "2475.0"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "(2100+2850)/2"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style=\"color:blue\">Feature Engineering</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Add new feature called price per square feet**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "scrolled": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Electronic City Phase II</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1056.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>39.07</td>\n",
       "      <td>2</td>\n",
       "      <td>3699.810606</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Chikka Tirupathi</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>2600.0</td>\n",
       "      <td>5.0</td>\n",
       "      <td>120.00</td>\n",
       "      <td>4</td>\n",
       "      <td>4615.384615</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Uttarahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1440.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>62.00</td>\n",
       "      <td>3</td>\n",
       "      <td>4305.555556</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Lingadheeranahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1521.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>95.00</td>\n",
       "      <td>3</td>\n",
       "      <td>6245.890861</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Kothanur</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1200.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>51.00</td>\n",
       "      <td>2</td>\n",
       "      <td>4250.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   location       size  total_sqft  bath   price  bhk  \\\n",
       "0  Electronic City Phase II      2 BHK      1056.0   2.0   39.07    2   \n",
       "1          Chikka Tirupathi  4 Bedroom      2600.0   5.0  120.00    4   \n",
       "2               Uttarahalli      3 BHK      1440.0   2.0   62.00    3   \n",
       "3        Lingadheeranahalli      3 BHK      1521.0   3.0   95.00    3   \n",
       "4                  Kothanur      2 BHK      1200.0   2.0   51.00    2   \n",
       "\n",
       "   price_per_sqft  \n",
       "0     3699.810606  \n",
       "1     4615.384615  \n",
       "2     4305.555556  \n",
       "3     6245.890861  \n",
       "4     4250.000000  "
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5 = df4.copy()\n",
    "df5['price_per_sqft'] = df5['price']*100000/df5['total_sqft']\n",
    "df5.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    1.320000e+04\n",
       "mean     7.920759e+03\n",
       "std      1.067272e+05\n",
       "min      2.678298e+02\n",
       "25%      4.267701e+03\n",
       "50%      5.438331e+03\n",
       "75%      7.317073e+03\n",
       "max      1.200000e+07\n",
       "Name: price_per_sqft, dtype: float64"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5_stats = df5['price_per_sqft'].describe()\n",
    "df5_stats"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 69,
   "metadata": {},
   "outputs": [],
   "source": [
    "df5.to_csv(\"bhp.csv\",index=False)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Examine locations which is a categorical variable. We need to apply dimensionality reduction technique here to reduce number of locations**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Whitefield                                         533\n",
       "Sarjapur  Road                                     392\n",
       "Electronic City                                    304\n",
       "Kanakpura Road                                     264\n",
       "Thanisandra                                        235\n",
       "Yelahanka                                          210\n",
       "Uttarahalli                                        186\n",
       "Hebbal                                             176\n",
       "Marathahalli                                       175\n",
       "Raja Rajeshwari Nagar                              171\n",
       "Bannerghatta Road                                  151\n",
       "Hennur Road                                        150\n",
       "7th Phase JP Nagar                                 148\n",
       "Haralur Road                                       141\n",
       "Electronic City Phase II                           131\n",
       "Rajaji Nagar                                       106\n",
       "Chandapura                                          98\n",
       "Bellandur                                           96\n",
       "KR Puram                                            88\n",
       "Hoodi                                               88\n",
       "Electronics City Phase 1                            87\n",
       "Yeshwanthpur                                        85\n",
       "Begur Road                                          84\n",
       "Sarjapur                                            80\n",
       "Kasavanhalli                                        79\n",
       "Harlur                                              79\n",
       "Hormavu                                             74\n",
       "Banashankari                                        74\n",
       "Ramamurthy Nagar                                    72\n",
       "Koramangala                                         72\n",
       "                                                  ... \n",
       "Ckikkakammana Halli                                  1\n",
       "Neelasandra                                          1\n",
       "Gangondanahalli                                      1\n",
       "Agara Village                                        1\n",
       "Sundara Nagar                                        1\n",
       "Binny Mills Employees Colony                         1\n",
       "Adugodi                                              1\n",
       "Uvce Layout                                          1\n",
       "Kenchanehalli R R Nagar                              1\n",
       "Whietfield,                                          1\n",
       "manyata                                              1\n",
       "Air View Colony                                      1\n",
       "Thavarekere                                          1\n",
       "Muthyala Nagar                                       1\n",
       "Haralur Road,                                        1\n",
       "Manonarayanapalya                                    1\n",
       "GKW Layout                                           1\n",
       "Marathalli bridge                                    1\n",
       "Banashankari 6th Stage ,Subramanyapura               1\n",
       "anjananager magdi road                               1\n",
       "akshaya nagar t c palya                              1\n",
       "Indiranagar HAL 2nd Stage                            1\n",
       "Maruthi HBCS Layout                                  1\n",
       "Gopal Reddy Layout                                   1\n",
       "High grounds                                         1\n",
       "CMH Road                                             1\n",
       "Chambenahalli                                        1\n",
       "Sarvobhogam Nagar                                    1\n",
       "Ex-Servicemen Colony Dinnur Main Road R.T.Nagar      1\n",
       "Bilal Nagar                                          1\n",
       "Name: location, Length: 1287, dtype: int64"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5.location = df5.location.apply(lambda x: x.strip())\n",
    "location_stats = df5['location'].value_counts(ascending=False)\n",
    "location_stats"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "13200"
      ]
     },
     "execution_count": 23,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "location_stats.values.sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "240"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(location_stats[location_stats>10])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1287"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(location_stats)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1047"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(location_stats[location_stats<=10])"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style=\"color:blue\">Dimensionality Reduction</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Any location having less than 10 data points should be tagged as \"other\" location. This way number of categories can be reduced by huge amount. Later on when we do one hot encoding, it will help us with having fewer dummy columns**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "BTM 1st Stage                                      10\n",
       "Sector 1 HSR Layout                                10\n",
       "Ganga Nagar                                        10\n",
       "Naganathapura                                      10\n",
       "1st Block Koramangala                              10\n",
       "Thyagaraja Nagar                                   10\n",
       "Dairy Circle                                       10\n",
       "Nagadevanahalli                                    10\n",
       "Sadashiva Nagar                                    10\n",
       "Gunjur Palya                                       10\n",
       "Dodsworth Layout                                   10\n",
       "Basapura                                           10\n",
       "Kalkere                                            10\n",
       "Nagappa Reddy Layout                               10\n",
       "2nd Phase JP Nagar                                  9\n",
       "Yemlur                                              9\n",
       "Medahalli                                           9\n",
       "Kaverappa Layout                                    9\n",
       "Ejipura                                             9\n",
       "Mathikere                                           9\n",
       "Lingarajapuram                                      9\n",
       "Peenya                                              9\n",
       "Vignana Nagar                                       9\n",
       "B Narayanapura                                      9\n",
       "Chandra Layout                                      9\n",
       "Jakkur Plantation                                   9\n",
       "Banagiri Nagar                                      9\n",
       "Chennammana Kere                                    9\n",
       "Richmond Town                                       9\n",
       "Vishwanatha Nagenahalli                             9\n",
       "                                                   ..\n",
       "Ckikkakammana Halli                                 1\n",
       "Neelasandra                                         1\n",
       "Gangondanahalli                                     1\n",
       "Agara Village                                       1\n",
       "Sundara Nagar                                       1\n",
       "Binny Mills Employees Colony                        1\n",
       "Adugodi                                             1\n",
       "Uvce Layout                                         1\n",
       "Kenchanehalli R R Nagar                             1\n",
       "Whietfield,                                         1\n",
       "manyata                                             1\n",
       "Air View Colony                                     1\n",
       "Thavarekere                                         1\n",
       "Muthyala Nagar                                      1\n",
       "Haralur Road,                                       1\n",
       "Manonarayanapalya                                   1\n",
       "GKW Layout                                          1\n",
       "Marathalli bridge                                   1\n",
       "Banashankari 6th Stage ,Subramanyapura              1\n",
       "anjananager magdi road                              1\n",
       "akshaya nagar t c palya                             1\n",
       "Indiranagar HAL 2nd Stage                           1\n",
       "Maruthi HBCS Layout                                 1\n",
       "Gopal Reddy Layout                                  1\n",
       "High grounds                                        1\n",
       "CMH Road                                            1\n",
       "Chambenahalli                                       1\n",
       "Sarvobhogam Nagar                                   1\n",
       "Ex-Servicemen Colony Dinnur Main Road R.T.Nagar     1\n",
       "Bilal Nagar                                         1\n",
       "Name: location, Length: 1047, dtype: int64"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "location_stats_less_than_10 = location_stats[location_stats<=10]\n",
    "location_stats_less_than_10"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "1287"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(df5.location.unique())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "241"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5.location = df5.location.apply(lambda x: 'other' if x in location_stats_less_than_10 else x)\n",
    "len(df5.location.unique())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Electronic City Phase II</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1056.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>39.07</td>\n",
       "      <td>2</td>\n",
       "      <td>3699.810606</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Chikka Tirupathi</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>2600.0</td>\n",
       "      <td>5.0</td>\n",
       "      <td>120.00</td>\n",
       "      <td>4</td>\n",
       "      <td>4615.384615</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Uttarahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1440.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>62.00</td>\n",
       "      <td>3</td>\n",
       "      <td>4305.555556</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Lingadheeranahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1521.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>95.00</td>\n",
       "      <td>3</td>\n",
       "      <td>6245.890861</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Kothanur</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1200.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>51.00</td>\n",
       "      <td>2</td>\n",
       "      <td>4250.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5</th>\n",
       "      <td>Whitefield</td>\n",
       "      <td>2 BHK</td>\n",
       "      <td>1170.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>38.00</td>\n",
       "      <td>2</td>\n",
       "      <td>3247.863248</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6</th>\n",
       "      <td>Old Airport Road</td>\n",
       "      <td>4 BHK</td>\n",
       "      <td>2732.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>204.00</td>\n",
       "      <td>4</td>\n",
       "      <td>7467.057101</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>7</th>\n",
       "      <td>Rajaji Nagar</td>\n",
       "      <td>4 BHK</td>\n",
       "      <td>3300.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>600.00</td>\n",
       "      <td>4</td>\n",
       "      <td>18181.818182</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8</th>\n",
       "      <td>Marathahalli</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1310.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>63.25</td>\n",
       "      <td>3</td>\n",
       "      <td>4828.244275</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>other</td>\n",
       "      <td>6 Bedroom</td>\n",
       "      <td>1020.0</td>\n",
       "      <td>6.0</td>\n",
       "      <td>370.00</td>\n",
       "      <td>6</td>\n",
       "      <td>36274.509804</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                   location       size  total_sqft  bath   price  bhk  \\\n",
       "0  Electronic City Phase II      2 BHK      1056.0   2.0   39.07    2   \n",
       "1          Chikka Tirupathi  4 Bedroom      2600.0   5.0  120.00    4   \n",
       "2               Uttarahalli      3 BHK      1440.0   2.0   62.00    3   \n",
       "3        Lingadheeranahalli      3 BHK      1521.0   3.0   95.00    3   \n",
       "4                  Kothanur      2 BHK      1200.0   2.0   51.00    2   \n",
       "5                Whitefield      2 BHK      1170.0   2.0   38.00    2   \n",
       "6          Old Airport Road      4 BHK      2732.0   4.0  204.00    4   \n",
       "7              Rajaji Nagar      4 BHK      3300.0   4.0  600.00    4   \n",
       "8              Marathahalli      3 BHK      1310.0   3.0   63.25    3   \n",
       "9                     other  6 Bedroom      1020.0   6.0  370.00    6   \n",
       "\n",
       "   price_per_sqft  \n",
       "0     3699.810606  \n",
       "1     4615.384615  \n",
       "2     4305.555556  \n",
       "3     6245.890861  \n",
       "4     4250.000000  \n",
       "5     3247.863248  \n",
       "6     7467.057101  \n",
       "7    18181.818182  \n",
       "8     4828.244275  \n",
       "9    36274.509804  "
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5.head(10)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style=\"color:blue\">Outlier Removal Using Business Logic</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**As a data scientist when you have a conversation with your business manager (who has expertise in real estate), he will tell you that normally square ft per bedroom is 300 (i.e. 2 bhk apartment is minimum 600 sqft. If you have for example 400 sqft apartment with 2 bhk than that seems suspicious and can be removed as an outlier. We will remove such outliers by keeping our minimum thresold per bhk to be 300 sqft**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>9</th>\n",
       "      <td>other</td>\n",
       "      <td>6 Bedroom</td>\n",
       "      <td>1020.0</td>\n",
       "      <td>6.0</td>\n",
       "      <td>370.0</td>\n",
       "      <td>6</td>\n",
       "      <td>36274.509804</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>45</th>\n",
       "      <td>HSR Layout</td>\n",
       "      <td>8 Bedroom</td>\n",
       "      <td>600.0</td>\n",
       "      <td>9.0</td>\n",
       "      <td>200.0</td>\n",
       "      <td>8</td>\n",
       "      <td>33333.333333</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>58</th>\n",
       "      <td>Murugeshpalya</td>\n",
       "      <td>6 Bedroom</td>\n",
       "      <td>1407.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>150.0</td>\n",
       "      <td>6</td>\n",
       "      <td>10660.980810</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>68</th>\n",
       "      <td>Devarachikkanahalli</td>\n",
       "      <td>8 Bedroom</td>\n",
       "      <td>1350.0</td>\n",
       "      <td>7.0</td>\n",
       "      <td>85.0</td>\n",
       "      <td>8</td>\n",
       "      <td>6296.296296</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>70</th>\n",
       "      <td>other</td>\n",
       "      <td>3 Bedroom</td>\n",
       "      <td>500.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>100.0</td>\n",
       "      <td>3</td>\n",
       "      <td>20000.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               location       size  total_sqft  bath  price  bhk  \\\n",
       "9                 other  6 Bedroom      1020.0   6.0  370.0    6   \n",
       "45           HSR Layout  8 Bedroom       600.0   9.0  200.0    8   \n",
       "58        Murugeshpalya  6 Bedroom      1407.0   4.0  150.0    6   \n",
       "68  Devarachikkanahalli  8 Bedroom      1350.0   7.0   85.0    8   \n",
       "70                other  3 Bedroom       500.0   3.0  100.0    3   \n",
       "\n",
       "    price_per_sqft  \n",
       "9     36274.509804  \n",
       "45    33333.333333  \n",
       "58    10660.980810  \n",
       "68     6296.296296  \n",
       "70    20000.000000  "
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5[df5.total_sqft/df5.bhk<300].head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Check above data points. We have 6 bhk apartment with 1020 sqft. Another one is 8 bhk and total sqft is 600. These are clear data errors that can be removed safely**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(13200, 7)"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df5.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(12456, 7)"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df6 = df5[~(df5.total_sqft/df5.bhk<300)]\n",
    "df6.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Outlier Removal Using Standard Deviation and Mean</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count     12456.000000\n",
       "mean       6308.502826\n",
       "std        4168.127339\n",
       "min         267.829813\n",
       "25%        4210.526316\n",
       "50%        5294.117647\n",
       "75%        6916.666667\n",
       "max      176470.588235\n",
       "Name: price_per_sqft, dtype: float64"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df6.price_per_sqft.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Here we find that min price per sqft is 267 rs/sqft whereas max is 12000000, this shows a wide variation in property prices. We should remove outliers per location using mean and one standard deviation**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(10242, 7)"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "def remove_pps_outliers(df):\n",
    "    df_out = pd.DataFrame()\n",
    "    for key, subdf in df.groupby('location'):\n",
    "        m = np.mean(subdf.price_per_sqft)\n",
    "        st = np.std(subdf.price_per_sqft)\n",
    "        reduced_df = subdf[(subdf.price_per_sqft>(m-st)) & (subdf.price_per_sqft<=(m+st))]\n",
    "        df_out = pd.concat([df_out,reduced_df],ignore_index=True)\n",
    "    return df_out\n",
    "df7 = remove_pps_outliers(df6)\n",
    "df7.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Let's check if for a given location how does the 2 BHK and 3 BHK property prices look like**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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npdf/MVfzIMf/OBlz1kc9fzCF76Q+fn5vOc977n32Jve9Kbccsst934tddlll+VRj3pUbrjhhvMrEgAAWBfWbfA7ePC+Tt+J5ueT2dlzf++77rorz3ve8/KCF7wgz33uc894/oUXXphnPOMZ+fCHPzzQ+3/DN3xD3ve+9+XXf/3X8+53v/vcCwUAANaFdXuN35YtvWv6lgt/ExPJ5s3n9r6ttezYsSNXX311du7cOfBrPvrRj5400nk6l112Wd7//vdneno6l156aZ7+9KefW8EAAEDnrduO38xMsuEUP/2GDb3j5+IjH/lI3vWud+WDH/zgvdfn7dmzZ9lzF6/xu/baa3P33XfnJ3/yJ8/qs6666qrceOONefGLX5ybbrrp3AoGAAA6r1pro67hnE1NTbUDBw7cb+3WW2/N1VdfPdDrl9vVc8OG89vVcy05m98FAAAwfqrq5tba1JnOW7ejnkkv3B050tvIZXa2N945M5P075UOAADQCes6+CW9kLdjx6irAAAAGJ51e40fAADAeiH4AQAAdJzgBwAAdN70rulM75oedRkjI/gBAAB0nOC3wo4fP54nPelJefzjH5/HPvaxec1rXrPsedddd12uuuqqbN26NY95zGPyute97t5j09PTWXqbittuuy3XXnttkmTv3r151rOede+xf/2v/3We/vSn52tf+9qQfiIAAGDcrftdPZPc2/Lde93e836viy66KB/84AezcePG3HXXXdm2bVue+cxn5ilPecpJ577pTW/K85///Bw/fjzXXHNNfvRHfzRXXXXVwJ/1hje8IR/5yEeyZ8+eXHTRReddOwAAdMnS0c59h/adtLYS//t/XAh+K6yqsrF/I8C77rord911V6rqtK85fvx4kmRiYmLgz3nzm9+cPXv25A/+4A/yoAc96NwLBgAAOk/wG4J77rkn3/Ed35HZ2dm89KUvzZOf/ORlz3vlK1+Z17/+9Zmdnc3LXvayPOxhD7v32Ate8IJ7A93Xv/71bNhw31TuRz7ykXzuc5/LzTfffG/IBAAA7m9pR28lp/zG0boNfsNs+z7gAQ/ILbfcki9/+ct5znOek09/+tP3XqO31OKo57Fjx/I93/M9+ehHP5rv/M7vTJK8+93vztTUVJLeNX5Lr+vbvHlz7rjjjnzgAx/I85///HOuEwAAWB9s7jJEl1xySaanp/P+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\n",
      "text/plain": [
       "<Figure size 1080x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "def plot_scatter_chart(df,location):\n",
    "    bhk2 = df[(df.location==location) & (df.bhk==2)]\n",
    "    bhk3 = df[(df.location==location) & (df.bhk==3)]\n",
    "    matplotlib.rcParams['figure.figsize'] = (15,10)\n",
    "    plt.scatter(bhk2.total_sqft,bhk2.price,color='blue',label='2 BHK', s=50)\n",
    "    plt.scatter(bhk3.total_sqft,bhk3.price,marker='+', color='green',label='3 BHK', s=50)\n",
    "    plt.xlabel(\"Total Square Feet Area\")\n",
    "    plt.ylabel(\"Price (Lakh Indian Rupees)\")\n",
    "    plt.title(location)\n",
    "    plt.legend()\n",
    "    \n",
    "plot_scatter_chart(df7,\"Rajaji Nagar\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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r3rVMX3XWWedlSuuuCIvf/nL8/nPf/74CgYAADqvWmuTruG4TU9Pt127dt3n2LXXXptzzjlnqPfPt6rnmjUntqrncnIs/xYAAMDKU1VXt9amj3bdqh31THrh7oYbegu57N3bG+/csiXp75UOAADQCas6+CW9kHfBBZOuAgAAYHxW7T1+AAAAq4XgBwAAsICZrTOZ2Toz6TJOmOAHAADQcYIfAABAxwl+I3bgwIH86I/+aJ785Cfn8Y9/fN7whjfMe93555+fs846K5s2bcpjH/vYvOlNb7r33MzMTAa3qbjuuuvyhCc8IUmyffv2PO95z7v33C//8i/n2c9+du64444x/SIAAFhd5sY7Z7bOZMf1O7Lj+h33ObYSCX4Z7dzuKaeckk9+8pP50pe+lN27d+ejH/1orrrqqnmvfetb35rdu3dn9+7dufzyy/ONb3zjmL7rzW9+cz7zmc/kQx/6UE455ZRRlA8AAHTQqt/OYdSqKuv7GwHeddddueuuu1JVi77nwIEDSZJ169YN/T1ve9vbcuWVV+bP//zPc//73//4CwYAAO5j+/nb730+1yAaPLYSCX5jcM899+RHfuRHsnfv3lx44YV52tOeNu91r3vd6/Jrv/Zr2bt3b1796lfnYQ972L3nXvrSl94b6O68886sWXOoOfuZz3wmX/va13L11VffGzIBAAAWsmqD3+Bo547rdxxx7EQS/UknnZTdu3fn1ltvzU//9E/nq1/96r336A1661vfmhe/+MW57bbb8qxnPSuf/exn82M/9mNJkg984AOZnp5O0rvHb/C+vrPPPju33HJLPvaxj+XFL37xcdcJAACsDu7xG6NTTz01MzMz+ehHP7rodevXr8/MzEx27tw51Od+//d/f6688sq89rWvzac+9alRlAoAAMxj+/nbV/yYZ7KKO37jmtu9+eabc/LJJ+fUU0/N7bffno9//ON5/etfv+h77r777nz+85/PL/7iLw79PY9+9KPzx3/8x3nBC16QP/uzP8umTZtOtHQAAKCjdPxG7MYbb8y5556bJz3pSXnqU5+an/iJn7jPmOag173uddm0aVOe9KQn5YlPfGJe+MIXHtN3PfWpT83v/d7v5ad+6qfyN3/zN6MoHwAA6KBqrU26huM2PT3dBve7S5Jrr70255xzzjF9TldW6jnc8fxbAAAAK0dVXd1amz7a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\n",
      "text/plain": [
       "<Figure size 1080x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plot_scatter_chart(df7,\"Hebbal\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**We should also remove properties where for same location, the price of (for example) 3 bedroom apartment is less than 2 bedroom apartment (with same square ft area). What we will do is for a given location, we will build a dictionary of stats per bhk, i.e.**\n",
    "```\n",
    "{\n",
    "    '1' : {\n",
    "        'mean': 4000,\n",
    "        'std: 2000,\n",
    "        'count': 34\n",
    "    },\n",
    "    '2' : {\n",
    "        'mean': 4300,\n",
    "        'std: 2300,\n",
    "        'count': 22\n",
    "    },    \n",
    "}\n",
    "```\n",
    "**Now we can remove those 2 BHK apartments whose price_per_sqft is less than mean price_per_sqft of 1 BHK apartment**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(7317, 7)"
      ]
     },
     "execution_count": 38,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "def remove_bhk_outliers(df):\n",
    "    exclude_indices = np.array([])\n",
    "    for location, location_df in df.groupby('location'):\n",
    "        bhk_stats = {}\n",
    "        for bhk, bhk_df in location_df.groupby('bhk'):\n",
    "            bhk_stats[bhk] = {\n",
    "                'mean': np.mean(bhk_df.price_per_sqft),\n",
    "                'std': np.std(bhk_df.price_per_sqft),\n",
    "                'count': bhk_df.shape[0]\n",
    "            }\n",
    "        for bhk, bhk_df in location_df.groupby('bhk'):\n",
    "            stats = bhk_stats.get(bhk-1)\n",
    "            if stats and stats['count']>5:\n",
    "                exclude_indices = np.append(exclude_indices, bhk_df[bhk_df.price_per_sqft<(stats['mean'])].index.values)\n",
    "    return df.drop(exclude_indices,axis='index')\n",
    "df8 = remove_bhk_outliers(df7)\n",
    "# df8 = df7.copy()\n",
    "df8.shape"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Plot same scatter chart again to visualize price_per_sqft for 2 BHK and 3 BHK properties**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAA34AAAJcCAYAAACmOnadAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDMuMC4zLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvnQurowAAIABJREFUeJzs3XuUpWddJ/rvr0lIsLowSALEBCbRbiQhQovFZbRnKFAHaFGuTnmGMxLoGbzgIPQMA8yaI+DALEYGET1eJooEOCiVg7ccbRAVupkGCdORyC3DdKmJaRsnLQRSXRJIUs/5Y+9KVzrV3bu7a9eu/dbns9Zeu/bzvu/ev917scJ3/Z73eaq1FgAAALpr06gLAAAAYLgEPwAAgI4T/AAAADpO8AMAAOg4wQ8AAKDjBD8AAICOE/wA2DCq6hFVdaSq7jfAuf+kqj6/7PVnq2p6qAUCwJCUffwAGCdVdVOShya5O8mRJB9I8pOttSMjrOnqJC9M8sTW2if6Y1uSHGit1ajqAoAlOn4AjKMfaK1tTrItyXckec2I60mSLyV5w6iLqKqzRl0DAOuP4AfA2Gqt/V2SP0ovACZJqur7q+qTVXV7Vd1SVa9bduySqmpL4aiqXlRVN1bVfFX9VVX96LJzp6vq4LLXN1XV956gnHcmeUxVPXmlgyf6rP7xf19VX6iqQ1X1r/p1bjmF77Szqv4myYcG+scDYEMR/AAYW1V1cZJnJJlbNryQ5EeSnJfk+5P8eFU9+zhvcWuSZyZ5YJIXJXlrVT3uNMv5hyT/OckbT/WzqurpSXYl+d4kW5IcGx4H+U5PTnJZkqedZv0AdJjgB8A4+r2qmk9yS3qB6rVLB1pre1prn26tLbbWPpXkt3LfILV07h+21v6y9exN8sEk/+QM6vpvSR5RVc84xc/650ne0Vr7bGvtH5K8/phrB/lOr2utLbTWvnoG9QPQUYIfAOPo2a21ySTTSR6V5PylA1X1xKr6cFUdrqqvJPmx5ceXq6pnVNXHq+pLVfXlJDuOd+4gWmtfS/Kf+o97Lepyks/65vRC7JJbjrl2kO90SwDgOAQ/AMZWv3N2dZL/umz4N5Ncm+ThrbVvTPKrOSaEJUlVnZPkt/vXPrS1dl6S3Sude4rekeQbkzznFD7rC0kuXvYeDz/mPQf5TpbpBuC4BD8Axt3PJ/m+qlpa4GUyyZdaa3dU1ROS/IvjXHf/JOckOZzkrv70zH92psW01u5K8rokrzqFz7omyYuq6rKq+oYkP33M2w76nQBgRYIfAGOttXY4ybuS/F/9oZ9I8jP9ewB/Or1QtdJ180le1j9+W3ph6tpVKuu30uviDfRZrbX3J/mFJB9Ob6GaP+sf+tqpfCcAOB4buAOwYVTVtyQ5kOSsdpL/AFbVU5P8emvtW9akuHt/9mVJPpPknH4HEQDOiI4fABvJFUluOlnoW3buXw+5nntU1XOq6v5V9aAk/yXJ/yf0AbBaBD8ANoSq2pXkqiSvHuDctyV5RY7ZVmHIfjS9ewD/MsndSX58DT8bgI4z1RMAAKDjdPwAAAA67qxRF3Amzj///HbJJZeMugwAAICRuP766/++tXbByc4b6+B3ySWXZP/+/aMuAwAAYCSq6uZBzjPVEwAAoOMEPwAAgI4T/AAAADpurO/xW8mdd96ZgwcP5o477hh1KSN17rnn5uKLL87ZZ5896lIAAIAR61zwO3jwYCYnJ3PJJZekqkZdzki01vLFL34xBw8ezKWXXjrqcgAAgBHr3FTPO+64Iw9+8IM3bOhLkqrKgx/84A3f9QQAAHo6F/ySbOjQt8S/AQAAsKSTwQ8AAICjBL9Vdsstt+QpT3lKLrvssjz60Y/O2972thXPe93rXpeLLroo27Zty6Me9aj8+I//eBYXF5MkV155Zd73vvfd6/zNmzcnSW666aZcccUV94z/2q/9Wh73uMfltttuG9I3AgAAxt2GD37z88mv/3ryqlf1nufnz+z9zjrrrLzlLW/JjTfemI9//OP5pV/6pXzuc59b8dxXvOIVueGGG/K5z30un/70p7N3795T+qx3v/vd+cVf/MV88IMfzIMe9KAzKxwAAOiszq3qeSr27Ut27EgWF5OFhWRiItm1K9m9O9m+/fTe88ILL8yFF16YJJmcnMxll12Wv/3bv83ll19+3Gu+/vWv54477jil8HbNNdfkTW96U/70T/80559//ukVCwAAbAgbtuM3P98LffPzvdCX9J6Xxo8cOfPPuOmmm/LJT34yT3ziE1c8/ta3vjXbtm3LhRdemEc+8pHZtm3bPcde+cpXZtu2bfc8lrv55pvzkz/5k/ngBz+Yhz3sYWdeKAAA0GkbNvjNzvY6fStZXOwdPxNHjhzJ8573vPz8z/98HvjAB654ztJUz1tvvTULCwt573vfe8+xN7/5zbnhhhvueSx3wQUX5BGPeESuueaaMysSAADYEDZs8Dtw4Gin71gLC8nc3Om/95133pnnPe95ecELXpDnPve5Jz3/7LPPztOf/vR85CMfGej9v+EbviHvf//786u/+qt5z3vec/qFAgAAG8KGvcdv69bePX0rhb+JiWTLltN739Zadu7cmcsuuyy7du0a+JqPfexj95nSeSIXXHBBPvCBD2R6ejrnn39+nva0p51ewQAAQOdt2I7fzEyy6TjfftOm3vHT8dGPfjTvfve786EPfeie+/N279694rlL9/hdccUVueuuu/ITP/ETp/RZl156aa699tq8+MUvznXXXXd6BQMAAJ1XrbVR13Dapqam2v79++81duONN+ayyy4b6PqVVvXctOnMVvVcT07l3wIAABg/VXV9a23qZOdt2KmeSS/cHTrUW8hlbq43vXNmJunvlQ4AANAJGzr4Jb2Qt3PnqKsAAAAYng17jx8AAMBGIfgBAAB0nOAHAAB03vTV05m+enrUZYyM4AcAANBxgt8qu+OOO/KEJzwhj33sY/PoRz86r33ta1c878orr8yll16abdu25VGPelRe//rX33Nseno6y7epuOmmm3LFFVckSfbs2ZNnPvOZ9xz7j//xP+ZpT3tavva1rw3pGwEAAONuw6/qmeSelu+eK/ec8Xudc845+dCHPpTNmzfnzjvvzPbt2/OMZzwjT3rSk+5z7pvf/OY8//nPzx133JHLL788P/IjP5JLL7104M964xvfmI9+9KPZvXt3zjnnnDOuHQAAumT51M69N++9z9hq/P//cSH4rbKqyub+RoB33nln7rzzzlTVCa+54447kiQTExMDf85b3vKW7N69O3/0R3+UBzzgAadfMAAA0HmC3xDcfffd+c7v/M7Mzc3lpS99aZ74xCeueN4rX/nKvOENb8jc3Fxe9rKX5SEPecg9x17wghfcE+i+/vWvZ9Omo7NyP/rRj+bzn/98rr/++ntCJgAAcG/LO3qrOctvHG3Y4DfMtu/97ne/3HDDDfnyl7+c5zznOfnMZz5zzz16yy1N9Txy5Ei+53u+Jx/72MfyXd/1XUmS97znPZmamkrSu8dv+X19W7ZsyW233ZYPfvCDef7zn3/adQIAABuDxV2G6Lzzzsv09HQ+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\n",
      "text/plain": [
       "<Figure size 1080x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plot_scatter_chart(df8,\"Rajaji Nagar\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "image/png": "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TjvttFx++eV58YtfnC996UtHVjAAANB51VobdQ1HbHx8vG3fvv1+Y9ddd13OOOOMgT4/06qeq1bNb1XPpeRw/i0AAIDlp6qubq2NH+q8FTvVM+mFu5tu6i3ksmtXb3rnpk1Jf690AACATljRwS/phbzzzx91FQAAAMOzYu/xAwAAWCkEPwAAgFlMXDqRiUsnRl3GvAl+AAAAHSf4AQAAdJzgt8D27t2bJz3pSXnCE56Qxz72sXnd614343nnnXdeTjvttGzYsCGPecxj8oY3vOG+YxMTE5m+TcX111+fxz3ucUmSLVu25DnPec59x37/938/z3zmM3PnnXcO6RcBAMDKMjW9c+LSiWy9YWu23rD1fmPLkeCXhZ23e8wxx+Szn/1svvrVr2bHjh258sorc9VVV8147lve8pbs2LEjO3bsyGWXXZZvf/vbh/Vdb3rTm/KFL3whH/3oR3PMMccsRPkAAEAHrfjtHBZaVWVdfyPAu+++O3fffXeqas7P7N27N0mydu3agb/nrW99a6644or87d/+bR7wgAccecEAAMD9bDlvy32vpxpE08eWI8FvCO6999784i/+Ynbt2pULLrggT37yk2c879WvfnX+8A//MLt27corXvGKPPShD73v2Ite9KL7At1dd92VVav2N2e/8IUv5Jvf/Gauvvrq+0ImAADAbFZs8Js+tXPrDVsPGptPoj/qqKOyY8eO3H777fn1X//1XHPNNffdozfdW97ylrzwhS/M7t2784xnPCNf/OIX89SnPjVJ8sEPfjDj4+NJevf4Tb+v7/TTT89tt92WT37yk3nhC194xHUCAAArg3v8hui4447LxMRErrzyyjnPW7duXSYmJrJt27aBrvuwhz0sV1xxRV71qlflc5/73EKUCgAAzGDLeVuW/TTPZAV3/IY1b/fWW2/N6tWrc9xxx+UnP/lJPv3pT+c1r3nNnJ+555578qUvfSn/4T/8h4G/51GPelT+6q/+Ks973vPy8Y9/PBs2bJhv6QAAQEfp+C2wm2++OWeffXYe//jH56yzzsqv/Mqv3G+a5nSvfvWrs2HDhjz+8Y/Pz//8z+f5z3/+YX3XWWedlT//8z/Pr/3ar+Uf//EfF6J8AACgg6q1Nuoajtj4+Hibvt9dklx33XU544wzDus6XVmp50BH8m8BAAAsH1V1dWtt/FDnrdipntN1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\n",
      "text/plain": [
       "<Figure size 1080x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plot_scatter_chart(df8,\"Hebbal\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Based on above charts we can see that data points highlighted in red below are outliers and they are being removed due to remove_bhk_outliers function**"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3 style='color:green'>Before and after outlier removal: Rajaji Nagar</h3>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<img src=\"rajaji_nagar_outliers.png\"></img>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3 style='color:green'>Before and after outlier removal: Hebbal</h3>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<img src=\"hebbal_outliers.png\"></img>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Text(0, 0.5, 'Count')"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1440x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib\n",
    "matplotlib.rcParams[\"figure.figsize\"] = (20,10)\n",
    "plt.hist(df8.price_per_sqft,rwidth=0.8)\n",
    "plt.xlabel(\"Price Per Square Feet\")\n",
    "plt.ylabel(\"Count\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Outlier Removal Using Bathrooms Feature</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([ 4.,  3.,  2.,  5.,  8.,  1.,  6.,  7.,  9., 12., 16., 13.])"
      ]
     },
     "execution_count": 42,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df8.bath.unique()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Text(0, 0.5, 'Count')"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1440x720 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.hist(df8.bath,rwidth=0.8)\n",
    "plt.xlabel(\"Number of bathrooms\")\n",
    "plt.ylabel(\"Count\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>5277</th>\n",
       "      <td>Neeladri Nagar</td>\n",
       "      <td>10 BHK</td>\n",
       "      <td>4000.0</td>\n",
       "      <td>12.0</td>\n",
       "      <td>160.0</td>\n",
       "      <td>10</td>\n",
       "      <td>4000.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8483</th>\n",
       "      <td>other</td>\n",
       "      <td>10 BHK</td>\n",
       "      <td>12000.0</td>\n",
       "      <td>12.0</td>\n",
       "      <td>525.0</td>\n",
       "      <td>10</td>\n",
       "      <td>4375.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8572</th>\n",
       "      <td>other</td>\n",
       "      <td>16 BHK</td>\n",
       "      <td>10000.0</td>\n",
       "      <td>16.0</td>\n",
       "      <td>550.0</td>\n",
       "      <td>16</td>\n",
       "      <td>5500.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9306</th>\n",
       "      <td>other</td>\n",
       "      <td>11 BHK</td>\n",
       "      <td>6000.0</td>\n",
       "      <td>12.0</td>\n",
       "      <td>150.0</td>\n",
       "      <td>11</td>\n",
       "      <td>2500.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>9637</th>\n",
       "      <td>other</td>\n",
       "      <td>13 BHK</td>\n",
       "      <td>5425.0</td>\n",
       "      <td>13.0</td>\n",
       "      <td>275.0</td>\n",
       "      <td>13</td>\n",
       "      <td>5069.124424</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "            location    size  total_sqft  bath  price  bhk  price_per_sqft\n",
       "5277  Neeladri Nagar  10 BHK      4000.0  12.0  160.0   10     4000.000000\n",
       "8483           other  10 BHK     12000.0  12.0  525.0   10     4375.000000\n",
       "8572           other  16 BHK     10000.0  16.0  550.0   16     5500.000000\n",
       "9306           other  11 BHK      6000.0  12.0  150.0   11     2500.000000\n",
       "9637           other  13 BHK      5425.0  13.0  275.0   13     5069.124424"
      ]
     },
     "execution_count": 44,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df8[df8.bath>10]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**It is unusual to have 2 more bathrooms than number of bedrooms in a home**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1626</th>\n",
       "      <td>Chikkabanavar</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>2460.0</td>\n",
       "      <td>7.0</td>\n",
       "      <td>80.0</td>\n",
       "      <td>4</td>\n",
       "      <td>3252.032520</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>5238</th>\n",
       "      <td>Nagasandra</td>\n",
       "      <td>4 Bedroom</td>\n",
       "      <td>7000.0</td>\n",
       "      <td>8.0</td>\n",
       "      <td>450.0</td>\n",
       "      <td>4</td>\n",
       "      <td>6428.571429</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>6711</th>\n",
       "      <td>Thanisandra</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1806.0</td>\n",
       "      <td>6.0</td>\n",
       "      <td>116.0</td>\n",
       "      <td>3</td>\n",
       "      <td>6423.034330</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>8408</th>\n",
       "      <td>other</td>\n",
       "      <td>6 BHK</td>\n",
       "      <td>11338.0</td>\n",
       "      <td>9.0</td>\n",
       "      <td>1000.0</td>\n",
       "      <td>6</td>\n",
       "      <td>8819.897689</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "           location       size  total_sqft  bath   price  bhk  price_per_sqft\n",
       "1626  Chikkabanavar  4 Bedroom      2460.0   7.0    80.0    4     3252.032520\n",
       "5238     Nagasandra  4 Bedroom      7000.0   8.0   450.0    4     6428.571429\n",
       "6711    Thanisandra      3 BHK      1806.0   6.0   116.0    3     6423.034330\n",
       "8408          other      6 BHK     11338.0   9.0  1000.0    6     8819.897689"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df8[df8.bath>df8.bhk+2]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Again the business manager has a conversation with you (i.e. a data scientist) that if you have 4 bedroom home and even if you have bathroom in all 4 rooms plus one guest bathroom, you will have total bath = total bed + 1 max. Anything above that is an outlier or a data error and can be removed**"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(7239, 7)"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df9 = df8[df8.bath<df8.bhk+2]\n",
    "df9.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>size</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>price_per_sqft</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>4 BHK</td>\n",
       "      <td>2850.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>428.0</td>\n",
       "      <td>4</td>\n",
       "      <td>15017.543860</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>3 BHK</td>\n",
       "      <td>1630.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>194.0</td>\n",
       "      <td>3</td>\n",
       "      <td>11901.840491</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              location   size  total_sqft  bath  price  bhk  price_per_sqft\n",
       "0  1st Block Jayanagar  4 BHK      2850.0   4.0  428.0    4    15017.543860\n",
       "1  1st Block Jayanagar  3 BHK      1630.0   3.0  194.0    3    11901.840491"
      ]
     },
     "execution_count": 47,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df9.head(2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>2850.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>428.0</td>\n",
       "      <td>4</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1630.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>194.0</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1875.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>235.0</td>\n",
       "      <td>3</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              location  total_sqft  bath  price  bhk\n",
       "0  1st Block Jayanagar      2850.0   4.0  428.0    4\n",
       "1  1st Block Jayanagar      1630.0   3.0  194.0    3\n",
       "2  1st Block Jayanagar      1875.0   2.0  235.0    3"
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df10 = df9.drop(['size','price_per_sqft'],axis='columns')\n",
    "df10.head(3)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Use One Hot Encoding For Location</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>1st Block Jayanagar</th>\n",
       "      <th>1st Phase JP Nagar</th>\n",
       "      <th>2nd Phase Judicial Layout</th>\n",
       "      <th>2nd Stage Nagarbhavi</th>\n",
       "      <th>5th Block Hbr Layout</th>\n",
       "      <th>5th Phase JP Nagar</th>\n",
       "      <th>6th Phase JP Nagar</th>\n",
       "      <th>7th Phase JP Nagar</th>\n",
       "      <th>8th Phase JP Nagar</th>\n",
       "      <th>9th Phase JP Nagar</th>\n",
       "      <th>...</th>\n",
       "      <th>Vishveshwarya Layout</th>\n",
       "      <th>Vishwapriya Layout</th>\n",
       "      <th>Vittasandra</th>\n",
       "      <th>Whitefield</th>\n",
       "      <th>Yelachenahalli</th>\n",
       "      <th>Yelahanka</th>\n",
       "      <th>Yelahanka New Town</th>\n",
       "      <th>Yelenahalli</th>\n",
       "      <th>Yeshwanthpur</th>\n",
       "      <th>other</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3 rows × 241 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   1st Block Jayanagar  1st Phase JP Nagar  2nd Phase Judicial Layout  \\\n",
       "0                    1                   0                          0   \n",
       "1                    1                   0                          0   \n",
       "2                    1                   0                          0   \n",
       "\n",
       "   2nd Stage Nagarbhavi  5th Block Hbr Layout  5th Phase JP Nagar  \\\n",
       "0                     0                     0                   0   \n",
       "1                     0                     0                   0   \n",
       "2                     0                     0                   0   \n",
       "\n",
       "   6th Phase JP Nagar  7th Phase JP Nagar  8th Phase JP Nagar  \\\n",
       "0                   0                   0                   0   \n",
       "1                   0                   0                   0   \n",
       "2                   0                   0                   0   \n",
       "\n",
       "   9th Phase JP Nagar  ...  Vishveshwarya Layout  Vishwapriya Layout  \\\n",
       "0                   0  ...                     0                   0   \n",
       "1                   0  ...                     0                   0   \n",
       "2                   0  ...                     0                   0   \n",
       "\n",
       "   Vittasandra  Whitefield  Yelachenahalli  Yelahanka  Yelahanka New Town  \\\n",
       "0            0           0               0          0                   0   \n",
       "1            0           0               0          0                   0   \n",
       "2            0           0               0          0                   0   \n",
       "\n",
       "   Yelenahalli  Yeshwanthpur  other  \n",
       "0            0             0      0  \n",
       "1            0             0      0  \n",
       "2            0             0      0  \n",
       "\n",
       "[3 rows x 241 columns]"
      ]
     },
     "execution_count": 49,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dummies = pd.get_dummies(df10.location)\n",
    "dummies.head(3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>location</th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>1st Block Jayanagar</th>\n",
       "      <th>1st Phase JP Nagar</th>\n",
       "      <th>2nd Phase Judicial Layout</th>\n",
       "      <th>2nd Stage Nagarbhavi</th>\n",
       "      <th>5th Block Hbr Layout</th>\n",
       "      <th>...</th>\n",
       "      <th>Vijayanagar</th>\n",
       "      <th>Vishveshwarya Layout</th>\n",
       "      <th>Vishwapriya Layout</th>\n",
       "      <th>Vittasandra</th>\n",
       "      <th>Whitefield</th>\n",
       "      <th>Yelachenahalli</th>\n",
       "      <th>Yelahanka</th>\n",
       "      <th>Yelahanka New Town</th>\n",
       "      <th>Yelenahalli</th>\n",
       "      <th>Yeshwanthpur</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>2850.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>428.0</td>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1630.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>194.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1875.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>235.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1200.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>130.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1st Block Jayanagar</td>\n",
       "      <td>1235.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>148.0</td>\n",
       "      <td>2</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 245 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "              location  total_sqft  bath  price  bhk  1st Block Jayanagar  \\\n",
       "0  1st Block Jayanagar      2850.0   4.0  428.0    4                    1   \n",
       "1  1st Block Jayanagar      1630.0   3.0  194.0    3                    1   \n",
       "2  1st Block Jayanagar      1875.0   2.0  235.0    3                    1   \n",
       "3  1st Block Jayanagar      1200.0   2.0  130.0    3                    1   \n",
       "4  1st Block Jayanagar      1235.0   2.0  148.0    2                    1   \n",
       "\n",
       "   1st Phase JP Nagar  2nd Phase Judicial Layout  2nd Stage Nagarbhavi  \\\n",
       "0                   0                          0                     0   \n",
       "1                   0                          0                     0   \n",
       "2                   0                          0                     0   \n",
       "3                   0                          0                     0   \n",
       "4                   0                          0                     0   \n",
       "\n",
       "   5th Block Hbr Layout  ...  Vijayanagar  Vishveshwarya Layout  \\\n",
       "0                     0  ...            0                     0   \n",
       "1                     0  ...            0                     0   \n",
       "2                     0  ...            0                     0   \n",
       "3                     0  ...            0                     0   \n",
       "4                     0  ...            0                     0   \n",
       "\n",
       "   Vishwapriya Layout  Vittasandra  Whitefield  Yelachenahalli  Yelahanka  \\\n",
       "0                   0            0           0               0          0   \n",
       "1                   0            0           0               0          0   \n",
       "2                   0            0           0               0          0   \n",
       "3                   0            0           0               0          0   \n",
       "4                   0            0           0               0          0   \n",
       "\n",
       "   Yelahanka New Town  Yelenahalli  Yeshwanthpur  \n",
       "0                   0            0             0  \n",
       "1                   0            0             0  \n",
       "2                   0            0             0  \n",
       "3                   0            0             0  \n",
       "4                   0            0             0  \n",
       "\n",
       "[5 rows x 245 columns]"
      ]
     },
     "execution_count": 50,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df11 = pd.concat([df10,dummies.drop('other',axis='columns')],axis='columns')\n",
    "df11.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>price</th>\n",
       "      <th>bhk</th>\n",
       "      <th>1st Block Jayanagar</th>\n",
       "      <th>1st Phase JP Nagar</th>\n",
       "      <th>2nd Phase Judicial Layout</th>\n",
       "      <th>2nd Stage Nagarbhavi</th>\n",
       "      <th>5th Block Hbr Layout</th>\n",
       "      <th>5th Phase JP Nagar</th>\n",
       "      <th>...</th>\n",
       "      <th>Vijayanagar</th>\n",
       "      <th>Vishveshwarya Layout</th>\n",
       "      <th>Vishwapriya Layout</th>\n",
       "      <th>Vittasandra</th>\n",
       "      <th>Whitefield</th>\n",
       "      <th>Yelachenahalli</th>\n",
       "      <th>Yelahanka</th>\n",
       "      <th>Yelahanka New Town</th>\n",
       "      <th>Yelenahalli</th>\n",
       "      <th>Yeshwanthpur</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2850.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>428.0</td>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1630.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>194.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 244 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   total_sqft  bath  price  bhk  1st Block Jayanagar  1st Phase JP Nagar  \\\n",
       "0      2850.0   4.0  428.0    4                    1                   0   \n",
       "1      1630.0   3.0  194.0    3                    1                   0   \n",
       "\n",
       "   2nd Phase Judicial Layout  2nd Stage Nagarbhavi  5th Block Hbr Layout  \\\n",
       "0                          0                     0                     0   \n",
       "1                          0                     0                     0   \n",
       "\n",
       "   5th Phase JP Nagar  ...  Vijayanagar  Vishveshwarya Layout  \\\n",
       "0                   0  ...            0                     0   \n",
       "1                   0  ...            0                     0   \n",
       "\n",
       "   Vishwapriya Layout  Vittasandra  Whitefield  Yelachenahalli  Yelahanka  \\\n",
       "0                   0            0           0               0          0   \n",
       "1                   0            0           0               0          0   \n",
       "\n",
       "   Yelahanka New Town  Yelenahalli  Yeshwanthpur  \n",
       "0                   0            0             0  \n",
       "1                   0            0             0  \n",
       "\n",
       "[2 rows x 244 columns]"
      ]
     },
     "execution_count": 51,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df12 = df11.drop('location',axis='columns')\n",
    "df12.head(2)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Build a Model Now...</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 52,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(7239, 244)"
      ]
     },
     "execution_count": 52,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df12.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 53,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>total_sqft</th>\n",
       "      <th>bath</th>\n",
       "      <th>bhk</th>\n",
       "      <th>1st Block Jayanagar</th>\n",
       "      <th>1st Phase JP Nagar</th>\n",
       "      <th>2nd Phase Judicial Layout</th>\n",
       "      <th>2nd Stage Nagarbhavi</th>\n",
       "      <th>5th Block Hbr Layout</th>\n",
       "      <th>5th Phase JP Nagar</th>\n",
       "      <th>6th Phase JP Nagar</th>\n",
       "      <th>...</th>\n",
       "      <th>Vijayanagar</th>\n",
       "      <th>Vishveshwarya Layout</th>\n",
       "      <th>Vishwapriya Layout</th>\n",
       "      <th>Vittasandra</th>\n",
       "      <th>Whitefield</th>\n",
       "      <th>Yelachenahalli</th>\n",
       "      <th>Yelahanka</th>\n",
       "      <th>Yelahanka New Town</th>\n",
       "      <th>Yelenahalli</th>\n",
       "      <th>Yeshwanthpur</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2850.0</td>\n",
       "      <td>4.0</td>\n",
       "      <td>4</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1630.0</td>\n",
       "      <td>3.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1875.0</td>\n",
       "      <td>2.0</td>\n",
       "      <td>3</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>...</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>3 rows × 243 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   total_sqft  bath  bhk  1st Block Jayanagar  1st Phase JP Nagar  \\\n",
       "0      2850.0   4.0    4                    1                   0   \n",
       "1      1630.0   3.0    3                    1                   0   \n",
       "2      1875.0   2.0    3                    1                   0   \n",
       "\n",
       "   2nd Phase Judicial Layout  2nd Stage Nagarbhavi  5th Block Hbr Layout  \\\n",
       "0                          0                     0                     0   \n",
       "1                          0                     0                     0   \n",
       "2                          0                     0                     0   \n",
       "\n",
       "   5th Phase JP Nagar  6th Phase JP Nagar  ...  Vijayanagar  \\\n",
       "0                   0                   0  ...            0   \n",
       "1                   0                   0  ...            0   \n",
       "2                   0                   0  ...            0   \n",
       "\n",
       "   Vishveshwarya Layout  Vishwapriya Layout  Vittasandra  Whitefield  \\\n",
       "0                     0                   0            0           0   \n",
       "1                     0                   0            0           0   \n",
       "2                     0                   0            0           0   \n",
       "\n",
       "   Yelachenahalli  Yelahanka  Yelahanka New Town  Yelenahalli  Yeshwanthpur  \n",
       "0               0          0                   0            0             0  \n",
       "1               0          0                   0            0             0  \n",
       "2               0          0                   0            0             0  \n",
       "\n",
       "[3 rows x 243 columns]"
      ]
     },
     "execution_count": 53,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "X = df12.drop(['price'],axis='columns')\n",
    "X.head(3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(7239, 243)"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "X.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    428.0\n",
       "1    194.0\n",
       "2    235.0\n",
       "Name: price, dtype: float64"
      ]
     },
     "execution_count": 55,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "y = df12.price\n",
    "y.head(3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "7239"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "len(y)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n",
    "X_train, X_test, y_train, y_test = train_test_split(X,y,test_size=0.2,random_state=10)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8629132245229449"
      ]
     },
     "execution_count": 58,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.linear_model import LinearRegression\n",
    "lr_clf = LinearRegression()\n",
    "lr_clf.fit(X_train,y_train)\n",
    "lr_clf.score(X_test,y_test)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Use K Fold cross validation to measure accuracy of our LinearRegression model</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "array([0.82702546, 0.86027005, 0.85322178, 0.8436466 , 0.85481502])"
      ]
     },
     "execution_count": 59,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.model_selection import ShuffleSplit\n",
    "from sklearn.model_selection import cross_val_score\n",
    "\n",
    "cv = ShuffleSplit(n_splits=5, test_size=0.2, random_state=0)\n",
    "\n",
    "cross_val_score(LinearRegression(), X, y, cv=cv)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**We can see that in 5 iterations we get a score above 80% all the time. This is pretty good but we want to test few other algorithms for regression to see if we can get even better score. We will use GridSearchCV for this purpose**"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Find best model using GridSearchCV</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>model</th>\n",
       "      <th>best_score</th>\n",
       "      <th>best_params</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>linear_regression</td>\n",
       "      <td>0.847796</td>\n",
       "      <td>{'normalize': False}</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>lasso</td>\n",
       "      <td>0.726738</td>\n",
       "      <td>{'alpha': 2, 'selection': 'cyclic'}</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>decision_tree</td>\n",
       "      <td>0.716064</td>\n",
       "      <td>{'criterion': 'friedman_mse', 'splitter': 'best'}</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               model  best_score  \\\n",
       "0  linear_regression    0.847796   \n",
       "1              lasso    0.726738   \n",
       "2      decision_tree    0.716064   \n",
       "\n",
       "                                         best_params  \n",
       "0                               {'normalize': False}  \n",
       "1                {'alpha': 2, 'selection': 'cyclic'}  \n",
       "2  {'criterion': 'friedman_mse', 'splitter': 'best'}  "
      ]
     },
     "execution_count": 60,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.model_selection import GridSearchCV\n",
    "\n",
    "from sklearn.linear_model import Lasso\n",
    "from sklearn.tree import DecisionTreeRegressor\n",
    "\n",
    "def find_best_model_using_gridsearchcv(X,y):\n",
    "    algos = {\n",
    "        'linear_regression' : {\n",
    "            'model': LinearRegression(),\n",
    "            'params': {\n",
    "                'normalize': [True, False]\n",
    "            }\n",
    "        },\n",
    "        'lasso': {\n",
    "            'model': Lasso(),\n",
    "            'params': {\n",
    "                'alpha': [1,2],\n",
    "                'selection': ['random', 'cyclic']\n",
    "            }\n",
    "        },\n",
    "        'decision_tree': {\n",
    "            'model': DecisionTreeRegressor(),\n",
    "            'params': {\n",
    "                'criterion' : ['mse','friedman_mse'],\n",
    "                'splitter': ['best','random']\n",
    "            }\n",
    "        }\n",
    "    }\n",
    "    scores = []\n",
    "    cv = ShuffleSplit(n_splits=5, test_size=0.2, random_state=0)\n",
    "    for algo_name, config in algos.items():\n",
    "        gs =  GridSearchCV(config['model'], config['params'], cv=cv, return_train_score=False)\n",
    "        gs.fit(X,y)\n",
    "        scores.append({\n",
    "            'model': algo_name,\n",
    "            'best_score': gs.best_score_,\n",
    "            'best_params': gs.best_params_\n",
    "        })\n",
    "\n",
    "    return pd.DataFrame(scores,columns=['model','best_score','best_params'])\n",
    "\n",
    "find_best_model_using_gridsearchcv(X,y)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Based on above results we can say that LinearRegression gives the best score. Hence we will use that.**"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Test the model for few properties</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {},
   "outputs": [],
   "source": [
    "def predict_price(location,sqft,bath,bhk):    \n",
    "    loc_index = np.where(X.columns==location)[0][0]\n",
    "\n",
    "    x = np.zeros(len(X.columns))\n",
    "    x[0] = sqft\n",
    "    x[1] = bath\n",
    "    x[2] = bhk\n",
    "    if loc_index >= 0:\n",
    "        x[loc_index] = 1\n",
    "\n",
    "    return lr_clf.predict([x])[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "83.86570258311222"
      ]
     },
     "execution_count": 62,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "predict_price('1st Phase JP Nagar',1000, 2, 2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "86.08062284985995"
      ]
     },
     "execution_count": 63,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "predict_price('1st Phase JP Nagar',1000, 3, 3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "193.31197733179556"
      ]
     },
     "execution_count": 64,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "predict_price('Indira Nagar',1000, 2, 2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 65,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "195.52689759854331"
      ]
     },
     "execution_count": 65,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "predict_price('Indira Nagar',1000, 3, 3)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Export the tested model to a pickle file</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 66,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pickle\n",
    "with open('banglore_home_prices_model.pickle','wb') as f:\n",
    "    pickle.dump(lr_clf,f)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 style='color:blue'>Export location and column information to a file that will be useful later on in our prediction application</h2>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 67,
   "metadata": {},
   "outputs": [],
   "source": [
    "import json\n",
    "columns = {\n",
    "    'data_columns' : [col.lower() for col in X.columns]\n",
    "}\n",
    "with open(\"columns.json\",\"w\") as f:\n",
    "    f.write(json.dumps(columns))"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}

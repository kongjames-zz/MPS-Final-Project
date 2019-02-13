import pandas as pd
import numpy as np
import os
os.chdir("./")

import matplotlib
import matplotlib.pyplot as plt
matplotlib.style.use('ggplot')
import random
random.seed(0)

#from scipy.signal import savgol_filter

z3data = pd.ExcelFile("./HPI_AT_3zip.xlsx")
z3data.sheet_names

z3data1 = z3data.parse(sheet_name='data', converters={'ZIP':str})
z3data2 = z3data.parse(sheet_name='State Look Up', converters={'ZIP':str})
Q = {1:'01-01',2:'04-01',3:'07-01',4:'12-01'}
z3data1['t'] = pd.to_datetime(map(lambda x,y:str(x)+'-'+Q[y], z3data1['Year'],z3data1['Quarter']))
z3data1.dtypes

z3data1.head(5)
z3data2.head(10)

#turn excel sheets to data frame 
z3data10 = pd.read_excel("./HPI_AT_3zip.xlsx", index_col = 0, sheet_name = "data")
z3data11 = pd.read_excel("./HPI_AT_3zip.xlsx", index_col = 0, sheet_name = "State Look Up")
z3data10['t'] = pd.to_datetime(map(lambda x,y:str(x)+'-'+Q[y], z3data1['Year'],z3data10['Quarter']))
z3data10.dtypes

#Merge ZIP from data and Zip code from State Look Up
z3data_join = pd.merge(z3data10, z3data11, on='ZIP', how='left')
if len(str(z3data_join["ZIP"])) == 1:
    number = "00"  + str(number)
    elif len(str(z3data_join["ZIP"])) ==2:
        number = "0"  + str(number)
    else:
         len(str(z3data_join["ZIP"])) ==3:
                str(number)
z3data_join.head(10)

a = z3data1.pivot_table(index='ZIP', columns='t', values='NSA').T
a.reset_index(level='t', inplace=True)
a.columns

a = z3data_join.pivot_table(index='ZIP', columns='t', values='NSA').T
a.reset_index(level='t', inplace=True)
a.columns

zipcols = a.columns[1:]
ax = a.plot(x='t',y=zipcols,kind='line', figsize=(12,12))
ax.set_xlabel('t')
ax.set_ylabel('NSA')

a['avg'] = a[zipcols].mean(axis=1)
def meanabsdiff(x):
    return np.sum(np.abs(x[1:]-x[:-1]))
    
deviations = a[zipcols].apply(np.std, axis=0)
stablecols = deviations[np.argsort(deviations)][:100].index
a['avgnew'] = a[stablecols].mean(axis=1)
mean_abs = a[zipcols].apply(meanabsdiff, axis=0)
stablecols = deviations[np.argsort(mean_abs)][:100].index
a['avgnew2'] = a[stablecols].mean(axis=1)

ax = a.plot(x='t',y=['avg','avgnew', 'avgnew2'],kind='line', figsize=(12,6))
ax.set_xlabel('t')
ax.set_ylabel('NSA')

#standard deviation
rescols = columns=['avg','avgnew','avgnew2']
a[rescols].apply(np.std, axis=0)

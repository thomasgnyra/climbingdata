import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

df = pd.read_csv('../input/climbing/ticks.csv') #these are databases i pulled out of SQL
df2 = pd.read_csv('../input/climbing/users.csv') 
df3 = pd.read_csv('../input/climbing/grades.csv')


max_grade = df.groupby(['user_id','climb_type'], as_index=False)['grade_id'].max()

# Get names of indexes for which column climb type has value 1 (bouldeirng)
indexNames = max_grade[ max_grade['climb_type'] == 1 ].index
# Delete these row indexes from dataFrame
max_grade.drop(indexNames , inplace=True)

max_grade['height'] = max_grade['user_id']
max_grade['weight'] = max_grade['user_id']
max_grade['sex'] = max_grade['user_id'] #this was used to change up the dataset


weight_dict = df2.set_index('id').to_dict()['weight']
height_dict = df2.set_index('id').to_dict()['height']
sex_dict = df2.set_index('id').to_dict()['sex']


max_grade['weight'] = max_grade['weight'].replace(weight_dict)
max_grade['height'] = max_grade['height'].replace(height_dict)
max_grade['sex'] = max_grade['sex'].replace(sex_dict)

indexNames = max_grade[ max_grade['weight'] == 0 ].index
max_grade.drop(indexNames , inplace=True)

indexNames = max_grade[ max_grade['height'] == 0 ].index
max_grade.drop(indexNames , inplace=True)

indexNames = max_grade[ max_grade['sex'] == 0 ].index
max_grade.drop(indexNames , inplace=True)

indexNames = max_grade[ max_grade['grade_id'] < 40 ].index
max_grade.drop(indexNames , inplace=True)

#change grades
grades_dic = df3.set_index('score').to_dict()['fra_routes_input']
max_grade['grade_id'] = max_grade['grade_id'].replace(grades_dic)


#bmi math
max_grade['bmi'] = max_grade['weight'] / (max_grade['height']/100)**2

indexNames = max_grade[ max_grade['bmi'] > 40 ].index
max_grade.drop(indexNames , inplace=True)
indexNames = max_grade[ max_grade['bmi'] < 10 ].index
max_grade.drop(indexNames , inplace=True)

max_grade = max_grade.sort_values(['grade_id']).reset_index(drop=True)

sns.set(rc={'figure.figsize':(11.7,8.27)})
sns.boxplot(x=max_grade['grade_id'], y=max_grade['bmi'])

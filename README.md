
# Varibase: Never Lose Your Variables Again!

Ever closed your Jupyter notebook by accident and immediately regretted it?
Or maybe your notebook decided to crash just when you had the perfect variable ready for analysis? 😱

Fear no more! __Varibase__ is here to save your day (and your variables)! 🦸‍♂️

This package was born out of frustration and necessity after repeatedly losing variables because I didn’t feel like rerunning the entire notebook for that one tiny value. So, I created __Varibase__—a simple, efficient, and life-saving (at least for devs) __tool to store and retrieve variables effortlessly.__

If you:

Lose variables like you lose your car keys 🗝️,
Hate running notebooks from the top just to recreate one little variable 🤦‍♂️,
Want to focus on scripting, not saving variables 🧑‍💻,
Varibase is for you. 💾✨

**No more variable loss. No more frustration. Just happy scripting.**

# Example 1: Dataframe
```python
from varibase import VarDB
import pandas as pd

the_main_sheet = pd.read_csv(r"/media/ubuntu/New Volume/Satsure/SAGE/POC/Deep_NPA-TS-26Nov24/Deep NPA  -TS - TS.csv",dtype=str).assign(uniq_ind = lambda file: file.index) #main file

the_req_dat = the_main_sheet[(the_main_sheet['district'].notna())&(the_main_sheet['SURVEY NO_UPDATED'].notna())] \
                            .assign(concatenated = lambda file: file.apply(lambda x: "_".join([x['district_id'],x['mandal_id'],x['village_id']]),axis=1)) 

VarDB().store_var('the_req_dat',the_req_dat)   # store the variable
the_req_dat_again = VarDB().fetch_var('the_req_dat') # get the variable from the variable db
VarDB().store_var('the_req_dat',the_main_sheet) # another variable will replace this key. Cannot have a duplicating key
VarDB().flush_db() # to delete the variable db permanently
```
# Example 2: List
```python
import json
the_list = [1,2,3,5,70]
VarDB().store_var('the_list',the_list) #list

the_out = VarDB().fetch_var('the_list')

json_file  = json.dumps({
                        "name": "John Doe",
                        "age": 30,
                        "isEmployed": True,
                        "skills": ["Python", "Data Analysis", "Machine Learning"]
                        }) #json                                                        
VarDB().store_var('json_file',json_file)
json_file_out = VarDB().fetch_var('json_file')

print(json_file_out)
print(the_out)
>>> {"name": "John Doe", "age": 30, "isEmployed": true, "skills": ["Python", "Data Analysis", "Machine Learning"]}
>>> [1, 2, 3, 5, 70]
```
# Example 3: Class instance
```python
class Addnew():
    def __init__(self,a,b):
        self.a =a
        self.b = b

    def add(self):
        return (self.a+self.b)
    
class_object = Addnew(1,2)
VarDB().store_var('class_object',class_object)

class_object_out = VarDB().fetch_var('class_object')
print(class_object_out.add()) 
>>> 3
```
> **Note:**  The current version of **_varibase_** requires class defination (**class Addnew** in the above case) to exist while calling back the class instance (**class_object** in the above case)





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

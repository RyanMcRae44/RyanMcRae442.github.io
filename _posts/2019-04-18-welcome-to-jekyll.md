---
title: "Graphing in Matplotlib using Python"
date: 2019-04-18T15:34:30-04:00
categories:
  - blog
tags:
  - Jekyll
  - update
---

Here you can find a project I completed where I graphed FECO2 and V̇CO2 over V̇O2. Below is the finished graph as well as the code


![Alt text](/assets/images/VO2-VE-4 (1).png "a title")

```ruby
### New code for assignment

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt

# Lets read in our file now
df = pd.read_csv('../input/demo-knes381/subject_1321.csv', header=[0], skiprows=[1,2,3])

# please note that while this is an output file from the parvo-metabolics cart we have
# I have edited this data set and simplied the header file on it

# rename our column headers
df = df.rename(columns={'VE/': 'VE/VO2','VE/.1': 'VE/VCO2'})

# simplify our terms to reduce future typing... 
# it is easier to write plot x, y than plot df['Time'], df['VO2']
x = df['VO2']
y1 = df['FECO2']
y2 = df['VCO2']

fig, ax = plt.subplots(2, 1, sharex=True, figsize=(8, 10)) # Note I increased the figure size here.

# this line seperates the two plots...
fig.subplots_adjust(hspace=0)

#defining where GET and RCP are
GET_VO2 = 0.8
RCP_VO2 = 2.3

GET_label_y = 0.8
RCP_label_y = 2.3

# Plot of FECO2
ax[0].plot(x, y1, 'o', label=('FECO2'), c='r')
ax[0].spines[['top', 'right']].set_visible(False)
# Lines
ax[0].axvline(GET_VO2, color='k', linestyle='-')
ax[0].axvline(RCP_VO2, color='k', linestyle='-')


ax[0].set(ylabel=('%'))
ax[0].legend(loc = 'upper left')


# Plot of VCO2
ax[1].plot(x, y2, 'o', label=('$\dot{V}CO_2$'), c='b')
ax[1].spines[['top', 'right']].set_visible(False)
# Lines
ax[1].axvline(GET_VO2, color='k', linestyle='-')
ax[1].axvline(RCP_VO2, color='k', linestyle='-')

ax[1].set(ylabel=('L/min'))
ax[1].legend(loc = 'upper left')

ax[1].annotate('GET',xy=(.87,2.7))
ax[1].annotate('RCP',xy=(2.37,2.7))

ax[1].set_xlabel('$\dot{V}O_2$ (L/min)')

# Title
fig.suptitle('$\dot{V}O_2$ vs. FECO2 and $\dot{V}CO_2$', fontsize=16)



# save the figure before we show it... or it will be blank
fig.savefig("VO2-VE-4.png", dpi=300, bbox_inches = "tight")
fig.show()
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

---
title: "info of .pb file"
enableToc: false
date: "2023-05-05"
lastmod: :git
tags:
- ml
- py
---

The shape of the input and output are needed to use a machine learning model. In a case where only a `.pb` 
file is available and the source code can't be checked, there are a few ways to get information about
the model from the `.pb` file.

[loading the model](https://support.huawei.com/enterprise/en/doc/EDOC1100206675/3dedcdbc/interpreting-a-pb-model-file)
I used this script by itself and it shows the node names. But it doesn't help me since I need to know the shapes
of the input and output... I can't do anything with these information. It's good to know info can be extracted
this way though.

[saved_model_cli](https://www.tensorflow.org/guide/saved_model#overview_of_commands)
This way seems to be the best way to find the i/o shapes but when I tried using it, it needed extra 
files that I don't have. My guess is that it assumes the processed model is saved with the current
version of tensorflow where it has other files other than the `.pb` file.  So it gave a bunch of errors saying
it need the extra files.

I tried using it the second time using a [[python virtual environment]], it didn't give any errors but it didn't
show any output either.

---
layout:       post
title:        "optuna"
author:       "cyalcher"
header-style: text
catalog:      true
tags:
    - deep learning
    - optuna
---

# 一、背景
深度学习调参是复杂的过程，如何借助工具的手段进行提效，找到合适的参数是关键。

# 二、目标
掌握optuna的应用，实现参数调优。
# 三、官网demo
## 添加实验注解
注解的作用：实验的标签，标注当前的实验；
实现两个功能：① 通过 study 对象的 set_user_attr 方法设定注解 ② 在1次实验中添加注解案例;
其中：set_user_attr 参数是(string,任意json对象)；
```
import logging
import sys
import optuna

optuna.logging.get_logger("optuna").addHandler(logging.StreamHandler(sys.stdout))
study_name = "user_attr"  # 命名唯一实验名称
# 会在sqlite中生成对应的 db
db_name = study_name
# sqlite的绝对路径 
db_path = f'/Users/sqlite/sqlite-tools-osx-x86-3420000/{db_name}.db'
# create_study的参数
storage_name = f"sqlite:////{db_path}"
study = optuna.create_study(study_name=study_name, storage=storage_name)

# 设定 k-v
study.set_user_attr("contributor",["Akiba","Sano"])
study.set_user_attr("dataset","MNIST")

# 通过 study.user_attr访问study对象绑定的注解
study.user_attrs
# 结果 {'contributor': ['Akiba', 'Sano'], 'dataset': 'MNIST'}

# 通过rdb 来访问注解；通常来分析实验使用
study_summaries = optuna.get_all_study_summaries(storage_name)
study_summaries[0].user_attrs
# 结果 {'contributor': ['Akiba', 'Sano'], 'dataset': 'MNIST'}

# 结合trail 使用
import sklearn.datasets
import sklearn.model_selection
import sklearn.svm
# 在实验中，设定注解
def objective(trail):
    iris = sklearn.datasets.load_iris()
    x,y = iris.data,iris.target
    svc_c = trail.suggest_float("svc_c",1e-10,1e10,log=True)
    clf = sklearn.svm.SVC(C=svc_c)
    accuracy = sklearn.model_selection.cross_val_score(clf,x,y).mean()

    trail.set_user_attr("contributor",'cyalcher')
    trail.set_user_attr("accuray",accuracy)
    
    return 1.-accuracy

study.optimize(objective,n_trials=1)

study.trials[0].user_attrs
# 结果： {'accuray': 0.9266666666666667, 'contributor': 'cyalcher'}
```
## 命令行页面
背景：在完整的案例中需要 定义 objective 函数及create_study等样板代码。 <br>
**通过命令行页面，省略样板代码，可完成自动化执行；** <br>
1. 开发foo.py 文件，只有objective函数；<br>
```
def objective(trial):
    x = trial.suggest_float("x", -10, 10)
    return (x - 2) ** 2
```
2. 开发bash文件内容如下，
```
echo '---- optuna test  ---- '
STUDY_NAME=`optuna create-study --storage cli.db`
optuna study optimize 0420_optuna_cli_foo.py --n-trials=1 --storage cli.db --study-name $STUDY_NAME  objective
```

# 参考
[用户定义属性](https://optuna.readthedocs.io/zh-cn/latest/tutorial/20_recipes/003_attributes.html)
[命令行页面](https://optuna.readthedocs.io/zh-cn/latest/tutorial/20_recipes/004_cli.html)

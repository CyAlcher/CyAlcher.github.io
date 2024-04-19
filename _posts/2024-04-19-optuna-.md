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
# 三、官网demo-RDB保存实验结果 
dbpath是**绝对路径**
```
import logging
import sys
import optuna

optuna.logging.get_logger("optuna").addHandler(logging.StreamHandler(sys.stdout))
study_name = "example-study"  # 命名唯一实验名称
# 会在sqlite中生成对应的 db
db_name = study_name
# sqlite的绝对路径 
db_path = f'/Users/sqlite/sqlite-tools-osx-x86-3420000/{db_name}.db'
# create_study的参数
storage_name = f"sqlite:////{db_path}"
study = optuna.create_study(study_name=study_name, storage=storage_name)
# 定义目标函数
def objective(trial):
    x = trial.suggest_float("x", -10, 10)
    return (x - 2) ** 2
# 执行后就可以在 sqlite中存入数据
study.optimize(objective, n_trials=3)
# 启动sqlite3 example-study.db 
# .tables 命令查看表
# select * from trail; 查看训练过程
```
# 参考
[用RDB后端保存/恢复Study](https://optuna.readthedocs.io/zh-cn/latest/tutorial/20_recipes/001_rdb.html#sphx-glr-tutorial-20-recipes-001-rdb-py)

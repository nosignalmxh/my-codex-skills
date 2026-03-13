# Repo Scan Checklist

扫描顺序建议：

1. `README*` 和顶层目录
2. `requirements*.txt` / `environment*.yml` / `pyproject.toml`
3. `configs/`, `conf/`, `yaml/`, `args/`
4. `train*.py`, `main*.py`, `run*.sh`, `evaluate*.py`, `inference*.py`
5. `models/`, `modules/`, `losses/`, `datasets/`, `data/`
6. `scripts/`, `notebooks/`, `logs/`, `results/`

重点问题：

- 入口脚本真正调用哪个模块？
- 默认配置是否与论文一致？
- 数据预处理是否藏在单独脚本里？
- 指标计算是否和论文表述一致？
- 结果文件是否能反推出实验设置？

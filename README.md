# 📊 数据分析项目集合 | Data Analysis Projects

一套完整的电商数据分析项目，涵盖用户行为分析、客户价值分析、情感分析和A/B测试，使用真实的业务场景和数据集。

## 🎯 项目概览

项目	核心功能	技术栈	快速查看代码
项目一：基于用户评论的品牌口碑与竞品情感分析	评论情感分析、品牌口碑对比、关键词提取	Python, Jieba, 情感词典	(project-1-sentiment-analysis/real_sentiment_analyzer.py) 
项目二：A/B测试与多渠道市场活动ROI分析	统计检验、转化率分析、渠道ROI优化	SciPy, 假设检验,置信区间	(project-2-ab-testing/real_abtest_analyzer.py) 
项目三：销售漏斗构建与转化瓶颈诊断	用户行为分析、转化漏斗、瓶颈诊断	Pandas, Matplotlib, 漏斗分析	(project-3-funnel-analysis/real_funnel_analyzer.py) 
项目四：基于RFM模型的客户价值分析与精准营销	RFM分析、客户分群、精准营销策略	K-means聚类, RFM模型	project-4-customer-value/real_rfm_analyzer.py) 

## 🚀 快速开始

### 1. 环境配置
```bash
# 克隆项目
git clone https://github.com/yourusername/data-analysis-projects.git
cd data-analysis-projects

# 安装依赖
pip install -r requirements.txt

# 创建数据目录
mkdir -p data/
```

2. 准备数据（两种方式任选）

```bash
# 方式一：下载示例数据
python download_sample_data.py

# 方式二：使用自己的数据
# 将CSV文件放入 data/ 目录，支持自动识别格式
```

3. 运行项目

```bash
# 运行所有项目
python run_all_projects.py

# 或单独运行某个项目
cd project-2-ab-testing
python real_abtest_analyzer.py
```

💻 核心代码预览

项目二：A/B测试分析器（核心逻辑）

```python
class RealABTestAnalyzer:
    """A/B测试分析器核心类"""
    
    def perform_statistical_tests(self, df):
        """执行统计检验（卡方检验 + T检验）"""
        # 卡方检验（转化率）
        contingency_table = pd.crosstab(df['group'], df['converted'])
        chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)
        
        # T检验（收入）
        control_revenue = df[df['group'] == 'control']['revenue']
        treatment_revenue = df[df['group'] == 'treatment']['revenue']
        t_stat, p_value_t = stats.ttest_ind(control_revenue, treatment_revenue)
        
        return {
            'conversion_chi2': chi2,
            'conversion_p_value': p_value,
            'revenue_t_stat': t_stat,
            'revenue_p_value': p_value_t
        }
    
    def calculate_confidence_intervals(self, df):
        """计算95%置信区间"""
        results = {}
        for group in df['group'].unique():
            group_data = df[df['group'] == group]
            n = len(group_data)
            p = group_data['converted'].mean()
            se = np.sqrt(p * (1 - p) / n)
            margin = 1.96 * se  # 95%置信区间
            results[group] = (max(0, p - margin), min(1, p + margin))
        return results
```

查看完整代码 →

项目三：销售漏斗分析器（核心算法）

```python
class RealFunnelAnalyzer:
    """销售漏斗分析器核心类"""
    
    def build_funnel_from_behavior(self, df):
        """从用户行为数据构建销售漏斗"""
        funnel_data = []
        for session_id, session_data in df.groupby('session_id'):
            funnel_stages = {
                '访问首页': 1 if len(session_data) > 0 else 0,
                '浏览商品': 1 if 'view' in session_data['event_type'].values else 0,
                '加入购物车': 1 if 'cart' in session_data['event_type'].values else 0,
                '发起支付': 1 if 'purchase' in session_data['event_type'].values else 0,
                '支付成功': 1 if self._is_payment_successful(session_data) else 0
            }
            funnel_data.append(funnel_stages)
        return pd.DataFrame(funnel_data)
```

查看完整代码 →

📁 项目文件结构

```
📁 data-analysis-projects/
├── 📁 project-1-sentiment-analysis/
│   ├── 📄 real_sentiment_analyzer.py (350行)      # ← 点击查看
│   └── 📄 requirements.txt
├── 📁 project-2-ab-testing/
│   ├── 📄 real_abtest_analyzer.py (420行)         # ← 点击查看
│   └── 📄 test_data/
├── 📁 project-3-funnel-analysis/
│   ├── 📄 real_funnel_analyzer.py (480行)         # ← 点击查看
│   └── 📄 config/
├── 📁 project-4-customer-value/
│   ├── 📄 real_rfm_analyzer.py (520行)            # ← 点击查看
│   └── 📄 output/
├── 📁 data/                                       # 放真实数据文件
│   ├── amazon_reviews.csv                         # 项目一数据
│   ├── marketing_ab_testing.csv                   # 项目二数据
│   ├── user_behavior.csv                          # 项目三数据
│   └── online_retail_ii.csv                       # 项目四数据
├── 📄 run_all_projects.py                         # 一键运行脚本
├── 📄 download_sample_data.py                     # 下载示例数据
└── 📄 requirements.txt                            # 依赖包列表
```

🔗 在线查看代码

GitHub原生代码浏览器

· 项目一完整代码
· 项目二完整代码
· 项目三完整代码
· 项目四完整代码

交互式查看（VS Code风格）

https://img.shields.io/badge/在线查看代码-GitHub1s-blue?logo=github

🎮 在线运行体验

https://colab.research.google.com/assets/colab-badge.svg
https://mybinder.org/badge_logo.svg

📊 项目特点

🎯 四大核心优势

1. 真实业务场景：解决电商核心数据分析问题
2. 完整代码实现：从数据加载到结果输出完整流程
3. 即插即用：支持真实数据和模拟数据无缝切换
4. 丰富可视化：专业的图表展示分析结果

🔧 技术特色

· 智能数据适配：自动识别多种数据格式和列名
· 中文友好：完整的中文支持和可视化
· 统计严谨：科学的假设检验和置信区间计算
· 模块化设计：每个项目独立，易于扩展和维护

📈 输出示例

每个项目都会生成：

1. CSV结果文件：详细的分析结果数据
2. 可视化图表：专业的统计图表
3. 分析报告：关键指标和优化建议
4. 可执行建议：基于数据的业务优化建议

🛠️ 使用真实数据

准备数据文件

```bash
# 将你的数据文件放入 data/ 目录，支持多种格式：
# 项目一：amazon_reviews.csv (评论数据)
# 项目二：marketing_ab_testing.csv (A/B测试数据)
# 项目三：user_behavior.csv (用户行为数据)
# 项目四：online_retail_ii.csv (交易数据)

# 或者使用示例数据生成器
python generate_sample_data.py
```

数据格式要求

各项目支持自动列名识别，详见各项目的 _clean_*_data 方法。

🤝 贡献指南

欢迎提交Issue或Pull Request！

1. Fork项目
2. 创建功能分支 (git checkout -b feature/AmazingFeature)
3. 提交更改 (git commit -m 'Add some AmazingFeature')
4. 推送到分支 (git push origin feature/AmazingFeature)
5. 打开Pull Request

📄 许可证

MIT License - 详见 LICENSE 文件

👥 联系方式

如有问题或建议：

· 📧 邮箱：your.email@example.com
· 💬 Issues：GitHub Issues
· 🐦 Twitter：@yourusername

---

⭐ 支持项目

如果这个项目对你有帮助，请给个⭐Star支持！

更新于：2024年1月 | 作者：Your Name

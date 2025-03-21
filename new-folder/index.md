<script type="text/javascript" async
  src="https://polyfill.io/v3/polyfill.min.js?features=es6">
</script>
<script type="text/javascript" async
  id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
# 半导体缺陷计算专题教程

**作者：陈霆熙**  

**相关工具：[CPLAP化学势计算工具](https://github.com/jbuckeridge/cplap)**

**相关工具：[缺陷相关文献与教程](https://github.com/chentingxi36/my-tutorial/tree/main/new-folder)**

**参考书目：材料缺陷的先进计算电子结构方法 [（瑞士）阿尔卡斯卡 编] 2015年.pdf**

---


## 目录
1. [半导体与缺陷基础](#1-半导体与缺陷基础)  
2. [缺陷计算核心理论](#2-缺陷计算核心理论)  
3. [缺陷计算实践流程](#3-缺陷计算实践流程)  
4. [缺陷计算新发展](#4-缺陷计算新发展)  

---

## 1. 半导体与缺陷基础

### 1.1 半导体材料
- **定义**：导电性介于导体与绝缘体之间（如Si、GaAs、GaN）。  
- **重要性**：电子器件（晶体管、LED、太阳能电池）的核心材料。
  <p align="center">     
    <img src="https://github.com/user-attachments/assets/fe146494-a70b-4263-92ac-08682502e0de" width="600"/>
  </p>
### 1.2 半导体的性质
- **重要性**：位错，点缺陷，光、电特性，表面与界面等决定了单位应用性能的价格空间

  <p align="center">     
    <img src="https://github.com/user-attachments/assets/6d426e2c-6330-4f17-beb8-ed48f5842bf9" width="600"/>
  </p>
  
### 1.3 半导体缺陷类型
- **点缺陷**  
  - 空位缺陷（如Vₙ：氮空位）  
  - 间隙原子（如Oᵢ：氧间隙）  
  - 替代缺陷（如Alₛᵢ：硅晶格中的铝原子）  
- **复合缺陷**：多缺陷组合（如Vₙ-Oᵢ复合体）  
- **扩展缺陷**：位错、晶界、层错  

  <p align="center">  
    <img src="https://github.com/user-attachments/assets/0ee90c8f-3ed8-49fa-844d-91267d9056bd" width="600"/>
  </p>
---

## 2. 缺陷计算核心理论

### 2.1 缺陷形成能与跃迁能级
- **形成能（Formation Energy）**

  $$
  \Delta H_f (\alpha, q) = E(\alpha, q) - E(\text{host}) + \sum n_i (\mu_i + E_i) + q[\varepsilon_{\text{VBM}} (\text{host}) + E_F]
  $$

  <img src="https://github.com/user-attachments/assets/48252b9b-4376-441e-bbf5-ae196d6c1568" width="600"/>

  <p align="center">  
    <img src="https://github.com/user-attachments/assets/53fd1be8-7750-458f-bbd6-11fc2fcfbef5" width="300"/>
  </p>
  
- **跃迁能级（Transition Level）**  

  跃迁能级，又称为离化能，与实验中用Hall测量或DLTS等方法测得的数值相对应，定义为  
  
  $$
  \varepsilon(q/q') = \frac{E(\alpha, q) - E(\alpha, q')}{q - q'}
  $$
  
  其中， 𝑞和𝑞′是同一种缺陷的两种不同的带电状态
  实际的计算中，若选择的体系比较大，则可以直接用上面的公式，因为对足够大的体系BZ内的所有的点都折叠到Gamma点。受计算条件的限制，一般都对小的supercell，此时对施受主离化能的计算可以采用通过G点与芯能级来对跃迁能级进行矫正.

- **受主能级**
  
  $$
  \varepsilon(0/q) = \left[ \varepsilon_D^\Gamma (0) - E(1s, \text{defect}) - (\varepsilon_{VBM}^\Gamma (\text{host}) - E(1s, \text{host})) \right] + \frac{E(\alpha, q) - (E(\alpha, 0) - q \varepsilon_D^k (0))}{-q}
  $$

- **施主能级**
  
  $$
  \varepsilon_g^\Gamma (\text{host}) - \varepsilon(0/q) = -\left[ \varepsilon_D^\Gamma (0) - E(1s, \text{defect}) - (\varepsilon_{CBM}^\Gamma (\text{host}) - E(1s, \text{host})) \right] + \frac{E(\alpha, q) - (E(\alpha, 0) - q \varepsilon_D^k (0))}{q}
  $$

  <p align="center">
    <img src="https://github.com/user-attachments/assets/49e72fa8-6207-491e-8bb7-e45d910d1539" width="300"/>
  </p>



- **形成能计算示例**
  <p align="center">
    <img src="https://github.com/user-attachments/assets/b81fa468-bb69-40ce-9be7-e7b8f4266b33" width="800"/>  
  </p>
  
### 2.2 载流子浓度与费米能级
- **载流子浓度公式**
  <p align="center">
    <img src="https://github.com/user-attachments/assets/9a8c2291-de1b-425c-8279-470f75e7c666" width="200"/>
  </p>
- **举例-V_Ta**

  $$
  N_{\text{site}} = \frac{32}{\text{Volume}_{\text{super}} (E - 24)}
  $$  
  $$
  N_C = \frac{\text{ITDOSCB}}{\text{Volume}_{\text{super}} (E - 24)}
  $$
  
  $$
  N_V = \frac{\text{ITDOSVB}}{\text{Volume}_{\text{super}} (E - 24)}
  $$  
  $$
  g_p = 1
  $$
  
  $N_{\text{site}}$: the density of possible sites on the defect form
  
  $g_q$: the degeneracy facto
  
  k$B$: Boltzmann constant
  
  T: the temperature
  
  $n_0$: the density of free electron carriers
  
  $p_0$: the density of free hole carriers
  
  $N_C$: the effective density of states at the conduction band edges
  
  $N_V$: the effective density of states at the valence band edges


### 2.3 位形坐标模型
- **光学转变能级**：通过位形坐标图分析缺陷发光/吸收特性

  <p align="center">
    <img src="https://github.com/user-attachments/assets/c5686503-4f20-45ba-a9e2-7195dd257be1" width="500"/>
  </p>
  
- **马库斯理论**：描述非辐射复合过程的经典模型
- 
  <p align="center">
    <img src="https://github.com/user-attachments/assets/076d463a-5cca-4a3a-bff2-54b2386cbf0f" width="500"/>
  </p>

### 2.4 缺陷的复合过程

  <p align="center">
    <img src="https://github.com/user-attachments/assets/dbfe5487-39a9-4cf9-92cc-8693b92a8dad" width="500"/>
  </p>
  
### 2.5 费米能级钉扎

  $$
  n(\alpha, q) = N_0 e^{-\frac{\Delta H_f (\alpha, q)}{k_B T}}
  $$
  
  $$
  p_0 + n_{\text{donor}} |q_{\text{donor}}| = n_0 + n_{\text{acceptor}} |q_{\text{acceptor}}|
  $$
  
  $$
  \Delta H_1 = k_B T \ln \left( \frac{g_B \cdot N_{\text{site}}}{N_v} \right) + E_F
  $$
  
  $$
  \Delta H_2 = k_B T \ln \left( \frac{g_A \cdot N_{\text{site}}}{N_C} \right) + (E_g - E_F)
  $$
  

  <p align="center">
    <img src="https://github.com/user-attachments/assets/5afc25ee-1112-4f14-9d34-b2aee017b0b3" width="700"/>
  </p>

---

## 3. 缺陷计算实践流程

### 3.1 缺陷结构搭建与优化
1. **超胞构建**  
   - 使用VASP构建含缺陷的超胞（如`POSCAR`中删除原子模拟空位）。  
2. **结构优化**  
   ```bash
   # 原胞
   ISIF = 3   # 优化原子与晶格
   # 超晶胞
   ISIF = 2   # 优化原子
   # 缺陷超晶胞
   ISIF = 2   # 优化原子
   NELECT = NELECT(supercell)±q
   #举例
   对于VN缺陷，不加电子，grep NELECT OUTCAR，得到NELECT=691
   考虑q=+1、+2、+3的情况，则NELECT分别为690、689、688

### 3.2 化学势计算
1. **确定材料中可能的竞争物种（如Si、SiO₂、O₂）**  
2. **构建线性规划方程组求解化学势范围** 
3. **使用工具自动化计算（推荐CPLAP）**

  <p align="center">
    <img src="https://github.com/user-attachments/assets/55e77356-81ea-476c-a307-59c7f5ce2841" width="600"/>
  </p>

### 3.3 形成能与跃迁能级计算
1. **中性缺陷计算** 
   <pre><code>
   # INCAR关键参数
   grep TOTEN OUTCAR        # 提取总能量
   grep "1s" OUTCAR         # 提取1s轨道能量（用于能级对齐）
   </code></pre>
    <p align="center">
      <img src="https://github.com/user-attachments/assets/96b30f9b-d982-4dc9-8424-2ea21085e36b" width="500"/>
    </p>

   
2. **相关参数获取**
修改NELECT参数模拟不同电荷态：
  <pre><code>
  # INCAR关键参数
  q=+1 → NELECT=690（原为691）
  q=+2 → NELECT=689
  </code></pre>

  <p align="center">
    <img src="https://github.com/user-attachments/assets/8f21696e-9cdf-4f7a-a90e-ae035e5edcf1" width="800"/>
  </p>


3. **形成能具体计算**   

  <p align="center">
    <img src="https://github.com/user-attachments/assets/bdcf5380-fb65-45dc-93cb-db19919bb33f" width="600"/>
  </p>

4. **电离能具体计算**
   
  <p align="center">
    <img src="https://github.com/user-attachments/assets/708cf7b8-987f-489e-b20a-7af95357640e" width="600"/>
  </p>

---

## 4. 缺陷计算新发展

  <p align="center">
    <img src="https://github.com/user-attachments/assets/f203a84e-d510-4c4e-89c5-4f8d413842d7" width="600"/>
  </p>


版权声明
本文档采用 CC BY-NC-SA 4.0 协议，转载需注明作者与来源。
问题反馈：欢迎在GitHub提交Issue或通过邮箱联系！

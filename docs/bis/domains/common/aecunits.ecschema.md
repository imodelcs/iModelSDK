# AECUnits (设计建模单位) Schema

**别名 (Alias):** AECU

**版本 (Version):** 1.0.3

本 Schema 包含在 AE Schemas 中使用的单位定义。

## 目录

- Kind Of Quantities (量种类)
  - ACCELERATION (加速度)
  - ANGLE (角度)
  - ANGULAR_VELOCITY (角速度)
  - AREA (面积)
  - AREA_FORCE (面力)
  - AREA_FORCE_LARGE (大面力)
  - AREA_FORCE_SMALL (小面力)
  - AREA_LARGE (大面积)
  - AREA_MOMENT (面矩)
  - AREA_MOMENT_LARGE (大面矩)
  - AREA_MOMENT_SMALL (小面矩)
  - AREA_SMALL (小面积)
  - AREA_SPRING_CONSTANT (面弹簧常数)
  - CURRENT (电流)
  - DENSITY (密度)
  - DYNAMIC_VISCOSITY (动力粘度)
  - ELECTRIC_POTENTIAL (电势)
  - ENERGY (能量)
  - FLOW (流量)
  - FORCE (力)
  - FORCE_DENSITY (力密度)
  - FORCE_LARGE (大力度)
  - FORCE_SMALL (小力度)
  - FREQUENCY (频率)
  - HEAT_TRANSFER (传热)
  - ILLUMINANCE (照度)
  - LENGTH (长度)
  - LENGTH_LONG (长长度)
  - LENGTH_SHORT (短长度)
  - LINEAR_DENSITY (线密度)
  - LINEAR_FORCE (线力)
  - LINEAR_FORCE_LARGE (大线力)
  - LINEAR_FORCE_SMALL (小线力)
  - LINEAR_MOMENT (线矩)
  - LINEAR_MOMENT_LARGE (大线矩)
  - LINEAR_MOMENT_SMALL (小线矩)
  - LINEAR_ROTATIONAL_SPRING_CONSTANT (线旋转弹簧常数)
  - LINEAR_SPRING_CONSTANT (线弹簧常数)
  - LIQUID_VOLUME (液体体积)
  - LIQUID_VOLUME_LARGE (大液体体积)
  - LIQUID_VOLUME_SMALL (小液体体积)
  - LUMINOUS_FLUX (光通量)
  - LUMINOUS_INTENSITY (发光强度)
  - MOMENT (力矩)
  - MOMENT_LARGE (大力矩)
  - MOMENT_OF_INERTIA (转动惯量)
  - MOMENT_SMALL (小力矩)
  - POWER (功率)
  - PRESSURE (压力)
  - PRESSURE_GRADIENT (压力梯度)
  - PROBABILITY (概率)
  - PROCESS_PIPING_FLOW (工艺管道流量)
  - PROCESS_PIPING_PRESSURE (工艺管道压力)
  - PROCESS_PIPING_TEMPERATURE (工艺管道温度)
  - ROTATIONAL_SPRING_CONSTANT (旋转弹簧常数)
  - SPECIFIC_HEAT_CAPACITY (比热容)
  - SPECIFIC_HEAT_OF_VAPORIZATION (汽化比热)
  - SPRING_CONSTANT (弹簧常数)
  - TEMPERATURE (温度)
  - THERMAL_CONDUCTIVITY (热导率)
  - THERMAL_EXPANSION_COEFFICIENT (热膨胀系数)
  - THERMAL_RESISTANCE (热阻)
  - TIME (时间)
  - VELOCITY (速度)
  - VOLUME (体积)
  - VOLUME_LARGE (大体积)
  - VOLUME_SMALL (小体积)
  - WARPING_CONSTANT (翘曲常数)
  - WEIGHT (重量)

## Kind Of Quantities (量种类)

### __ACCELERATION__ (加速度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** M_PER_SEC_SQ

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ M_PER_SEC_SQ ]
- DefaultRealU(4) [ CM_PER_SEC_SQ ]
- DefaultRealU(4) [ FT_PER_SEC_SQ ]

### __ANGLE__ (角度) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** RAD

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ ARC_DEG ]
- AngleDMS

### __ANGULAR_VELOCITY__ (角速度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** RAD_PER_SEC

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ RAD_PER_SEC ]
- DefaultRealU(4) [ DEG_PER_SEC ]
- DefaultRealU(4) [ RPM ]

### __AREA__ (面积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ SQ_M ]
- DefaultRealU(4) [ SQ_FT ]

### __AREA_FORCE__ (面力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** PA

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KILOPASCAL ]
- DefaultRealU(4) [ PSF ]

### __AREA_FORCE_LARGE__ (大面力) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** PA

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAPASCAL ]
- DefaultRealU(4) [ KSF ]

### __AREA_FORCE_SMALL__ (小面力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** PA

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ PA ]
- DefaultRealU(4) [ PSF ]

### __AREA_LARGE__ (大面积) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ SQ_KM ]
- DefaultRealU(4) [ SQ_MILE ]

### __AREA_MOMENT__ (面矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M_PER_SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KN_M_PER_SQ_M ]
- DefaultRealU(4) [ LBF_FT_PER_SQ_FT ]

### __AREA_MOMENT_LARGE__ (大面矩) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** N_M_PER_SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAN_M_PER_SQ_M ]
- DefaultRealU(4) [ KPF_FT_PER_SQ_FT ]

### __AREA_MOMENT_SMALL__ (小面矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M_PER_SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ N_M_PER_SQ_M ]
- DefaultRealU(4) [ LBF_IN_PER_SQ_IN ]

### __AREA_SMALL__ (小面积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ SQ_MM ]
- DefaultRealU(4) [ SQ_IN ]

### __AREA_SPRING_CONSTANT__ (面弹簧常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** AREA_SPRING_CONSTANT_N_PER_CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ AREA_SPRING_CONSTANT_N_PER_CUB_M ]
- DefaultRealU(4) [ AREA_SPRING_CONSTANT_KN_PER_CUB_M ]
- DefaultRealU(4) [ AREA_SPRING_CONSTANT_KPF_PER_CUB_FT ]

### __CURRENT__ (电流) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** A

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ A ]
- DefaultRealU(4) [ KILOAMPERE ]

### __DENSITY__ (密度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** KG_PER_CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KG_PER_CUB_M ]
- DefaultRealU(4) [ LBM_PER_CUB_FT ]
- DefaultRealU(4) [ G_PER_CUB_CM ]
- DefaultRealU(4) [ LBM_PER_CUB_IN ]
- DefaultRealU(4) [ KIP_PER_CUB_FT ]

### __DYNAMIC_VISCOSITY__ (动力粘度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** PA_S

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ PA_S ]
- DefaultRealU(4) [ POISE ]
- DefaultRealU(4) [ CENTIPOISE ]
- DefaultRealU(4) [ LBM_PER_FT_S ]

### __ELECTRIC_POTENTIAL__ (电势) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** VOLT

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ VOLT ]
- DefaultRealU(4) [ KILOVOLT ]
- DefaultRealU(4) [ MEGAVOLT ]

### __ENERGY__ (能量) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** J

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ J ]
- DefaultRealU(4) [ KJ ]
- DefaultRealU(4) [ BTU ]
- DefaultRealU(4) [ KWH ]

### __FLOW__ (流量) KindOfQuantity

**相对误差 (Relative Error):** 0.00001

**持久化单位 (Persistence Unit):** CUB_M_PER_SEC

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LITRE_PER_MIN ]
- DefaultRealU(4) [ CUB_FT_PER_MIN ]
- DefaultRealU(4) [ GALLON_PER_MIN ]

### __FORCE__ (力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KN ]
- DefaultRealU(4) [ LBF ]

### __FORCE_DENSITY__ (力密度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** N_PER_CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ N_PER_CUB_M ]
- DefaultRealU(4) [ KN_PER_CUB_M ]
- DefaultRealU(4) [ N_PER_CUB_FT ]
- DefaultRealU(4) [ KN_PER_CUB_FT ]

### __FORCE_LARGE__ (大力度) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** N

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAN ]
- DefaultRealU(4) [ KPF ]

### __FORCE_SMALL__ (小力度) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ N ]
- DefaultRealU(4) [ LBF ]

### __FREQUENCY__ (频率) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** HZ

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ HZ ]
- DefaultRealU(4) [ KHZ ]
- DefaultRealU(4) [ MHZ ]

### __HEAT_TRANSFER__ (传热) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** W_PER_SQ_M_K

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ W_PER_SQ_M_K ]
- DefaultRealU(4) [ W_PER_SQ_M_CELSIUS ]
- DefaultRealU(4) [ BTU_PER_SQ_FT_HR_FAHRENHEIT ]

### __ILLUMINANCE__ (照度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** LUX

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LUX ]
- DefaultRealU(4) [ LUMEN_PER_SQ_FT ]

### __LENGTH__ (长度) KindOfQuantity

**相对误差 (Relative Error):** 0.00001

**持久化单位 (Persistence Unit):** M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ M ]
- DefaultRealU(4) [ MM ]
- AmerFI
- AmerFI(16)
- DefaultRealU(4) [ FT ]

### __LENGTH_LONG__ (长长度) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KM ]
- DefaultRealU(4) [ M ]
- AmerFI
- AmerFI(16)
- DefaultRealU(4) [ FT ]

### __LENGTH_SHORT__ (短长度) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** M

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ MM ]
- DefaultRealU(4) [ CM ]
- AmerFI
- AmerFI(16)
- DefaultRealU(4) [ IN ]

### __LINEAR_DENSITY__ (线密度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** KG_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KG_PER_M ]
- DefaultRealU(4) [ KG_PER_MM ]
- DefaultRealU(4) [ LBM_PER_FT ]

### __LINEAR_FORCE__ (线力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KN_PER_M ]
- DefaultRealU(4) [ LBF_PER_FT ]

### __LINEAR_FORCE_LARGE__ (大线力) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** N_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAN_PER_M ]
- DefaultRealU(4) [ KPF_PER_FT ]

### __LINEAR_FORCE_SMALL__ (小线力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ N_PER_M ]
- DefaultRealU(4) [ LBF_PER_FT ]

### __LINEAR_MOMENT__ (线矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KN_M_PER_M ]
- DefaultRealU(4) [ LBF_FT_PER_FT ]

### __LINEAR_MOMENT_LARGE__ (大线矩) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** N_M_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAN_M_PER_M ]
- DefaultRealU(4) [ KPF_FT_PER_FT ]

### __LINEAR_MOMENT_SMALL__ (小线矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ N_M_PER_M ]
- DefaultRealU(4) [ LBF_FT_PER_FT ]

### __LINEAR_ROTATIONAL_SPRING_CONSTANT__ (线旋转弹簧常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** N_PER_RAD

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ N_PER_RAD ]
- DefaultRealU(4) [ KN_PER_RAD ]
- DefaultRealU(4) [ KPF_PER_RAD ]

### __LINEAR_SPRING_CONSTANT__ (线弹簧常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** LINEAR_SPRING_CONSTANT_N_PER_SQ_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LINEAR_SPRING_CONSTANT_N_PER_SQ_M ]
- DefaultRealU(4) [ LINEAR_SPRING_CONSTANT_KN_PER_SQ_M ]
- DefaultRealU(4) [ LINEAR_SPRING_CONSTANT_KPF_PER_SQ_FT ]

### __LIQUID_VOLUME__ (液体体积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LITRE ]
- DefaultRealU(4) [ GALLON ]

### __LIQUID_VOLUME_LARGE__ (大液体体积) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ THOUSAND_LITRE ]
- DefaultRealU(4) [ THOUSAND_GALLON ]

### __LIQUID_VOLUME_SMALL__ (小液体体积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LITRE ]
- DefaultRealU(4) [ GALLON ]

### __LUMINOUS_FLUX__ (光通量) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** LUMEN

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LUMEN ]

### __LUMINOUS_INTENSITY__ (发光强度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** CD

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ CD ]

### __MOMENT__ (力矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ KN_M ]
- DefaultRealU(4) [ LBF_FT ]

### __MOMENT_LARGE__ (大力矩) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** N_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ MEGAN_M ]
- DefaultRealU(4) [ KPF_FT ]

### __MOMENT_OF_INERTIA__ (转动惯量) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** M_TO_THE_FOURTH

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ M_TO_THE_FOURTH ]
- DefaultRealU(4) [ MM_TO_THE_FOURTH ]
- DefaultRealU(4) [ CM_TO_THE_FOURTH ]
- DefaultRealU(4) [ IN_TO_THE_FOURTH ]
- DefaultRealU(4) [ FT_TO_THE_FOURTH ]

### __MOMENT_SMALL__ (小力矩) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** N_M

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ N_M ]
- DefaultRealU(4) [ LBF_FT ]

### __POWER__ (功率) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** W

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ W ]
- DefaultRealU(4) [ KW ]
- DefaultRealU(4) [ MEGAW ]
- DefaultRealU(4) [ BTU_PER_HR ]
- DefaultRealU(4) [ KILOBTU_PER_HR ]
- DefaultRealU(4) [ HP ]

### __PRESSURE__ (压力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** PA

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ PA ]
- DefaultRealU(4) [ PSIG ]
- DefaultRealU(4) [ PSI ]

### __PRESSURE_GRADIENT__ (压力梯度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** PA_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ PA_PER_M ]
- DefaultRealU(4) [ BAR_PER_KM ]

### __PROBABILITY__ (概率) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** PROBABILITY_FRACTION

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ PROBABILITY_PERCENT ]

### __PROCESS_PIPING_FLOW__ (工艺管道流量) KindOfQuantity

**相对误差 (Relative Error):** 0.00001

**持久化单位 (Persistence Unit):** CUB_M_PER_SEC

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ LITRE_PER_MIN ]
- DefaultRealU(4) [ CUB_FT_PER_MIN ]
- DefaultRealU(4) [ GALLON_PER_MIN ]

### __PROCESS_PIPING_PRESSURE__ (工艺管道压力) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** PA

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ PA ]
- DefaultRealU(4) [ PSIG ]
- DefaultRealU(4) [ PSI ]

### __PROCESS_PIPING_TEMPERATURE__ (工艺管道温度) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** K

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ CELSIUS ]
- DefaultRealU(2) [ FAHRENHEIT ]
- DefaultRealU(4) [ K ]

### __ROTATIONAL_SPRING_CONSTANT__ (旋转弹簧常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** N_M_PER_RAD

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ N_M_PER_RAD ]
- DefaultRealU(4) [ KN_M_PER_RAD ]
- DefaultRealU(4) [ KPF_FT_PER_RAD ]

### __SPECIFIC_HEAT_CAPACITY__ (比热容) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** J_PER_KG_K

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ J_PER_KG_K ]
- DefaultRealU(4) [ BTU_PER_LBM_RANKINE ]

### __SPECIFIC_HEAT_OF_VAPORIZATION__ (汽化比热) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** J_PER_KG

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ J_PER_KG ]
- DefaultRealU(4) [ KJ_PER_KG ]
- DefaultRealU(4) [ BTU_PER_LBM ]

### __SPRING_CONSTANT__ (弹簧常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** SPRING_CONSTANT_N_PER_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ SPRING_CONSTANT_N_PER_M ]
- DefaultRealU(4) [ SPRING_CONSTANT_KN_PER_M ]
- DefaultRealU(4) [ SPRING_CONSTANT_KPF_PER_FT ]

### __TEMPERATURE__ (温度) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** K

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ CELSIUS ]
- DefaultRealU(4) [ FAHRENHEIT ]
- DefaultRealU(4) [ K ]

### __THERMAL_CONDUCTIVITY__ (热导率) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** W_PER_M_K

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ W_PER_M_K ]
- DefaultRealU(4) [ W_PER_M_C ]
- DefaultRealU(4) [ BTU_IN_PER_SQ_FT_HR_FAHRENHEIT ]

### __THERMAL_EXPANSION_COEFFICIENT__ (热膨胀系数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** STRAIN_PER_KELVIN

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ STRAIN_PER_KELVIN ]
- DefaultRealU(4) [ STRAIN_PER_CELSIUS ]
- DefaultRealU(4) [ STRAIN_PER_FAHRENHEIT ]

### __THERMAL_RESISTANCE__ (热阻) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** SQ_M_KELVIN_PER_WATT

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ SQ_M_KELVIN_PER_WATT ]
- DefaultRealU(4) [ SQ_M_CELSIUS_PER_WATT ]
- DefaultRealU(4) [ SQ_FT_HR_FAHRENHEIT_PER_BTU ]

### __TIME__ (时间) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** S

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ S ]
- DefaultRealU(4) [ MIN ]
- DefaultRealU(4) [ HR ]
- DefaultRealU(4) [ DAY ]
- DefaultRealU(4) [ MS ]

### __VELOCITY__ (速度) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** M_PER_SEC

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ M_PER_SEC ]
- DefaultRealU(4) [ FT_PER_SEC ]
- DefaultRealU(4) [ MPH ]
- DefaultRealU(4) [ KM_PER_HR ]

### __VOLUME__ (体积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ CUB_M ]
- DefaultRealU(4) [ CUB_FT ]
- DefaultRealU(4) [ CUB_YRD ]

### __VOLUME_LARGE__ (大体积) KindOfQuantity

**相对误差 (Relative Error):** 0.01

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ CUB_KM ]
- DefaultRealU(4) [ CUB_M ]
- DefaultRealU(4) [ CUB_YRD ]
- DefaultRealU(4) [ CUB_FT ]

### __VOLUME_SMALL__ (小体积) KindOfQuantity

**相对误差 (Relative Error):** 0.0001

**持久化单位 (Persistence Unit):** CUB_M

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ CUB_MM ]
- DefaultRealU(4) [ CUB_CM ]
- DefaultRealU(4) [ CUB_IN ]
- DefaultRealU(4) [ CUB_FT ]

### __WARPING_CONSTANT__ (翘曲常数) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** M_TO_THE_SIXTH

**展示格式 (Presentation Formats)**
- DefaultRealU(4) [ M_TO_THE_SIXTH ]
- DefaultRealU(4) [ FT_TO_THE_SIXTH ]

### __WEIGHT__ (重量) KindOfQuantity

**相对误差 (Relative Error):** 0.001

**持久化单位 (Persistence Unit):** KG

**展示格式 (Presentation Formats)**
- DefaultRealU(2) [ KG ]
- DefaultRealU(2) [ LBM ]

---

**来源:** https://www.itwinjs.org/bis/domains/aecunits.ecschema/

**最后更新:** 2025年6月11日

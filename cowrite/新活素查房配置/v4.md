新活素查房配置

## 一、产品与医院映射

新活素(XZ) 覆盖 17 家医院：

1. 乌兰察布市第三医院
2. 化德县医院
3. 察右后旗医院
4. 兴和县医院
5. 商都县医院
6. 卓资县人民医院
7. 商都县中医院
8. 化德县中蒙医院
9. 锡盟苏尼特右旗医院
10. 内蒙古自治区兴和县蒙中医院
11. 深圳市南山医院
12. 龙岗区儿童医院
13. 福田妇幼保健院（新增）

## 二、采集 Schema（模型-新活素查房日反馈）

| 字段 | 说明 |
|---|---|
| heartFailurePatientCount | 心衰患者数 |
| admittedPatientCount | 收治患者数 |
| indicatedPatientCount | 有用药指征患者数 |
| heartFailureMedicationPatientCount | 心衰用药患者数 |
| indicatedMedicationPatientCount | 有用药指征用药患者数 |
| heartFailureMedicationDoseCount | 心衰用药支数 |
| indicatedSelfPayDoseCount | 有用药指征自费用药支数 |
| heartFailureSelfPayDoseCount | 心衰自费用药支数 |
| heartFailureShortCoursePatientCount | 心衰疗程低于3天患者数 |
| heartFailureLowDosagePatientCount | 心衰剂量低于0.01的患者数 |
| indicatedLowDosagePatientCount | 有用药指征剂量低于0.01的患者数 |

## 三、原始 JSON Schema

```json
{"model":{"type":"object","title":"模型-新活素查房日反馈","properties":{"heartFailureLowDosagePatientCount":{"x-ai":true,"type":"string","title":"心衰剂量低于0.01的患者数"},"indicatedLowDosagePatientCount":{"x-ai":true,"type":"string","title":"有用药指征剂量低于0.01的患者数"},"hcoId":{"x-ai":true,"x-hidden":true,"type":"string","title":"医院ID"},"hcoName":{"x-ai":true,"type":"string","title":"医院名称"},"indicatedSelfPayDoseCount":{"x-ai":true,"type":"string","title":"有用药指征自费用药支数"},"heartFailureMedicationDoseCount":{"x-ai":true,"type":"string","title":"心衰用药支数"},"indicatedMedicationPatientCount":{"x-ai":true,"type":"string","title":"有用药指征用药患者数"},"heartFailureShortCoursePatientCount":{"x-ai":true,"type":"string","title":"心衰疗程低于3天患者数"},"heartFailurePatientCount":{"x-ai":true,"type":"string","title":"心衰患者数"},"indicatedPatientCount":{"x-ai":true,"type":"string","title":"有用药指征患者数"},"admittedPatientCount":{"x-ai":true,"type":"string","title":"收治患者数"},"heartFailureSelfPayDoseCount":{"x-ai":true,"type":"string","title":"心衰自费用药支数"},"heartFailureMedicationPatientCount":{"x-ai":true,"type":"string","title":"心衰用药患者数"}}}}
```

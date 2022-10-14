# ผลการวิเคราะห์ข้อมูล จังหวัดที่นิยมไปเที่ยวในแต่ละเดือน

# ข้อมูล
ได้มีการนำข้อมูล **สถานการณ์การท่องเที่ยวในประเทศ รายจังหวัด** จาก [กระทรวงการท่องเที่ยวและกีฬา(Ministry of Tourism & Sports)](https://www.mots.go.th/more_news_new.php?cid=411)

> ข้อมูลปี 2563 (มกราคม ถึง ธันวาคม) = 924 Row
> ข้อมูลปี 2564 (มกราคม ถึง ธันวาคม) = 924 Row
> ข้อมูลปี 2565 (มกราคม ถึง มิถุนายน) = 462 Row
> รวมทั้งหมด 2310 Row

![This is an image](/assets/images/ตัวอย่างไฟล์Excel.png)

นำข้อมูลจากไฟล์ Excel มาจัดให้อยู่ในรูปแปป csv โดยหยิบข้อมูล
- ปี (year)
- เดือน (month)
- ภูมิภาค (region)
- จังหวัด (province)
- จำนวนผู้เยี่ยมเยือนคนไทย/คน (thai_visitors)
- จำนวนผู้เยี่ยมเยือนชาวต่างชาติ/คน (foreign_visitors)
- รายได้จากผู้เยี่ยมเยือนคนไทย/ล้านบาท (income_from_thai_visitors)
- รายได้จากผู้เยี่ยมเยือนชาวต่างชาติ/ล้านบาท (income_from_foreign_visitors)

![This is an image](/assets/images/ตัวอย่างไฟล์CSV.png)

มีการตรวยสอบพบข้อมูลที่เป็น null

```
data.isnull().any()

year                            False
month                           False
region                          False
province                        False
thai_visitors                    True
foreign_visitors                False
income_from_thai_visitors        True
income_from_foreign_visitors    False
dtype: bool
```

พบว่ามีข้อมูล จำนวนผู้เยี่ยมเยือนคนไทย และ รายได้จากผู้เยี่ยมเยือนคนไทย เป็น null จึงขอเปลี่ยนเป็นค่า 0

```
data.loc[data['thai_visitors'].isnull(), 'thai_visitors'] = 0
data.loc[data['income_from_thai_visitors'].isnull(), 'income_from_thai_visitors'] = 0
```

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

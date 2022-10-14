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

พบว่ามีข้อมูล thai_visitors และ income_from_thai_visitors เป็น null จึงขอเปลี่ยนเป็นค่า 0

```
data.loc[data['thai_visitors'].isnull(), 'thai_visitors'] = 0
data.loc[data['income_from_thai_visitors'].isnull(), 'income_from_thai_visitors'] = 0
```

นำข้อมูลของ thai_visitors รวมกับ foreign_visitors สร้าง column ใหม่ชื่อ thai_and_foreign_visitors

```
data = data.astype({"thai_visitors":'int', "foreign_visitors":'int'}) 
data["thai_and_foreign_visitors"] = data["thai_visitors"] + data["foreign_visitors"]
```

ได้จับกลุ่มข้อมูลตามเดือน พบว่าจังหวัด กรุงเทพมหานคร มีผู้มาเยี่ยมเยือนมากในทุกเดือน จึงขอตัด

```
thaiAndForeignVisitorsMax = data.groupby(['month'])['thai_and_foreign_visitors'].transform(max) == data['thai_and_foreign_visitors']
data[thaiAndForeignVisitorsMax].loc[:, ["month","province"]]
```

พบว่าในแต่ละเดือน กรุงเทพมหานคร มีผู้เยี่ยมเยือนมากที่สุด

| index | month | province | mean |
| ------------- | ------------- | ------------- | ------------- |
| 0 | กรกฎาคม | กรุงเทพมหานคร | 598675.5 |
| 1 | กันยายน | กรุงเทพมหานคร | 1115421.0 |
| 2 | กุมภาพันธ์ | กรุงเทพมหานคร | 2670254.0 |
| 3 | ตุลาคม | กรุงเทพมหานคร | 1237583.5 |
| 4 | ธันวาคม | กรุงเทพมหานคร | 2421903.0 |
| 5 | พฤศจิกายน | กรุงเทพมหานคร | 1829488.5 |
| 6 | พฤษภาคม | กรุงเทพมหานคร | 1202940.0 |
| 7 | มกราคม | กรุงเทพมหานคร | 2950722.0 |
| 8 | มิถุนายน | กรุงเทพมหานคร | 1363841.0 |
| 9 | มีนาคม | กรุงเทพมหานคร | 1931712.0 |
| 10 | สิงหาคม | กรุงเทพมหานคร | 1001080.0 |
| 11 | เมษายน | กรุงเทพมหานคร | 1390232.0 |

จึงตัด กรุงเทพมหานคร ออกและแสดง Top 5 ของแต่ละเดือน

![This is an image](/assets/images/bar1.png)
![This is an image](/assets/images/bar2.png)
![This is an image](/assets/images/bar3.png)
![This is an image](/assets/images/bar4.png)
![This is an image](/assets/images/bar5.png)
![This is an image](/assets/images/bar6.png)
![This is an image](/assets/images/bar7.png)
![This is an image](/assets/images/bar8.png)
![This is an image](/assets/images/bar9.png)
![This is an image](/assets/images/bar10.png)
![This is an image](/assets/images/bar11.png)
![This is an image](/assets/images/bar12.png)
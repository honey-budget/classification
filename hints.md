-> the problem to tranform from library sklearn

`

    x_train_scaled = scaler.fit_transform(x_train)
    x_test_scaled = scaler.transform(x_test)

`

=-> ValueError Traceback (most recent call last)  Cell In[115], line 9

hint : i think that problem from the shape there are not matching between x_train and x_test 

_____________________________________________________________________________________
Case study (1)
_____________________________________________________________________________________

#Split test and train datasets

from sklearn.model_selection import train_test_split

x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, stratify=y)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
'''

    ในส่วนตรงนี้มีข้อจำกัดในการเรียงลำดับของการทำงาน ปัญหาที่พบจะเป็นการที่ shape สูญหาย 
    (85, ) ซึ่งเราต้องการมให้ได้ shape ในลักษณะ (85, 30) แต่ผลมาจาก train_test_split
    มีลำดับของ parameter เป็นคู่ เช่น x_trian x_test และ y_trian y_test ดังนี้ 
    แต่จากกรณีดังกล่าว ผู้เขียน ได้เขียนในรูปแบบ x_train x_test .... จึงก่อให้เกิดปัญหาทางด้าน shape ที่ได้มีปัญหา

'''

$ Result : 
`
    shape of x_test : (85, 30) 
    shape of x_train: (85, 30)
`


# test and train datasets are imbalanced
'''

    ในส่วนนี้ก็อย่างที่ได้กล่าวไปเราพยายามที่จะแก้ปัญหาของความ imbalanced ของข้อมูล test กับ train ที่มีความแตกต่างกันให้เท่ากัน 


    !!! แก้ไข

        ในความเป็นจริง การที่ trian และ test ไม่เท่ากัน ไม่ก่อให้เกิดปัญหาของ imbalanced เนื่องจาก เปรียบ train เป็นข้อสอบที่นักศึกษาต้องทำ ส่วน test เป็นเหมือนเฉลยของปัญหาเท่านั้น เหมือนให้ทำหลายข้อแต่คำตอบที่เกิดขึ้นอาจจะใช้จากแหล่ง test เพียงพอแล้ว

'''
arr_x_train = x_train.index 


x_train_rand_num = np.random.permutation(arr_x_train).reshape(len(arr_x_train), 1)

x_train.drop(index=x_train_rand_num[0:254, 0], inplace=True)

_____________________________________________________________________________________
Case study (2)
_____________________________________________________________________________________
    
    y_train = y_train.map({'B': 0, 'M': 1}).astype(int)
    y_train.dropna()
    fpr, tpr, _ = roc_curve(y_train, y_scores)
    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
'''
    !!! ปัญหาจาก roc_curve โดยเป็นปัญหาที่ y_true จาก doc หมายถึง
    sklearn.metrics.roc_curve(y_true, y_score, *, pos_label=None, sample_weight=None, drop_intermediate=True)

    หรือ parameter ตัวแรก ของเราก็คือ y_train นั้นมีปัญหา

'''
    roc_auc = auc(fpr, tpr)

- Error > ValueError: y_true takes value in {'B', 'M'} and pos_label is not specified: either make y_true take value in {0, 1} or {-1, 1} or pass pos_label explicitly.
- Error > valueerror: input y_true contains nan.
'''

    !!! แก้ไข
            1) จาก Error เห็นได้ว่ามีค่าที่ไม่ถูกต้องอยู่นั้นคือ จาก Dataset เราให้ B M เป็นคำตอบของ Model แต่เมื่อจะนำมาใช้งานต่อ นั้นมีปัญหาที่ ROC นั้นรับ parameter
        เป็นประเภท {0, 1} หรือ {-1 ,1 } เท่านั้น
            2) จาก Error มีข้อมูลที่มีค่าเป็น NaN



        แนวทางการแก้ไขเราจะแบ่งเป็น 2 ขั้นตอน 
            1) แก้ไขปัญหาของ 'M' และ 'B' โดยวิธีการแปลงโดยใช้การ map

            >       y_train = y_train.map({'B': 0, 'M': 1}).astype(int)

            โดยเราจะ map จาก 'B' ไปเป็น 0 และ 'M' ไปเป็น 1 โดยที่กำหนดค่าให้เป็นจำนวนเต็ม

            2) แก้ไขข้อมูลที่มีค่าเป็น NaN โดย
            
            >       y_train.dropna()


    โดยจาก doc ทำให้เราทราบว่า y_true ที่ lib หมายถึงก็คือ y_train ที่มีปัญหา

'''


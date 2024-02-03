#คำถามจากปัญหา

1. จากการใช้ sklearn ทดสอบหลากหลาย Models ที่เป็นไปได้จะเห็นได้ว่า มีบาง Model ที่ทำงานได้ดีซึ่งมีอยู่หลาย Models แล้วเราจะทราบได้อยากใดว่า Model ใดทำงานได้ดีที่สุด
นอกจากคะแนนจากการทำนาย

ข้อมูลจาก Breast_cancer.csv

ผลการทำนาย 

$ Decision Tree                             #1
c_chart= [[170   0]
         [  0 169]]

 $ Random Forest                            #1
c_chart= [[170   0]
         [  0 169]]

 $ Gradient Boosting                        #1
c_chart= [[170   0]
         [  0 169]]

 $ AdaBoost                                 #1
c_chart= [[170   0]
         [  0 169]]

$ Logistic Regression
c_chart= [[168  2]                          #2
         [  5 164]]

 $ Neural Network                           #3
c_chart= [[170   0]
         [  4 165]]

 $ SVM                                      #4
c_chart= [[167   3]
         [  6 163]]

 $ K-Nearest Neighbors                      #5
c_chart= [[166   4]
         [  7 162]]

 $ Naive Bayes                              #6
c_chart= [[160  10]
         [ 18 151]]



2. มีวิธีการสร้าง Dataset หรือดัดแปลงเพื่อเพิ่มปริมาณ Dataset ที่ใช้ในการ train หรือไม่ เช่น ถ้าเป็นรูปภาพ อาจเป็นการใส่ noise เป็นต้น


3. ผลลัพธ์ให้ผลที่แตกต่างกับ Dataset อีกเรื่องเล็กน้อยด้านความแม่นยำ ปัจจัยใดบ้างที่มีผลต่อความแม่นยำของโมเดล
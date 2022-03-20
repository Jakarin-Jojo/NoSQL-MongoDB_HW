# NoSQL-MongoDB_HW Answer for Question 5  
### Create MongoDB database with following information   
```SQL
use HW8
```
![image](https://user-images.githubusercontent.com/72879083/159142131-a3041211-201a-49f2-ad39-1a90320a7eaa.png)
```SQL
db.createCollection("Students")  
```
![image](https://user-images.githubusercontent.com/72879083/159142245-42d5178e-905d-43b5-929a-4d659698af50.png)
```SQL
db.Students.insertMany([
        {"name":"Ramesh","subject":"maths","marks":87},
        {"name":"Ramesh","subject":"english","marks":59},
        {"name":"Ramesh","subject":"science","marks":77},
        {"name":"Rav","subject":"maths","marks":62},
        {"name":"Rav","subject":"english","marks":83},
        {"name":"Rav","subject":"science","marks":71},
        {"name":"Alison","subject":"maths","marks":84},
        {"name":"Alison","subject":"english","marks":82},
        {"name":"Alison","subject":"science","marks":86},
        {"name":"Steve","subject":"maths","marks":81},
        {"name":"Steve","subject":"english","marks":89},
        {"name":"Steve","subject":"science","marks":77},
        {"name":"Jan","subject":"english","marks":0,"reason":"absent"}
    ]
)
```
![image](https://user-images.githubusercontent.com/72879083/159142413-329b1ae4-c888-4fc6-bde4-b085a50c1852.png)  
## Find the total marks for each student across all subjects.
```SQL
db.Students.aggregate([{$group:{_id:"$name",totalMark:{$sum:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/72879083/159142652-d6a10c91-ac21-4f27-8afa-29caf01cdf58.png)
## Find the maximum marks scored in each subject.
```SQL
db.Students.aggregate([{$group:{_id:"$subject",maxScore:{$max:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/72879083/159142634-c3a152ac-0154-45eb-b514-ed2d006978f5.png)

## Find the minimum marks scored by each student.
```SQL
db.Students.aggregate([{$group:{_id:"$name",minMark:{$min:"$marks"}}}])
```
![image](https://user-images.githubusercontent.com/72879083/159142698-96e290ef-c6a1-46b3-9d70-30b4c70d7869.png)
## Find the top two subjects based on average marks.
```SQL
db.Students.aggregate([{$group:{_id:"$subject",averageMark:{$avg:"$marks"}}}, {$sort:{"averageMark":-1}},{$limit:2}])
```
![image](https://user-images.githubusercontent.com/72879083/159143013-79b22178-db2a-4916-89ae-640441d7b3a0.png)

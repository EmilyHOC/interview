* //1.进入my_test数据库
use my_test;
show dbs;
* //2.向数据库的user集合中插入一个文档 
db.users.insert({username:"sunwukong"});
show dbs;
show collections;
* //3.查询user集合中的文档
db.users.find();
* //4.向数据库的user集合中插入一个文档 
db.users.insert({username:"zhibajie"});
* //5.查询数据库user集合中的文档
db.users.find();
* //6.统计数据库user集合中的文档数量
db.users.find().count();

* //7.查询数据库user集合中username为sunwukong的文档
db.users.find({username:'sunwukong'});
* //8.向数据库user集合中的username为sunwukong的文档，添加一个address属性，属性值为huaguoshan
db.users.update({username:'sunwukong'},{$set:{address:'huaguoshan'}});
* //9.使用{username:"tangseng"} 替换 username 为 zhubajie的文档
db.users.replaceOne({username:'zhibajie'},{username:'tangseng'});
* //10.删除username为sunwukong的文档的address属性
db.users.update({username:'sunwukong'},{$unset:{address:1}});

* //11.向username为sunwukong的文档中，添加一个hobby:{cities:["beijing","shanghai","shenzhen"] , movies:["sanguo","hero"]}
db.users.update({username:'sunwukong'},{$set:{hobby:{cities:["beijing","shanghai","shenzhen"], movies:["sanguo","hero"]}}});
db.users.find();

* //12.向username为tangseng的文档中，添加一个hobby:{movies:["A Chinese Odyssey","King of comedy"]}
db.users.update({username:'tangseng'},{$set:{hobby:{movies:["A Chinese Odyssey","King of comedy"]}}});
db.users.find();
* //13.查询喜欢电影hero的文档
db.users.find({"hobby.movies":"hero"});/*支持。来匹配*/

* //14.向tangseng中添加一个新的电影Interstellar
/*$addToSet如果数组中已经存在不添加*/
db.users.update({username:'tangseng'},{$push:{"hobby.movies":"Interstellar"}});
db.users.find();

* //15.删除喜欢beijing的用户
db.users.remove({"hobby.cities":"beijing"});
db.users.find();

* //16.删除user集合
db.users.drop();
show dbs;
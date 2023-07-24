//-----delete.html-------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style type="text/css">
           #app{
          width: 300px;
          height: 300px;
          border: 2px solid red;
          border-radius: 10px;
          position: absolute;
          top: 10%;
          right: 40%;
          text-align: center;
        }
        input{
          width: 200px;
          height: 20px;
          border: 2px solid black;
          border-radius: 20px;
          font-size: 15px;
          font-weight: bold;
          text-align: center;
          margin-top: 10%;
        }
       #spt{
        width: 270px;
        height: 40px;
        background-color: blue;
        font-size: 20px;
        font-weight: bold;
       } 
       #spt:hover{
        background-color: red;
       }
 
    </style>

</head>
<body>
       
    <h2><center><u>delete data to database</u></center></h2>
         <form action="http://127.0.0.1:8484/delete" method="post" id="app">
              <h2><center><u><font color="red">delete data</font></u></center></h2>
      <input type="number" placeholder="enter Roll no" name="t1"><br><br>    
      <input type="submit" value="delete" id="spt"><br><br> 
       </form>
</body>
</html>
delete.js:------------
      // -----------delete data in post method------------------------------
var app=require("express")()
var bodyparser=require("body-parser")
var urlencode=bodyparser.urlencoded({extended:false})
app.post("/delete",urlencode,(request,response)=>{
    var ad=require("mongodb").MongoClient
    var url="mongodb://127.0.0.1:27017/"
    ad.connect(url,(err,db)=>{
      var empid=parseFloat(request.body.t1)
     var dbobj=db.db("students")
    // dbobj.collection("studentdata").deleteMany({id:empid},(err,res)=>{
        dbobj.collection("studentdata").deleteOne({id:empid},(err,res)=>{
            if(err)
        console.log(err.tostring())
        else{
            response.send("<h1>successfully deleted in database</h1>")
            console.log("successfully deleted")
             console.log("result:",res)
    
        }
       db.close
     })
    })  
}).listen(8484)
console.log("port server running in--8484-----")

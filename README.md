# multerConfig


          const multer = require("multer")

          const multerStorage =  multer.diskStorage({

            destination: function(req,file,cb){
                cb(null,"images/post")
            },filename : function(req,file,cb){
                const ext = file.mimetype.split("/")[1];
                const orgFile =   file.mimetype.split("/")[0];
                const uniqueSuffix = Date.now() + '-' + Math.round(Math.random()*1E9)
                const fileName = `${orgFile}-${uniqueSuffix}.${ext}`;

                cb(null,fileName)
            }
             })
           module.exports =   multer(
           {
            storage : multerStorage,
            limits : {
                fieldSize : 100000
            },
             fileFilter:(req,file,cb)=>{
              if(file.fieldname === "file"){
                  if(file.mimetype === "image/png" ||
                  file.mimetype === "image/jpg" ||
                  file.mimetype === "image/jpeg"){
                      cb(null,true)
                  }else{
                      cb(new Error("Image Mustbe JPG, JPEG, PNG formate"))
                  }
              }
            }

           })

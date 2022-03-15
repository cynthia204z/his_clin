# node.js Note

[【NodeJS 编程入门】保证零基础初学者也能轻松入门NodeJS后端编程！自学编程就从这个NodeJS教学开始！](https://www.youtube.com/watch?v=PQoK7r4MJoQ)

如果只在終端機打node，會進入REPL環境，可以用來直接執行js程式碼

> 補充：port >1023

- npm init -y

  產生package.json



- 安裝模組

  npm install modules

  會在package.json的dependencies(依賴)中出現模組名:版本



- 解除安裝模組

  npm uninstall 模組名



## express

[【Express入門】Node.jsでWebアプリケーションの作り方を１から学ぼう！](https://www.youtube.com/watch?v=Zk7tpzaKv0U)

`npm install express`

server.js

```js
const express = require('express');
const app = express();
const PORT = 3000;

// 路徑, callback(request, response)
app.get("/", (req, res)={
  // do something
})

app.listen(PORT, ()=>{
  console.log(`server listening on ${PORT}`);
})
```

> 補充：
>
> `npm install nodemon`
>
> package.json
>
> ```json
> "scripts": {
> 	"dev": "nodemon server.js"
> }
> ```
>
> `npm run dev`



### express.Router

`express.Router` 類別用來建立可裝載的模組路由處理程式。

`Router` 實例是一個完整的中介軟體與路由系統； 因此，常被稱為「迷你應用程式」。

server.js

```js
const express = require('express');
const app = express();
const userRouter = require('./routes/user');
const PORT = 3000;

// 接到"/"路徑會直接在這裡處理
app.get("/", (req,  res)=>{
    // do something
});

// 接到"/user"開頭的路徑會把接下來的路徑交給userRouter處理
// 詳見中介軟體函數
app.use("/user", userRouter);

app.listen(PORT, ()=>{
    console.log(`server listening on ${PORT}`);
});
```

routes/user.js

```js
const express = require('express');
const router = express.Router();

// EX: lacalhost:3000/user
router.get("/", (req, res)=>{
    res.send("user home page");
});
// EX: localhost:3000/user/info
router.get("/info", (req, res)=>{
    res.send("user info");
});
// EX: localhost:3000/user/卡加布列島
// => show: 卡加布列島's info
router.get("/:id", (req, res)=>{
    res.send(`${req.params.id}'s info`);
});

module.exports = router;
```

> 重複定義路由：
>
> 不會報錯，但第二個永遠不會被呼叫。
>
> ```js
> router.get("/info", (req, res)=>{
>   res.render('hello')
> });
> router.get("/info", (req, res)=>{
>   res.end(res.params.id)
> });
> ```



### server、app、router、controller

[Routes and Controllers - Create REST API with NodeJS and MySQL (2020)](https://www.youtube.com/watch?v=pRV6pe2bnbQ)

server.js

```js
const http = require('http');
const app = require('./app');
const PORT = 3000;

const server = http.createServer(app);

server.listen(PORT, ()=>{
    console.log(`server listening on ${PORT}`);
});

```

app.js

```js
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const pathNameRoute = require('./routes/routerName');

app.use(bodyParser.json());
app.use('/pathName', pathNameRoute);

module.exports = app;
```

routes/routerName.js

```js
const express = require('express');
const controllerName = require('../controllers/controllerName.controller');

const router = express.Router();

router.post("/", controllerName.save);
router.get("/", controllerName.index);
router.get("/:id", controllerName.show);
router.patch("/:id", controllerName.update);
router.delete("/:id", controllerName.destroy);

module.exports = router;
```

controller/controllerName.controller.js

```js
const models = require('../models');

// C
function save(req, res){
  const postObj = {
    columnName: req.body.column_name
  };
  models.modelName.create(postObj).then(result => {
    res.status(201).json({
      message: 'Post created seccessfully.',
      post: result
    });
  }).catch(error => {
    res.status(500).json({
      message: 'Something went wrong.',
      error: error
    });
  });
}

// R
// get all
function index(req, res){
  models.modelName.findAll().then(result => {
    res.status(200).json(result);
  }).catch(error => {
    // status: 500, show error message
  });
}
// search by id
function show(req, res){
  const id = req.params.id;
  models.modelName.findByPk(id).then(result => {
    if(result){
      res.status(200).json(result);
    }else{
      res.status(404).json({
        message: 'Post not found.'
      });
    }
  }).catch(error = > {
    // status: 500, show error message
  });
}

// U
function update(req, res){
  const id = req.params.id;
  const updatedObj = {
    columnName: req.body.column_name
  };
  const otherSearchColumnVal = blablabla;
  models.modelName.update(updatedObj, {where: {id: id, searchColumnName: otherSearchColumnVal}}).then(result => {
    res.status(200).json({
      message: 'Post updated successfully.',
      post: updatedPost
    })
  }).catch(error => {
    // status: 500, show error message
  })
}

// D
function destroy(req, res){
  const id = req.params.id;
  const otherSearchColumnVal = blablabla;
  models.modelName.destroy({where: {id: id, searchColumnName: otherSearchColumnVal}}).then(result => {
    // status: 200, show delete success message
  }).catch(error => {
    // status: 500, show error message
  })
}

module.exports = {
    save: save,
    show: show,
    index: index,
    update: update,
    destroy: destroy
};
```

> 可以用`npm start`啟動
>



### mysql + sequelize

#### 指令

```shell
npm install --save mysql2

npm install sequelize

sequelize init

sequelize model:generate --name Post --attributes title:string,content:text,imageUrl:string,categoryId:integer,userId:integar
>會在migrations資料夾裡生出長得像"20220309061819-create-post.js"的檔案

sequelize db:migrate
>建立Table, 會建立在config.json中"development"中設定的資料庫
```

#### 實際範例(ChartEditor)

config/db.config.js

```js
module.exports = {
  HOST: "localhost",
  USER: "root",
  PASSWORD: "",
  DB: "chred",
  dialect: "mysql",
  pool: {
    max: 5,
    min: 0,
    acquire: 30000,
    idle: 10000
  }
};
```

models/index.js

```js
const dbConfig = require("../config/db.config.js");

const Sequelize = require("sequelize");
const sequelize = new Sequelize(dbConfig.DB, dbConfig.USER, dbConfig.PASSWORD, {
  host: dbConfig.HOST,
  dialect: dbConfig.dialect,
  // operatorsAliases: false,
  operatorsAliases: 0,
  define: {
    timestamps: false,
    freezeTableName: true
  },
  pool: {
    max: dbConfig.pool.max,
    min: dbConfig.pool.min,
    acquire: dbConfig.pool.acquire,
    idle: dbConfig.pool.idle
  }
});

const db = {};

db.Sequelize = Sequelize;
db.sequelize = sequelize;

db.concept = require("./concept.model.js")(sequelize, Sequelize);
db.conceptdata = require("./conceptdata.model.js")(sequelize, Sequelize);

module.exports = db;
```

controllers/name.controller.js

```js
const db = require("../models");
const Transmst = db.transmst;
const Op = db.Sequelize.Op;

exports.functionName = (req, res) => {
  let conditionObj = {
    // ▼ where條件
    where: {
      dept: '測試部門', // 等於條件
      [Op.or]: [
        { name: "林春嬌" },
        { name: "王志明" },
        { type: "聘僱人員" },
      ]
    }, 
    // 會產生SQL語句像：*註1

    limit: limit,
    offset: limit * (page - 1)
  }

  modelName.findAll(conditionObj).then(data=>{
    // do something
  })
}
```

```sql
-- 註1
WHERE dept = '測試部門' AND (name = '林春嬌' OR name = '王志明' OR type = '聘僱人員')
```

routes/name.routes.js

```js
module.exports = app => {
  const nameController = require("../controllers/name.controller.js");

  var router = require("express").Router();

  router.get("/apiPathName", nameController.functionName);

  app.use('/api/pathBefore', router);
};
```

[sequelize数据库查询的Op方法](https://blog.csdn.net/skyblacktoday/article/details/104351546)



#### 關聯表

[Node.js Sequelize 模型(表)之间的关联及关系模型的操作](https://itbilu.com/nodejs/npm/EJarwPD8W.html)

[Sequelize 系列教程之一对多模型关系](https://cloud.tencent.com/developer/article/1533442)





### 中介軟體

放在後續路徑的method處理之前，每當收到req就會先被執行。

1. 沒有裝載路徑的中介軟體函數：所有路徑的請求都會處理

```js
// 也可以直接用app
const router = express.Router();
```

```js
// 收到所有路徑的所有種類請求，都會先執行中介軟體函數
// 寫法一
router.use((req, res, next)=>{
  // console.log(req.method)
  // do somwthing
});
router.get("/", (req, res)=>{
  // end
});
router.post("/info", (req, res)=>{
  // end
});

// 寫法二
router.use(handleMethod);
router.get("/", (req, res)=>{
  // end
});
router.post("/info", (req, res)=>{
  // end
});
function handleMethod(req, res, next){
  // do something
}
```

2. 裝載路徑的中介軟體函數：特定路徑的請求才處理

```js
// TYPE 1: 收到任何類型的 /info HTTP請求都會執行
router.use("/info", (req, res, next)=>{
  // do something
  next();
});
router.get("/info", (req, res)=>{
  // end
});
router.post("/info", (req, res)=>{
  // end
})

// TYPE 2: 針對 /info 路徑的get請求執行
// 寫法一
router.get("/info", (req, res, next)=>{
  // do something
  next();
}, (res, req)=>{
  // end
});
// 寫法二
router.get("/info", handleGetInfo, (req, res)=>{
  // end
});
function handleGetInfo(req, res, next){
  // do something
  next();
}
```

3. 中介軟體函數可堆疊

```js
// 收到任何類型的 /info HTTP請求都會執行
router.use("/info", (req, res, next)=>{
  // do step 1
  next();
}, (req, res, next)=>{
  // do step 2
  next();
});
```

4. 跳過剩下的中介軟體函數：`next('route')`

```js
router.get("/info", (req, res, next)=>{
  if(req.params.id === 0){
    next('route'); // 將控制權交給下一個路由
  }else{
    next();
  }
}, (req, res, next)=>{
  // do something if req.params.id !== 0
});
router.get("/info", (req, res, next)=>{
  // do something if req.params.id === 0
});
```



